# Logout

Fire whenever a user logs out of an account.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({ user_data: null });  
dataLayer.push({
  event: "logout",
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
|user_id|string|recommended|The user identifier|1234567890|
|user_login_state|string|contextual|Set on all events with the authentication status of the visitor.|anonymous|
