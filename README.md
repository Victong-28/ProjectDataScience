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

### 2.3 Key Analysis & Visualizations

Our analysis involved comprehensive data cleaning, feature engineering (e.g., `is_fatal_accident`, `damage_score`), and rigorous aggregation to quantify risk. We specifically filtered for `Airplane` category and `Purpose_of_Flight` relevant to commercial and private operations (e.g., Personal, Business, Instructional, Ferry, Flight Test, Executive/Corporate).

Below are three key visualizations that drive our recommendations:

---

#### **Figure 1: Top 10 Lowest Fatal Accident Rate by Aircraft Make**

This chart highlights manufacturers with the best safety records in terms of fatal accident occurrences, considering only makes with substantial accident history to ensure statistical reliability. This directly informs which manufacturers to prioritize for procurement.

![Top 10 Lowest Fatal Accident Rate by Aircraft Make](images/fatal_accident_rate_by_make.png)

---

#### **Figure 2: Trend of Fatal Accident Rate Over Time**

This visualization illustrates the long-term trend of fatal accident rates for airplanes in commercial and private operations. It provides an essential historical context, revealing whether overall aviation safety has improved, declined, or remained stable over the decades.

![Trend of Fatal Accident Rate Over Time](images/fatal_accident_rate_trend.png)

---

#### **Figure 3: Fatal Accident Rate by Phase of Flight**

Understanding *when* accidents are most likely to occur is crucial for operational safety. This chart identifies the phases of flight with the highest fatal accident rates, offering insights that can inform targeted training and procedural enhancements.

![Fatal Accident Rate by Phase of Flight](images/fatal_accident_rate_by_phase.png)

---

## Conclusion

Our comprehensive aviation risk analysis provides critical, data-driven insights for the Head of the New Aviation Division, directly addressing the challenge of identifying lowest-risk aircraft for procurement.

### Summary of Key Findings & Implications:

1.  **Prioritized Manufacturers:** Our analysis clearly identifies manufacturers such as **CESSNA**, **PIPER**, and **BEECH** as having consistently lower fatal accident rates among aircraft with significant operational history. This implies that focusing initial acquisition efforts on models from these manufacturers can significantly de-risk the company's entry into the aviation sector.
2.  **Improving Safety Trends:** The overall fatal accident rate for relevant airplane operations has shown a general **decreasing trend** over the past decades. This positive industry-wide progression implies that aviation is becoming safer, providing a favorable environment for the company's new venture, provided robust safety practices are maintained.
3.  **High-Risk Operational Phases:** We've identified specific phases of flight, notably **Takeoff, Landing, and Maneuvering**, as having significantly higher fatal accident rates. This finding is critical for stakeholders, implying that operational strategies, pilot training, and pre-flight planning should place heightened emphasis on these phases to minimize incident risk.

These findings empower the aviation division to make strategic, data-informed decisions, fostering a safety-first approach from the foundation of our new fleet.

