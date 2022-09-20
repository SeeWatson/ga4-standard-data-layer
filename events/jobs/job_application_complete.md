# Job Application Complete

Fire whenever a user completes a job application. 

## Javascript Code

```js

window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({
  event: "job_application_complete",
  eventModel: {
    count_job_application_complete: 1,
    hiring_organization: "<hiring_organization>",
    identifier: "<identifier>",
    method: "<method>",
  }
})
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|hiring_organization|object|recommended|Organization offering the job position. See https://schema.org/hiringOrganization.|`{"@type": "Organization", "name": "Google", "sameAs": "https://www.google.com", "logo": "https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png"}`|
|identifier|string|recommended|A unique machine-readible identifier whose purpose will vary by event, but generally is used to differentiate one "thing" (form, link, video) from another. See https://schema.org/identifier.|`108589376369238726-software-engineer-silicon`|
|method|string|recommended|The method by which a user is applying|`webform,phone,chat`|