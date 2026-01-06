# **Project Cost & Scope Calculator v2.1**

This repository contains a standalone, single-file web application designed to help Nidec’s Data Team estimate the financial investment and timeline required for data-related projects.

## **Overview**

The **Calculadora de Projetos de Dados** is built with HTML5, CSS3, and Vanilla JavaScript. It uses a multi-factor logic system to calculate hours and costs based on ingestion complexity, engineering requirements, visualization needs, and project management overhead.

### **Key Features**

* **Dynamic Cost Calculation:** Real-time updates as you toggle project parameters.  
* **Customizable Rates:** Adjustable hourly rates for different roles (Ingestion, Engineering, Visualization, and PM).  
* **Complexity Weighting:** Automatically detects "High Complexity" systems (e.g., SAP, Oracle, Salesforce) and adjusts the effort multipliers.  
* **Multi-Factor Analysis:** Accounts for LGPD (Sensitive Data), AI modeling, data quality, and business area availability.  
* **Export Options:** Built-in "Save to PDF" (print-friendly) and "Copy Summary" to clipboard for quick sharing via email or Slack.

## **Calculation Logic Explained**

The calculator uses a **Base Effort \+ Multiplier** methodology. It transforms qualitative complexity into quantitative hours.

### **1\. Data Ingestion**

This section measures the effort to get the data and bring it into the GCP environment.

* **Base:** 40 hours per table.  
* **System Multiplier:** If a "Complex System" (any system that is not SAP) is selected, the system count is multiplied by **30** to account for API authentication, security protocols, and connector setup. Standard systems (SAP/Excel/Sheets) have a multiplier of **1**.  
* **Legacy Factor:** Choosing "Legacy/Web Scraping" adds a **30% (1.3x)** increase to the total ingestion time.  
* **Formula:** ((numSystems \* complexityMult) \+ (numTables \* 40)) \* legacyMult

### **2\. Data Engineering**

This focuses on the "T" (Transform) of ETL—cleaning and modeling.

* **Base:** 20 hours for initial cleaning per table \+ 20 hours per calculated KPI.  
* **Cascading Multipliers:** The base hours are multiplied by five distinct risk/complexity factors:  
  * **Data Quality:** Low quality adds **30%**.  
  * **History:** Historical loads add **10%**.  
  * **Latency:** Streaming/Real-time data adds **30%**.  
  * **LGPD:** Sensitive data requirements add **10%**.  
  * **AI:** Implementing Machine Learning adds **50%**.  
* **Formula:** eng\_base \* qualityMult \* historyMult \* freqMult \* sensMult \* aiMult

### **3\. Data Visualization**

Focuses on the frontend/dashboarding effort.

* **Base:** 30 hours per dashboard screen.  
* **UX/Storytelling:** If "Executive" is selected, the effort is multiplied by **1.5x** to account for advanced design, prototyping, and stakeholder feedback loops.  
* **Formula:** (numScreens \* 30\) \* vizTypeMult

### **4\. PO & Management**

Covers documentation, meetings, and agile ceremonies.

* **Base:** **20%** of the total technical hours (Ingestion \+ Engineering \+ Viz).  
* **Friction Multipliers:** This overhead increases if:  
  * Documentation is missing (**\+30%**).  
  * Business area availability is low (**\+25%**).  
  * The project is "Innovation/P\&D" rather than standard automation (**\+20%**).  
* **Formula**: base\_pm \* docMult \* availMult \* natureMult

---

## **Customization**

You can modify the default hourly rates directly in the HTML file by searching for the Configurar Valor Hora section:

| Role | Default Rate (BRL) |
| :---- | :---- |
| Ingestion | R$ 176,00 |
| Engineering | R$ 200,00 |
| Visualization | R$ 150,00 |
| PO/Management | R$ 170,00 |

## 

## **Timeline Estimation**

The project duration is estimated by taking the **Total Hours** and dividing by **6 hours of daily productivity**. It then spreads this across a standard 30-day month cycle to provide a realistic "delivery window" rather than just a technical work-hour sum.

