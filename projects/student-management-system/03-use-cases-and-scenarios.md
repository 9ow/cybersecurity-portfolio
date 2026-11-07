# Actors and Five Detailed Use Cases

## Actors and supporting services
The submitted actor glossary identifies **Student, Admin, Tutor, Auditor** and a general authenticated User. Students handle applications, enrolment, transcripts and notifications. Admins manage users and approve registration; tutors manage attendance; auditors create reports. The use-case glossary also includes login, payment, prerequisite checks, seat availability, uploaded documents, reports and account activation.

A use-case narrative records **trigger, preconditions, normal actor actions, system responses, alternate/exception flows, postconditions, business rules, assumptions and open issues**.

## 1. Application to Programme
**Goal:** Submit an application and supporting academic documents for review.
**Main flow:** Open the system, submit registration details, validate the input, proceed to a programme application, enter application information, upload academic evidence, submit, receive an administrative decision and notification.
**Exceptions:** Invalid initial details, incomplete application or incorrect upload require corrections; the narrative raises the possibility of reminders and application tracking.
**Lesson:** Separate initial account identity, programme application and final approval. Files with identity documents require protection and input validation.

## 2. Enrol to Programme
**Goal:** Official programme enrolment.
**Preconditions:** Authenticated account, maintained programme data and a functioning payment method.
**Main flow:** Choose programme, check requirements, upload documents, complete payment, enter review, obtain administrative/academic decision, update status and notify the student.
**Exceptions:** Ineligibility, programme full, wrong/missing documents, payment failure and tutor rejection.
**Lesson:** Approval and payment are separate states. Failed payment should not silently create a final enrolment record.

## 3. Enrol to Course
**Goal:** Register in one or more available courses for the selected academic term.
**Main flow:** Log in, select term and courses, examine availability, confirm, verify prerequisites, academic-year restrictions, seat capacity and timetable collisions; store enrolment, update timetable and send confirmation.
**Exceptions:** Wrong credentials, wrong term, unavailable data, invalid eligibility or timetable conflict, and full sections with waitlist handling.
**Lesson:** A registration transaction should be consistent, especially if multiple students attempt to claim the final seat concurrently.

## 4. Record Attendance
**Goal:** A tutor marks the students assigned to a course session.
**Main flow:** Log in, choose course/section/date, display roster, mark Present/Absent/Late, validate every status, save and update absence totals.
**Exceptions:** An unassigned section is denied; an incomplete roster is rejected; cancelled or unavailable course data requires explanation.
**Business rules:** Attendance thresholds and automated notices are defined in the design, not measured as working production behavior.
**Lesson:** Restrict tutors to their own sections and preserve an accurate audit trail.

## 5. Registration / Sign-up
**Goal:** Create and activate a verified account.
**Main flow:** Select user type, enter unique email and strong credentials, submit, queue admin verification, send a time-limited activation link and permit login after successful activation.
**Exceptions:** Missing data, duplicate email, rejected approval, expired link and server outage.
**Lesson:** Registration, review, activation and authentication are different states. Multi-factor authentication is a proposed open question, not a proven implemented feature.

## What I demonstrated
Across all five narratives I documented the success path, failure paths and outcome requirements. These are **completed design narratives within an academic project**, not proof of executing a live application. No participant names or other identifying information are reproduced.