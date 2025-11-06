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