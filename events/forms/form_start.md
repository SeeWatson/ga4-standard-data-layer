# Form Start

Fire whenever a user starts filling out a form. 

This event is generally fired after user input in the first form field. Historically this has been done via an HTMLElement change event on a form field, though it could be done via an HTMLElement focus event on a form field instead if that proves easier to implement. It should only be fired once per form, but if that is too technically complicated to implement, it can be limited on the GTM side instead.

## HTML Data Attributes

This could be done with data attributes and detected via GTM at DOM Ready, but if a form is dynamically added to the page at any time, it would not have the listeners properly set up. As such, manually firing the data layer push whenever a form is submitted is a more reliable approach.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'form_start',
  eventModel: {
    category: '<category>',
    count_form_start: 1,
    identifier: '<identifier>',
    name: '<name>',
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|category|string|recommended|A human-readible identifier whose purpose will vary by event, but generally is used to group things (forms, links, videos) into loose assocations based upon shared characteristics. If running low on custom dimensions, you may combine multiple categories together in this field, separated by greater than (>) or slash (/). See https://schema.org/category.|Registration Form|
|identifier|string|recommended|The form machine-readable name. This should be a unique value specific to this form, if one exists. If one does not exist, this can also be populated with the same value as the `<name>`.|form-12345|
|name|string|required|The form human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the form with. It should be lowercase snake_case if possible.|event_registration_form|