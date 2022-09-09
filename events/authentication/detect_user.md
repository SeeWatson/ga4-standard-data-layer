# Detect User

This is a conditional event that should only be fired in very specific cases. It is intended to cover cases where a user authentication system exists on the site but the user authentication state may not be known by the time the page_view event is sent. In that case, send this event as soon as the user authentication state or ID is known.

For instance, send this after a Salesforce conversion form is submitted as the user id becomes known at that point.

Do not clear the page_data variable before setting user_login_state here as this is not a page view.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "detect_user",
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
|user_login_state|string|contextual|Set on all events with the authentication status of the visitor.|authenticated, anonymous|