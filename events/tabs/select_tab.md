# Select Tab

Fired when a user selects a specific tab out of a tab group.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "select_tab",
  eventModel: {
    count_select_tab: 1,
    name: "<name>",
    index: "<index>",
  }
});
```

## Variable Definitions
|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|name|string|recommended|The human-readible tab name.|Specifications|
|index|integer|recommended|The numerical index of the item position (1-indexed). For instance, if this is the 5th tab, you would send 5 here.|`5`|
