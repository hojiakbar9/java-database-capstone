## MySQL Database Design

### Table: patients
- id: INT, PRIMARY KEY, AUTOINCREMENT
- first_name: VARCHAR(100), NOT NULL
- last_name: VARCHAR(100), NOT NUL
- date_of_birth: DATE, NOT NULL
- email: VARCHAR(255), NOT NULL UNIQUE
- phone_number: VARCHAR(255), NOT NULL, UNIQUE
- address: VARCHAR(255)
- created_at: DATETIME NOT NULL, DEFAULT CURRENT_TIMESTAMP

### Table: doctors
- id: INT, PRIMARY KEY, AUTOINCREMENT
- first_name: VARCHAR(100), NOT NULL
- last_name: VARCHAR(100), NOT NULL
- specialization: VARCHAR(100), NOT NULL
- licence_number: VARCHAR(50), NOT NULL, UNIQUE
- email: VARCHAR(255), NOT NULL, UNIQUE
- is_active: BOOLEAN, NOT NULL, DEFAULT TRUE


### Table: admins
- id: INT, PRIMARY KEY, AUTOINCREMENT
- first_name: VARCHAR(255), NOT NULL
- last_name: VARCHAR(255), NOT NULL
- email: VARCHAR(255), NOT NULL

### Table: appointments
- id: INT, PRIMARY KEY, AUTO INCREMENT
- doctor_id: INT, FOREIGN KEY → doctors(id), NOT NULL
- patient_id: INT, FOREIGN KEY → patients(id), NOT NULL
- start_time: DATETIME, NOT NULL
- end_time: DATETIME, NOT NULL
- status: ENUM(Scheduled, Completed, Canceled), NOT NULL, DEFAULT 'Scheduled'
- reason_for_visit: TEXT

  Foreign Key Policy: If a patient is deleted, their past appointments should be retained (for legal/historical records),
  so the foreign key should use ON DELETE SET NULL for patient_id. If a doctor is deleted (rare, usually just deactivated),
  their appointments should remain as historical records.


### Table: doctor_availability
- id: INT, PRIMARY KEY, AUTO INCREMENT
- doctor_id: INT, FOREIGN KEY → doctors(id), NOT NULL
- start_time: DATETIME, NOT NULL
- end_time: DATETIME, NOT NULL
- status: ENUM(Scheduled, Completed, Canceled), NOT NULL, DEFAULT 'Scheduled'
- reason_for_visit: TEXT



## MongoDB Collection Design

### Collection prescriptions
This collection is designed for the flexible, potentially rich, and frequently updated data associated with a prescription, 
allowing for nested documents and arrays for complex drug regimens and history.

```json
{
  "_id": "ObjectId('655a9c9f6a7d8e9f01234567')",
  "prescription_uuid": "PRX-20251107-001234", // Unique identifier for external tracking
  "appointment_id": 12345, // Reference to the MySQL appointments table (core link)
  "patient_id": 501,       // Reference to the MySQL patients table
  "doctor_id": 105,        // Reference to the MySQL doctors table
  "date_prescribed": "ISODate('2025-11-07T14:00:00Z')",
  "status": "Active", // e.g., 'Active', 'Filled', 'Expired', 'Cancelled'

  "medications": [ // Array to handle multi-drug prescriptions or complex regimens
    {
      "drug_name": "Amoxicillin",
      "strength": "500mg",
      "form": "Capsule",
      "quantity_dispensed": 21,
      "refill_count": 0,
      "instructions": {
        "sig": "Take one capsule by mouth three times daily.",
        "duration_days": 7,
        "notes": "Take with food to avoid stomach upset."
      },
      "tags": ["antibiotic", "oral"]
    },
    {
      "drug_name": "Cetirizine",
      "strength": "10mg",
      "form": "Tablet",
      "quantity_dispensed": 30,
      "refill_count": 3,
      "instructions": {
        "sig": "Take one tablet once daily at bedtime.",
        "duration_days": 30,
        "notes": ""
      },
      "tags": ["antihistamine", "chronic"]
    }
  ],

  "pharmacy_details": {
    "pharmacy_name": "CVS Pharmacy - Main Street",
    "npi": "1234567890",
    "contact_phone": "555-123-4567",
    "delivery_required": false
  },

  "history": [ // Tracking refills and status changes
    {
      "event": "Prescription Sent to Pharmacy",
      "timestamp": "ISODate('2025-11-07T14:05:00Z')"
    },
    {
      "event": "Refill Request Approved (Refill 1)",
      "timestamp": "ISODate('2025-12-07T09:15:00Z')"
    }
  ],
  "metadata": {
    "version": "1.0.1",
    "external_system_id": "EPCS-98765" // Link to an e-Prescribing system ID
  }
}
```