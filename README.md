# Gym Data Analysis

## 📌 Project Overview
A structured record of my personal gym journey over three months, detailing each workout day, exercises performed, weights, reps, and additional cardio, core, wrist, and forearm training.  

This project demonstrates:
- Data organization  
- Tracking progress  
- Cleaning and transforming raw inputs  
- Analyzing performance trends  

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
## Analysis - Questions, Answers, Reasoning, and Insights

### 1. Dataset Timeframe
**My data spans from April 28 to August 6, covering a total of 100 calendar days.**

### 2. Average Trainings per Week
Using the **Real Week** column from our central table, we can see in which weeks of 2025 workouts were performed.  
**On average, I trained 4 times per week.**

### 3. Day of the Week with Most Gym Visits
**Tuesday** was the day with the most sessions, totaling **13 visits (22% of workouts)**, while **Thursday** had the fewest, with **6 sessions (10%)**.  
No workouts were recorded on **Sundays** during this period.

### 4. Training Count by Weekday Plan
The **push routine** was the most frequent, with **24 sessions out of 58 workouts (41%)**.  
This aligns with personal observations, as these muscle groups showed the greatest strength and muscle development.  
*While anecdotal, this illustrates the link between training frequency and muscle development.*

### 5. Muscle Group Count
Across **58 training days**, I worked **10 different muscle groups**, with the greatest focus on **Shoulders (64%)** and the least on **Glutes (9%)**.

### 6. Type of Training After Strength Workouts
- **No additional training (neither cardio nor core/wrist/forearm):** 30 times (**52%**)  
- **Cardio:** 23 times (**40%**)  
- **Core/Wrist/Forearm (CWF):** 5 times (**9%**)  

### 7. Total Training in 3 Months (100 Days)
I trained on **58 of 100 days**, accounting for **58% of the period**.

### 8. Average Weekly Frequency per Muscle Group
Between **weeks 18 and 32 of 2025**, I recorded **58 workouts**.  
- Most muscle groups were trained **once per week**.  
- **Shoulders** and **Triceps** were trained **twice per week**, showing an emphasis on the upper body.  
- Leg muscles (**Quadriceps, Glutes, Hamstrings**) were trained less frequently, highlighting an opportunity for a more balanced plan.  
*Note: Cardio days were entered in all three “muscle group” columns but counted as only one session per day.*

### 9. Upper vs. Lower Body Training
- **Upper body:** 44 sessions  
- **Lower body:** 12 sessions  
- **Other (full cardio days):** 2 sessions  

### 10. Average Rest Days
The average rest period between workouts was **2 days**.  
While consistency was maintained, some weeks included longer breaks for deeper recovery.  
Overall, most rests were **short (1–2 days)**, complemented by occasional longer breaks.

### 11. Average Session Volume
Excluding cardio and null entries, the 47 recorded training days consistently involved 3 muscle groups per session. This reflects a balanced and consistent approach to workout planning.

---
## Methodology, Reasoning, and Motivation

All of these questions arose from **pure curiosity** and a desire to understand my training patterns, identify trends, and discover areas for improvement. I wanted to quantify how often I trained, which muscle groups were prioritized, and how consistent my workouts were over time.

### 1. Real Week Column
I created a new column called **“Real week”** to map each workout to its actual calendar week in 2025. The original **week** column only counted weeks based on the order of training days, not the actual calendar dates, so it did not provide accurate weekly frequency. With **Real week**, I could calculate **average trainings per week** more reliably.

### 2. Training Focus Column
I added a **“Training Focus”** column to categorize workouts as **Upper body**, **Lower body**, or **Other**:

- **Upper body**: Chest, Back, Biceps, Triceps, Shoulders  
- **Lower body**: Quadriceps, Glutes, Hamstrings, Calves  
- **Other**: Any session that doesn’t fall into the above categories  

This allowed me to answer questions like how often each area was trained in total and compare upper vs. lower body frequency.

### 3. Muscle Group Analysis (Question 5)
For the **muscle group count**, I copied the columns **Date, Weekday Plan, Muscle_Group_1, Muscle_Group_2, and Muscle_Group_3** into **Power Query**, then **unpivoted** them to a **long format**. I also added the **Real week** column to this new table.

This step enabled me to see **how many times each muscle group was trained** across the 58 total workouts. It was necessary because some muscle groups, like Shoulders, appeared multiple times per week, and I wanted the total frequency over the period.

### 4. Pivot Table & Average per Week (Question 8)
Using my central dataset (**GymTracker**), I created a **Pivot Table** to count how many times each muscle group was trained per week. I then enabled the **Data Model** and added a **DAX measure** to calculate the **average number of times each muscle group was trained per week**:

```DAX
measure_name = avg_count
=DIVIDE(
    COUNTROWS(question_5),              -- total number of training records
    DISTINCTCOUNT(question_5[real_week]) -- number of unique weeks
)

This measure ensured that the average was calculated **per week** rather than per day or overall, giving a more accurate reflection of training consistency.

## Overall Reasoning

Each step was designed to systematically analyze my workouts:

- **Frequency per week** shows consistency
- **Day-of-week analysis** identifies patterns in gym attendance
- **Muscle group count and focus** highlights emphasis on certain muscles and identifies potential imbalances
- **Rest patterns** reveal recovery periods and pacing
- **Session volume** shows training intensity and structure

By combining these methods, I was able to construct a **complete picture of my 100-day training period**, quantify habits, and highlight opportunities for a **more balanced and efficient routine**.

---
## 📊 Next Steps
- Perform analysis of progress and performance trends (weights lifted, reps, RIR).  
- Build visualizations to show improvement over time.  
- Generate actionable insights on training patterns.  

---

- During analysis, I detected 2 typos (‘Caardio’ instead of ‘Cardio’ in the column muscle_group_1, "Shoulder" instead of "Shoulders" in the column muscle_group_2). The errors were corrected in the cleaning stage to maintain consistency

## 🚀 Skills Demonstrated
- Data cleaning and transformation with **Power Query (M language)**  
- Data typing and error handling (`try...otherwise`)  
- Structuring raw exercise logs into a quantifiable dataset  
- Preparing the foundation for **analysis and visualization**  

---
