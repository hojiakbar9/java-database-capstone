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