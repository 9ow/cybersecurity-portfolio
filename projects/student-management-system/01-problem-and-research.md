# Business Problem, Service Request and Stakeholder Research

## Existing problem
The source report describes a growing academic institution whose existing student-management processes require too much manual administrative work and are not handling increasing enrolment volume efficiently. A replacement student-management system was proposed to make student registration, admissions, programme/course enrolment and attendance more reliable, manageable and scalable.

## Service request and expected value
The service-request form proposes replacing or modernizing the student-management capability. The expected benefits are reduced routine manual processing, more structured data storage, better information exchange between staff and students, easier reporting and more reliable administration.

**Important distinction:** A service request establishes a business need and a proposed response; it does not by itself demonstrate the future system has already been developed.

## Stakeholders and actors
The analysis distinguishes:
- **Students:** register, submit applications, enrol in programmes and courses, pay fees, view academic information and receive notifications.
- **Administrative staff:** review applications, manage users and courses, activate accounts and maintain information.
- **Tutors:** manage course activities and record attendance.
- **Auditors:** generate, validate and export records and reports.
- **Generic user:** common authentication behavior across roles.

**What I learned:** An actor in a UML use-case diagram describes a role interacting with a system, not a specific individual or necessarily a separate database table.

## Problem analysis with Ishikawa / cause-and-effect diagram
The report uses an Ishikawa (fishbone) diagram focused on inefficiency in student-management processes. Factors considered include people/staff load, processes and methods, technology/infrastructure, training and environmental/organizational issues.

Instead of labeling a visible problem as a single root cause, cause-and-effect analysis encourages looking for contributing factors such as manual data handling, lack of consistent procedures, insufficient training or inadequate system support.

## Stakeholder interview and elicitation
An interview template in the report explores additional system-module priorities, whether the application should be limited to the institution, forgotten-password procedures, verification of identity and inactivity-session logout. Such discussions translate stakeholder preferences into concrete security and usability requirements.

**Learning:** Interviews can expose ambiguous statements such as "make the system secure" or "log out after inactivity." The analyst should resolve these into explicit requirements: who can reset credentials, what verification is necessary, and what timeout is acceptable.

## Source areas
Service request: source report's opening section; Ishikawa diagram: early problem-analysis section; interview template: later requirements-gathering section. Personal names, roles associated with named people and direct contact details were omitted.
