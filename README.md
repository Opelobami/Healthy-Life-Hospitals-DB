# 🏥 Healthy Life Hospitals Database  

A robust **SQL-based relational database** designed to model and manage hospital operations from **patient admissions** to **diagnosis tracking**, **GP management**, and **ward allocation**. This project showcases strong skills in **data modeling**, **relational integrity**, and **SQL querying**, demonstrating how well-structured databases can enhance hospital administration, improve efficiency, and support data-driven healthcare delivery.  

---

## 📘 Overview  

The **Healthy Life Hospitals Database** simulates a modern hospital information system that captures essential data about **patients**, **medical staff**, **diagnoses**, and **hospital units**.  

It is designed to:  
- Ensure **data accuracy, consistency, and integrity** across all hospital entities.  
- Facilitate **efficient patient tracking** from admission to discharge.  
- Enable **data-driven reporting** on hospital operations and clinical performance.  

---

## 🎯 Project Objectives  

- Build a **normalized relational database** for hospital management.  
- Establish **entity relationships** between patients, GPs, diagnoses, and wards.  
- Provide **SQL-based insights** into patient care, GP performance, and diagnosis trends.  
- Support analytical reporting through **joins, aggregations, and subqueries**.  

---

## 🧱 Database Schema Overview  

The database consists of **seven interrelated tables**, ensuring comprehensive coverage of hospital workflows.  

### 🏨 `Admission`  
Captures details of each patient’s admission into the hospital.  
**Key Fields:**  
- AdmissionID *(Primary Key)*  
- PatientID *(Foreign Key referencing Patient)*  
- WardCode *(Foreign Key referencing Ward)*  
- SpecialtyCode *(Foreign Key referencing Specialty)*  
- Method-of-admission-code *(Foreign Key referencing MethodOfAdmission)*  
- AdmissionDate  
- DischargeDate  

---

### ⚕️ `Diagnosis`  
Records medical diagnoses linked to patient admissions.  
**Key Fields:**  
- DiagnosisCode *(Primary Key)*  
- AdmissionID *(Foreign Key referencing Admission)*  
- Diagnosis-Description *(Description of the patient's diagnosis)* 

---

### 👨‍⚕️ `GP` (General Practitioner)  
Contains information about medical practitioners providing patient care.  
**Key Fields:**  
- GPCode *(Primary Key)*  
- GPName *(General Practitioner's name)*
- GP-Practice-Code *(Foreign key referencing GP Practice)* 

---

### 🏥 `GP Practice`  
Represents the medical facilities or clinics that employ or manage GPs.  
**Key Fields:**  
- PracticeCode *(Primary Key)*  
- PracticeName *(Name of the medical facility)*
- Practice-Post-Code *(GP-Practice address)* 

---

### 🚪 `Method of Admission`  
Defines the mode or method through which a patient was admitted.  
**Key Fields:**  
- Method-of-admission-code *(Primary Key)*  
- Method-of-admission-type *(e.g., Emergency, Referral, Direct, Elective)*  

---

### 🧍 `Patient`  
Holds demographic and identification details of each patient.  
**Key Fields:**  
- PatientID *(Primary Key)*  
- FirstName
- Surname  
- DateOfBirth  
- Gender  
- Post-Code

---

### 🩺 `Specialty`  
Specifies the area of medical expertise for GPs or hospital departments.  
**Key Fields:**  
- SpecialtyCode *(Primary Key)*  
- SpecialtyName *(e.g., Pediatrics, Cardiology, Orthopedics)*  

---

### 🛏️ `Ward`  
Represents hospital wards where patients are admitted.  
**Key Fields:**  
- WardCode *(Primary Key)*  
- WardName  
- WardType 

---

## 🧩 Entity Relationships  

The schema enforces **referential integrity** through foreign keys, connecting the entities as follows:  

- Each **Patient** can have multiple **Admissions**.  
- Each **Admission** is linked to a **Ward**, **Specialty**, and **Method of Admission**.  
- Each **GP** belongs to a **GP Practice**.  
- Each **Admission** can have multiple **Diagnoses**.  
 
```markdown
![ERD Preview](https://github.com/Opelobami/Healthy-Life-Hospitals/blob/main/assets/ERD_Diagram.png)
