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
 
[ERD Preview] (https://drive.google.com/file/d/1zE87fWG0Xk6OdTz2y1oD4Bd-UF9bUyLI/view?usp=sharing)

---

## 🧰 Tools & Technologies  

- **SQL Server** – Database design, creation, querying, and ERD Diagram 
- **Power BI (Optional)** – Dashboard reporting and KPI visualization  
- **Excel / CSV** – Data entry, cleaning, and validation  

---

## ⚙️ Project Workflow  

1. **Database Design**  
   - Developed an ERD to visualize entity relationships.  
   - Normalized all tables up to **Third Normal Form (3NF)** to eliminate redundancy and ensure efficiency.  

2. **Database Creation & Population**  
   - Implemented `CREATE TABLE` scripts with **primary** and **foreign keys**.  
   - Loaded and validated sample datasets using `INSERT INTO` commands.  

3. **Data Querying & Analysis**  
   - Performed **joins, subqueries, and aggregations** for relational insights.  
   - Generated analytical reports on patient admissions, diagnosis frequency, and ward occupancy.  

4. **Insights & Visualization**  
   - Integrated results with **Power BI** to visualize key healthcare metrics like admission trends and GP workload.  

---

## 🧩 Sample SQL Queries

```sql
-- 1️. List all patients with their details (ID, Name, Gender, Date of Birth, Postcode)
SELECT *
FROM Patient;

-- 2. Retrieve the total number of admissions per patient
SELECT CONCAT(p.Firstname, ' ', p.Surname) AS FullName, COUNT(*) AS TotalAdmission
FROM Patient p
JOIN Admission a ON p.PatientID = a.Patient_ID
GROUP BY p.Firstname, p.Surname
ORDER BY TotalAdmission DESC;

-- 3. Find the maximum length of stay in FY 2014/15 for Endoscopy Suite (Elective)
SELECT MAX(DATEDIFF(DAY, Admission_Date, Discharge_Date)) AS MaxLengthOfStay
FROM Admission a
JOIN Ward w ON w.Ward_Code = a.WardCode
JOIN Method_of_admission m ON m.Method_of_admission_code = a.Method_of_admission_code
WHERE Discharge_Date BETWEEN '2014-04-01' AND '2015-03-31'
  AND w.Ward_Name = 'Endoscopy Suite'
  AND m.Method_of_admission_type = 'Elective';

-- 4. Total number of admissions per ward in FY 2015/16
SELECT w.Ward_Name, COUNT(*) AS TotalAdmission
FROM Admission a
JOIN Ward w ON a.WardCode = w.Ward_Code
WHERE Admission_Date BETWEEN '2015-04-01' AND '2016-03-31'
GROUP BY w.Ward_Name
ORDER BY TotalAdmission DESC;

-- 5. Most common primary diagnosis (Emergency, SK2 area, FY 2015/16)
SELECT TOP 1 d.Diagnosis_code, d.Diagnosis_Description
FROM Admission a
JOIN Method_of_admission m ON m.Method_of_admission_code = a.Method_of_admission_code
JOIN Diagnosis d ON d.Admission_ID = a.AdmissionID
JOIN Patient p ON p.PatientID = a.Patient_ID
WHERE Discharge_Date BETWEEN '2015-04-01' AND '2016-03-31'
  AND m.Method_of_admission_type = 'Emergency'
  AND p.Postcode = '8064 akinfenwa ibadan'
GROUP BY d.Diagnosis_code, d.Diagnosis_Description;

-- 6. Primary diagnosis with longest avg. length of stay (≥100 episodes)
SELECT TOP 1 d.Diagnosis_code, d.Diagnosis_Description,
       AVG(DATEDIFF(DAY, a.Admission_Date, a.Discharge_Date)) AS AvgLengthOfStay
FROM Admission a
JOIN Diagnosis d ON d.Admission_ID = a.AdmissionID
JOIN Method_of_admission m ON m.Method_of_admission_code = a.Method_of_admission_code
WHERE Discharge_Date BETWEEN '2015-04-01' AND '2016-03-31'
  AND m.Method_of_admission_type IN ('Emergency', 'Elective')
GROUP BY d.Diagnosis_code, d.Diagnosis_Description
HAVING COUNT(*) >= 100
ORDER BY AvgLengthOfStay DESC;

-- 7. GP Practice with largest number of admissions (GP Referral, FY 2015/16)
SELECT TOP 1 g.Practice_name, COUNT(DISTINCT a.AdmissionID) AS TotalAdmission
FROM Admission a
JOIN GPPractice g ON g.GPPractice_code = a.GPPractice_code
JOIN Method_of_admission m ON m.Method_of_admission_code = a.Method_of_admission_code
WHERE Admission_Date BETWEEN '2015-04-01' AND '2016-03-31'
  AND m.Method_of_admission_type = 'GP Referral'
GROUP BY g.Practice_name
ORDER BY TotalAdmission DESC;

-- 8. Admission within 7 days of discharge (Elective → Emergency)
SELECT a1.Patient_ID,
       a1.AdmissionID AS FirstADMID,
       a1.Discharge_Date AS FirstDiscDate,
       ma1.Method_of_admission_type AS FirstMethodType,
       a1.SpecialtyCode AS FirstSpecialty,
       a2.AdmissionID AS SecondADMID,
       a2.Admission_Date AS SecondAdmDate,
       ma2.Method_of_admission_type AS SecondMethodType,
       a2.SpecialtyCode AS SecondSpecialty,
       DATEDIFF(DAY, a1.Discharge_Date, a2.Admission_Date) AS Days_Between_Episode
FROM Admission a1
JOIN Admission a2 ON a1.Patient_ID = a2.Patient_ID
  AND a1.AdmissionID <> a2.AdmissionID
JOIN Method_of_admission ma1 ON ma1.Method_of_admission_code = a1.Method_of_admission_code
JOIN Method_of_admission ma2 ON ma2.Method_of_admission_code = a2.Method_of_admission_code
JOIN Specialty s1 ON s1.SpecialtyCode = a1.SpecialtyCode
JOIN Specialty s2 ON s2.SpecialtyCode = a2.SpecialtyCode
WHERE a2.Admission_Date > a1.Discharge_Date
  AND DATEDIFF(DAY, a1.Discharge_Date, a2.Admission_Date) <= 7
  AND ma1.Method_of_admission_type = 'Elective'
  AND ma2.Method_of_admission_type = 'Emergency';

-- 9. Patients with more than one admission in FY 2015/16
SELECT CONCAT(p.Firstname, ' ', p.Surname) AS FullName, COUNT(*) AS TotalAdmission
FROM Admission a
JOIN Patient p ON p.PatientID = a.Patient_ID
WHERE Admission_Date BETWEEN '2015-04-01' AND '2016-03-31'
GROUP BY p.Firstname, p.Surname
HAVING COUNT(*) > 1
ORDER BY TotalAdmission DESC;

-- 10. Average length of stay by ward in FY 2015/16
SELECT w.Ward_Name, AVG(DATEDIFF(DAY, a.Admission_Date, a.Discharge_Date)) AS AvgLengthOfStay
FROM Admission a
JOIN Ward w ON w.Ward_Code = a.WardCode
WHERE Admission_Date BETWEEN '2015-04-01' AND '2016-03-31'
GROUP BY w.Ward_Name
ORDER BY AvgLengthOfStay DESC;

-- 11. Top 5 specialties with highest number of admissions (FY 2015/16)
SELECT TOP 5 s.SpecialtyName, COUNT(*) AS HighestAdmission
FROM Admission a
JOIN Specialty s ON s.SpecialtyCode = a.SpecialtyCode
WHERE Admission_Date BETWEEN '2015-04-01' AND '2016-03-31'
GROUP BY s.SpecialtyName
ORDER BY HighestAdmission DESC;

-- 12. GP with most patients admitted (FY 2015/16)
SELECT TOP 1 g.GP_Name, COUNT(DISTINCT a.Patient_ID) AS MostAdmittedPatient
FROM Admission a
JOIN GP g ON g.GP_code = a.GP_code
JOIN Patient p ON p.PatientID = a.Patient_ID
WHERE Admission_Date BETWEEN '2015-04-01' AND '2016-03-31'
GROUP BY g.GP_Name
ORDER BY MostAdmittedPatient DESC;

-- 13. List all patients admitted to ICU and their diagnoses
SELECT CONCAT(p.Firstname, ' ', p.Surname) AS FullName, d.Diagnosis_Description
FROM Admission a
JOIN Patient p ON p.PatientID = a.Patient_ID
JOIN Diagnosis d ON d.Admission_ID = a.AdmissionID
JOIN Ward w ON w.Ward_Code = a.WardCode
WHERE w.Ward_Name = 'ICU'
GROUP BY p.Firstname, p.Surname, d.Diagnosis_Description;
