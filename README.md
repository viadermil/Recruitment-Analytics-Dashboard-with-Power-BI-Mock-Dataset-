# Recruitment Analytics Dashboard with Power BI (Mock Dataset)

## 📊 Overview

This project showcases a **Recruitment Analytics Dashboard** built using **Power BI**, based on a mock dataset of 1,000 candidate records. It demonstrates how organizations can monitor recruitment performance, track pipeline stages, and evaluate recruiter effectiveness through interactive visuals.

The data was generated using [Mockaroo](https://mockaroo.com) with realistic recruitment fields, covering various aspects of a typical hiring process including application dates, hire status, recruiters, and sourcing channels.

---

## 🎯 Objectives

- Visualize the **recruitment funnel** from application to hire.
- Track **key performance indicators (KPIs)** such as total candidates, hires, time to hire, and offer acceptance rate.
- Identify hiring trends and peaks in **applications over time**.
- Assess the **efficacy of sourcing channels** (LinkedIn, Website, etc.).
- Evaluate **recruiter performance** based on number of successful hires.
- Enable interactive filtering by **date, source, job title, and recruiter**.

---

## 📌 Key Metrics Displayed

| Metric                    | Description |
|--------------------------|-------------|
| **Total Candidates**     | Total number of job applicants received. |
| **Total Hires**          | Number of applicants successfully hired. |
| **Average Days to Hire** | Average number of days between application and hiring. |
| **Offer Acceptance Rate**| Percentage of offers accepted out of total offers made. |

---

## 🧮 Metrics Calculation Details

### Metrics Calculated in Mockaroo

- **hire_date**  
  ```mockaroo
  if field("status") == 'Hired' then random(date('2024-04-01'), date('2024-04-31')) else '' end
  ```
  Assigns a random hire date in April 2024 for hired candidates; blank otherwise.

- **time_to_hire**  
  ```mockaroo
  if field("status") == 'Hired' then date_diff('days', field("application_date"), field("hire_date")) else '' end
  ```
  Calculates the number of days between application date and hire date for hired candidates.

---

### Metrics Calculated in Power BI (DAX)

- **is_hired**  
  ```DAX
  is_hired = IF('MOCK_DATA'[status] = "Hired", 1, 0)
  ```
  Binary indicator if candidate is hired.

- **offer_accepted**  
  ```DAX
  offer_accepted = IF('MOCK_DATA'[offer_status] = "Accepted", 1, 0)
  ```
  Binary indicator if offer was accepted.

- **Average Time to Hire**  
  ```DAX
  Average Time to Hire = AVERAGE(MOCK_DATA[time_to_hire])
  ```
  Computes average days to hire across candidates.

- **Offer Acceptance Rate**  
  ```DAX
  Offer Acceptance Rate = DIVIDE(SUM(MOCK_DATA[offer_accepted]), COUNT(MOCK_DATA[offer_status]))
  ```
  Calculates the percentage of offers accepted out of total offers made.

---

## 📈 Visualizations Used

- **Card Tiles**: High-level KPIs for quick insights.
- **Line Chart**: Application volume over time.
- **Pie Chart**: Hires segmented by source (LinkedIn, Website, etc.).
- **Bar Chart** *(Horizontal)*: Recruiter performance (total hires).
- **Funnel Chart**: Candidate pipeline stages from Applied to Hired.
- **Slicers**: Interactive filters for Date, Source, Job Title, and Recruiter.

---

## 🔍 Candidate Pipeline Definition

The **candidate pipeline** tracks the journey of applicants through recruitment stages:

1. **Applied**  
2. **Screened**  
3. **Interviewed**  
4. **Offered**  
5. **Hired**  

This helps monitor pipeline efficiency, identify bottlenecks, and improve time-to-fill metrics.

---

## 🛠️ Tools & Technologies

- **Power BI Desktop** – Data modeling, transformation & dashboard design
- **Mockaroo** – For generating realistic, fictitious recruitment data
- **DAX** – Calculated columns and measures for time-to-hire and offer acceptance rate

---

## 📁 Dataset Details

- 1,000 rows
- Fields: Candidate ID, Application Date, Hire Date, Source, Job Title, Recruiter, Status, Offer Status, Time to Hire
- Metrics and formulas implemented both in Mockaroo and Power BI as outlined above.

---

## 📬 Contact

If you have any questions or feedback about this dashboard or want to collaborate, feel free to reach out via GitHub issues or [LinkedIn](https://linkedin.com/in/viadermil).
