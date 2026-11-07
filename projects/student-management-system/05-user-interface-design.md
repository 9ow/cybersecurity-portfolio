# User Interface Design — Academic System Mockups

The submitted document shows interface **design mockups**, not a running deployed application.

## Programme application
A two-part application form collects applicant data, selected programme and later supporting documents. It separates basic details from document uploads and shows navigation between pages.

**Learning:** Use progressive disclosure, clearly mark required fields, validate user inputs, safely handle uploads and show state when the user moves between form pages.

## Programme enrolment
Screens demonstrate a multi-stage journey: **Select Programme → Upload Documents → Payment → Review and Submit**. A progress indicator helps students know what is complete and what remains. The flow also shows payment options and confirmation of selected programme details.

**Learning:** Users need validation and a clear review step before a consequential action such as payment or enrolment. The visual payment page is not proof a real payment gateway exists.

## Course enrolment
A course-selection screen includes major, term and subject, with filtering for classes with spare seats. A second screen lists sections and schedule/seat information and provides enrolment actions.

**Learning:** Seat availability and timetable conflicts must be checked by the backend during confirmation, not just conveyed through a green button.

## Attendance
A tutor chooses course, section and session date, loads a student roster and marks attendance. The design shows **Present**, **Absent** and **Late**, then a submit action.

**Learning:** Ensure only authorized staff can update the right section; validate that every required attendance status is selected and record changes for audit purposes.

## Login / registration
The source contains a login mockup with username and password fields. Other project narratives add administrator approval and email-based activation to the account lifecycle.

**Learning:** A design for a password field does not prove secure authentication; encryption, hashing, login throttling and recovery must be designed and validated separately.

## Privacy
The original pages show identifying organization/member information and potentially personal data. No original UI screenshots have been copied here. These textual notes describe technical design and usability decisions instead.
