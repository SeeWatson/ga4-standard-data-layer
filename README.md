# GA4 Standard Data Layer Specification

The objective of this spec is to propose a standard data layer specification for Google Analtyics 4 (GA4) implementations.

The specification takes Google's [automatically-collected](https://support.google.com/analytics/answer/9234069?hl=en) events, [enhanced measurement events](https://support.google.com/analytics/answer/9216061?hl=en&ref_topic=9756175), and [recommended events](https://support.google.com/analytics/answer/9267735?hl=en&ref_topic=9756175) (better organized in the [event reference](https://developers.google.com/analytics/devguides/collection/ga4/reference/events)) and builds upon them to provide a standardized and reusable set of events and parameters and the exact data layer code you should implement to send these events to GTM/GA4.

## FAQs
<details>
  <summary>How and why was this specification developed?</summary>
  
  This data layer specification was initially developed while working as a consultant across more than a dozen GA4 implementations. It was built to provide a standard naming convention and set of events and parameters that can be used over and over again. There are many benefits from using a standard approach like this:

  1. Implementations can be built much more consistently. This allows for much better reuse of resources like implementation documentation. Dashboards can be built that work across implementations with minimal adjustments needed.
  2. Implementations can be built much more quickly, which is a benefit for brands with many sites or for agencies building sites across a variety of clients. This spec aims to standardize the "stupid" things that soak up a lot of time in implementations so more brain power can be spent on actual challenges.
  3. If a standard like this is adopted across a large swath of the industry, these gains can begin to scale. Individuals moving between companies or agencies can ramp up far more quickly.
  
</details>
<details>
  <summary>For custom events, what naming conventions are used and why?</summary>

  1. **Custom event and parameter names are all [snake_case](https://en.wikipedia.org/wiki/Snake_case)**. This means all characters are lower-case and underscores separate words. This matches Google's conventions they used in their [automatically-collected](https://support.google.com/analytics/answer/9234069?hl=en) events, [enhanced measurement events](https://support.google.com/analytics/answer/9216061?hl=en&ref_topic=9756175), and [recommended events](https://support.google.com/analytics/answer/9267735?hl=en&ref_topic=9756175).

  2. **Custom event names always contain a single object/subject and a single present tense action/verb.** This matches Google's conventions. Exceptions can be made for semantically awkward event names.

  3. **Custom event names should always take the form of `object_action`/`subject_verb`.** Google's predefined events are inconsistent in their ordering of the subject and verb (`tutorial_begin` vs `begin_checkout`, `generate_lead` vs `file_download`), so a choice had to be made as to which approach to use to ensure consistency. Given that events are generally sorted alphabetically in most downstream systems, it seemed clustering events with the same subject would make for better findability and easier analysis, thus `object_action` was chosen. The decision could easily have gone the other way, but the choice has been made, so now we have to live with it...

  4. **Custom parameters should be reused as often as possible, and therefore should not be namespaced** For instance, `category` is preferred over `form_category`. This one is fairly controversial as namespaced parameters are objectively better in nearly all cases to make data analysis easier in downstream systems. However, it became clear after just a couple of large implementations that custom dimension limits are going to be a problem, especially in non-360 implementations. For a parameter to be of any use for reporting or audience generation in GA4, it must be updated to a custom dimension...and Google has some fairly low limits on event-scoped custom dimension slots available (at time of writing 50 for free users and 125 for 360 users...see [Google's documentation](https://support.google.com/analytics/answer/10075209?hl=en) for current limits. 125 might seem like a lot, but they go very very quickly on complex sites. It is for this reason that `category`, `identifier`, and `name` can be found on nearly every custom event...and also why built-in parameters like `method` appear in many events as well.

  5. **When creating new custom parameter names, refer to existing parameters and then to schema.org.** Naming parameters is easy. Naming them really well is really hard. For this reason, existing standards were used where possible. Google's existing parameters were the first point of reference...and Schema.org was the next. For instance, it's because of Schema.org that we use `identifier` instead of `id` throughout the spec. There are multiple benefits of using Schema.org, including the ability to dynamically generate and insert structured data from the data layer into pages using GTM such that search engines can better understand pages. The hope is to add additional @params over time to help this process along.
</details>
<details>
  <summary>Why are the events and parameters in the data layer identical to the final names in GA4? Couldn't you just name them whatever you want (perhaps using an external or 3rd party specification) and map them in GTM?</summary>

  While there's nothing inherently wrong with naming your events and parameters arbitrarily and mapping them to the final parameter slots in GTM, there are multiple downsides:

  1. Implementations should be as clear and simple as possible so as to be transferrable from one owner/implementer to another. Mappings provide a layer of abstraction and obscurity that is just one more thing a new implementer will have to learn to be able to fully understand, modify, and QA an implementation.

  2. GA4's only example of actual data layer events are in the [eCommerce documentation](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm). In that documentation, they show the final GA4 event and parameter names in the data layer event and parameter names. Given the desire for clear and simple implementations, we should always prefer adhering to written documentation.
</details>
<details>
  <summary>Some events overlap with enhanced measurement. Why should I send these instead of just enabling enhanced measurement?</summary>
  
  Enhanced measurement is a great feature. It allows for very quickly standing up a GA4 property and collecting basic information. However, the emphasis there is on basic. Enhanced measurement events are not very configurable, miss a lot of use cases, and are missing many key parameters. Each event in this spec that replicates or replaces an enhanced measurement event offers an explanation for the shortcomings of enhanced measurement for that event and why implementing it yourself is superior.
</details>
<details>
  <summary>Why do you include an count_{{event_name}} parameter on each event?</summary>
  
  If you've spent any time in the GA4 explore interface or in Data Studio, you know it can be a pain to get simple event counts. You have to use event count as the metric and then filter down to the specific `event_name` you want. Sending an `count_{{event_name}}` parameter that can be upgraded to a custom dimension saves you a step in the GA4 UI, Data Studio, and any other downstream data analysis tool yo umay use.
</details>
<details>
  <summary>Why use traditional data layer pushes instead of using gtag/Google Tag?</summary>

  While Google's `gtag` container has been around for a decade, Google has leaned much more heavily into recommending that approach to send data since GA4 was released. The Universal Analytics documentation was updated in Q3 of 2022 to recommend this approach exclusively with no mention of the old data layer push approach. Additionally, though it was quickly removed, [an update to the GA4 documentation appeared for a few hours in September 2022](https://twitter.com/tyssejc/status/1565047950761394176?cxt=HHwWgICwmbe0lbgrAAAA) that discouraged using the traditional data layer in favor of `gtag`. They even rebranded it to ["The Google Tag" in August of 2022](https://www.blog.google/products/ads-commerce/simplify-measurement-with-google-tag/). 

  While `gtag` is a good tool and provides a very simple way to send data to GTM, it does have one significant shortcoming that prevents a full recommendation. All parameters sent via `gtag` are wrapped in an `eventModel` object...and that object is reset after each event. This functionality is actually the preferred behavior in most cases as parameters persisting between events can cause incorrect data to be sent. However, this lack of persistence can cause significant issues when combined with the peculiar behavior of the GTM configuration tag. For an example why this can cause issues, check out the next FAQ below (`Why are all event parameters in this spec contained within wrapper objects and why are these wrappers sometimes reset before new event pushes?`) for an example scenario.
</details>
<details>
  <summary>Why are all event parameters in this spec contained within wrapper objects and why are these wrappers sometimes reset before new event pushes?</summary>

  This spec uses the `eventModel` wrapper object for most parameters because Google itself quietly adds this wrapper to its `gtag` calls and Google Tag Manager (GTM) has built-in behavior that leverages this wrapper (mostly by resetting all parameters wrapped by it between events). However, the spec expands upon Google's recommended wrapper, adding `pageModel`, `userModel`, and `sessionModel` as options due to some eccentricities in how GTM's configuration tags work.
  
  ### Some history from UA
  To send enhanced ecommerce events to Universal Analytics, Google historically recommended performing data layer pushes with all parameters wrapped by an `ecommerce` object (the documentation has since been updated to only use gtag, but you can see the old DL pushes on [Simo Ahava's implementation guide](https://www.simoahava.com/analytics/enhanced-ecommerce-guide-for-google-tag-manager/)).

  ```js
    window.dataLayer = window.dataLayer || [];
    window.dataLayer.push({
      event: 'eec.purchase',
      ecommerce: {
        purchase: {
          actionField: {
            id: '1'
          },
          products: [{
            id: 'p'
          }]
        }
      }
    });
  ```
  
  Sending data in this format along with flippiing a switch in Google Tag Manager enabled automatic consumption, formatting, and forwarding of ecommerce data to Google Analytics. Google also recommended clearing this ecommerce object between events, likely due to the nature of Google Tag Manager's data layer processing where values pushed into the data layer typically persist in an internal state until overwritten. Google recommended adding `dataLayer.push({ ecommerce: null });` before each ecommerce push would ensure that values did not persist between events and were not incorrectly sent.

  ### What's new in GA4
  Google's GA4 documentation provides two different approches to sending ecommerce data to GTM: traditional data layer pushes or its `gtag` "library". For traditional data layer pushes, the [measure ecommerce documentation](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm) gives the same recommmendation as in UA...to wrap ecommerce parameters with `ecommerce` and to clear all parameters in that wrapper before each event. 
  
  This is interesting as parameters in ecommerce events that are sent via `gtag` are not automatically wrapped by an object called `ecommerce`, but rather are automatically wrapped by an object called `eventModel`. Even more interestingly, experimentation has shown that the `evenModel` wrapper is automatically reset on every event regardless of whether the push was via `gtag` or the traditional data layer.

  Given that Google's tool wraps parameters `eventModel` and automatically clears them, leveraging the `eventModel` wrapper is the preferred approach as it calls for less code and should provide the most future compatibiity.

  ### Other wrappers and Example scenario
  So...why does this spec contain other wrappers if `eventModel` is what Google uses? It's because Google's new Configuration Tag approach required to leverage GA4 introduces some complications.

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

  The only real solve for this that keeps us in a pure EDDL paradigm is to send page-scoped parameters in their own wrapper that won't get automatically cleared. As that's not currently possible using `gtag`, we recommend using `dataLayer.push` instead of `gtag` and sending parameters in their own scopes (`pageModel`). If this approach is taken, in the case of single page apps we can run into another persistence issue because paramers in `pageModel` could stick around when they shouldn't, so we recommend clearing `pageModel` between events.
</details>
<details>
  <summary>What do I do when multiple events could represent the same user action?</summary>

  A user submits an account creation form. Should you fire `sign_up` or `form_complete`? A user clicks on a download link that counts as a lead generating event. Should you fire `file_download` or `generate_lead`?
  
  The answer, suprisingly, is usually to fire both. Whereas in UA you rarely fired more than 1 event at a time, GA4 automatically fires multiple events in many situations (`session_start` is the best example), gives you a dedicated UI for triggering events off of other events, and can batch multiple events through GTM. Given this, it's recommended that as long as it's not going to cost you significantly more money in your 360 account, just fire multiple events.
</details>
<details>
  <summary>Why do this spec's recommended HTML data attributes start with data-layer-?</summary>

  HTML data attributes have to start with `data-` to be valid. After spec'ing a lot of implementations in Google, Adobe, and other tools, it became clear that adding data attributes specifically for analytics without a namespace/prefix can be problematic as they can collide with data attributes intended for other uses. For instance, say you need to add a data attribute to a page of your site with the `page_category`. You decide to add `data-category` to the HTML `body` tag to store this data. However, the particular CMS system you use for your site adds a `data-category` attribute automatically with the first taxonomy category the page has been tagged with in the site. There is a conflict, and that data could be sent incorrectly to GA or another system. To avoid this, we generally will need to namespace the data attribute like so: `data-{{namespace}}-category`. The namespace is somewhat arbitrary. Lots of sites choose `data-analytics-`. This spec uses `data-layer-` for two reasons: 
  
  1. The "data layer" is a known concept in the analytics world as a way to pass data from your website to a variety of 3rd party tools (mostly tag managers, but lots of other tools leverage the data layer as well)
  2. Data attributes added specifically for tag managers often end up in the data layer

  If you want to use another namespace/prefix feel free to...but know that it may break integrations with the pre-built GTM containers referenced in this spec.
</details>
