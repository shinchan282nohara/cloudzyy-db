# ShieldStat COVID-19 Vaccine Effectiveness Analysis

## Final Research Report

### Executive Summary

This report presents a comprehensive analysis of COVID-19 vaccine effectiveness conducted by Team ShieldStat. Using machine learning approaches combined with the PICO framework from evidence-based medicine, we investigated the extent to which COVID-19 vaccines reduce severe outcomes such as hospitalization and death across different demographics. Our analysis of CDC data demonstrates that vaccination status—particularly booster status—significantly impacts health outcomes, with boosted individuals showing substantially lower rates of hospitalization and death compared to their unvaccinated counterparts. Age remains an important but secondary factor in predicting COVID-19 outcomes when vaccination status is considered.

### Team Members

- Ashutosh Agarwal (22B2187) - Statistical analysis and healthcare interpretation
- Rahul Majumder (22B2482) - Data collection and exploratory data analysis
- Shubham Raj (22B0665) - Machine learning modeling and feature engineering
- Himanshu (22B2131) - Report structuring and healthcare implications

### 1. Introduction

#### 1.1 Motivation

The COVID-19 pandemic has fundamentally reshaped global healthcare systems, highlighting the critical importance of vaccines in mitigating severe illness and mortality. Despite widespread vaccination efforts, questions remain about vaccine effectiveness across different population segments and against evolving viral variants. These questions became personally significant to our team when a family member contracted COVID-19 despite receiving a full course of COVAXIN, prompting us to investigate factors that might influence vaccine protection.

#### 1.2 Research Question

Our core research question was formulated using the PICO framework:

> "To what extent do COVID-19 vaccines reduce severe outcomes such as hospitalization and death across different age cohorts?"

Specifically, we sought to determine:

- Whether there exists a statistically significant difference in outcomes between vaccinated and unvaccinated individuals
- If vaccine effectiveness varies by age, time period, or geographical region

#### 1.3 Project Objectives

1. Evaluate real-world effectiveness of COVID-19 vaccination using healthcare hypothesis frameworks
2. Apply machine learning tools to quantify and validate observed effects
3. Identify key factors influencing vaccine effectiveness
4. Provide evidence-based insights to inform public health policy

### 2. Methodology

#### 2.1 PICO Framework Implementation

We structured our research using the PICO framework:

- **Population**: Individuals exposed to COVID-19, grouped by age
- **Intervention**: Receipt of at least one vaccine dose
- **Comparison**: Individuals who remained unvaccinated
- **Outcome**: Infection incidence, hospitalizations, and deaths (per 100,000 population)

The PICO framework was selected over alternatives (FINER, SPIDER, PEO, ECLIPSE) due to its:

- Ability to enable systematic comparison between vaccinated and unvaccinated populations
- Support for quantification of impact on severe outcomes
- Allowance for demographic and temporal subgroup analysis
- Alignment with evidence-based medicine practices used in public health policy

#### 2.2 Dataset Description

Our primary data source was the U.S. CDC COVID-19 Case and Death Rates by Vaccination Status dataset, which:

- Is publicly available and regularly updated
- Covers data from April 2021 to the present
- Spans major COVID-19 variants (Delta, Omicron, etc.)
- Provides aggregate-level (not patient-specific) data
- Is stratified by:
  - Age group (18-29, 30-49, 50-64, etc.)
  - Vaccination status (Unvaccinated, Fully Vaccinated, Boosted)
  - Outcome type (Cases, Hospitalizations, Deaths)
- Uses rates per 100,000 population as its core metric for comparability

Key data fields included:

- `date`: Reporting date used for time-series analysis
- `outcome`: Type measured (case, hospitalization, or death)
- `age_group`: Population age category
- `vaccination_status`: Status at time of outcome
- `rate_per_100k`: Normalized outcome rate
- `count`: Absolute number of observed outcomes
- `population`: Denominator for rate calculations

#### 2.3 Confounding Variable Analysis

We identified several potential confounding variables:

1. **Age**: Older individuals are both more likely to be vaccinated and at higher risk of severe outcomes, potentially inflating perceived vaccine ineffectiveness if not adjusted for.

2. **Comorbidities**: Chronic conditions may increase risk independently of vaccination status.

3. **Prior Infection/Natural Immunity**: Some unvaccinated individuals may have immunity from prior infection, not captured in the dataset.

4. **Health-Seeking Behavior & Access**: Vaccinated individuals may differ in healthcare access, testing frequency, or risk avoidance behavior.

We employed stratified analysis by age groups and rate standardization per 100,000 population to partially address these confounding factors.

#### 2.4 Machine Learning Approach

We implemented a Random Forest Classifier with the following specifications:

- **Target Variable**: Outcome category (Case, Hospitalization, Death)
- **Features**:
  - Age Group (encoded)
  - Unvaccinated Rate
  - Vaccinated Rate
  - Boosted Rate
- **Training Process**:
  - Data encoding using LabelEncoder
  - Train-test split (80:20)
  - Random Forest model fitting
- **Evaluation Metrics**:
  - Classification Report (Precision, Recall, F1-Score)
  - Confusion Matrix
  - Feature Importance

Random Forest was selected due to its:

- Ability to handle non-linear relationships between age and vaccination rates
- Robustness to noise and outliers in health datasets
- Suitability for small-to-moderate sized datasets
- Non-reliance on normal distribution assumptions
- Interpretability through feature importance scores

### 3. Results and Analysis

#### 3.1 Initial Data Overview

Our exploratory data analysis revealed that:

- Deaths and hospitalizations represent only a small fraction of total COVID-19 cases
- Base vaccination somewhat reduced hospitalization rates, while boosting led to a significant reduction
- Monthly averages showed distinct peaks corresponding to COVID-19 waves

#### 3.2 Age Stratification Analysis

Death rates among unvaccinated individuals were over twice as high as those in the vaccinated group. Booster shots further reduced the rate dramatically, approaching one-tenth the death rate of unvaccinated individuals.

#### 3.3 Model Performance

Our Random Forest Classifier achieved:

- Overall accuracy: 90%
- Strong performance in real-world outcome prediction based on vaccination status and age
- High recall (0.94) for death prediction, crucial for mortality risk assessment
- Slightly lower recall (0.82) for hospitalizations, indicating some false negatives
- Clear differentiation between cases and deaths, supporting reliable vaccine-linked severity prediction

#### 3.4 Feature Importance

Feature importance analysis revealed:

1. **Boosted Rate**: Most important predictor, directly supporting our hypothesis that boosters significantly reduce severe COVID outcomes
2. **Vaccinated Rate**: Also highly important, confirming that base vaccination provides protective effects, though less than boosters
3. **Age Group**: Lowest importance among our features, suggesting that vaccination status dominates in predicting outcomes in our dataset

#### 3.5 Age-wise Analysis

- Higher unvaccinated rates correlated with worse outcomes across age groups
- Boosted groups consistently showed better protection
- Children (0-4, 5-11) and teenagers (12-17) showed mixed signals due to lower vaccination coverage
- Elderly populations still faced risks despite vaccination, suggesting age-related vulnerability remains a concern

#### 3.6 Variant-wise Analysis

- Omicron variants (especially XBB.1.5 and BA.2+) dominated in terms of all outcomes
- Outcome counts were nearly identical within each variant period
- Delta caused more severe outcomes than earlier variants like Alpha and Omicron BA.1
- Alpha and Omicron BA.1 showed the lowest impact
- Emerging subvariants continued to pose high burdens

#### 3.7 Confounding Effect Analysis

Cluster analysis identified:

- Older adults (80+, 65-79, 50-64) were more likely to be boosted and had lower unvaccinated rates
- Younger groups showed lower booster rates and higher unvaccinated rates
- Age was confirmed as a confounder: older individuals had both higher baseline risk and higher vaccination rates

### 4. Discussion

#### 4.1 Public Health Implications

Our findings support several key public health takeaways:

1. **Boosters are critical**: The strong predictive power of the boosted rate underscores the importance of booster campaigns in reducing severe COVID-19 outcomes.

2. **Base vaccination helps, but boosting amplifies protection**: While vaccinated individuals fare better than unvaccinated ones, boosted individuals show the best outcomes across all outcome classes.

3. **Age matters, but less than vaccination status**: Though age group is a known risk factor, our model shows that vaccination status has a more direct and dominant influence on predicting outcomes.

4. **Variant-specific considerations**: Different viral variants show varying impacts, suggesting the need for continued surveillance and updated booster formulations.

#### 4.2 Study Limitations

Several limitations should be considered when interpreting our results:

1. **Aggregate data**: The use of population-level data rather than individual-level data limits our ability to control for all potential confounders.

2. **Unmeasured confounders**: We could not account for factors such as comorbidities, prior infection status, and health-seeking behaviors.

3. **Temporal changes**: Vaccine effectiveness may wane over time, and our cross-sectional analysis cannot fully capture this dynamic.

4. **Reporting biases**: Differences in testing and reporting practices may affect the accuracy of our data.

### 5. Conclusion

#### 5.1 Key Findings

Our analysis demonstrates that after adjusting for age, COVID-19 vaccines—particularly booster doses—show a protective effect against severe outcomes. This protection is strongest in high-risk elderly populations and most evident during high-transmission variant waves.

#### 5.2 Future Research Directions

Future studies should:

1. Incorporate individual-level data to better control for confounders
2. Assess vaccine effectiveness against newer variants
3. Examine the impact of different vaccine types and combinations
4. Investigate the duration of protection and optimal timing for booster doses

### 6. References

1. Polack FP, Thomas SJ, Kitchin N, et al. Safety and Efficacy of the BNT162b2 mRNA COVID-19 Vaccine. N Engl J Med. 2020;383(27):2603–2615.

2. Baden LR, El Sahly HM, Essink B, et al. Efficacy and Safety of the mRNA-1273 SARS-CoV-2 Vaccine. N Engl J Med. 2021;384(5):403–416.

3. Thompson MG, Burgess JL, Naleway AL, et al. Prevention and Attenuation of Covid-19 with the BNT162b2 and mRNA-1273 Vaccines. MMWR Morb Mortal Wkly Rep. 2021;70(13):495–500.

4. Ritchie H, Mathieu E, Rodés-Guirao L, et al. Coronavirus Pandemic (COVID-19). Our World in Data. Updated January 2025. Accessed April 10, 2025.

5. Centers for Disease Control and Prevention. COVID-19 Vaccine Effectiveness Research. CDC; 2024. Accessed April 10, 2025.

6. World Health Organization. COVID-19 Vaccine Position Paper. WHO; 2021. Accessed April 10, 2025.

7. European Centre for Disease Prevention and Control. COVID-19 Vaccine Effectiveness Report. ECDC; 2021. Accessed April 10, 2025.

8. Office for National Statistics. COVID-19 Vaccination and Hospital Admissions. ONS; 2022. Accessed April 10, 2025.

9. Obermeyer Z, Emanuel EJ. Predicting the Future — Big Data, Machine Learning, and Clinical Medicine. N Engl J Med. 2016;375(13):1216–1219.

10. Straus SE, Richardson WS, Glasziou P, Haynes RB. Evidence-Based Medicine: How to Practice and Teach EBM. 5th ed. Churchill Livingstone; 2018.
