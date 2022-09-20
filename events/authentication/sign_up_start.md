# Sign Up Start

Fire whenever a user begins filling out an account creation form.

Generally triggered via an HTML change, focus, or click event [listener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) on `input`, `textarea`, and `radio` elements.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'sign_up_start'
  eventModel: {
    count_sign_up_start: 1,
    method: '<method>'
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|method|string|recommended|The method by which a user creates a new account.|email-password, google, facebook, github, oauth|