# Logout

Fire whenever a user logs out of an account.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({ user_data: null });  
dataLayer.push({
  event: "logout",
  userModel: {
    count_logout: 1,
    user_login_state: '<user_login_state>',
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|user_login_state|string|contextual|Set on all events with the authentication status of the visitor.|authenticated, anonymous|
