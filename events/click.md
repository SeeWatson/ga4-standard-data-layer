# Click

This event will be automatically sent whenever a user clicks on an HTML anchor `<a>` tag.

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
|category|string|optional|A human-readible identifier whose purpose will vary by event, but generally is used to group things (forms, links, videos) into loose assocations based upon shared characteristics. If running low on custom dimensions, you may combine multiple categories together in this field, separated by greater than (>) or slash (/). See https://schema.org/category.||
|component_ancestry|string|optional|A hierarchical list of all components that a link is contained within|main>hero>cta-box|
|identifier|string|optional|A unique machine-readible identifier whose purpose will vary by event, but generally is used to differentiate one "thing" (form, link, video) from another. See https://schema.org/identifier.|unique-identifier|
|link_url|string|required|The HREF of the link interacted with.|https://www.comfortkeepers.com/download.pdf|
|link_id|string|required|The HTML ID of the link interacted with.|html-id-goes-here|
|link_classes|string|required|The list of HTML classes of the link interacted with.|html-classes-go-here|
|link_text|string|required|The text of the link interacted with.|Apply Now >>|
|navigation_ancestry|string|optional|A hierarchical list of all navigation (menu) links that a link is contained within. Generally used within dropdown/mega menus to show the path to the menu item clicked.|About Us>Testimonials|
|outbound|boolean|recommended|Set to "true" to indicate that the user clicked on an exit link|FALSE|
|region_ancestry|string|optional|A hierarchical list of all regions that a link is contained within.|header|






