# Page View

Fire whenever a user loads in a new page, whether that is done synchronously or asynchronously.

This event should be the first pushed into the data layer on each page. Given many 3rd party scripts push events to the data layer, this event push should be placed in the page `<head>` and should be the first `<script>` tag on the page to ensure it is the first event.

On single page apps (SPAs), this event should be fired whenever a virtual page view would have been fired in the past, such as when a new page/screen is loaded asyncronously within an angular, react, or vue app/embed.

## Javascript Code
```js

window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({pageModel: null, sessionModel: null, userModel: null}) 
window.dataLayer.push({
  "event": "page_view",
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
  },
  // Send this portion if user data is consistently available at page_load. If not send this with the user_detect event
  "userModel": {
    "user_id": "<userId>"
  },
})
```

## Variable Definitions
|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|breadcrumb|string|optional|The breadcrumb heirarchy of the page, separated by greater than (>), slash (/), or pipe (|).|Home>Blog|
|language|string|required|The language of the page, usually retrieved from the `<html>` tag on the page|en|
|page_category|string|recommended|A human-readible value used to group pages into clusters. If running low on custom dimensions, you may combine multiple categories together in this field, separated by greater than (>), slash (/), or pipe (|). See https://schema.org/category.|Blog|
|page_category2|string|optional|page_category2 through page_category5 can be used to break down category if additional detail is needed and you have space for more custom dimensions|Google Products|
|page_category3|string|optional|page_category2 through page_category5 can be used to break down category if additional detail is needed and you have space for more custom dimensions|Google Tag Manager|
|page_category4|string|optional|page_category2 through page_category5 can be used to break down category if additional detail is needed and you have space for more custom dimensions|Implementation|
|page_category5|string|optional|page_category2 through page_category5 can be used to break down category if additional detail is needed and you have space for more custom dimensions|Data Layer|
|page_id|string|recommended||12345|
|page_name|string|optional|The page name originally developed for Adobe Analytics.|Take-a-Deep-Breath:-Stress-Relief-Techniques-for-Seniors|
|page_location|string|required|The full URL of the page. Equivalent to document.location.href.|https://www.comfortkeepers.com/articles/info-center/senior-health-and-wellbeing/take-a-deep-breath-stress-relief-techniques-for-se|
|page_referrer|string|required|The page referrer. Equivalent to document.referrrer.|https://www.google.com|
|page_title|string|required|The page title. Generally set to the HTML <title> tag.|Take a Deep Breath: Stress Relief Techniques for Seniors | Comfort Keepers|
|site_section|string|recommended|Set on all events with a value which designates what portion (i.e., section) the visitor is on.  Previously the "channel" in Adobe Analytics.|Article Library|
|site_section2|string|optional||Info Center|
|site_section3|string|optional||Senior Health and Wellbeing|
|site_section4|string|optional||Section 4|
|site_section5|string|optional||Section 5|
|@type|string|recommended|The schema.org type for this event. For instance, for a page_view event, the page being viewed is a WebPage, but it could also be a more specific subtype like AboutPage or event a custom type your organization creates such as HomePage. Differs from type in that "@type" always should be populated with a schema.org type, while "type" can be populated with arbitrary values.|AboutPage, CheckoutPage, CollectionPage, ArticlePage|