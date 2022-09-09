# Job Application Complete

Fire whenever a user completes a job application. 

## Javascript Code

```js

window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({
  "event": "job_application_complete",
  "eventModel": {
    "hiring_organization": "<hiring_organization>",
    "identifier": "<identifier>",
    "method": "<method>",
  }
})
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|hiring_organization|object|recommended|Organization offering the job position. See https://schema.org/hiringOrganization.|`{"@type": "Organization", "name": "Comfort Keepers Home Care", "sameAs": "https://www.comfortkeepers.com/offices/north-carolina/greensboro", "logo": "https://www.comfortkeepers.com/assets/logo.png"}`|
|identifier|string|recommended|A unique machine-readible identifier whose purpose will vary by event, but generally is used to differentiate one "thing" (form, link, video) from another. See https://schema.org/identifier.|ckfi:56f9dd7d-80e6-445c-b638-4e1759789077|
|method|string|recommended|The method by which a user is applying|webform,phone,chat|