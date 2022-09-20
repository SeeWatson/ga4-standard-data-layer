# Sign Up

Fire whenever a user successfully creates an account.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  "event": 'sign_up',
  "eventModel": {
    "count_sign_up": 1,
    "method": '<method>'
  }
  "userModel": {
    "user_id": "<user_id>",
    "user_login_state": '<user_login_state>',
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|method|string|recommended|The method used to login.|email-password, google, facebook, github, oauth|
|user_id|string|recommended|The user identifier|1234567890|
|user_login_state|string|contextual|Set on all events with the authentication status of the visitor.|authenticated, anonymous|
