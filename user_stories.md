## Admin User Stories

**Secure Login**

_As an Admin, I want to log into the portal with my username and password so that I can securely access and manage the platform._

**Acceptance Criteria:**
1.  The system must validate the entered username and password against stored credentials.
2. If credentials are valid, the system redirects the Admin to the main dashboard.
3. If credentials are invalid, the system displays an error message ("Invalid username or password") and keeps the Admin on the login page.

**Priority:** High

**Story Points:** 3

**Notes:**
- Password should be hashed and securely stored.

**Secure Logout**

_As an Admin, I want to log out of the portal, so that I can terminate my session and protect system access from unauthorized users._

**Acceptance Criteria:**
1. A "Logout" button must be prominently displayed on every secured page.
2. Clicking "Logout" must invalidate the current session on the server.
3. Upon successful logout, the user is redirected to the public login page.

**Priority:** High

**Story Points:** 2

**Notes:**
- Logout must be instantaneous and clear all session cookies/tokens.

**Doctor Addition**

_As an Admin, I want to add a new Doctor's profile to the portal so that they can begin scheduling appointments and accessing their dashboard._

**Acceptance Criteria:**
1. The Admin must access a dedicated "Add Doctor" form.
2. The form must include mandatory fields for the Doctor's name, email, specialty, and an initial password.
3. Upon successful submission, the system must create the new Doctor's record in the database.

**Priority:** High

**Story Points:** 5

**Notes:**
- Email must be validated for unique existence before creation.

**Doctor Removal**

_As an Admin, I want to delete a Doctor's profile from the portal so that they no longer have system access and their information is removed or deactivated._

**Acceptance Criteria:**
1. The Admin can search for and select an existing Doctor's profile.
2. The system must display a confirmation dialog before deletion.
3. Upon confirmation, the Doctor's user account is deactivated/deleted, and all associated records (appointments, etc.) are handled according to data retention policy.

**Priority:** Medium

**Story Points:** 5

**Notes:**
- Implement a soft-delete mechanism (setting an is_active=false flag) instead of hard-deleting the record, for historical data integrity.

**Usage Tracking**

_As an Admin, I want to run a stored procedure in the MySQL CLI to retrieve the number of appointments per month so that I can track usage statistics and analyze trends in platform utilization._

**Acceptance Criteria:**
1. A dedicated stored procedure (e.g., sp_get_monthly_appointments) must exist in the MySQL database.
2. Executing the stored procedure in the MySQL CLI must return a result set with two columns: appointment_month (e.g., YYYY-MM) and appointment_count.
3. The results must accurately reflect all appointments confirmed/completed within the specified date range.

**Priority:** Medium

**Story Points:** 8

**Notes:**
- The stored procedure should be optimized for performance.


## Patient User Stories

**Doctor Browsing**

_As a Patient, I want to view a list of available doctors without logging in, so that I can explore options and specialties before deciding to register._

**Acceptance Criteria:**
1. The home page or a dedicated "Find a Doctor" page is publicly accessible (no authentication required).
2. The list displays essential doctor information (Name, Specialty, Location, Availability Status).
3. The list can be filtered or searched by specialty or name.

**Priority:** High

**Story Points:** 3

**Notes:**
- Booking actions should be disabled or prompt the user to register/login.
- Only non-sensitive, public profile details should be displayed.

**Patient Registration**

_As a Patient, I want to sign up using my email and password, so that I can create an account and gain the ability to book appointments._

**Acceptance Criteria:**
1. The system provides a clear "Sign Up" form requiring email, password, and basic personal information (e.g., name, date of birth).
2. The system validates the email address for correct format and uniqueness.
3. Upon successful registration, the user receives a confirmation email and is logged in or redirected to the login page.

**Priority:** High

**Story Points:** 5

**Notes:**
- Password must meet minimum complexity requirements (length, characters).
- Password should be securely hashed and stored (Data Tier concern).

**Account Access**

_As a Patient, I want to log into the portal using my credentials, so that I can securely access and manage my bookings and personal health information._

**Acceptance Criteria:**
1. The system validates the entered email and password against stored patient credentials.
2. Upon successful validation, the user is redirected to the Patient Dashboard.
3. Error messages are provided for incorrect credentials or deactivated accounts.

**Priority:** High

**Story Points:** 3

**Notes:**
- Must use the same authentication mechanism as the Admin login

**Secure Account Exit**

_As a Patient, I want to log out of the portal, so that I can terminate my session and secure my account._

**Acceptance Criteria:**
1. A "Logout" option is available in the user profile menu.
2. Clicking "Logout" invalidates the current session token/cookie.
3. The user is redirected to the public home page or login page.

**Priority:** High

**Story Points:** 2

**Notes:**
- A security check should prevent access to protected routes after logging out.

**Appointment Booking**

_As a Patient, I want to log in and book an hour-long appointment with a doctor so that I can consult with a medical professional regarding my health concerns._

**Acceptance Criteria:**
1. The user must be logged in to access the booking functionality.
2. The system displays a calendar/list of available 60-minute time slots for the selected doctor.
3. Upon selection and confirmation, the system creates a new appointment record in the database, and reduces the doctor's availability.
4. The patient receives an immediate confirmation on screen and via email.

**Priority:** High

**Story Points:** 8

**Notes:**
- Requires real-time availability checking against the Doctor's schedule.
- The default duration for this appointment must be 60 minutes.


## Doctor User Stories

**Secure Account Access**

_As a Doctor, I want to log into the portal with my credentials so that I can access and manage my appointments and professional schedule._

**Acceptance Criteria:**
1. The system validates the entered credentials against the stored Doctor accounts.
2. If successful, the system redirects the Doctor to their main dashboard/calendar view.
3. If validation fails, an appropriate error message is displayed, and access is denied.

**Priority:** High

**Story Points:** 3

**Notes:**
- Authentication mechanism should be consistent with Admin and Patient roles.

**Secure Account Exit**

_As a Doctor, I want to log out of the portal, so that I can terminate my session and protect my professional and patient data._

**Acceptance Criteria:**
1. A "Logout" option is easily accessible within the application interface.
2. Clicking "Logout" must invalidate the server-side session and related tokens.
3. The user is redirected to the public login page after logging out.

**Priority:** High

**Story Points:** 2

**Notes:**
- Implement a clear session termination process.

**Schedule Management**

_As a Doctor, I want to view my appointment calendar so that I can stay organized and efficiently manage my daily and weekly schedule._

**Acceptance Criteria:**
1. The calendar view clearly displays all scheduled appointments with patient names and times.
2. The view supports switching between Day, Week, and Month views.
3. Appointments are displayed in the time slot they occupy

**Priority:** High

**Story Points:** 5

**Notes:**
- Requires fetching data from the appointment records in the Data Tier.

**Availability Control**

_As a Doctor, I want to mark specific dates or time blocks as unavailable so that the booking system only presents valid appointment slots to patients._

**Acceptance Criteria:**
1. The Doctor can select a date range or recurring time period on their schedule.
2. The system allows the Doctor to designate this selected time as "Unavailable" (e.g., for vacation, surgery, meetings).
3. The booking engine automatically blocks these marked slots from being viewed or booked by patients.

**Priority:** High

**Story Points:** 8

**Notes:**
- Should handle both one-time and recurring unavailability.
- Requires updating the availability schedule record, which the Service Layer uses for booking logic.

**Profile Maintenance**

_As a Doctor, I want to update my profile with my specialization, contact information, and biography, so that patients have accurate and up-to-date information when searching and booking._

**Acceptance Criteria:**
1. The Doctor can access a dedicated "Edit Profile" page.
2. Changes made to specialization, contact details, and other public-facing information are immediately reflected in the publicly viewable Doctor List
3. The system validates the format of updated contact information (e.g., email, phone number).

**Priority:** High

**Story Points:** 5

**Notes:**
- Requires careful handling of data validation and persistence in the Data Tier.

