# Statistical Analysis of Heart Disease Dataset

## Overview
This notebook presents a statistical analysis of a heart disease dataset.
The aim of the study is to investigate whether there is a statistically significant difference
in age between individuals with and without heart disease.
Appropriate statistical tests are selected after formally checking the required assumptions.

## Research Question
Is there a statistically significant difference in age between individuals
with heart disease and those without heart disease?

## Statistical Hypotheses

Let:
- Group 1 represent individuals without heart disease
- Group 2 represent individuals with heart disease

**Null Hypothesis (H₀):**  
There is no significant difference in age between individuals with and without heart disease.

**Alternative Hypothesis (H₁):**  
There is a significant difference in age between individuals with and without heart disease.

**Significance Level:**
The significance level for this analysis is set at α = 0.05.

## Dataset Description
The dataset contains clinical and demographic information of individuals. The primary variables used in this analysis are:
- **Age:** Age of the individual (continuous variable)
- **HeartDisease:** Indicator variable
  - 0 = No heart disease
  - 1 = Heart disease
The dataset is divided into two independent groups based on heart disease status and has been loaded into a pandas DataFrame.

### Initial Data Exploration (EDA)
The dataset contains 1025 entries and 14 columns. An initial check for missing values across all columns revealed that there are no missing entries, ensuring data completeness for the analysis.

Descriptive statistics for the numerical columns (age, trestbps, chol, thalach, oldpeak) show their central tendency, spread, and range, including mean, standard deviation, minimum, maximum, and quartile values.

#### Numerical Feature Distributions
- **Age:** The age distribution is somewhat symmetric to slightly left-skewed, indicating a wide range of ages in the dataset. Some potential outliers were observed at the higher end of the age spectrum.
- **Trestbps (Resting Blood Pressure):** The distribution appears slightly right-skewed, suggesting that most individuals have lower to moderate resting blood pressure, with some individuals exhibiting higher values, potentially as outliers.
- **Chol (Cholesterol):** The cholesterol distribution is right-skewed, with a notable number of outliers at higher cholesterol levels.
- **Thalach (Maximum Heart Rate Achieved):** This distribution shows a left-skew, indicating that a majority of individuals achieved higher heart rates, with fewer at lower rates.
- **Oldpeak (ST Depression Induced by Exercise):** This variable is heavily right-skewed, with a significant concentration of values at the lower end (including zero), and several outliers representing higher ST depression values.

#### Categorical Feature Distributions
- **Sex:** The dataset contains more male (1) than female (0) individuals.
- **CP (Chest Pain Type):** Chest pain type 0 (typical angina) is the most frequently observed, followed by type 2 (non-anginal pain).
- **FBS (Fasting Blood Sugar > 120 mg/dl):** A large majority of individuals have a fasting blood sugar below or equal to 120 mg/dl (0).
- **Restecg (Resting Electrocardiographic Results):** Types 0 (normal) and 1 (ST-T wave abnormality) are the dominant categories.
- **Exang (Exercise Induced Angina):** More individuals do not experience exercise-induced angina (0) compared to those who do (1).
- **Slope (Slope of the Peak Exercise ST Segment):** Type 2 (upsloping) is the most frequent slope, followed by type 1 (flat).
- **CA (Number of Major Vessels Colored by Fluoroscopy):** A significant majority of individuals have 0 major vessels colored, indicating less severe coronary artery disease.
- **Thal (Thalassemia):** Types 2 (normal) and 3 (fixed defect) are the most dominant categories for thalassemia.
- **Target (Heart Disease Status):** The dataset is relatively balanced, with a slightly higher count of individuals with heart disease (1) than without (0).

## Assumption Checking and Statistical Test Results

### Normality Assumption Checking
Normality of the age distributions for both groups (individuals with and without heart disease) was assessed using the Shapiro–Wilk test. The test yielded the following p-values:
- **Heart Disease Group:** p-value = 7.323e-05
- **No Heart Disease Group:** p-value = 1.836e-09

Since both p-values are significantly less than the significance level (α = 0.05), we reject the null hypothesis of normality for both groups. This indicates that the age distributions are not normally distributed, necessitating the use of a non-parametric statistical test.

### Mann-Whitney U Test Results
Given the violation of the normality assumption and the presence of two independent groups, the non-parametric Mann–Whitney U test was performed to compare the age distributions between individuals with and without heart disease.

- **Mann-Whitney U statistic:** 167644.0
- **P-value:** 1.4676e-14

With a p-value (1.4676e-14) far less than the significance level (α = 0.05), we reject the null hypothesis. This indicates that there is a statistically significant difference in age between individuals with heart disease and those without heart disease.

## Clinical Variable Analysis and Effect Size

This section summarizes the key differences observed in various clinical variables between individuals with and without heart disease, based on the exploratory data analysis and statistical tests performed.

### Numerical Clinical Variables

Analysis of numerical clinical variables (`trestbps`, `chol`, `thalach`, `oldpeak`) revealed distinct patterns between the two groups. The box plots (as shown in **Section 11, Cell 629de205**) provide a visual comparison of these distributions, complemented by the descriptive statistics.

*   **Resting Blood Pressure (trestbps)**:
    *   **No Heart Disease (target=0)**: Mean `134.11` mmHg (Std `18.58`)
    *   **Heart Disease (target=1)**: Mean `129.25` mmHg (Std `16.11`)
    *   Individuals without heart disease tend to have slightly higher resting blood pressure on average.

*   **Cholesterol (chol)**:
    *   **No Heart Disease (target=0)**: Mean `251.29` mg/dl (Std `49.56`)
    *   **Heart Disease (target=1)**: Mean `240.98` mg/dl (Std `53.01`)
    *   Individuals without heart disease show a slightly higher mean cholesterol level.

*   **Maximum Heart Rate Achieved (thalach)**:
    *   **No Heart Disease (target=0)**: Mean `139.13` bpm (Std `22.57`)
    *   **Heart Disease (target=1)**: Mean `158.59` bpm (Std `19.10`)
    *   Individuals with heart disease, on average, achieve a significantly higher maximum heart rate.

*   **Oldpeak (ST depression induced by exercise relative to rest)**:
    *   **No Heart Disease (target=0)**: Mean `1.60` (Std `1.29`)
    *   **Heart Disease (target=1)**: Mean `0.57` (Std `0.77`)
    *   Individuals with heart disease tend to have a lower 'oldpeak' value, suggesting less ST depression during exercise.

These quantitative summaries align with the visual representations in the box plots, highlighting differences in central tendency and variability.

### Categorical Clinical Variables

The distributions of categorical clinical variables (`sex`, `cp`, `fbs`, `restecg`, `exang`, `slope`, `ca`, `thal`) also showed notable differences between individuals with and without heart disease. The count plots (as shown in **Section 11, Cell d4dd19cf**) offer a visual breakdown of these distributions, which are further quantified by frequency and proportion tables.

*   **Sex**:
    *   Among those without heart disease, a higher proportion are male (0.83). 
    *   Among those with heart disease, males still represent a larger group (0.57) but the proportion of females is higher (0.43) compared to the no heart disease group.

*   **Chest Pain Type (cp)**:
    *   Individuals without heart disease predominantly have atypical angina (`cp=0`, 0.75 proportion). 
    *   Individuals with heart disease show a more diverse distribution, with a higher proportion having non-anginal pain (`cp=2`, 0.42) and atypical angina (`cp=1`, 0.25).

*   **Fasting Blood Sugar (fbs)**:
    *   The proportion of individuals with `fbs > 120 mg/dl` (`fbs=1`) is slightly higher in the group without heart disease (0.16) compared to the group with heart disease (0.13).

*   **Resting Electrocardiographic Results (restecg)**:
    *   **No Heart Disease**: Primarily showing normal (`restecg=0`, 0.57) or ST-T wave abnormality (`restecg=1`, 0.41).
    *   **Heart Disease**: A higher proportion shows ST-T wave abnormality (`restecg=1`, 0.59) and a lower proportion of normal (`restecg=0`, 0.41).

*   **Exercise Induced Angina (exang)**:
    *   A higher proportion of individuals without heart disease experience exercise-induced angina (`exang=1`, 0.55).
    *   Conversely, a much higher proportion of individuals with heart disease do *not* experience exercise-induced angina (`exang=0`, 0.87).

*   **Slope of the peak exercise ST segment (slope)**:
    *   **No Heart Disease**: Mostly flat (`slope=1`, 0.65).
    *   **Heart Disease**: Predominantly upsloping (`slope=2`, 0.65), indicating a positive relationship with heart disease status.

*   **Number of major vessels (0-3) colored by flourosopy (ca)**:
    *   A very high proportion of individuals with heart disease have `ca=0` (0.79), meaning no major vessels colored.
    *   Individuals without heart disease show a more even distribution across `ca=0`, `ca=1`, and `ca=2` (around 0.33, 0.32, 0.23 respectively), suggesting a higher likelihood of vessel abnormalities in this group compared to those with heart disease for the `ca` variable.

*   **Thal**:
    *   **No Heart Disease**: Most frequently reversible defect (`thal=3`, 0.64).
    *   **Heart Disease**: Mostly normal (`thal=2`, 0.78), indicating a strong association with heart disease status.

These categorical analyses indicate substantial differences in the prevalence of specific categories within each variable, offering insights into potential risk factors and diagnostic markers.

### Effect Size of Age Difference

Beyond the statistical significance indicated by the Mann-Whitney U test (p-value: 1.47e-14), we calculated Rosenthal's r effect size to quantify the practical significance of the observed age difference.

*   **Rosenthal's r effect size**: `r = 0.2402`
*   **Interpretation**: This value indicates a **small effect size**. While statistically significant, the magnitude of the age difference between the groups is not very large.

*   **Direction of Age Difference**: Contrary to some intuitive expectations, the analysis revealed that individuals **without heart disease** tend to be **older** on average (mean age: `56.57` years) than individuals **with heart disease** (mean age: `52.41` years) in this dataset. This finding is consistent with the descriptive statistics for age and warrants further investigation into potential confounding factors or unique characteristics of this dataset.

## Overall Conclusion

This comprehensive statistical analysis of the heart disease dataset aimed to identify statistically significant differences in various clinical variables between individuals with and without heart disease. The initial analysis focused on age, revealing a statistically significant difference between the two groups, as indicated by the Mann-Whitney U test (p-value = 1.47e-14, far below α = 0.05). This suggests that age is a relevant factor in heart disease. However, the calculated Rosenthal's r effect size of 0.2402 indicates a "small" practical effect, implying that while the difference is statistically significant, age alone may not be a strong predictor.

Further exploratory data analysis and comparative visualizations highlighted several key differences:

- **Age**: Individuals without heart disease tend to be older on average (mean age ~56.57) than those with heart disease (mean age ~52.41), which was an unexpected direction given initial assumptions, but is robustly supported by the Mann-Whitney U test and visual analysis.
- **Sex**: There is a higher proportion of males (sex=1) among individuals with heart disease (57.03%) compared to those without heart disease (82.77%). Conversely, females (sex=0) appear to have a higher prevalence of heart disease in this dataset (42.97% vs 17.23%).
- **Chest Pain Type (cp)**: A significantly higher proportion of individuals with heart disease exhibit asymptomatic chest pain (cp=0) compared to those without heart disease (75.15% vs 23.19%). Conversely, individuals without heart disease show a higher prevalence of typical angina (cp=3).
- **Thalach (Maximum Heart Rate Achieved)**: Individuals with heart disease generally have a higher maximum heart rate (mean ~158.59 bpm) compared to those without heart disease (mean ~139.13 bpm). This is also visually evident from the box plots.
- **Oldpeak (ST depression induced by exercise relative to rest)**: Individuals with heart disease tend to have lower `oldpeak` values (mean ~0.57) compared to those without heart disease (mean ~1.60), suggesting different exercise-induced ST depression patterns.
- **Slope (The slope of the peak exercise ST segment)**: A larger proportion of individuals with heart disease have an upsloping ST segment (slope=2) (64.64%) compared to those without heart disease (25.85%). Conversely, a higher proportion of individuals without heart disease exhibit flat (slope=1) or downsloping (slope=0) ST segments.
- **CA (Number of major vessels (0-3) colored by fluoroscopy)**: Individuals with heart disease overwhelmingly have fewer major vessels colored (ca=0) (78.90%) compared to those without heart disease (32.67%).
- **Thal (Thalassemia)**: Individuals with heart disease show a much higher proportion of fixed defect (thal=2) (78.33%) compared to those without heart disease (26.45%).

These findings suggest that a combination of factors, including age, sex, chest pain characteristics, exercise-related indicators, and vessel status, are significantly associated with heart disease status. The comprehensive EDA provided strong visual and statistical evidence for these relationships.

## Future Work

To build upon this exploratory analysis and align with MSc-level aspirations, the following future work is recommended:

1.  **Advanced Statistical Modeling**: While the Mann-Whitney U test identified significant differences, exploring multivariate statistical models (e.g., logistic regression, ANCOVA) could help understand the independent and combined effects of clinical variables on heart disease, while controlling for potential confounders.

2.  **Machine Learning for Predictive Analysis**: Develop and evaluate machine learning models (e.g., Support Vector Machines, Random Forests, Gradient Boosting Machines, Neural Networks) to predict heart disease presence. This would involve:
    *   **Feature Engineering**: Create new features from existing ones (e.g., BMI from height/weight if available, or interaction terms).
    *   **Model Training and Evaluation**: Split data into training, validation, and test sets, and rigorously evaluate model performance using metrics like accuracy, precision, recall, F1-score, and ROC AUC.
    *   **Hyperparameter Tuning**: Optimize model parameters to achieve the best predictive performance.

