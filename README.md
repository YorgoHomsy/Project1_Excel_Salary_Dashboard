# 📈 Excel Salary Dashboard

![Final Dashboard Preview](./assets/1_Salary_Dashboard.gif)

## 🌟 Introduction
I designed this interactive **Salary Dashboard** to empower job seekers in the data industry. By providing a clear view of market rates, this tool helps professionals negotiate better compensation and understand the financial landscape of their target roles.

The project was built using a dataset of **2023 Data Science Job Postings**, focusing on transforming raw data into a user-friendly decision-making tool.

### 📁 Project Files
* **Main Dashboard:** [1_Salary_Dashboard.xlsx](1_Salary_Dashboard.xlsx)
* **Dataset:** Real-world job data including titles, salaries, locations, and schedules.

### 🛠️ Core Excel Stack
* **📊 Advanced Charting:** Map charts and formatted bar charts.
* **🧮 Complex Formulas:** Array formulas (`MEDIAN`, `IF`) and Dynamic Arrays (`FILTER`).
* **❎ UX Design:** Data validation and interactive dropdowns for a seamless UI.

---

## 🏗️ Dashboard Build

### 1️⃣ Visual Analysis (Charts)

#### 📊 Salary Benchmarking - Bar Chart
<img src="./assets/1_Salary_Dashboard_Chart1.png" width="850" alt="Salary Dashboard Bar Chart">

* **Logic:** Created a horizontal bar chart to compare median salaries across job titles.
* **Design:** Data is sorted in descending order to immediately highlight top-paying roles (Senior positions and Engineers) versus entry-level Analyst roles.
* **Insight:** Clearly shows the "Experience Premium"—Senior roles often command 40-60% higher medians than standard Analyst tracks.

#### 🗺️ Global Distribution - Map Chart
![Country Median Salary Map](./assets/1_Salary_Dashboard_Country_Map.gif)

* **Logic:** Utilized Excel’s Map Chart feature to visualize geographic salary disparities.
* **Design:** Color-coded regions allow users to identify high-compensation tech hubs versus emerging markets at a glance.
* **Insight:** Highlights the significant salary variance between US-based roles and international markets.

---

### 2️⃣ The Engine (Formulas & Functions)

#### 💰 Dynamic Median Salary Calculation
To power the dashboard, I developed an array formula that calculates medians based on three different user-selected filters.

```excel
=MEDIAN(
    IF(
        (jobs[job_title_short]=A2)*
        (jobs[job_country]=country)*
        (ISNUMBER(SEARCH(type,jobs[job_schedule_type])))*
        (jobs[salary_year_avg]<>0),
        jobs[salary_year_avg]
    )
)
```

### 💰 Technical Breakdown: Median Calculation
* **Boolean Logic:** The formula uses multiplication as a logical `AND` operator to filter the `jobs` table across multiple criteria.
* **Data Integrity:** It explicitly excludes $0 values to ensure the median reflects actual reported salaries and is not skewed by missing data.
* **Relational Mapping:** This logic acts as the backend "engine" that powers the Job Title comparison table.

#### Backend Architecture vs. Dashboard UI
| Background Processing | Dashboard Implementation |
| :---: | :---: |
| ![Background Logic](./assets/1_Salary_Dashboard_Screenshot1.png) | ![Dashboard UI](./assets/1_Salary_Dashboard_Job_Title.png) |

---

### ⏰ Intelligent Schedule Filtering
I implemented **Dynamic Arrays** to generate a clean, unique list of job types. This was necessary to strip out "messy" data entries that would clutter the user interface.



```excel
=FILTER(J2#, (NOT(ISNUMBER(SEARCH("and",J2#)) + ISNUMBER(SEARCH(",",J2#)))) * (J2#<>0))
```

* **Technical Breakdown:** This formula uses string searching to automatically identify and remove combined entries (e.g., "Full-time and Part-time"). This ensures the user sees a "clean" dropdown menu with distinct, individual job categories.

---

### 3️⃣ User Experience (Data Validation)
To ensure the dashboard is robust and "break-proof," I implemented strict **Data Validation** rules. By linking dropdown menus to the dynamic filtered lists, I achieved:

* **Data Integrity:** Users are restricted to selecting job titles and locations that actually exist in the underlying dataset.
* **Error Prevention:** Eliminates the risk of `#REF!` or `#VALUE!` errors caused by manual typing or typos.
* **Professional UI:** Provides a polished, software-like experience with responsive dropdown menus.

<img src="./assets/1_Salary_Dashboard_Data_Validation.gif" width="450" alt="Data Validation Demo">

---

## ✅ Conclusion
This dashboard transforms a static dataset into a functional **Business Intelligence tool**. By combining advanced **Data Modeling** with **UX Design**, I have created a resource that provides actionable career insights—demonstrating how location, title, and job type dictate market value in the 2023 data economy.
