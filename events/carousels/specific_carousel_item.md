# Specific Carousel Item

Fired whenever a user manually selects a specific carousel item.

## Javascript Code

```js
window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "specific_carousel_item",
  eventModel: {
    count_specific_carousel_item: 1,
    identifier: "<identifier>",
    name: "<name>",
  },
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|identifier|string|recommended|The carousel machine-readable name. This should be a unique value specific to this carousel, if one exists. If one does not exist, this can also be populated with the same value as the `<name>`.|carousel-12345|
|name|string|recommended|The carousel human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the carousel with. It should be in regular sentence case or capital case.|Carousel 12345|