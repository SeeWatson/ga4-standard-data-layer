# User Detect

This is an optional event that is intended to cover cases where a user authentication system exists on the site but the user authentication state may not be known by the time the page_view event nees to be sent.

One use case is in a single page app where the authentication module is loaded asynchronously. We cannot be sure when the module will load (or if it will load) and we may want to send a page_view quickly to ensure that the visit is captured. Granted, that page_view would not be associated with the user, but this sort of tradeoff is common in implementations. In that case, we would send this event as soon as the authentication module completes loading to re-fire the configuration tag and set the `user_login_state` and `user_id`.

Another use case would be on a site that doesn't acttually offer authentication but does offer conversion forms that send to a CRM system that can return a `user_id`. When a user fills out the conversion form, we retrieve the newly generated `user_id` and fire this event to capture that ID.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "user_detect",
  user_data: {
    user_id: "<user_id>",
    user_login_state: '<user_login_state>',
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|user_id|string|recommended|The user identifier|1234567890|
|user_login_state|string|contextual|Set on all events with the authentication status of the visitor.|authenticated, anonymous|