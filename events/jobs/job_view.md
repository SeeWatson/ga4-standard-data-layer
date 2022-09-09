# Job Application Start

Fire whenever a user views a job.

## Javascript Code

```js

window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({
  "event": "job_view",
  "eventModel": {
    "date_posted": "<date_posted>",
    "description": "<description>",
    "employment_type": "<employment_type>",
    "hiring_organization": "<hiring_organization>",
    "identifier": "<identifier>",
    "job_location": "<job_location>",
    "title": "<title>",
    "@type": "<@type>"
  }
})
```

## Variable Definitions
|date_posted|string|recommended|Publication date of an online listing. See https://schema.org/datePosted.|44594|
|description|string|recommended|A description of the item. See https://schema.org/description.|Here at Comfort Keepers of Atlanta, GA our expert caregivers’ provide a personalized in-home care experience for seniors and disabled individuals to remain independent and comfortable in their own homes. Comfort Keepers uses Interactive Caregiving to ensure our clients are receiving the best care possible.\n\nLearn more on how our Comfort Keepers In-home Caregivers are bringing comfort to home while providing companionship, respite care, and more.\n\nOur team is dedicated to caring for seniors and loved ones within their homes and ensuring their safety during everyday outings and errands.|
|employment_type|string|recommended|Type of employment (e.g. full-time, part-time, contract, temporary, seasonal, internship). See https://schema.org/employmentType.|full-time|
|hiring_organization|object|recommended|Organization offering the job position. See https://schema.org/hiringOrganization.|`{"@type": "Organization","name": "Comfort Keepers Home Care","sameAs": "https://www.comfortkeepers.com/offices/north-carolina/greensboro","logo": "https://www.comfortkeepers.com/assets/logo.png"}`|
|identifier|object|recommended|A unique machine-readible identifier whose purpose will vary by event, but generally is used to differentiate one "thing" (form, link, video) from another. See https://schema.org/identifier.|`{"@type": "PropertyValue","name": "Comfort Keepers Home Care","value": "ckfi:56f9dd7d-80e6-445c-b638-4e1759789077"}`|
|job_location|object|recommended|A (typically single) geographic location associated with the job position. See https://schema.org/jobLocation.|`{"@type": "Place","address": {  "@type": "PostalAddress",  "streetAddress": "1932 Fleming Rd",  "addressLocality": "Greensboro",  "addressRegion": "NC",  "postalCode": "27410",  "addressCountry": "US"}  }`|
|title|string|required|The human-readible title. When used in a page_view event to represent the page title, this should be set to document.title.|Caregiver|
|@type|string|recommended|The schema.org type for this event. For instance, for a page_view event, the page being viewed is a WebPage, but it could also be a more specific subtype like AboutPage or event a custom type your organization creates such as HomePage. Differs from type in that "@type" always should be populated with a schema.org type, while "type" can be populated with arbitrary values.|JobPosting|