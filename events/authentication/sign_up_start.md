# Sign Up Start

Fire whenever a user views the first step of the account creation form.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'sign_up_start'
  eventModel: {
    method: '<method>'
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|method|string|recommended|The method by which a user created a new account.|local, social_login|