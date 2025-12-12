# New Aviation Low-Risk Aircraft Purchase Project

## Introduction
This project analyzes aviation accidents and incident data collected from **1962–2023**, covering civil aviation accidents in the USA and selected international waters.
The goal is to provide actionable insights to the business stakeholders to support **informed investment decisions** when purchasing and operating low-risk aircraft for  commercial and private enterprises.  

By analysing historical accident trends, aircraft types, and incident patterns, this analysis will help identify **aircraft with lower operational risk**, ensuring safer investments for the New Aviation division.  

## Key Analysis Questions
To guide the analysis and provide insights relevant to decision-making, I will explore the following questions:

1. **Aircraft Risk Assessment**
   - Which aircraft models have the lowest accident and incident rates historically?
   - Are there trends in accident frequency based on aircraft age or manufacturer?
   
2. **Geographical Patterns**
   - Are certain regions or airspaces associated with higher incident rates?
   - Do accidents in international waters differ significantly from those in the USA?

3. **Operational and Safety Insights**
   - What factors (pilot experience, aircraft type, weather conditions) correlate with higher accident risk?
   - Are there particular operational conditions that consistently show low-risk performance?

## Stakeholder Questions
From a business and investment perspective, stakeholders would want to know:

- Which aircraft models are **safe and reliable for commercial or private operations**?  
- Are there aircraft types that offer **lower insurance costs or regulatory risk**?  
- How does historical safety performance inform **fleet diversification and procurement strategy**?  
- What operational precautions can be implemented to **minimize accident risk** for purchased aircraft?

---

## Project Structure

New-Aviation-LowRisk-AircraftPurchase-Project/
├── .ipynb_checkpoints/   # Auto-saved notebook files (ignored by .gitignore)
├── Data/                 # Dataset folder (tracked)
├── Presentation/         # Powerpoint Slides file(tracked)       
├── .gitignore            # Git ignore rules (tracked)
├── Brian.ipynb           # Main Jupyter notebook (tracked)
└── README.md             # Project overview and instructions (tracked)


## Dataset loading & initial Exploration
The analysis begins by loading the AviationData.csv, which entails approx. 88,000 aviation accidents and incident records from 1962-2023.
This step shows the dataset's structure:
- The number or row and columns
- Features available for analysis
- The initial distribution of the key attributes
- Red flags: missing values, inconsistent formatting or duplicated columns

**N/B This stage informs as on the strategy of cleaning and also ensures that each approach is based on accurate and well understood data.**


### ** Standardizing Column Names**

The original dataset included column names with spaces, punctuation marks, and inconsistent formatting.  
To ensure correct analysis and avoid errors when referencing columns in Python, all column names were standardized by:

- Converting to lowercase  
- Replacing spaces and punctuation with underscores  
- Removing inconsistent characters  

This normalization step ensures that all variables can be accessed easily and consistently throughout the project.

### ** Parsing Date Columns & Missing Values Assessment**

A key part of preparing the dataset involved identifying and converting date fields into proper datetime format. Since aviation accidents are recorded chronologically, parsing these columns correctly allows for trend analysis and time-based insights.

Additionally, a missing values assessment was performed to quantify the completeness of each column.  
Understanding missingness early helps guide decisions on whether to drop, impute, or engineer features during the cleaning and modeling stages.

A working cleaned dataset (`AviationData_working.csv`) was saved after this transformation.


### Missing Value Assessment & Cleaning Decisions

To understand the overall quality of the dataset and guide effective preprocessing, a missing-value analysis was performed. This allowed us to identify columns that contain too many missing values to be analytically useful, as well as columns that are important for safety-risk assessment and must be retained.

##  Key Findings
Several columns show extremely high missing percentages (60–85%). These include:
- `schedule`
- `aircarrier`
- `fardescription`
- `longitude`
- `latitude`

Columns with such high missingness provide limited value for risk evaluation and will be removed from the dataset.

Other columns show moderate missingness but are important for aircraft safety profiling. These will be retained and cleaned through imputation:
- `aircraftcategory`
- `purposeofflight`
- `weathercondition`
- `broadphaseofflight`

Columns related to injuries, aircraft specifications, and event characteristics show low missingness and will be kept for further analysis.

##  Cleaning Decisions
1. **Drop columns with extremely high missingness (>60%)**  
   These fields do not contribute meaningfully to risk analysis and will be removed.

2. **Impute key categorical fields with `'Unknown'`**  
   For important analytical columns that contain some missing values, imputation will ensure consistency without losing valuable records.

3. **Retain all operational, aircraft-specific, injury-related, and event-detail columns**  
   These form the foundation for the aircraft risk evaluation models and dashboards that will be built later in the project.

This step ensures the dataset is clean, consistent, and aligned with the project’s goal of identifying low-risk aircraft for stakeholder procurement.

##  Handling Missing Data

After identifying the missing value percentages, we applied a targeted cleaning strategy to preserve data quality while removing unusable columns.

**Columns Removed (Too Much Missing Data)**  
The following columns had more than 50% missing values and were removed from the dataset because they were unreliable for analysis and not essential to the stakeholder’s risk evaluation:

- `schedule` (85.85% missing)  
- `aircarrier` (81.27% missing)  
- `fardescription` (63.97% missing)  
- `aircraftcategory` (63.68% missing)  
- `longitude` (61.33% missing)  
- `latitude` (61.32% missing)

**Columns Kept and Cleaned Where Necessary**  
Columns below 50% missing were kept because they contain useful safety or aircraft information relevant to assessing accident risks. These will be cleaned further using imputation or domain-based corrections in later steps.

This step prepares the dataset for deeper analysis by removing noise and preserving high-value fields that support the stakeholder’s decision-making.

## Outlier Inspection

We inspected outliers in key injury/fatality counts using an IQR method. Outliers were flagged but not removed. Each flagged case will be reviewed manually if needed during deeper investigation.


## Outlier Check – What I Found

When I checked the data for unusually high or low numbers in the injury columns, I discovered that many rows were marked as “outliers.” Specifically:

- 17,813 cases for total fatal injuries

- 15,502 cases for total minor injuries

- 13,090 cases for total serious injuries

What this really means

These numbers may look surprising, but they don’t mean the data is wrong. Aviation accident data naturally has:

Many incidents with no injuries at all, and

A smaller number of incidents with very high injury counts

Because of this, the computer labels a lot of these high-injury cases as “unusual,” even though they are real and important events.

Why this matters

For stakeholders who want to understand accident severity or make decisions about aircraft operations, these high-injury events are crucial. Removing them would hide the most serious accidents.

What I decided

I will keep all these values in the dataset.
They represent real incidents, and they help us understand true accident patterns rather than just the averages.
