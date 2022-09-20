# Page View

Fire whenever a user loads in a new page, whether that is done synchronously in a traditional site or asynchronously in a single page app (SPA).

This event should be the first pushed into the data layer on each page (except for the case where you're using [custom_session_start](./custom_session_start.md)). Given many 3rd party scripts push events to the data layer, this event push should be placed in the page `<head>` and should be the first `<script>` tag on the page to ensure it is the first event.

On SPA sites, this event should be fired whenever a virtual page view would have been fired in the past, such as when a new page/screen is loaded asyncronously within an angular, react, or vue app/embed.

Firing this event manually instead of using enhanced measurement provided the opportunity to set a significant number of additional parameters that enhanced measurement misses...as well as counting page views

## Javascript Code
```js

window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({pageModel: null, sessionModel: null, userModel: null}) 
window.dataLayer.push({
  "event": "page_view",
  "eventModel": {
    "count_page_view": 1,
  }
  "pageModel": {
    "breadcrumb": "<breadcrumb>",
    "page_category": "<page_category>",
    "page_category2": "<page_category2>",
    "page_category3": "<page_category3>",
    "page_category4": "<page_category4>",
    "page_category5": "<page_category5>",
    "page_id": "<page_id>",
    "language": "<language>",
    "page_name": "<page_name>",
    "page_location": "<page_location>",
    "page_referrer": "<page_referrer>",
    "page_title": "<page_title>",
    "site_section": "<site_section>",
    "site_section2": "<site_section2>",
    "site_section3": "<site_section3>",
    "site_section4": "<site_section4>",
    "site_section5": "<site_section5>",
    "@type": "<@type>"
    "count_page_view": 1,
  },
  // Send this portion if user data is consistently available at page_load. If not send this with the user_detect event.
  "userModel": {
    "user_id": "<userId>"
  },
  /*
  This is a placeholder for session scoped parameters. Omit this for now in actual data layer pushes. See Variable Definitions for more info...
  "sessionModel": {
    "session_parameter_placeholder": "<session_parameter_placeholder>"
  }
  */
})
```

## Variable Definitions
|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|breadcrumb|string|optional|The breadcrumb heirarchy of the page, separated by greater than (>), slash (/), or pipe (\|).|Home>Products|
|language|string|required|The language of the page, usually retrieved from the `<html>` tag on the page|en|
|page_category|string|recommended|A human-readible value used to group pages into clusters. If running low on custom dimensions, you may combine multiple categories together in this field, separated by greater than (>), slash (/), or pipe (\|). See https://schema.org/category.|Products|
|page_category2|string|optional|page_category2 through page_category5 can be used to break down category if additional detail is needed and you have space for more custom dimensions|Google Products|
|page_category3|string|optional|page_category2 through page_category5 can be used to break down category if additional detail is needed and you have space for more custom dimensions|Google Tag Manager|
|page_category4|string|optional|page_category2 through page_category5 can be used to break down category if additional detail is needed and you have space for more custom dimensions|Implementation|
|page_category5|string|optional|page_category2 through page_category5 can be used to break down category if additional detail is needed and you have space for more custom dimensions|Data Layer|
|page_id|string|recommended||12345|
|page_name|string|optional|The page name. This is primarily here for parity with Adobe Analytics, which wants a page name.|Products|
|page_location|string|required|The full URL of the page. Equivalent to document.location.href.|https://www.yoursite.com/yourpath|
|page_referrer|string|required|The page referrer. Equivalent to document.referrrer.|https://www.google.com|
|page_title|string|required|The page title. Generally set to the HTML `<title>` tag.|YourSite: our products|
|session_parameter_placeholder|any|optional|This is a placeholder for any session scoped dimensions you may want to set. This is here because at the time this spec was developed, it was unclear how session scoped dimensions were going to be handled. Will they have to go in the configuration tag or will they just be sent as normal parameters?|???
|site_section|string|optional|Set on all events with a value which designates what section of the site the visitor is on. Used primarily when site structure matters and the `page_category` does not adequately convey the portion of the site that the page lives in, such as in a multinational company.|EMEA|
|site_section2|string|optional|Set on all events with a value which designates what portion (i.e., section) the visitor is on.|Europe|
|site_section3|string|optional|Set on all events with a value which designates what portion (i.e., section) the visitor is on.|UK|
|site_section4|string|optional|Set on all events with a value which designates what portion (i.e., section) the visitor is on.|England|
|site_section5|string|optional|Set on all events with a value which designates what portion (i.e., section) the visitor is on.|London|
|@type|string|recommended|The schema.org type for this event. For instance, for a page_view event, the page being viewed is a WebPage, but it could also be a more specific subtype like AboutPage or event a custom type your organization creates such as HomePage. Differs from type in that "@type" always should be populated with a schema.org type, while "type" can be populated with arbitrary values.|AboutPage, CheckoutPage, CollectionPage, ArticlePage|