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

### Collection clinical_records
This collection is designed to hold the medical notes, prescriptions, and any uploaded documents associated with an appointment. 
This data is often unstructured (notes) or has an evolving structure (prescriptions, test results).

```json
{
  "_id": "ObjectId('655a9c9f6a7d8e9f01234567')",
  "appointment_id": 12345, // Reference to the MySQL appointments table
  "patient_id": 501,       // Reference to the MySQL patients table
  "doctor_id": 105,        // Reference to the MySQL doctors table
  "record_type": "Consultation_Notes", // 'Consultation_Notes', 'Lab_Results', 'Prescription', 'Procedure_Summary'
  "created_at": "ISODate('2025-11-20T10:30:00Z')",
  "last_updated": "ISODate('2025-11-20T11:45:00Z')",
  "doctor_notes": {
    "chief_complaint": "Persistent headache for 3 days.",
    "hpi": "Symptoms began gradually. No fever. Denies trauma.",
    "assessment": "Migraine without aura, likely stress-induced.",
    "plan": "Hydration, rest, and new prescription.",
    "tags": ["headache", "migraine", "acute"]
  },
  "prescription": [
    {
      "medication_name": "Ibuprofen",
      "dosage": "400mg",
      "frequency": "Every 6 hours as needed (PRN)",
      "duration": "7 days",
      "refill_count": 0,
      "dispensed_on": "2025-11-20"
    },
    {
      "medication_name": "Sumatriptan",
      "dosage": "50mg",
      "frequency": "Take at onset of migraine",
      "duration": "PRN",
      "refill_count": 1,
      "dispensed_on": "2025-11-20"
    }
  ],
  "attachments": [
    {
      "file_name": "MRI_Scan_2025_11_19.pdf",
      "storage_path": "/uploads/files/105/501/mri_112025.pdf",
      "file_size_kb": 5120
    }
  ],
  "metadata": {
    "is_sensitive": true,
    "version": "1.1"
  }
}
```