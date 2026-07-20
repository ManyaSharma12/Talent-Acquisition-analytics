# Talent Acquisition Performance & Risk Analytics System

## Project Overview
This project features a comprehensive **dual-view Talent Acquisition Analytics tracking system** engineered in Power BI. The architecture bridges the gap between high-level executive demand and granular daily recruiting operations. It delivers targeted operational tracking by separating metrics isolated across 5 primary recruiters from an all-inclusive organizational dashboard equipped with dynamic cross-filtering capabilities.


---

## The Dual-Dashboard System

### 1. Corporate Services Dashboard (Recruiter-Focused View)
* **Objective:** Operates as a granular performance workspace focused exclusively on monitoring individual pipeline metrics, closing conversion rates, and workload balances across **5 specific recruiters**.
* **Key Visualizations & Benchmarks:** 
  * **Core KPI Layout:** Captures a subset baseline of **143 Total Open Requisitions**, showcasing **62 Successful Hires**, **17 Offers in Process**, **16 Offered**, **32 Work in Progress (WIP)**, and a highly optimized **8.08-day Average Turnaround Time (TAT)**.
  * **Operational Metrics:** Features horizontal recruiter performance plots including *Successful Hires by Recruiter Name* (led by Mehak Dhar at 24 and Anurag Sharma at 22) and *TAT by Recruiter Name* metrics to isolate individual pipeline velocity bottlenecks.

### 2. Departments Overview Dashboard (Organization-Wide Macro View)
* **Objective:** Serves as the macro-level organizational dashboard giving talent acquisition executives a unified corporate view to track broad recruitment lifecycles. 
* **Key Visualizations & Cross-Filtering:** 
  * **Core KPI Layout:** Aggregates all corporate volume metrics across the organization to show a grand total of **226 Total Open Requisitions**, **78 Successful Hires**, **41 Offers in Process**, **19 Offered**, **62 Work in Progress (WIP)**, and a **7.81-day global Average Turnaround Time (TAT)**.
  * **Interactive Department Slicer:** Features a custom master department dropdown component enabling stakeholders to dynamically select and filter the entire dashboard view by isolated organizational business units.
  * **Risk Segmentation Table:** Integrates a conditional visual formatting matrix to highlight severe hiring lags across individual operational components (e.g., flagging Banking at a critical 96.00 Average Ageing Days).

---

## Core Analytics Engineering & DAX Blueprint
Both dashboards share a synchronized data model built on high-performance DAX measures designed to bypass candidate status duplicates and calculate lifecycles with strict mathematical accuracy:

```dax
// 1. Total Open Requisitions (Distinct count prevents row inflation from status changes)
Total Open Requisitions = DISTINCTCOUNT('Req Tracker-26_27'[Job Req Number])

// 2. Successful Hires (Total onboarding completions)
Successful Hires = CALCULATE(COUNT('Req Tracker-26_27'[Job Req Number]), 'Req Tracker-26_27'[ORC Status] = "Hired")

// 3. Work in Progress (Active pipeline openings)
WIP = CALCULATE(COUNT('Req Tracker-26_27'[Job Req Number]), 'Req Tracker-26_27'[ORC Status] = "WIP")

// 4. Offer in Process (Candidates currently in the closing pipeline)
Offer in Process = CALCULATE(COUNT('Req Tracker-26_27'[Job Req Number]), 'Req Tracker-26_27'[ORC Status] = "Offer In Process")

// 5. Offered (Total extended job offers outstanding)
Offered = CALCULATE(COUNT('Req Tracker-26_27'[Job Req Number]), 'Req Tracker-26_27'[ORC Status] = "Offered")

// 6. Average Turnaround Time (Calculates day difference between Approval and Offer dates only for Hired candidates)
Avg TAT = 
AVERAGEX(
    FILTER('Req Tracker-26_27', 'Req Tracker-26_27'[ORC Status] = "Hired"),
    DATEDIFF(
        VALUE('Req Tracker-26_27'[Requisition Approved Date]),
        VALUE('Req Tracker-26_27'[Offered Date]),
        DAY
    )
)

// 7. Requisition Ageing (Evaluates exposure time of all active openings excluding already Hired positions)
Avg Ageing Days = 
CALCULATE(
    AVERAGE('Req Tracker-26_27'[Ageing]),
    'Req Tracker-26_27'[ORC Status] <> "Hired"
)
Here is the complete, final text for your `README.md` file with the updated DAX formulas integrated.

Simply copy everything in the block below and paste it directly into your GitHub code editor:

```markdown
# Talent Acquisition Performance & Risk Analytics System

## Project Overview
This project features a comprehensive **dual-view Talent Acquisition Analytics tracking system** engineered in Power BI. The architecture bridges the gap between high-level executive demand and granular daily recruiting operations. It delivers targeted operational tracking by separating metrics isolated across 5 primary recruiters from an all-inclusive organizational dashboard equipped with dynamic cross-filtering capabilities.

*Note: To comply with strict corporate data governance and confidentiality agreements, the original dataset has been omitted. Parameterized tracking templates and anonymized mock schemas are utilized for system demonstration.*

---

## The Dual-Dashboard System

### 1. Corporate Services Dashboard (Recruiter-Focused View)
* **Objective:** Operates as a granular performance workspace focused exclusively on monitoring individual pipeline metrics, closing conversion rates, and workload balances across **5 specific recruiters**.
* **Key Visualizations & Benchmarks:** 
  * **Core KPI Layout:** Captures a subset baseline of **143 Total Open Requisitions**, showcasing **62 Successful Hires**, **17 Offers in Process**, **16 Offered**, **32 Work in Progress (WIP)**, and a highly optimized **8.08-day Average Turnaround Time (TAT)**.
  * **Operational Metrics:** Features horizontal recruiter performance plots including *Successful Hires by Recruiter Name* (led by Mehak Dhar at 24 and Anurag Sharma at 22) and *TAT by Recruiter Name* metrics to isolate individual pipeline velocity bottlenecks.

### 2. Departments Overview Dashboard (Organization-Wide Macro View)
* **Objective:** Serves as the macro-level organizational dashboard giving talent acquisition executives a unified corporate view to track broad recruitment lifecycles. 
* **Key Visualizations & Cross-Filtering:** 
  * **Core KPI Layout:** Aggregates all corporate volume metrics across the organization to show a grand total of **226 Total Open Requisitions**, **78 Successful Hires**, **41 Offers in Process**, **19 Offered**, **62 Work in Progress (WIP)**, and a **7.81-day global Average Turnaround Time (TAT)**.
  * **Interactive Department Slicer:** Features a custom master department dropdown component enabling stakeholders to dynamically select and filter the entire dashboard view by isolated organizational business units.
  * **Risk Segmentation Table:** Integrates a conditional visual formatting matrix to highlight severe hiring lags across individual operational components (e.g., flagging Banking at a critical 96.00 Average Ageing Days).

---

## Core Analytics Engineering & DAX Blueprint
Both dashboards share a synchronized data model built on high-performance DAX measures designed to bypass candidate status duplicates and calculate lifecycles with strict mathematical accuracy:

```dax
// 1. Total Open Requisitions (Distinct count prevents row inflation from status changes)
Total Open Requisitions = DISTINCTCOUNT('Req Tracker-26_27'[Job Req Number])

// 2. Successful Hires (Total onboarding completions)
Successful Hires = CALCULATE(COUNT('Req Tracker-26_27'[Job Req Number]), 'Req Tracker-26_27'[ORC Status] = "Hired")

// 3. Work in Progress (Active pipeline openings)
WIP = CALCULATE(COUNT('Req Tracker-26_27'[Job Req Number]), 'Req Tracker-26_27'[ORC Status] = "WIP")

// 4. Offer in Process (Candidates currently in the closing pipeline)
Offer in Process = CALCULATE(COUNT('Req Tracker-26_27'[Job Req Number]), 'Req Tracker-26_27'[ORC Status] = "Offer In Process")

// 5. Offered (Total extended job offers outstanding)
Offered = CALCULATE(COUNT('Req Tracker-26_27'[Job Req Number]), 'Req Tracker-26_27'[ORC Status] = "Offered")

// 6. Average Turnaround Time (Calculates day difference between Approval and Offer dates only for Hired candidates)
Avg TAT = 
AVERAGEX(
    FILTER('Req Tracker-26_27', 'Req Tracker-26_27'[ORC Status] = "Hired"),
    DATEDIFF(
        VALUE('Req Tracker-26_27'[Requisition Approved Date]),
        VALUE('Req Tracker-26_27'[Offered Date]),
        DAY
    )
)

// 7. Requisition Ageing (Evaluates exposure time of all active openings excluding already Hired positions)
Avg Ageing Days = 
CALCULATE(
    AVERAGE('Req Tracker-26_27'[Ageing]),
    'Req Tracker-26_27'[ORC Status] <> "Hired"
)

```

---

## Data Architecture & ETL Pipeline (Power Query)

A read-only, automated data processing pipeline was configured in Power Query to handle daily updates seamlessly:

1. **Source Connection:** Parameterized local file path strings to hook directly into the operational tracker files.
2. **Data Scrubbing:** Programmed cleansing loops to strip out empty field definitions and eliminate `(Blank)` visualization gaps.
3. **Data Type Compliance:** Enforced column structure validation by explicit conversion mapping (Alphanumeric Keys -> Numeric Indices; Chronological Strings -> Date Dimensions).

```

```
