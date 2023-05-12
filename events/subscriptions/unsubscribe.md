# Unsubscribe

Fire whenever a user unsubscribes from something. This typically is used for subscriptions to email lists, but could actually represent terminating any subscription.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'unsubscribe',
  eventModel: {
    category: '<category>',
    identifier: '<identifier>',
    name: '<name>',
    method: '<method>'
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|category|string|recommended|A human-readible identifier whose purpose will vary by event, but generally is used to group things (forms, links, videos) into loose assocations based upon shared characteristics. If running low on custom dimensions, you may combine multiple categories together in this field, separated by greater than (>) or slash (/). See https://schema.org/category.|newsletter, updates, advocacy|
|identifier|string|recommended|The subscription machine-readable name. This should be a unique value specific to this subscription, if one exists. If one does not exist, this can also be populated with the same value as the `name`.|newsletter_123|
|name|string|required|The subscription human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the subscription with. It should be lowercase snake_case.|whatever_newsletter|
|method|string|recommended|The channel through which the subscription is delivered. This is usually email.|email|
