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
