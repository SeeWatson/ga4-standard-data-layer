# Job Application Start

Fire whenever a user views a job.

## Javascript Code

```js

window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({
  event: "job_view",
  eventModel: {
    count_job_view: 1,
    date_posted: "<date_posted>",
    description: "<description>",
    employment_type: "<employment_type>",
    hiring_organization: "<hiring_organization>",
    identifier: "<identifier>",
    job_location: "<job_location>",
    title: "<title>",
    "@type": "<@type>"
  }
})
```

## Variable Definitions
|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|date_posted|string|recommended|Publication date of an online listing. See https://schema.org/datePosted.|2022-09-19|
|description|string|recommended|A description of the item. See https://schema.org/description.|Google's software engineers develop the next-generation technologies that change how billions of users connect, explore, and interact with information and one another. Our products need to handle information at massive scale, and extend well beyond web search. We're looking for engineers who bring fresh ideas from all areas, including information retrieval, distributed computing, large-scale system design, networking and data storage, security, artificial intelligence, natural language processing, UI design and mobile; the list goes on and is growing every day. As a software engineer, you will work on a specific project critical to Google’s needs with opportunities to switch teams and projects as you and our fast-paced business grow and evolve. We need our engineers to be versatile, display leadership qualities and be enthusiastic to take on new problems across the full-stack as we continue to push technology forward.|
|employment_type|string|recommended|Type of employment (e.g. full-time, part-time, contract, temporary, seasonal, internship). See https://schema.org/employmentType.|full-time|
|hiring_organization|object|recommended|Organization offering the job position. See https://schema.org/hiringOrganization.|`{"@type": "Organization", "name": "Google", "sameAs": "https://www.google.com", "logo": "https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png"}`|
|identifier|string|recommended|A unique machine-readible identifier whose purpose will vary by event, but generally is used to differentiate one "thing" (form, link, video) from another. See https://schema.org/identifier.|`108589376369238726-software-engineer-silicon`|
|job_location|object|recommended|A (typically single) geographic location associated with the job position. See https://schema.org/jobLocation.|`{"@type": "Place","address": {  "@type": "PostalAddress",  "streetAddress": "1600 Amphitheatre Parkway",  "addressLocality": "Mountain View",  "addressRegion": "CA",  "postalCode": "94043",  "addressCountry": "US"}}`|
|title|string|required|The human-readible title. When used in a page_view event to represent the page title, this should be set to document.title.|Analytics Engineer|
|@type|string|recommended|The schema.org type for this event. For instance, for a page_view event, the page being viewed is a WebPage, but it could also be a more specific subtype like AboutPage or event a custom type your organization creates such as HomePage. Differs from type in that "@type" always should be populated with a schema.org type, while "type" can be populated with arbitrary values.|JobPosting|