# Click event data attributes

These data attributes can be added to site components, regions, and navigation links to provide additional context to click events that take place within them.

## All site regions and components
It is recommend to add these HTML attributes to the topmost HTML element of each component and region on a site so code can be written to quickly retrieve all the ancester components and regions for a specific clicked link.

```html
<div
  data-layer-component="<component>"
  data-layer-region="<region>"
>
```

## Navigation links
It is recommended to add the `data-layer-menu_item` parameter to the HTML `<li>` that wraps each menu item so code can be written to quickly retrieve all the ancester menu items for a specific clicked link.

```html
<li
  data-layer-menu_item="<menu_item>"
>
  <a>...</a>
</li>
```