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


OVERVIEW
--------
This program automates end-to-end media analysis for GDACS disaster events and
produces a fully structured Excel report. Given a GDACS event list and nearby
client facilities, it:

1) Detects the appropriate Google News language/country for each client location.
2) Builds localized disaster search terms (translated/adapted with GPT).
3) Queries Google News (via PyGoogleNews) within the event’s date range.
4) Fetches article HTML and extracts comprehensive article content using GPT.
5) Analyzes each article in the context of the GDACS event and scores it on six
   dimensions, plus an overall “final_risk_score”.
6) Derives per-client address risk scores (0–10) based on proximity/severity
   context and mentions in the media.
7) Aggregates results, computes per-event summaries, and exports a multi-sheet
   Excel workbook with results, summary statistics, and client risk details.

KEY CAPABILITIES
----------------
• Localization
  - CountryLanguageAnalyzer chooses {lang, country} codes for Google News
    based on client country/address (uses a small default map + GPT).
  - LocalizedPyGoogleNewsClient runs searches with date filtering and applies
    basic deduping/cleanup.
  - Optional GPT-driven term localization translates/adapts disaster terms to
    local usage (e.g., typhoon vs. hurricane, country/region names).

• Article Content Extraction
  - GPTURLAnalyzer downloads the article HTML with requests and asks GPT to
    extract comprehensive text + a 13–15 sentence summary + “key_details_found”.
  - Ensures a consistent JSON payload is returned and validates success flags.

• Disaster-Context Analysis
  - EnhancedDisasterAnalyzer builds a GDACS-aware prompt per article using a
    GDACS knowledge base (per disaster type) and alert level definitions.
  - GPT outputs:
      - disaster_severity_score (0–100)
      - response_capability_score (0–100)
      - response_timeliness_score (0–100)
      - disaster_relevance_score (0–100)
      - gdacs_alignment_score (0–100)
      - media_coverage_score (0–100)
      - is_disaster_related (bool)
      - primary_disaster_type (string)
      - disaster/response/timeliness keywords (lists)
      - analysis summaries (plain text)
      - final_risk_score (0–100)
      - confidence_score (0–100)
  - Client Country Match: checks if article content mentions any client
    countries/addresses associated with the same Event_ID.

• Client Address Risk (0–10)
  - For the current event, collects client entries (address, country,
    severity_text, distance summary) and asks GPT to assign a risk score per
    *address*. These appear in the export under:
      - client_risk_scores_json (JSON)
      - risk_<shortened_address> columns (one per matched address)
      - client_risk_scores_summary (readable summary)


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
