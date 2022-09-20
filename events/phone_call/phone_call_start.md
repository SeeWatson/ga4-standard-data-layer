# Phone call start

Fire whenever a user starts a phone call using a provider like Invoca, CallRail, or others.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'phone_call_start',
  eventModel: {
    "telephone": '<telephone>',
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|telephone|string|recommended|The telephone number dialed. Used to distinguish dynamically generated numbers.|1234567890|^\d{10}$|