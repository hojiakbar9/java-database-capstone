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