# Form Error

Fire whenever a user unsuccessfully completes a form. 

This is in contrast to `form_complete` which occurs when a submission succeeds.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'form_error',
  eventModel: {
    category: '<category>',
    error_message: '<error_message>',
    identifier: '<identifier>',
    name: '<name>',
    type: '<type>'
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|error_message|string|required|The specific error that occurred. If an error message is shown to the user, this should be populated with that text.|Phone number should follow the format (xxx) xxx-xxxx, Must be a valid email address|
|category|string|recommended|A human-readible identifier whose purpose will vary by event, but generally is used to group things (forms, links, videos) into loose assocations based upon shared characteristics. If running low on custom dimensions, you may combine multiple categories together in this field, separated by greater than (>) or slash (/). See https://schema.org/category.|Job Application|
|identifier|string|recommended|The form machine-readable name. This should be a unique value specific to this form, if one exists. If one does not exist, this can also be populated with the same value as the <name>.|form-12345|
|name|string|required|The form human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the form with. It should be lowercase snake_case.|Caregiver 1078 Application||type|string|recommended|The type of error that occurred.|form_field_validation, server_error|
