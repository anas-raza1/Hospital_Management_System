# Hospital_Management_System

# Hospital Management System

A Java-based console application for managing hospital operations including patient records, doctor information, and appointment scheduling.

## Features

- **Patient Management**
  - Add new patients with name, age, and gender
  - View all registered patients
  - Patient record validation

- **Doctor Management**
  - View all available doctors with their specializations
  - Doctor availability verification

- **Appointment Booking**
  - Book appointments between patients and doctors
  - Doctor availability checking to prevent double bookings
  - Appointment scheduling with specific dates

## Project Structure

```
Hospital_Management_System/
├── src/
│   ├── module-info.java
│   └── HospitalManagementSystem/
│       ├── HospitalManagementSystem.java (Main application)
│       ├── Patient.java (Patient operations)
│       └── Doctor.java (Doctor operations)
```

## Prerequisites

- Java 11 or higher
- MySQL Server
- MySQL JDBC Driver (`mysql-connector-java`)

## Database Setup

Create a MySQL database with the following schema:

```sql
CREATE DATABASE hospital;

CREATE TABLE doctors (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    specialization VARCHAR(100) NOT NULL
);

CREATE TABLE patients (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL,
    gender VARCHAR(20) NOT NULL
);

CREATE TABLE appointments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    patient_id INT NOT NULL,
    doctor_id INT NOT NULL,
    appointment_date DATE NOT NULL,
    FOREIGN KEY (patient_id) REFERENCES patients(id),
    FOREIGN KEY (doctor_id) REFERENCES doctors(id)
);
```

## Configuration

Update database credentials in [`HospitalManagementSystem.java`](HospitalManagementSystem/HospitalManagementSystem.java):

```java
private static final String url = "jdbc:mysql://127.0.0.1:3306/hospital";
private static final String username = "root";
private static final String password = "your_password";
```

## Running the Application

1. Compile the project
2. Run the main class: `HospitalManagementSystem`
3. Follow the console menu to manage patients, doctors, and appointments

## Main Menu Options

1. **Add Patient** - Register a new patient
2. **View Patients** - Display all patients in a formatted table
3. **View Doctors** - Display all available doctors and their specializations
4. **Book Appointment** - Schedule an appointment between a patient and doctor
5. **Exit** - Close the application

## Class Overview

- **[`HospitalManagementSystem.java`](HospitalManagementSystem/HospitalManagementSystem.java)**: Main application class with menu and appointment booking logic
- **[`Patient.java`](HospitalManagementSystem/Patient.java)**: Handles patient-related operations
- **[`Doctor.java`](HospitalManagementSystem/Doctor.java)**: Handles doctor-related operations

## Dependencies

- `java.sql.*` - Database connectivity and operations

## Notes

- Doctor availability is checked by date to prevent multiple appointments on the same date
- All user inputs are validated before database operations
- Prepared Statements are used to prevent SQL injection attacks
