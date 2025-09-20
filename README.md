# Gym Data Analysis

## 📌 Project Overview
A structured record of my personal gym journey over three months, detailing each workout day, exercises performed, weights, reps, and additional cardio, core, wrist, and forearm training.  

---

## 📊 Excel Workbook
All visualizations, pivot tables, and the full analysis workflow are stored in the Excel file included in this repository:  
`gym_tracker_project.xlsx`

Open this file to explore:  
- Interactive charts (progress over time, weight vs reps, exercise frequency)  
- PivotTables for muscle group and training balance  
- Set-level breakdowns (kg, reps, RIR)  

---

## Executive Summary
This analysis covers **100 days of workout data** (58 training sessions) with the goal of uncovering trends in training frequency, muscle group balance, and overall efficiency.

### Key Findings
- Trained on average **4 times per week**, with **Tuesday** as the most frequent gym day. This rhythm reflects consistent time management and adequate recovery between sessions.  
- Most muscle groups were trained **once per week**, except for **shoulders and chest**, which averaged twice weekly. **Upper body** was prioritized significantly over **lower body** (44 vs. 12 sessions).  
- Average rest period between sessions was **2 days**, which allowed recovery but left room for better planning.  
- Progress was most notable in the **Incline Dumbbell Press, Dumbbell Military Press, and Squats**. The scatterplot confirmed the expected trade-off: **higher weights → fewer reps**.  
- Each workout averaged **6 exercises**, with consistent tracking across weight, reps, and RIR per set.  

### Recommended Actions
1. **Balance training** – Increase lower-body sessions to correct the imbalance and promote overall muscle growth.  
2. **Prioritize quality over quantity** – Reduce average exercises per session to improve focus and efficiency, especially for weaker muscle groups.  
3. **Maintain consistency** – Keep the current workflow and time management structure, which has proven effective.  

### Next Steps
To deepen the analysis, I plan to expand the dataset with lifestyle metrics such as **workout start/finish times, sleep hours, and post-session wellness (self-rated 1–10)**. Including diet and recovery data will provide a more holistic picture and enable more precise conclusions.  

**Key takeaway:** The system works — but improving lower body training, fine-tuning exercise volume, and integrating wellness metrics will drive more balanced and sustainable progress.

---

## 🛠 Data Collection
- **Type:** Primary data (self-collected and documented)  
- **Period:** The dataset covers a period of a little over 3 months (from April 28, 2025 to August 6, 2025).  
- **Content:** Exercises, sets, reps, weights (kg), RIR (Reps in Reserve), cardio and accessory training.  

---

## 🔄 Data Cleaning (Power Query in Excel)
I used **Power Query (M language)** for cleaning and structuring the dataset.

### Key steps:
1. **Extracting numbers and text**  
   - Original data contained mixed formats (e.g., `4 per hand` in the `kg` and `reps` columns).  
   - Used `Text.Select` to separate numeric values and text into **two temporary columns**.  

2. **Error handling with `try...otherwise`**  
   - Replaced error rows with values from the other column using:
     ```m
     try [kg_set_1_number] otherwise [kg_set_1]
     ```
   - This produced a clean column with numeric values for `kg` and text (`per hand`) stored in the `exercise_name` column.  

3. **Correct data types applied**  
   - `kg` → Decimal Number  
   - `reps` → Whole Number  
   - `RIR` → Whole Number  
   - `exercise_name` → Text  

4. **Validation**  
   - Dataset contains many zeros → these are intentional (they represent exercises not performed, not missing values).  
   - ✅ No `null` or `NA` values remain.  

---

## Analysis – Questions, Answers, Reasoning, and Insights

### 1. Dataset Timeframe
**My data spans from April 28 to August 6, covering a total of 100 calendar days.**

### 2. Average Trainings per Week
On average, I trained **4 times per week**.  

### 3. Day of the Week with Most Gym Visits
**Tuesday** was the most frequent with **13 visits (22%)**, while **Thursday** had the fewest (**6 sessions, 10%**).  
No workouts were recorded on **Sundays**.  

### 4. Training Count by Weekday Plan
- **Push routine** dominated with **24 sessions (41%)**.  
- This aligns with observed muscle development.  

### 5. Muscle Group Count
Worked **10 muscle groups** across 58 training days.  
- Most trained: **Shoulders (64%)**  
- Least trained: **Glutes (9%)**  

### 6. Type of Training After Strength Workouts
- **No additional training:** 30 times (**52%**)  
- **Cardio:** 23 times (**40%**)  
- **Core/Wrist/Forearm (CWF):** 5 times (**9%**)  

### 7. Total Training in 3 Months
**58 of 100 days trained → 58% coverage**  

### 8. Average Weekly Frequency per Muscle Group
- Most muscle groups trained **once/week**.  
- **Shoulders and Triceps** → twice/week.  
- Legs under-trained.  

### 9. Upper vs. Lower Body Training
- **Upper body:** 44 sessions  
- **Lower body:** 12 sessions  
- **Other (cardio only):** 2 sessions  

### 10. Average Rest Days
**2 days average rest** between sessions.  

### 11. Average Session Volume
Typical day: **3 muscle groups/session**, excluding cardio.  

---

## Methodology, Reasoning, and Motivation
Curiosity drove me to quantify my training consistency, intensity, and balance.  

### Real Week Column
Mapped workouts to **actual calendar weeks** for accurate averages.  

### Training Focus Column
Categorized sessions as **Upper**, **Lower**, or **Other**.  

### Muscle Group Analysis
Unpivoted muscle group columns → long format → counted training frequency.  

### Pivot Table & DAX
Measured average muscle group frequency/week:  
```DAX
measure_name = avg_count
=DIVIDE(
    COUNTROWS(question_5),
    DISTINCTCOUNT(question_5[real_week])
)
```
# Excel Strength Tracker Workflow

## 1. Extracting Exercises
- Filtered exercises performed ≥5 times → **23 valid exercises**.

## 2. Data Validation
- Drop-down list (`=exercises_filtered`) for analysis.

## 3. Progress Line Chart
- Line chart: **Date (X)** vs. **Weight (Y, Set 1 only)**.

## 4. Supporting Table
- Shows **reps, RIR, times trained, averages, and maximums**.

## 5. Weight vs Reps Scatterplot
- Displays **weight/reps relationship**.

## 13. Average Exercises per Session
- Created binary **Value** column (1 = exercise, 0 = null) → grouped → average = **6 exercises/session**.

## 14. Typical Exercise Order
- Confirmed **compound lifts** (squat, press, pulldown) usually appear first.

## 15. Set-level Exercise Breakdown
- Pivot tables + DAX for **average kg, reps, RIR per set**.

```
measure_name = avg_kg_set_1
=AVERAGEX (
    FILTER (Table14, Table14[kg_set_1_clean] <> 0),
    Table14[kg_set_1_clean]
)
```
---
## Technical Implementation

To make the analysis possible, I designed a custom logging system in **Visual Basic for Applications (VBA).**

- Input each workout efficiently → stored directly in Excel table  
- Automated data entry → eliminated errors  
- Enforced consistent format → ensured data integrity  
- Enabled repeatable process for tracking  

This highlights my ability to combine **automation, data engineering, and analysis in Excel**, transforming raw inputs into structured datasets for **Power Query, PivotTables, and DAX**.

🎥 Demo Video: (https://youtu.be/g9m971bRQEU)

---
## 💡 Skills Demonstrated

This project showcases a combination of **technical, analytical, and automation skills**:

- **VBA Automation (Visual Basic for Applications)**  
  - Designed a custom logging system to input workouts quickly and store them in a structured Excel table.  
  - Automated data entry, enforced data integrity, and eliminated manual errors.  

- **Data Engineering in Excel**  
  - Structured raw workout logs into a clean, analysis-ready dataset.  
  - Built repeatable workflows for continuous tracking and updating.  

- **Power Query (M Language)**  
  - Applied text/number extraction, type conversion, and error handling (`try…otherwise`).  
  - Created a long-format dataset through unpivoting for muscle group analysis.  

- **Data Analysis with PivotTables & DAX**  
  - Designed custom measures for averages, frequencies, and trends.  
  - Calculated training balance (upper vs. lower body) and per-week metrics.  

- **Visualization & Insights**  
  - Built line charts, scatterplots, and frequency charts to track strength progress and exercise efficiency.  
  - Identified imbalances and trends in training routines.  

- **Project Documentation**  
  - Summarized methodology, findings, and recommendations clearly.  
  - Created a structured README with executive summary, methods, and actionable insights.  

👉 These skills demonstrate my ability to bridge **data collection, cleaning, analysis, and visualization** into a single, well-documented workflow — all within Excel enhanced by automation.

---
## Notes
During cleaning, corrected typos (Caardio → Cardio, Shoulder → Shoulders).
All null/missing values addressed.

---

## 👤 Contact
**Author:** Gerardo Abarca  
📧 abarcagerardoj777@gmail.com 
💼 https://www.linkedin.com/in/gerardo-abarca-2389b6328/

---
