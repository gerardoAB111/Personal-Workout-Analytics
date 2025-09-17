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

## 📊 Next Steps
- Perform analysis of progress and performance trends (weights lifted, reps, RIR).  
- Build visualizations to show improvement over time.  
- Generate actionable insights on training patterns.  

---

- During analysis, I detected 2 typos (‘Caardio’ instead of ‘Cardio’, "Shoulder" instead of "Shoulders"). The errors were corrected in the cleaning stage to maintain consistency

## 🚀 Skills Demonstrated
- Data cleaning and transformation with **Power Query (M language)**  
- Data typing and error handling (`try...otherwise`)  
- Structuring raw exercise logs into a quantifiable dataset  
- Preparing the foundation for **analysis and visualization**  

---
