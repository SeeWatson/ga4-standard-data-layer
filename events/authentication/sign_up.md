# Sign Up

Fire whenever a user successfully creates an account.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'sign_up',
  eventModel: {
    method: '<method>'
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|method|string|recommended|The method by which a user created a new account.|local, social_login|

