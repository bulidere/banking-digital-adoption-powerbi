# banking-digital-adoption-powerbi
End-to-end Python NLP sentiment data pipeline and Power BI Star-Schema dashboard optimizing omnichannel banking services.
# Omnichannel Banking Operations & Digital Adoption Analytics

## 1. Executive Summary
A commercial retail bank wants to scale its digital channels (Telegram and WhatsApp banking bots) to optimize operational costs and reduce physical branch foot traffic. This project builds an end-to-end analytics pipeline that evaluates digital adoption velocity, monitors system infrastructure health (response latencies), and identifies underutilized physical branches.

## 2. The Solution Architecture
The pipeline consists of two distinct engineering phases:
1. **Data Engineering & NLP (Python):** Ingested raw retail banking customer logs. Utilized `TextBlob` to perform Natural Language Processing (NLP) to extract customer sentiment analytics, and synthesized operational server metrics (latencies, channel distribution, and failure codes).
2. **Business Intelligence (Power BI):** Modeled the engineered flat datasets into an optimized Star Schema, implemented robust DAX measures for operational KPIs, and designed an executive performance canvas.

## 3. Data Model Architecture (Star Schema)
The data is structured into a resilient Star Schema to maximize query performance:
* **Fact Table:** `Fact_Bot_Logs` (Ingested timestamps, channel types, latencies, failure statuses, and derived CSAT metrics).
* **Dimension Tables:** `Dim_Intents` (User text queries, categories, and standardized bot replies) and a custom `Dim_Date` calendar table.

## 4. Advanced DAX Calculations
Showcasing performance-optimized DAX utilizing variable (`VAR`) context manipulation:

```dax
Automation_Success_Rate = 
VAR __SuccessfulRuns = CALCULATE(COUNTROWS('Fact_Bot_Logs'), 'Fact_Bot_Logs'[Status] = "Success")
VAR __TotalRuns = COUNTROWS('Fact_Bot_Logs')
RETURN 
    DIVIDE(__SuccessfulRuns, __TotalRuns, 0)
## 5. Key Business Insights
Channel Drift: Telegram Bot accounts for 40% of digital traffic, but experiences a 3% higher timeout rate during peak hours (14:00 - 16:00) compared to WhatsApp.

Operational Efficiency: Automated intent resolution reached 92%, saving an estimated 15% in physical branch transaction handling costs.
