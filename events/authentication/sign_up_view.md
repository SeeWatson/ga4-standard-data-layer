# Sign Up View

Fire whenever a user initially views an account creation form.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'sign_up_view'
  eventModel: {
    count_sign_up_view: 1,
    method: '<method>'
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|method|string|recommended|The method by which a user creates a new account.|email-password, google, facebook, github, oauth|