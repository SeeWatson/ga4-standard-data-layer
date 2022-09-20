# GA4 Standard Data Layer Spec

The objective of this spec is to propose a standard data layer spec for Google Analtyics 4 (GA4) implementations.

## FAQs
<details>
  <summary>How was this spec developed?</summary>
  
  This data layer spec was initially developed while working across more than a dozen GA4 implementations. The spec takes Google's [automatically-collected](https://support.google.com/analytics/answer/9234069?hl=en) events, [enhanced measurement events](https://support.google.com/analytics/answer/9216061?hl=en&ref_topic=9756175), and [recommended events](https://support.google.com/analytics/answer/9267735?hl=en&ref_topic=9756175) and builds upon them to provide a data layer spec to send data in a standardized way.
</details>
<details>
  <summary>For custom events, what naming conventions did you use and why?</summary>

    1. Custom event and parameter names are all [snake_case](https://en.wikipedia.org/wiki/Snake_case), meaning all characters are lower-case and underscores separate words. This matches Google's conventions they used in their automatically-collected, enhanced measurement, and recommended events.

    2. Custom event names always contain a subject and a present tense verb. This matches Google's conventions. Exceptions can be made for semantically awkward event names.

    3. Custom event names take of the form of subject_verb. Google's predefined events are inconsistent in their ordering of the subject and verb (`tutorial_begin` vs `begin_checkout`, `generate_lead` vs `file_download`), so a choice had to be made as to which approach to use to ensure consistency. Given that events are generally sorted alphabetically in most systems, it seemed clustering events with the same subject would make for better findability and easier analysis, thus subject_verb was chosen. The decision could easily have gone the other way, so don't feel bound by this. Also, exceptions to the convention can be made for semantically awkward event names [see detect_user](events/authentication/detect_user).

</details>
<details>
  <summary>Why use traditional data layer pushes instead of using the gtag approach?</summary>

  While Google's `gtag` container has been around for a decade, Google has leaned much more heavily into recommending that approach to send data since GA4 was released. The Universal Analytics documentation was updated in Q3 of 2022 to recommend this approach exclusively with no mention of the old data layer push approach. Additionally, though it was quickly removed, an update to the GA4 documentation appeared for a few hours in September 2022 that discouraged using the traditional data layer in favor of `gtag`.

  While `gtag` is a good tool and provides a very simple way to send data to GTM, it does have one significant shortcoming that prevents a full recommendation. This shortcoming is that all parameters sent via `gtag` are wrapped in an `eventModel` object...and that object is reset between each event. This functionality is actually the preferred behavior in most cases as parameters persisting between events can cause incorrect data to be sent. However, this lack of persistence can cause significant issues when combined with the peculiar behavior of the GTM configuration tag.

  ### Example scenario
  Here's an example scenario where a lack of persistence becomes a problem. A website has an authentication module that loads asynchronously from when the page loads. As such, at the time the `page_view` event goes out, we cannot be certain we will know the authentication status of the user. Additionally, for all of the events subsequent to `page_view` such as `click` or `video_start`, the site owner wants to know the `page_category` of the page they occured on. This is fairly common scenario encountered in many implementations.
  
  The typical approach to sending a parameter along with every event in GTM/GA4 is to set the parameter in the "fields to set" section of the configuration tag. So, we ask the developers to send `page_category` in the `page_view` event, like so:

  ```js
  window.dataLayer.push({
    event: "page_view",
    eventModel: {
      "page_category": "blog"
    }
  })
  ```

  We set up GTM to fire a configuration tag and page_view event on the page_view data layer push (named History Change in preview mode unfortunately 🙄) and to grab the `page_category` with a data layer variable. We test it, the tag fires, we "lock in" the `page_category` parameter for future events, and we're set.

  However, we realize that the authentication module loading asynchronously means we're going to have to re-fire the configuration tag as the only place to capture the `user_id` in GTM is in the "fields to set" portion of configuration tag. Re-firing the configuration tag is generally fine...but when we do it this time we have a problem. The `page_category` data layer variable is returning null...because the `eventModel` that the data was in was cleared between the `page_view` event and our `detect_user` event. In order to get this value to persist, we would have to store it and source it from somewhere outside of the data layer...perhaps in a window-scoped variable...which breaks us out of the event-driven data layer (EDDL) paradigm and makes implementation more confusing for the developers.

  The only real solve for this that keeps us in a pure EDDL paradigm is to send page-scoped parameters in their own wrapper that won't get automatically cleared, but that's not currently possible using `gtag`. Thus, for the purposes of this standard, we recommend using `dataLayer.push` instead of gtag and sending parameters in their own scopes.
</details>
<details>
  <summary>Why are all event parameters in this spec contained within wrapper objects and why are these wrappers sometimes reset before new event pushes?</summary>

  This spec uses the `eventModel` wrapper object for most parameters because Google itself quietly adds this wrapper to its `gtag` calls and Google Tag Manager (GTM) has built-in behavior that can leverage this wrapper. However, the spec expands upon Google's recommended wrapper, adding `pageModel`, `userModel`, and `sessionModel` due to some eccentricities in how GTM's configuration tags work.
  
  ### Some history from UA
  To send enhanced ecommerce events to Universal Analytics, Google historically recommended performing data layer pushes with parameters wrapped by an `ecommerce` object. Sending data in this format along with enabling on a setting in Google Tag Manager enabled automatic consumption, formatting, and sending this data to Google Analytics. Google also recommended clearing this ecommerce object between events, likely due to the nature of Google Tag Manager's data layer processing where values typically persist in an internal state until overwritten. Adding `dataLayer.push({ ecommerce: null });` before each ecommerce push would ensure that values did not persist between events and were not incorrectly sent.

  ### GA4
  Google's GA4 documentation provides two different approches to sending ecommerce data to GTM: traditional data layer pushes or its `gtag` "library". For traditional data layer pushes, the [measure ecommerce documentation](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm) gives the same recommmendation as in UA...to wrap ecommerce paramters with `ecommerce` and to clear it before each event. This is interesting as parameters in ecommerce events that are sent via `gtag` are not automatically wrapped by an object called `ecommerce`, but rather are automatically wrapped by an object called `eventModel`. Even more interestingly, experimentation has shown that the `evenModel` wrapper is automatically reset on every event regardless of whether the push was via `gtag` or the traditional data layer.

  Given that Google's tool wraps parameters `eventModel` and automatically clears them, leveraging the `eventModel` wrapper is the preferred approach as it calls for less code and should provide the most future compatibiity.
</details>
