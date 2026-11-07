# Requirements Engineering and Traceability

The source project sets requirements for a proposed Student Management System, with a traceability matrix separating **functional** features from **non-functional** quality attributes.

## Functional capabilities
- Account login, registration, recovery and approval.
- Programme application, document submission, eligibility verification and acceptance notification.
- Programme enrolment after review and payment confirmation.
- Course enrolment with prerequisites, seat availability, academic-year restrictions and timetable conflicts.
- Course content, grades and attendance views.
- Tutor attendance marking and assessment records.
- Admin maintenance of users, courses and programme information.
- Auditor reporting, export, merging and validation.

## Non-functional capabilities
Usability, mobile/browser compatibility, uptime/availability, support for many simultaneous users, privacy, encryption, reliable backups, maintainability and extensibility.

## Traceability principles learned
A requirement should be traceable from stakeholder need to use case, design and planned acceptance test. For example, **course seats must be available** maps to the enrolment use case, to the course selection interface and to a test that rejects full classes; **role-based management access** maps to actor permissions and negative tests that prevent student access to admin functions.

The matrix describes **proposed requirements**, not measured system performance or a verified database implementation.

## Key learning
Functional requirements explain *what* a system does; non-functional ones describe *how well and under what constraints*. Terms like "secure" and "fast" require operational definitions and measurable acceptance criteria. No personal identities or student numbers from the source appear here.