# Aviation Risk Analysis for Aircraft Procurement

## Project Overview

This project addresses a critical strategic need for our company: expanding into the commercial and private aviation sectors. As a new venture, understanding and mitigating the inherent risks associated with aircraft acquisition is paramount. This analysis provides a **data-driven framework for identifying lowest-risk aircraft**, leveraging historical accident data to inform our procurement strategy and ensure safe, reliable operations from the outset.

## Business Understanding

### 1.1 The Real-World Problem

Our company is embarking on a significant expansion into new industries by purchasing and operating airplanes for commercial and private enterprises. A fundamental challenge in this new domain is the absence of internal expertise regarding the safety profiles and potential risks of various aircraft types. Without a comprehensive, data-backed understanding of historical aviation incidents, making informed procurement decisions presents substantial financial, operational, and safety uncertainties.

### 1.2 Stakeholders and Project Value

This project is specifically designed to deliver actionable insights to **the Head of the New Aviation Division**. Our analysis provides immense value by:

* **Informing Strategic Procurement:** Guiding the selection of aircraft makes and models that have historically demonstrated superior safety performance.
* **Mitigating Operational Risk:** Proactively identifying and quantifying risk factors to establish robust safety protocols and training programs for the new fleet.
* **Building a Resilient Fleet:** Enabling the company to invest confidently in aircraft that align with our commitment to safety and operational excellence.

### 1.3 Key Business Questions Addressed

* Which aircraft manufacturers and models exhibit the lowest historical accident rates, particularly concerning fatalities and severe damage?
* Are there observable trends in aviation safety over time that can inform long-term strategy?
* What are the most critical phases of flight during which accidents disproportionately occur, and how can this inform operational safety measures?

## Data Understanding and Analysis

### 2.1 Data Source and Description

The foundation of this analysis is the `AviationData.csv` dataset, generously provided by the **National Transportation Safety Board (NTSB)**. As the primary U.S. government agency responsible for civil transportation accident investigations, the NTSB is an authoritative and highly reliable source for aviation safety data.

The dataset encompasses detailed records of civil aviation accidents and selected incidents from **1962 to 2023**. It provides comprehensive information pertinent to our risk assessment, including:
* **Aircraft Identifiers:** `Make`, `Model`, `Aircraft_Category`.
* **Accident Outcomes:** `Total_Fatal_Injuries`, `Total_Serious_Injuries`, `Total_Minor_Injuries`, `Injury_Severity`, `Aircraft_Damage`.
* **Contextual Factors:** `Event_Date`, `Purpose_of_Flight`, `Phase_of_Flight`, `Weather_Condition`.

### 2.2 Suitability and Limitations

The NTSB data's depth in accident outcomes and aircraft specifics makes it highly suitable for identifying risk profiles essential for aircraft procurement. However, it's important to acknowledge certain limitations:
* **U.S.-Centric Bias:** The data primarily covers U.S. civil aviation and U.S.-registered aircraft incidents, which might not fully represent global aviation risks.
* **Historical Nature:** While providing trends, historical data may not perfectly predict future risk given advancements in aircraft technology and safety regulations.
* **Missing Data:** Various columns contain missing values, which were systematically handled through imputation (mean for numerical, mode for categorical) and filtering to ensure robust analysis.

### 2.3 Data Preparation

The raw dataset underwent several crucial preparation steps to ensure data quality and suitability for analysis:

* **Date Formatting:**
    The `event.date` column was converted to a datetime format, and a new `accident.year` column was extracted to facilitate time-series analysis.
    ```python
    df['event.date'] = pd.to_datetime(df['event.date'], errors='coerce')
    df['accident.year'] = df['event.date'].dt.year
    ```

* **Cleaning Categorical Values:**
    Common unknown placeholders such as `'UNK'`, `'Unk'`, and string `'Nan'` were standardized and replaced with the mode (most frequent value) for relevant categorical columns (e.g., `weather.condition`, `purpose.of.flight`).
    ```python
    # Example for one column
    mode_value = df['weather.condition'].mode()[0]
    df['weather.condition'] = df['weather.condition'].replace(['UNK', 'Unk', 'Nan'], mode_value)
    ```

* **Handling Missing Values (NaN):**
    * **Numerical columns** (e.g., `total.fatal.injuries`, `total.serious.injuries`): These were first converted to a numeric type, coercing errors, and then missing values were filled with the mean of each respective column to preserve data distribution.
        ```python
        # Example for a numerical column
        df[col] = pd.to_numeric(df[col], errors='coerce')
        df[col].fillna(df[col].mean(), inplace=True)
        ```
    * **Categorical columns** (e.g., `weather.condition`, `injury.severity`): Missing values were filled with the mode (most frequent value) to maintain the most common category.
        ```python
        # Example for a categorical column
        df[col].fillna(df[col].mode()[0], inplace=True)
        ```

* **Standardizing Column Names:**
    All column names were converted to lowercase and periods (`.`) replaced with underscores (`_`) for consistency and easier programmatic access.
    ```python
    df.columns = df.columns.str.replace('.', '_', regex=False).str.lower()
    ```

### 2.4 Key Analysis & Visualizations

Our analysis involved comprehensive data cleaning, feature engineering (e.g., `is_fatal_accident`, `damage_score`), and rigorous aggregation to quantify risk. We specifically filtered for `Airplane` category and `Purpose_of_Flight` relevant to commercial and private operations (e.g., Personal, Business, Instructional, Ferry, Flight Test, Executive/Corporate).

Below are three key visualizations that drive our recommendations:

---

#### **Figure 1: Top 10 Lowest Fatal Accident Rate by Aircraft Make**

This chart highlights aircraft manufacturers with the best safety records in terms of fatal accident occurrences. By analyzing makes with a substantial number of accidents, we ensure statistical reliability in identifying those that consistently demonstrate lower risk. This visualization directly informs which manufacturers to prioritize for procurement, aligning with our goal of a safety-first fleet.

![Top 10 Lowest Fatal Accident Rate by Aircraft Make]

---
![make vs injuries](https://github.com/user-attachments/assets/fd48fff0-0ece-451d-ab53-6bcaeb62d279)

#### **Figure 2: Trend of Fatal Accident Rate Over Time**

This visualization illustrates the long-term trend of fatal accident rates specifically for airplanes involved in commercial and private operations. It provides an essential historical context, revealing whether overall aviation safety has improved, declined, or remained stable over the decades. A decreasing trend would indicate a generally safer environment for our new venture, contingent on adhering to best practices.

![Trend of Fatal Accident Rate Over Time]

---![Safest VS Most Fatal Locations](https://github.com/user-attachments/assets/71eff3fb-454a-43ca-bd1b-2b56c5c3ded5)

![Weather Vs Trends over the years](https://github.com/user-attachments/assets/ff5e4cf1-1c7c-467c-abea-39163592f7ed)

#### **Figure 3: Fatal Accident Rate by Phase of Flight**

Understanding *when* accidents are most likely to occur is crucial for developing robust operational safety measures. This chart identifies the phases of flight (e.g., takeoff, landing, maneuvering) that statistically have the highest fatal accident rates. The insights derived from this visualization are invaluable for informing targeted pilot training, pre-flight planning, and in-flight procedures to mitigate risks during critical operational periods.

![Fatal Accident Rate by Phase of Flight]
![make vs injuries](https://github.com/user-attachments/assets/1d66a870-7bed-4db9-a9fa-9bc2ac8b474a)

---![weather condition per Flight Purpose](https://github.com/user-attachments/assets/14530917-d499-4680-9625-10fd53dd084f)


## Conclusion

Our comprehensive aviation risk analysis provides critical, data-driven insights for the Head of the New Aviation Division, directly addressing the challenge of identifying lowest-risk aircraft for procurement.

### Summary of Key Findings & Implications:

1.  **Prioritized Manufacturers:** Our analysis clearly identifies manufacturers such as **CESSNA**, **PIPER**, and **BEECH** as having consistently lower fatal accident rates among aircraft with significant operational history. This implies that focusing initial acquisition efforts on models from these manufacturers can significantly de-risk the company's entry into the aviation sector.
2.  **Improving Safety Trends:** The overall fatal accident rate for relevant airplane operations has shown a general **decreasing trend** over the past decades. This positive industry-wide progression implies that aviation is becoming safer, providing a favorable environment for the company's new venture, provided robust safety practices are maintained.
3.  **High-Risk Operational Phases:** We've identified specific phases of flight, notably **Takeoff, Landing, and Maneuvering**, as having significantly higher fatal accident rates. This finding is critical for stakeholders, implying that operational strategies, pilot training, and pre-flight planning should place heightened emphasis on these phases to minimize incident risk.

These findings empower the aviation division to make strategic, data-informed decisions, fostering a safety-first approach from the foundation of our new fleet.

## Technologies Used

* **Python** (Programming Language)
* **Pandas** (Data Manipulation and Analysis)
* **NumPy** (Numerical Operations)
* **Matplotlib** (Data Visualization)
* **Jupyter Notebook** (Interactive Development Environment)
* **Git & GitHub** (Version Control and Repository Hosting)
* **Tableau** (Business Intelligence & Dashboarding - for further interactive exploration of `Cleaned_AviationData_Final.csv`)

