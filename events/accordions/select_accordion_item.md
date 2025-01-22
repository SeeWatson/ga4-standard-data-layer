# Select Accordion Item

Fired when a user selects/expands a specific accordion item.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "select_accordion_item",
  eventModel: {
    count_select_accordion_item: 1,
    name: "<name>",
    index: "<index>",
  }
});
```

## Variable Definitions
|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|name|string|recommended|The human-readible accordion name.|Specifications|
|index|integer|recommended|The numerical index of the item position (1-indexed). For instance, if this is the 5th accordion item, you would send 5 here.|`5`|
