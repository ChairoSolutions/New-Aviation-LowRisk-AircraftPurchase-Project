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

