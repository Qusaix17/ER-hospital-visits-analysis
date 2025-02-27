# Methodology

## 1️⃣ ASK: Defining the Problem

### Why do this project?

The main goal of this analysis is to understand emergency room (ER) visit patterns across multiple hospitals. The key questions driving this project are:

- Which hospitals have the highest number of emergency visits?
- Which hospital has the most ER re-visits?
- Is there a trend in ER visits based on gender and age?
- Which age group visits the ER the most?

### Purpose of this Analysis

This project serves as a statistical exploration of emergency hospital visits within MNGH hospitals. By analyzing available data, the goal is to identify patterns and trends in patient demographics, visit frequency, and hospital utilization. While the findings may not directly lead to actionable solutions due to data limitations, the project serves as a practical exercise in data collection, cleaning, querying, and visualization.

## 2️⃣ PREPARE: Data Collection

### What data is needed?

To answer these questions, the following datasets were gathered from MNGH open data and Ministry of Health resources:

| Type of Data                    | Source                | Status   | Notes                     |
|----------------------------------|-----------------------|----------|---------------------------|
| Emergency hospital visit data    | MNGH Open Data        | Collected| Data recorded monthly     |
| Demographics (age, gender, etc.) | MNGH Open Data        | Collected| Included in hospital data |
| Healthcare facility data         | Ministry of Health (MOH) | Collected| Included in hospital data |

**Table 1.1:** Data used in the project

### Data Cleaning & Preparation

Once the datasets were collected, the following steps were taken to prepare the data for analysis:

✔ Removed empty or inconsistent records to ensure accuracy  
✔ Created a new column for age (in months and years) for detailed analysis of newborns  
✔ Added a location column to classify hospitals based on city (for potential geographic insights)  
✔ Merged all datasets into a single structured table to enable SQL querying and analysis  

## 3️⃣ PROCESS: Data Transformation & Queries

To extract meaningful insights, SQL queries were used to analyze the cleaned dataset:

### Key Data Transformations & Queries

- **Hospital-wise ER Visit Count**:  
  → Summed total ER visits for each hospital to identify the busiest hospitals
  
- **Gender-Based Trends**:  
  → Counted visits by male vs. female patients to detect gender-based differences
  
- **Age Group Distribution**:  
  → Categorized visits into age groups for better visualization
  
- **Age & Gender Cross-Analysis**:  
  → Mapped age groups with gender to identify trends in specific demographics

## 4️⃣ ANALYZE & SHARE: Insights from the Data

This section presents insights derived from the collected data. Note that some hospital data is missing for later years, meaning a value of zero in the dataset does not indicate an actual absence of ER visits but rather a lack of available data.

### 1️⃣ Total ER Visits by Hospital (2020 - 2023)

- King Fahad Hospital recorded the highest number of ER visits (307K) in 2020, but data is missing for 2023.
- Dammam Imam Abdulrahman Bin Faisal Hospital showed an increasing trend, reaching 76K visits in 2022 and 70K in 2023.  
  📝 *Possible Interpretation*: Dammam Hospital’s rising numbers could indicate higher patient demand or better accessibility. Due to data gaps in later years, it’s difficult to analyze the full trend, meaning the real visit numbers could be higher than reported.

### 2️⃣ ER Revisits by Hospital

- King Fahad Hospital had the highest number of revisits (424K), indicating that many patients returned multiple times.
- Dammam Hospital recorded 144K revisits, significantly lower but still notable.  
  📝 *Possible Interpretation*: Frequent revisits could suggest chronic illness cases, recurring medical issues, or patients returning for follow-ups. King Fahad Hospital’s high revisit rate might indicate that it serves a higher number of critical or recurring cases compared to other hospitals. However, missing revisiting data complicates full interpretation.

### 3️⃣ ER Visits by Gender

- Female patients accounted for 568K visits, while male patients had 480K visits. The higher number of female visits was consistent across all hospitals.  
  📝 *Possible Interpretation*: This could indicate that women are more proactive in seeking medical care. Potential explanations include maternal health visits, chronic conditions, or healthcare-seeking behavior differences.

### 4️⃣ ER Visits by Age Group

- Young Adults (~18-30) made up the largest group (29.65%).
- Adults (~30-45) followed with 26.59%.
- Elderly (~60+) accounted for 16.4%, while children had the lowest share (6.2%).  
  📝 *Possible Interpretation*: Young adults leading ER visits might be linked to work stress, accidents, or lifestyle-related conditions. Elderly patients (16.4%) still form a significant portion, likely due to chronic illnesses or age-related health conditions. Lower ER visits for children (6.2%) could mean most pediatric cases are managed in specialized clinics rather than ERs.

### 5️⃣ Gender & Age Group Trends

- Across all age groups, females consistently visited the ER more than males.  
  📝 *Possible Interpretation*: This supports the trend that women may seek medical care more frequently than men. Young and middle-aged adult women may have higher medical care needs due to maternity, chronic illnesses, or increased health awareness.

### 6️⃣ Data Limitations & Considerations

While this analysis provides valuable insights, there are limitations due to missing data:

- **Missing Hospital Data**:  
  Some hospitals have zero values in certain years due to data unavailability, not because there were no visits.
  
- **Lack of Tourism Data**:  
  The project initially aimed to analyze tourism's impact on ER visits, but no open-source tourism data was found.

- **Generalization Limitations**:  
  Data only includes MNGH hospitals, meaning results may not reflect national healthcare trends.

- **Time Constraints**:  
  The dataset covers 2020-2023, but missing values make it difficult to analyze long-term trends or seasonal patterns.

**Final Note:** Despite these limitations, this project serves as a statistical exploration of ER visit trends, demonstrating data analysis techniques using SQL, Power BI, and Python. The findings offer insights into hospital utilization, gender and age trends, and revisit rates, providing a foundation for future research when more complete data is available.

## 5️⃣ LIMITATIONS & CHALLENGES

While this analysis provides valuable insights into ER visit trends, there are some limitations that should be considered:

- **Missing Data**:  
  Some hospital records were incomplete or unavailable in the MNGH open data source, which may affect accuracy.

- **Lack of Tourism Data**:  
  Initially, the project aimed to analyze the impact of tourism on hospital ER visits, but no open-source data was found to support this comparison.

- **Generalization**:  
  The dataset is limited to MNGH hospitals and may not fully represent all ER visits across Saudi Arabia.

- **Time Constraints**:  
  Data was collected only for specific years and months, which may not capture long-term trends or seasonal variations.
