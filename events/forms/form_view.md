# Form View

Fire whenever a user is presented with a form on a page.

## HTML Data Attributes

This could be done with data attributes and detected via GTM at DOM Ready, but if a form is dynamically added to the page at any time, it would not be picked up. As such, manually firing the data layer push whenever a form is loaded is a more reliable approach.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: 'form_view',
  eventModel: {
    category: '<category>',
    identifier: '<identifier>',
    name: '<name>',
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|category|string|recommended|A human-readible identifier whose purpose will vary by event, but generally is used to group things (forms, links, videos) into loose assocations based upon shared characteristics. If running low on custom dimensions, you may combine multiple categories together in this field, separated by greater than (>) or slash (/). See https://schema.org/category.|Job Application|
|identifier|string|recommended|The form machine-readable name. This should be a unique value specific to this form, if one exists. If one does not exist, this can also be populated with the same value as the <name>.|form-12345|
|name|string|required|The form human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the form with. It should be lowercase snake_case.|Caregiver 1078 Application