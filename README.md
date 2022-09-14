# GA4 Standard Data Layer Spec

The objective of this spec is to propose a standard data layer spec for Google Analtyics 4 (GA4) implementations.

## FAQs
<details>
  <summary>How was this spec developed?</summary>
  
  This data layer spec was initially developed while working across more than a dozen GA4 implementations. The spec takes Google's [automatically-collected](https://support.google.com/analytics/answer/9234069?hl=en) events, [enhanced measurement events](https://support.google.com/analytics/answer/9216061?hl=en&ref_topic=9756175), and [recommended events](https://support.google.com/analytics/answer/9267735?hl=en&ref_topic=9756175) and builds upon them to provide a data layer spec to send data in a standardized way.
</details>
<details>
  <summary>For custom events, what naming conventions did you use and why?</summary>

    1. Custom event and parameter names are all [snake_case](https://en.wikipedia.org/wiki/Snake_case), meaning all characters are lower-case and underscores separate words. This matches Google's conventions they used in their automatically-collected, enhanced measurement, and recommended events.

    2. Custom event names always contain a subject and a present tense verb. This matches Google's conventions. Exceptions can be made for semantically awkward event names.

    3. Custom event names take of the form of subject_verb. Google's predefined events are inconsistent in their ordering of the subject and verb (`tutorial_begin` vs `begin_checkout`, `generate_lead` vs `file_download`), so a choice had to be made as to which approach to use to ensure consistency. Given that events are generally sorted alphabetically in most systems, it seemed clustering events with the same subject would make for better findability and easier analysis, thus subject_verb was chosen. The decision could easily have gone the other way, so don't feel bound by this. Also, exceptions to the convention can be made for semantically awkward event names [see detect_user](events/authentication/detect_user).

</details>
