# Batch and Near Real-Time Data Pipelines with Node-RED and Grafana

**Course:** SEP 6DA3 – Data Analytics and Big Data  
**Institution:** McMaster University  
**Semester:** Fall 2025  
**Team:** Group 6  
**Contributors:** Andi Dong, Zhiyu Hu, Foram Brahmbhatt, Jiarui Yang, Linghe Shen, Shannon Chen  
**Instructor:** Prof. Pedro Tondo  

---

## 🧠 Project Overview
This project demonstrates the design and implementation of two complementary **data-engineering pipelines** using **Node-RED** and **Grafana**:

1. **Batch Pipeline —** Processes the full *Bike Sharing Demand* dataset (`hour.csv`) in one execution, applies cleaning + feature engineering, and outputs a structured file (`batch_output.csv`) for historical visualization.  
2. **Streaming Pipeline —** Simulates near real-time data ingestion by appending one new record every 5 seconds to `stream_output.csv`, enabling live Grafana dashboards.

The aim was to compare **batch vs. streaming processing**, understand their trade-offs, and gain practical skills in real-time visualization and low-code data integration.

Dataset source: [Kaggle – Bike Sharing Dataset](https://www.kaggle.com/datasets/lakshmi25npathi/bike-sharing-dataset/data)

---

## ⚙️ Tools and Technologies
- **Node-RED 3.x** for flow-based ETL and real-time simulation  
- **Grafana 10.x** with Infinity Plugin for CSV visualization  
- **JavaScript Function Nodes** for feature transformation & prediction  
- **CSV IO nodes** for batch and stream exports  
- **HTTP local server integration** for Grafana auto-refresh  

---

## 🧩 Pipeline Design

### 🟦 Batch Pipeline
- Reads `hour.csv` → parses to JSON → transforms → writes to `batch_output.csv`.
- Added derived features (timestamp combination, weekday, hour).  
- Used Debug and File nodes to verify data flow.  
- Grafana visualizations:
  - **Total rentals over time**
  - **Hourly patterns (peaks at 8–9 AM and 5–6 PM)**
  - **Seasonal and weather aggregations**

### 🟩 Streaming Pipeline
- Emits one record every 5 seconds via an Inject node.  
- Uses `flow.get()` and `flow.set()` to track current index and preserve state.  
- Appends each record to `stream_output.csv`.  
- Integrates a **moving-average predictor** (Function node) producing `predicted_cnt`.  
- Grafana dashboard auto-refreshes every 5 seconds to display live updates.  

---

## 📊 Grafana Dashboard
- **Batch Panel →** Long-term historical trend line.  
- **Streaming Panel →** Near real-time plot of actual vs. predicted rental counts.  
- **Season / Weather Aggregations →** Bar charts showing contextual patterns.  
- **Hourly Aggregation →** Typical daily usage curve.  

This dashboard provides both **retrospective** (batch) and **live** (stream) insights within a single view.

---

## 💡 Key Insights
| Aspect | Batch Pipeline | Streaming Pipeline |
|---------|----------------|--------------------|
| Processing Mode | Full dataset at once | One record every few seconds |
| Best Use Case | Historical analysis & stable aggregation | Real-time monitoring & forecasting |
| Advantages | Complete coverage, deterministic | Continuous updates, immediate insight |
| Challenges | Not reactive to new data | Requires context management & timing control |

Additional observations:
- **Data schema consistency** is critical for Grafana integration.  
- **Timestamp alignment** and **column mapping** affect real-time accuracy.  
- **Moving average forecasting** adds predictive value even in low-code pipelines.

---

## 🛠️ Technical Highlights & Solutions
- Fixed Node-RED installation issues using `nvm` for environment consistency.  
- Solved timestamp offset (+5 hours) by reconstructing UTC dates manually.  
- Defined explicit CSV schemas for clean Grafana parsing.  
- Installed and configured **Infinity Plugin** for CSV via HTTP source.  
- Ensured continuous stream with `flow.context` for index tracking.  

---

## 🧮 Results Summary
- **Batch R² analysis:** Stable historical patterns confirmed seasonality.  
- **Streaming dashboard:** Predicted vs. actual curves align closely over time.  
- **5-panel Grafana layout:** Provides both macro and micro views of bike rental demand.  

---

## ✨ Reflection
Building batch and streaming pipelines from scratch reinforced our understanding of how data flows from ETL to visual analytics.  
We learned that while batch pipelines are simpler and deterministic, streaming architectures require state control and synchronization but enable real-time decision making.  
Integrating Node-RED and Grafana taught us practical skills in **data pipeline design, monitoring, and debugging** — essential for modern data engineering workflows.

---

## 📁 Repository Structure
