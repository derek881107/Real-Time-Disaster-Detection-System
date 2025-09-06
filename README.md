# Real-Time Disaster Detection System with Regional Risk Scoring
This system is designed to detect risk indices across different regions of the global supply chain. By entering supplier addresses in the specified format, it can generate specific risk scores for you.




# Real-Time Disaster Detection and Risk Assessment System

This project integrates the **GDACS platform** with the **Google News API** to provide real-time disaster detection, automated news collection, and risk scoring. By combining official alerts with media coverage, the system helps organizations evaluate disaster severity, assess local response capabilities, and generate risk scores for supply chain resilience.  

---

## 📌 Features

- **Real-Time Detection**: Automatically detect disasters with Orange-level alerts or higher from GDACS.  
- **Email Alerts**: Send disaster summaries and instructions to internal teams and OEM partners.  
- **Historical Analysis**: Collect and analyze past disaster records to identify seasonal and high-risk regions.  
- **Risk Scoring**: Combine Google News data with GPT-3.5 Turbo for risk evaluation.  
- **Data Export**: Output results in Excel for easy integration with Power BI.  

---

## 🔎 System Components

### 1. Real-Time Disaster Detection System

- File: **real_time_disaster_detection.ipynb**
- Connects to GDACS and detects disasters with **Orange-level or higher alerts**.  
- Sends notifications with disaster details and response instructions via **email**.  
- Helps global HQ and supply chain teams monitor risks in real time.  

### 2. Historical Disaster Data Collection

- File: **historical_dataset_processing.ipynb**
- Loads **historical GDACS disaster records** for specific regions.  
- Matches with company **client and warehouse coordinates** to create training datasets.  
- Enables:  
  1. Seasonal disaster pattern analysis.  
  2. High-risk vs. low-risk region identification.  
  3. Predictive modeling for monthly disaster risks.  

### 3. Risk Scoring with News Integration

- File: **google_news_scraper.ipynb**
- Collects **Google News articles** related to disasters in specific regions and timeframes.  
- Analyzes content with **GPT-3.5 Turbo** to assign **risk scores**.  
- Exports enriched results to **Excel** for visualization in Power BI.  

---

## 📊 Excel Output Columns

The output file contains both GDACS context and GPT-enhanced evaluation:  

- **News Metadata**  
  `title`, `url`, `date_text`, `parsed_date`, `summary`, `extraction_method`, `lang_country`  

- **GDACS Context**  
  `gdacs_event_id`, `gdacs_event_type`, `gdacs_event_name`,  
  `gdacs_alert_level`, `gdacs_alert_score`, `gdacs_country`,  
  `gdacs_description`, `gdacs_severity_value`, `gdacs_severity_text`,  
  `gdacs_from_date`, `gdacs_to_date`  

- **Search Parameters**  
  `search_from_date`, `search_to_date`, `search_language`,  
  `search_country`, `client_country`, `client_address`, `distance_km`  

- **Risk Scores**  
  - `disaster_severity_score`  
  - `response_capability_score`  
  - `response_timeliness_score`  
  - `disaster_relevance_score`  
  - `gdacs_alignment_score`  
  - `media_coverage_score`  
  - `final_risk_score`  
  - `confidence_score`  

- **Categorical Levels**  
  `severity_level`, `response_level`, `timeliness_level`,  
  `relevance_level`, `gdacs_alignment_level`, `media_coverage_level`  

- **GPT Analysis**  
  `primary_disaster_type`, `client_country_match`,  
  `gpt_disaster_keywords`, `gpt_response_keywords`,  
  `gpt_timeliness_keywords`, `gpt_analysis_summary`, `gdacs_context_analysis`  

- **Client Risk Evaluation**  
  `client_risk_scores_json`, `matched_client_addresses`, `matched_location`  
  + location-specific risk columns (e.g., `risk_CARRETERA_BASE_AEREA_5850_23`, `risk_268_SUHONG_ROAD`, etc.)  

---

## 🚀 Future Applications

- Benchmark new disasters against historical datasets.  
- Improve accuracy of risk scores with past response insights.  
- Enhance supply chain crisis management with real-time + predictive analysis.  

---

⚡ With this system, organizations gain a powerful tool to monitor global disasters, assess supply chain vulnerabilities, and make data-driven risk management decisions.  
