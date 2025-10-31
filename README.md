# 🩺 mHealth Analysis Project

## Overview
This project analyzes **multi-subject wearable sensor data** from mHealth logs to explore how **physical activity levels** affect **acceleration** and **heart rate**.  
It includes data cleaning, feature engineering, statistical testing, and visual analytics.

---

# This project is not ``` Open Sourced ``` , No external PR's will be accepted 

## 📁 Project Structure

```
Data-Analytics-Assignment-4/
│
├── CONTRIBUTORS.md        
├── LICENSE                              
├── README.md        
├── RULES.md
└── DA IA/                     
    ├── DA_IA_4.ipynb                    <-- Main Project
    ├── activity_summary_statistics.csv
    ├── mHealth_subject1.log
    ├── mHealth_subject10.log
    ├── mHealth_subject2.log
    ├── mHealth_subject3.log
    ├── mHealth_subject4.log
    ├── mHealth_subject5.log
    ├── mHealth_subject6.log
    ├── mHealth_subject7.log
    ├── mHealth_subject8.log
    ├── mHealth_subject9.log
    ├── pairwise_comparisons.csv
    └─── .ipynb_checkpoints
        ├── Untitled0-checkpoint.ipynb
```
---

##  Usage Instructions

### Step-by-Step Execution

#### 1. *Setup Phase* (Blocks 1-2)
- Run Block 1 to import libraries
- Run Block 2 to load all subject data files
- *Expected Output*: Confirmation of loaded subjects and total samples

#### 2. *Data Exploration* (Block 3)
- Displays basic dataset information
- Shows first few rows and data types
- *Expected Output*: DataFrame preview and statistics

#### 3. *Data Cleaning* (Blocks 4-6)
- Block 4: Check and impute missing values
- Block 5: Remove null class (label 0)
- Block 6: Detect and remove outliers using IQR method
- *Expected Output*: Cleaning summary statistics

#### 4. *Feature Engineering* (Block 7)
- Creates acceleration magnitude features
- Estimates heart rate from ECG
- Adds activity name labels
- *Expected Output*: New feature confirmation

#### 5. *Exploratory Data Analysis* (Blocks 8-12)
- Block 8: Activity distribution visualization
- Block 9: Descriptive statistics by activity
- Block 10: Acceleration comparison plots
- Block 11: Heart rate visualization
- Block 12: Correlation analysis
- *Expected Output*: Multiple visualizations and statistics tables

#### 6. *Hypothesis Testing* (Blocks 13-20)
- Block 13: Setup test data
- Blocks 14-16: T-tests (High vs Low intensity)
- Blocks 17-18: ANOVA (Multiple activities)
- Block 19: Post-hoc pairwise comparisons
- Block 20: ANOVA visualizations
- *Expected Output*: Statistical test results with p-values

#### 7. *Additional Analysis* (Block 21)
- Inter-subject variation analysis
- Subject-activity heatmaps
- *Expected Output*: Variation metrics and heatmaps

#### 8. *Final Summary* (Block 22)
- Comprehensive results summary
- Data export options
- *Expected Output*: Summary statistics and saved files

---

## 🔬 Analysis Pipeline

### 1. Data Loading

Load 10 subject files → Combine into single DataFrame → Validate data integrity


### 2. Data Cleaning

Check missing values → Imputation (forward/backward fill) → 
Remove null class → Outlier detection (IQR method) → 
Remove outliers → Validate cleaned data


*Outlier Detection Method*: 
- Uses Interquartile Range (IQR)
- Threshold: 3 × IQR
- Formula: [Q1 - 3×IQR, Q3 + 3×IQR]

### 3. Feature Engineering

Raw sensor data → Calculate magnitude:
- Chest acceleration magnitude = √(x² + y² + z²)
- Ankle acceleration magnitude = √(x² + y² + z²)
- Arm acceleration magnitude = √(x² + y² + z²)

ECG signals → Heart rate estimation:
- Group by subject and activity
- Calculate standard deviation
- Apply scaling factor: HR = 70 + (ECG_std × 30)


### 4. Statistical Analysis

*A. Descriptive Statistics*
- Mean, standard deviation, min, max for each activity
- Sample sizes and distributions
- Coefficient of variation across subjects

*B. Inferential Statistics*
- Independent T-tests for binary comparisons
- One-way ANOVA for multiple group comparisons
- Post-hoc pairwise tests with Bonferroni correction

---

## 📈 Statistical Tests Explained

### T-Test (Independent Samples)

*Purpose*: Compare means between two independent groups

*Hypotheses*:
- H₀ (Null): μ₁ = μ₂ (no difference in means)
- H₁ (Alternative): μ₁ ≠ μ₂ (means are different)

*Test Statistic*: 

t = (x̄₁ - x̄₂) / √(s₁²/n₁ + s₂²/n₂)


*Interpretation*:
- *p < 0.05*: Reject null hypothesis (significant difference)
- *p ≥ 0.05*: Fail to reject null hypothesis (no significant difference)

*Effect Size (Cohen's d)*:

d = (μ₁ - μ₂) / σ_pooled

- |d| < 0.2: Small effect
- 0.2 ≤ |d| < 0.5: Medium effect
- |d| ≥ 0.5: Large effect

*Our Application*:
- Compare high-intensity (Jogging, Running) vs low-intensity (Sitting, Standing)
- Variables: chest acceleration magnitude, heart rate estimate

### One-Way ANOVA

*Purpose*: Compare means across three or more groups

*Hypotheses*:
- H₀: μ₁ = μ₂ = μ₃ = ... = μₖ (all group means equal)
- H₁: At least one group mean differs

*Test Statistic*:

F = MS_between / MS_within


*Interpretation*:
- *p < 0.05*: At least one group differs significantly
- *p ≥ 0.05*: No significant differences between groups

*Post-Hoc Tests*:
- When ANOVA is significant, conduct pairwise comparisons
- *Bonferroni Correction*: α_adjusted = α / number_of_comparisons
- Controls for Type I error inflation in multiple comparisons

*Our Application*:
- Compare 5 activities: Walking, Jogging, Running, Sitting, Cycling
- Variables: chest acceleration magnitude, heart rate estimate

---

## Results Interpretation

### Expected Findings

#### 1. *Acceleration Magnitude*

*High-Intensity Activities* (Jogging, Running):
- Expected Mean: 12-20 m/s²
- Higher variability due to dynamic movements
- Significant difference from low-intensity activities

*Low-Intensity Activities* (Sitting, Standing):
- Expected Mean: 9-11 m/s² (close to gravity)
- Lower variability due to minimal movement
- Primarily captures gravitational acceleration

*Statistical Significance*:
- T-test p-value: Expected < 0.001 (highly significant)
- Cohen's d: Expected > 0.8 (large effect size)

#### 2. *Heart Rate Estimate*

*High-Intensity Activities*:
- Expected Range: 100-140 bpm
- Reflects increased cardiovascular demand

*Low-Intensity Activities*:
- Expected Range: 65-80 bpm
- Near resting heart rate

*Statistical Significance*:
- T-test p-value: Expected < 0.01 (significant)
- Moderate to large effect size

#### 3. *ANOVA Results*

*Expected Pattern* (Acceleration Magnitude):

Running > Jogging > Walking > Cycling > Sitting


*F-statistic*: Expected > 100 (very large)
*P-value*: Expected < 0.0001 (extremely significant)

*Post-Hoc Comparisons*:
- Running vs Sitting: Highly significant (p < 0.001)
- Jogging vs Walking: Moderately significant (p < 0.05)
- Walking vs Sitting: Significant (p < 0.01)

### Interpretation Guidelines

#### P-Value Interpretation
- *p < 0.001: Very strong evidence against H₀ ()
- *p < 0.01: Strong evidence against H₀ (*)
- *p < 0.05: Moderate evidence against H₀ ()
- *p ≥ 0.05*: Insufficient evidence to reject H₀ (ns)

#### Practical Significance
- Consider both statistical and practical significance
- Large sample sizes can yield significant p-values for trivial differences
- Always examine effect sizes and mean differences

#### Visualizations
- *Box plots*: Show distribution, median, quartiles, outliers
- *Violin plots*: Show full distribution shape
- *Heatmaps*: Reveal patterns across subjects and activities

---
