# Generate lead

Fire whenever a lead is generated from a user action. This could be through a form submission, chat session, or phone call.

## Javascript Code
```js

window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({
  "event": "generate_lead",
  "eventModel": {
    "currency": "<currency>",
    "category": "<category>",
    "value": "<value>"
  }
})
```

## Variable Definitions
|currency|string|recommended|The currency, in 3-letter ISO 4217 format. Multiple currencies per event is not supported. Each item within the items array should set the same currency.
|USD|
|category|string|recommended|A human-readible identifier whose purpose will vary by event, but generally is used to group things (forms, links, videos) into loose assocations based upon shared characteristics. If running low on custom dimensions, you may combine multiple categories together in this field, separated by greater than (>) or slash (/). See https://schema.org/category.|qualified|
|value|number|recommended|For the "purchase" event this is the total revenue after coupons, but before tax and shipping.|100|