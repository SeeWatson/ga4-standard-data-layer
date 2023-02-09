# Click

Google Analytics has never really managed to capture link clicks very well, especially since they retired the old click overlay UI (it wasn't that great anyway). Entire products exist solely to provide extensive click tracking, so many companies rely on such products instead of doing any click tracking in GA. Also, GA4 charges by number of events and tracking click events adds a LOT. However, we should still strive to do the best we can within GA to gather as much data as we can, and so this spec exists.

Perhaps because of the rise of dedicated link tracking tools, GA4 can now automatically collect outbound link clicks easily via enhanced measurement. However, the enhanced measurement approach has a few weaknesses:

1. It only captures outbound clicks and misses internal link clicks entirely
2. It is limited to only clicks on HTML `<a>` tags, missing `<button>` tags that act as links or other Javascript-powered links
3. It only captures limited identifying information about the link clicked (href/url, HTML classes/IDs, and the link text). If you have two links on the same page with identical information for all of these paramters, the link will not be able to be uniquely identified.

Given these shortcomings, this event spec may be used by your site developers to manually send click events whenever a user clicks on an HTML anchor `<a>` tag or any other link. If that sounds like a lot of work for your developers...it is...but thankfully there is an alternative.

## Alternative (recommended) approach
The recommended approach instead of relying on enhanced ecommerce or your developers to reliably send data layer events is to configure GTM to automatically detect most clicks without needing an explicit data layer push. If you want to try that approach it is recommended to use [this implementation](#) and limit data layer pushes to situations where GTM cannot easily detect a click at all, such as inside of iframes.

## Javascript Code
```js
window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({
  "event": "click",
  "eventModel": {
    "category": "<category>",
    "component_ancestry": "<component_ancestry>",
    "identifier": "<identifier>",
    "link_url": "<link_url>",
    "link_id": "<link_id>",
    "link_classes": "<link_classes>",
    "link_text": "<link_text>",
    "navigation_ancestry": "<navigation_ancestry>",
    "outbound": "<outbound>",
    "region_ancestry": "<region_ancestry>"
  }
})
```

## Variable Definitions
|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|category|string|optional|A human-readible identifier whose purpose will vary by event, but generally is used to group things (forms, links, videos) into loose assocations based upon shared characteristics. If running low on custom dimensions, you may combine multiple categories together in this field, separated by greater than (>) or slash (/). See https://schema.org/category.||
|component_ancestry|string|optional|A hierarchical list of all components that a link is contained within|main>hero>cta-box|
|identifier|string|optional|A unique machine-readible identifier whose purpose will vary by event, but generally is used to differentiate one "thing" (form, link, video) from another. See https://schema.org/identifier.|unique-identifier|
|link_url|string|required|The HREF of the link interacted with.|https://www.yoursite.com/yourpath|
|link_id|string|required|The HTML ID of the link interacted with.|html-id-goes-here|
|link_classes|string|required|The list of HTML classes of the link interacted with.|html-classes-go-here|
|link_text|string|required|The text of the link interacted with.|Apply Now >>|
|navigation_ancestry|string|optional|A hierarchical list of all navigation (menu) links that a link is contained within. Generally used within dropdown/mega menus to show the path to the menu item clicked.|About Us>Testimonials|
|outbound|boolean|recommended|Set to "true" to indicate that the user clicked on an exit link|FALSE|
|region_ancestry|string|optional|A hierarchical list of all regions that a link is contained within.|header|