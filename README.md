# Healthy Life Hospital Database  

A **SQL-based relational database** designed to model and manage hospital operations from **patient admissions** and **diagnosis tracking** to **GP performance** and **ward allocation**.  

This project demonstrates strong capabilities in **data modeling**, **database normalization**, and **SQL querying**, revealing how structured databases can enhance hospital efficiency, clinical decision-making, and data-driven healthcare delivery.  

---

## Overview  

The **Healthy Life Hospital Database** is a data management solution simulating a modern hospital information system. It provides an integrated view of how patients, doctors, diagnoses, and wards interact enabling seamless **tracking, analysis, and reporting** across hospital functions.  

Through this project, I designed a **normalized relational database** that ensures data **accuracy**, **consistency**, and **integrity** allowing hospital management to make evidence-based decisions and optimize resources.

---

## Project Objectives  

- Design and implement a **relational database** for hospital management.  
- Establish **entity relationships** between patients, admissions, diagnoses, and GPs.  
- Enable **insightful SQL-based queries** to monitor hospital activities.  
- Support **analytical reporting** for operational and clinical performance.  

---

## Why This Project Matters  

In healthcare, every decision counts. Hospitals generate massive data daily yet much of it remains underutilized due to poor structuring or lack of integration.  

The **Healthy Life Hospital Database** addresses this gap by creating a **single source of truth** for hospital operations. With this system, stakeholders can:  
- Understand patient flow and admission patterns.  
- Identify overworked wards and optimize capacity.  
- Monitor GP workload and performance.  
- Track the most frequent diagnoses and resource demands.  

---

## 🧰 Tools & Technologies  

| **Tool / Technology** | **Purpose** |
|------------------------|-------------|
| SQL Server | Database creation, relational modeling, querying |
| Power BI | Visualization and reporting |
| ERD (Entity Relationship Diagram) | Schema design and normalization verification |

**Database Design:**  
- 7 interrelated tables (Patient, GP, Ward, Admission, Diagnosis, Specialty, Method of Admission)  
- Fully normalized up to **3NF** for optimal performance and minimal redundancy  

---

## Methodology  

1. **Database Creation & Structuring**  
   - Designed schema ensuring **referential integrity** with primary and foreign keys.  
   - Applied constraints to enforce valid and consistent data entry.  

2. **Data Population & Cleaning**  
   - Inserted mock datasets to replicate real hospital operations.  
   - Validated relationships through joins and foreign key constraints.  

3. **SQL Query Analysis**  
   - Wrote analytical queries for insights on admissions, diagnoses, and GP performance.  
   - Conducted temporal analysis (2014–2016) to reveal admission trends.  

4. **Data Visualization**  
   - Integrated Power BI for interactive dashboards on admission rates, top diagnoses, and GP activity.  

---

## 🗂️ Database Relationships  

- Each **Patient** can have multiple **Admissions**.  
- Each **Admission** links to a **Ward**, **GP**, **Specialty**, and **Method of Admission**.  
- Each **Admission** can have multiple **Diagnoses**.  
- Each **GP** is assigned to one **GP Practice**.  

🔗 [**View ERD Diagram**](https://drive.google.com/file/d/1zE87fWG0Xk6OdTz2y1oD4Bd-UF9bUyLI/view?usp=sharing)

---

## Key Insights  

| **Metric** | **Insight** |
|-------------|-------------|
| **Total Admissions** | 100 |
| **Average Length of Stay** | 14 days |
| **Most Active GP** | Dr. Aisha - 37 patient admissions |
| **Top GP Practice** | Ibadan Central Hospital - 13 admissions |
| **Leading Specialty (2015/16)** | Oncology - 15 admissions |
| **Most Occupied Ward** | General Medicine - 14 admissions |
| **Dominant Admission Method** | GP Referral - 29 cases |
| **Gender Distribution** | 53% Male · 47% Female |

---

## Yearly Diagnosis Summary  

| **Year** | **Top Diagnosis** | **Frequency** | **Lowest Diagnosis** | **Frequency** |
|-----------|------------------|----------------|----------------------|----------------|
| 2014/15 | Asthma | 6 | Typhoid | 2 |
| 2015/16 | Hypertension | 7 | Asthma | 3 |
| 2016 | Hepatitis | 3 | Ulcer | 1 |

---

## Admission Method Breakdown  

- **Emergency Admissions:** 20 → *Top Diagnosis: Hypertension*  
- **Transfers:** 23 → *Top Diagnosis: Diabetes*  
- **Referrals:** 29 → *Top Diagnosis: COVID-19*  

---

## Key Takeaways  

- **Admissions peaked through GP referrals**, indicating strong primary care reliance.  
- **Oncology and General Medicine** are the busiest departments, signaling demand for specialized staff allocation.  
- **Average stay duration of 14 days** suggests moderate bed turnover — an opportunity for efficiency improvement.  
- **Hypertension and Diabetes** appear frequently, reinforcing the need for preventive care programs.  

---

## Conclusion  

The **Healthy Life Hospital Database** proves that well-modeled data can revolutionize hospital management.  

By leveraging **SQL relational integrity** and **data normalization**, this system enables accurate tracking of patient admissions, diagnosis frequency, and staff performance.  

Hospitals adopting similar frameworks can improve:  
- **Operational efficiency**  
- **Clinical decision-making**  
- **Data-driven management strategies**  

---

## Recommendations  

| **Action** | **Expected Impact** | **Implementation Approach** |
|-------------|--------------------|-----------------------------|
| Integrate BI Dashboards | Real-time visibility on admissions, occupancy, and diagnosis trends | Use Power BI / Tableau connected to SQL Server |
| Automate Alerts | Reduce discharge delays and readmission risks | Schedule stored procedures or SQL triggers |
| Predictive Analytics | Forecast patient inflow and high-risk diagnoses | Apply ML models to historical SQL data |
| Strengthen Security | Ensure compliance with data privacy laws | Introduce role-based access and encryption |

---

## ⚠️ Risk of Inaction  

If data-driven improvements are not implemented:  
- **Admission bottlenecks** and **ward congestion** may increase.  
- **Critical readmissions** may go unnoticed.  
- **Decision-making** will remain reactive instead of proactive.  
- **Regulatory non-compliance** could expose the hospital to data risks.  

---

## ✅ Benefits of Acting on Insights  

By implementing the above recommendations, stakeholders can expect:  
- Improved **bed utilization** and **operational efficiency**.  
- Data-backed **policy and staffing decisions**.  
- Enhanced **patient satisfaction** through faster turnaround.  
- Compliance with **modern healthcare data standards**.  

---

## 📊 Visualization  

[**Healthy Life Hospital**](https://app.powerbi.com/view?r=eyJrIjoiN2I5MDhhM2QtYjY0Ny00NWMwLWJlNzUtYzM5YzlkNGUxNTllIiwidCI6ImRkYjk1YzMwLWU3OWUtNDdiNy05YTVmLWE0MmNkZDljOTk5ZCJ9)

The dashboard visualizes:  
- Admission trends and ward occupancy rates  
- GP workload and patient distribution  
- Diagnosis frequency by year and department  

---

## 📬 Contact  

If you’re looking for a **data analyst passionate about healthcare intelligence**, let’s connect:  

- **👤 Name:** Opeyemi Ayodeji  
- **🔗 LinkedIn:** [Opeyemi Ayodeji](https://www.linkedin.com/in/opeyemi-ayodeji-86a696b0/)  
- **📧 Email:** sopeyemi65@gmail.com  

---

> ✨ “Healthy decisions start with healthy data — the heartbeat of every efficient hospital.”  
