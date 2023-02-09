# Scroll Milestone

Automatically fired when a user scrolls to the bottom of the page.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'scroll',
  eventModel: {
    count_scroll: 1,
  }
});
```