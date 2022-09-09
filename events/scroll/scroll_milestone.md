# Scroll Milestone

Fire when a user scrolls past a certain scroll depth. The built-in `scroll` event can be set up to automatically on 90% scroll depth, but this event will allow for more milestones to be recorded.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'scroll_milestone',
  eventModel: {
    milestone: '<milestone>'
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|milestone|string|required|The depth to which user scrolled on the page.|25,50,75|
