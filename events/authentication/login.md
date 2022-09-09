# Login

Fire whenever a user logs in to an account.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "login",
  eventModel: {
    method: "<method>",
  },
  page_data: {
    user_login_state: '<user_login_state>',
  },
  user_data: {
    user_id: "<user_id>",
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|method|string|recommended|The method used to login.|google, linkedin, email and password|
|user_id|string|recommended|The user identifier|1234567890|
|user_login_state|string|contextual|Set on all events with the authentication status of the visitor.|authenticated, anonymous|
