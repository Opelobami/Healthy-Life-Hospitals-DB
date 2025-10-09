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
--Database implementation project for HealthyLife Hospitals to manage patient admissions, diagnoses, wards, and related information.
--Also analyze patient admissions, understand common diagnoses, and optimize hospital operations.

CREATE DATABASE HealthyLifeHospitals;

USE HealthyLifeHospitals;


--Setting Standard SQL Practices in place.

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

-- Now, lets create our first table [Patient]

CREATE TABLE [dbo].[Patient](
	[PatientID] [INT] IDENTITY(1,1) NOT NULL,
	[Firstname] [NVARCHAR](20) NOT NULL,
	[Surname] [NVARCHAR](20) NOT NULL,
	[DateofBirth] [DATETIME] NOT NULL,
	[Gender] [NVARCHAR](10) NOT NULL,
	[Postcode] [NVARCHAR](50) NOT NULL,

--Add primary key constraint to patientID identifying it as clustered primary key.

CONSTRAINT [PK_Patient_PatientID] PRIMARY KEY CLUSTERED ([PatientID] ASC)
	WITH (PAD_INDEX = OFF,
		STATISTICS_NORECOMPUTE = OFF,
		IGNORE_DUP_KEY = OFF,
		ALLOW_ROW_LOCKS = ON,
		ALLOW_PAGE_LOCKS = ON,
		OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF
		)ON [PRIMARY]
		) ON [PRIMARY]
		GO

--Add constraint to firstname, surname, gender, postcode and DOB ensuring that they do not come up empty or filled with white spaces or in the future.
ALTER TABLE [dbo].[Patient] ADD CONSTRAINT [CK_Patient_FirstName]
CHECK(LEN(LTRIM(RTRIM(Firstname))) > 0)
GO

ALTER TABLE [dbo].[Patient] ADD CONSTRAINT [CK_Patient_Surname]
CHECK(LEN(LTRIM(RTRIM(Surname))) >0)
GO

ALTER TABLE [dbo].[Patient] ADD CONSTRAINT [CK_Patient_Postcode]
CHECK(LEN(LTRIM(RTRIM(Postcode))) >0)
GO

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
```

---

👉 **[View Interactive Power BI Dashboard →]** (https://app.powerbi.com/view?r=eyJrIjoiN2I5MDhhM2QtYjY0Ny00NWMwLWJlNzUtYzM5YzlkNGUxNTllIiwidCI6ImRkYjk1YzMwLWU3OWUtNDdiNy05YTVmLWE0MmNkZDljOTk5ZCJ9)  

## 📊 Key Insights  

| **Metric** | **Insight** |
|-------------|-------------|
| **Total Admissions** | 100 |
| **Average Length of Stay** | 14 days |
| **Most Active GP** | Dr. Aisha *(37 patient admissions)* |
| **Top GP Practice** | Ibadan Central Clinic *(13 admissions)* |
| **Leading Specialty (2015/16)** | Oncology *(15 admissions)* |
| **Most Occupied Ward** | General Medicine *(14 admissions)* |
| **Dominant Admission Method** | GP Referral *(29 cases)* |
| **Gender Distribution** | 53% Male · 47% Female |

---

## 📅 Yearly Diagnosis Summary  

| **Year** | **Top Diagnosis** | **Frequency** | **Lowest Diagnosis** | **Frequency** |
|-----------|------------------|----------------|----------------------|----------------|
| 2014/15 | Asthma | 6 | Typhoid | 2 |
| 2015/16 | Hypertension | 7 | Asthma | 3 |
| 2016 | Hepatitis | 3 | Ulcer | 1 |

---

## 🏥 Admission Method Breakdown  

- **Emergency Admissions:** 20 → *Top Diagnosis: Hypertension*  
- **Transfers:** 23 → *Top Diagnosis: Diabetes*  
- **Referrals:** 29 → *Top Diagnosis: COVID-19*

---

## 🧠 Conclusion  

The **Healthy Life Hospitals Database** demonstrates how structured data management can **transform hospital operations** through reliable, consistent, and integrated information systems.  

By employing **SQL relational principles** and **data normalization standards**, the database ensures:
- Seamless **patient tracking**
- Improved **clinical oversight**
- Enhanced **analytical reporting**

This project mirrors the data architecture of modern **Hospital Information Systems (HIS)** and **Electronic Health Records (EHR)**, aligning with **global healthcare data standards** and showcasing data-driven excellence in hospital analytics.  

---

## 💡 Recommendations  

1. **Integration with BI Tools**  
   → Extend the database into **Power BI** or **Tableau** for real-time monitoring of KPIs such as bed occupancy, readmission rates, and length of stay.  

2. **Automation & Alerts**  
   → Implement **SQL triggers** or scheduled stored procedures to track delayed discharges or identify critical readmissions.  

3. **Scalability & Interoperability**  
   → Integrate **ICD-10** diagnosis codes and ensure **HL7/FHIR** compliance to connect with other hospital systems.  

4. **Security & Access Control**  
   → Introduce **role-based access permissions** and encryption for data confidentiality in compliance with **HIPAA** or **GDPR** standards.  

5. **Predictive Analytics**  
   → Use **machine learning models** to forecast admission trends, diagnosis frequencies, and staff workload — enabling proactive hospital management.  

---

## 📬 Contact  

If you’re looking for a data-driven problem solver who can turn complex datasets into actionable stories, let’s connect:  

- **Name:** Opeyemi Ayodeji  
- **LinkedIn:** (https://www.linkedin.com/in/opeyemi-ayodeji-86a696b0/)  
- **Email:** sopeyemi65@gmail.com  

✨ *A data-driven healthcare system begins with clean, connected, and well-modeled databases.*  
**Healthy Life Hospitals Database** proves the power of SQL in delivering actionable healthcare insights.
