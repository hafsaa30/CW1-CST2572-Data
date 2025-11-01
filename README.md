# CW1-CST2572-Data

Medical Clinic Data Repository for MedHaven Application

## 📋 Overview

This repository contains all the JSON data files used by the MedHaven Medical Clinic website application. The data is fetched dynamically by the main application to populate its IndexedDB database.

## 🗂️ Repository Structure

```
CW1-CST2572-Data/
├── README.md
├── extra-admin-data.json          # Admin passwords and credentials
├── extra-doctor-data.json         # Doctor passwords and specializations
├── extra-patient-data.json        # Patient passwords
├── appointments.json               # Appointment records
├── prescriptions.json              # Prescription data
├── medical-notes.json              # Doctor's medical notes
├── medical-history.json            # Patient medical histories
└── request-prescription.json       # Prescription refill requests
```

## 📊 Data Files Description

### **extra-admin-data.json**
Contains supplementary admin account information including encrypted passwords.

**Structure:**
```json
{
  "email": "admin@email.com",
  "Password": "encryptedPasswordString"
}
```

**Fields:**
- `email` - Admin email address (matches main admin.json)
- `Password` - Encrypted password using AES encryption

---

### **extra-doctor-data.json**
Contains doctor specializations and encrypted passwords.

**Structure:**
```json
{
  "email": "doctor@email.com",
  "Specialization": "Cardiology",
  "Password": "encryptedPasswordString"
}
```

**Fields:**
- `email` - Doctor email address (matches main doctors.json)
- `Specialization` - Medical specialization field
- `Password` - Encrypted password using AES encryption

**Available Specializations:**
- General Practice
- Cardiology
- Neurology
- Pediatrics
- Orthopedics
- Obstetrics
- Psychiatry
- Radiology
- Dermatology

---

### **extra-patient-data.json**
Contains patient encrypted passwords.

**Structure:**
```json
{
  "Email": "patient@email.com",
  "Password": "encryptedPasswordString"
}
```

**Fields:**
- `Email` - Patient email address (matches main patients.json)
- `Password` - Encrypted password using AES encryption

---

### **appointments.json**
Contains all appointment records between patients and doctors.

**Structure:**
```json
{
  "patient_id": 101,
  "doctor_id": 1,
  "date": "2025-11-15",
  "time": "10:30",
  "reason": "General checkup",
  "status": "confirmed"
}
```

**Fields:**
- `patient_id` - Patient identifier (references patients table)
- `doctor_id` - Doctor identifier (references doctors table)
- `date` - Appointment date (YYYY-MM-DD format)
- `time` - Appointment time (HH:MM 24-hour format)
- `reason` - Reason for appointment
- `status` - Appointment status (confirmed, completed, cancelled, upcoming)

**Sample Data:** 20+ appointment records across various doctors and patients

---

### **prescriptions.json**
Contains prescription records issued by doctors to patients.

**Structure:**
```json
{
  "dosage": "500mg",
  "duration": "7 days",
  "patient_id": 101,
  "doctor_id": 1,
  "drug_id": 1,
  "appt_id": 1
}
```

**Fields:**
- `dosage` - Medication dosage (e.g., "500mg", "10ml")
- `duration` - Treatment duration (e.g., "7 days", "2 weeks")
- `patient_id` - Patient identifier
- `doctor_id` - Prescribing doctor identifier
- `drug_id` - Medication identifier (references medicines table)
- `appt_id` - Associated appointment identifier (optional)

**Sample Data:** 30+ prescription records

---

### **medical-notes.json**
Contains medical notes written by doctors for patients.

**Structure:**
```json
{
  "patient_id": 101,
  "doctor_id": 1,
  "note": "Patient presented with chest pain. ECG normal. Prescribed medication.",
  "appt_id": 1,
  "date": "2025-11-01"
}
```

**Fields:**
- `patient_id` - Patient identifier
- `doctor_id` - Doctor who wrote the note
- `note` - Detailed medical note content
- `appt_id` - Associated appointment identifier (optional)
- `date` - Date note was created (YYYY-MM-DD format)

**Sample Data:** 25+ medical note records

---

### **medical-history.json**
Contains patient medical history records.

**Structure:**
```json
{
  "patient_id": 101,
  "history": "Patient has history of hypertension. Family history of heart disease.",
  "last_edited": "2025-11-01"
}
```

**Fields:**
- `patient_id` - Patient identifier
- `history` - Comprehensive medical history text
- `last_edited` - Last modification date (YYYY-MM-DD format)

**Sample Data:** 15+ medical history records

---

### **request-prescription.json**
Contains prescription refill requests from patients to doctors.

**Structure:**
```json
{
  "patient_id": 101,
  "doctor_id": 1,
  "drug_id": 5,
  "prescription_id": 10
}
```

**Fields:**
- `patient_id` - Patient requesting refill
- `doctor_id` - Doctor receiving the request
- `drug_id` - Medication being requested
- `prescription_id` - Reference to original prescription (optional)

**Sample Data:** 10+ prescription request records

---

## 🔗 Data Relationships

```
patients (main repo) ←→ extra-patient-data.json (email)
doctors (main repo)  ←→ extra-doctor-data.json (email)
admins (main repo)   ←→ extra-admin-data.json (email)

appointments.json → patient_id → patients
appointments.json → doctor_id → doctors

prescriptions.json → patient_id → patients
prescriptions.json → doctor_id → doctors
prescriptions.json → drug_id → medicines (main repo)
prescriptions.json → appt_id → appointments.json

medical-notes.json → patient_id → patients
medical-notes.json → doctor_id → doctors
medical-notes.json → appt_id → appointments.json

medical-history.json → patient_id → patients

request-prescription.json → patient_id → patients
request-prescription.json → doctor_id → doctors
request-prescription.json → drug_id → medicines (main repo)
request-prescription.json → prescription_id → prescriptions.json
```

## 🔐 Security & Encryption

**Password Encryption:**
- All passwords are encrypted using **AES (Advanced Encryption Standard)**
- Encryption library: CryptoJS 4.1.1

**Note:** This is for educational/demonstration purposes. In production, passwords should never be stored in publicly accessible repositories, even encrypted.

## 📡 API Endpoints (Raw GitHub URLs)

The MedHaven application fetches data from these URLs:

```javascript
// Base URL
const BASE_URL = 'https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/';

// File URLs
const ADMIN_DATA = BASE_URL + 'extra-admin-data.json';
const DOCTOR_DATA = BASE_URL + 'extra-doctor-data.json';
const PATIENT_DATA = BASE_URL + 'extra-patient-data.json';
const APPOINTMENTS = BASE_URL + 'appointments.json';
const PRESCRIPTIONS = BASE_URL + 'prescriptions.json';
const MEDICAL_NOTES = BASE_URL + 'medical-notes.json';
const MEDICAL_HISTORY = BASE_URL + 'medical-history.json';
const PRESCRIPTION_REQUESTS = BASE_URL + 'request-prescription.json';
```

**CORS:** Raw GitHub content is CORS-enabled and can be fetched from any origin.

## 🛠️ Usage in Main Application

The main MedHaven application uses these files in the following way:

1. **Database Initialization** (`database.js`):
   - Fetches all JSON files asynchronously
   - Creates IndexedDB tables
   - Populates tables with fetched data
   - Merges extra data with main data based on email

2. **Data Fetching Example:**
```javascript
// Fetch appointments data
await fetch('https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/appointments.json')
    .then(response => response.json())
    .then(data => {
        appointment_data = data;
        console.log('Appointments loaded:', data.length);
    })
    .catch(error => {
        console.error('Error fetching appointments:', error);
    });
```

3. **Data Insertion:**
```javascript
// Insert appointments into IndexedDB
function insertAppointments() {
    const transaction = db.transaction('appointments', 'readwrite');
    const store = transaction.objectStore('appointments');
    
    appointment_data.forEach(appointment => {
        const data = {
            patientId: appointment.patient_id,
            doctorId: appointment.doctor_id,
            date: appointment.date,
            time: appointment.time,
            reason: appointment.reason,
            status: appointment.status
        };
        store.add(data);
    });
}
```

## 📊 Sample Data Statistics

| Data Type | Record Count | Purpose |
|-----------|-------------|---------|
| Admin Passwords | 3 | Authentication |
| Doctor Data | 15 | Specializations & Auth |
| Patient Passwords | 100+ | Authentication |
| Appointments | 20+ | Scheduling |
| Prescriptions | 30+ | Medication tracking |
| Medical Notes | 25+ | Clinical documentation |
| Medical History | 15+ | Patient records |
| Prescription Requests | 10+ | Refill system |

## 📚 Related Resources

- **Main Application:** MedHaven Medical Clinic Website
- **Course:** CST2572 - Web Secure Technologies

## ⚠️ Important Notes

- **Educational Purpose:** This repository is for coursework demonstration
- **Not Production Ready:** Security measures are simplified for learning
- **Public Access:** Data is publicly accessible via GitHub
- **Sample Data:** All patient/doctor data is fictional
- **Password Security:** Real applications should never expose passwords

## 📄 License

This project is submitted as coursework for CST2572.
All data is original work by the development team.
Not for commercial use or redistribution.

## 📞 Support

For issues or questions:
- Check main application documentation
- Refer README file in Coursework zipped folder
- Verify URL references exist and is valid
- Contact development team through university channels

---

**Last Updated:** November 01, 2025  
**Repository Version:** 1.0  
**Status:** Active - Supporting MedHaven v1.0

---

## Quick Reference

### File URLs (Copy-Paste Ready)
```
https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/extra-admin-data.json
https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/extra-doctor-data.json
https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/extra-patient-data.json
https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/appointments.json
https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/prescriptions.json
https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/medical-notes.json
https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/medical-history.json
https://raw.githubusercontent.com/hafsaa30/CW1-CST2572-Data/refs/heads/main/request-prescription.json
```
