# 🌍 Earthquake Data Pipeline with Microsoft Fabric

This project demonstrates how to build a **fully automated data pipeline** using **Microsoft Fabric** and the **Medallion Architecture**. It ingests earthquake data from the **USGS API**, transforms it through Bronze → Silver → Gold layers, and visualises insights in **Power BI**. The pipeline is orchestrated using **Data Factory** and runs **daily**.

---

## 📌 Business Case

Earthquake data is critical for:

* **Government agencies** – supporting disaster response planning.
* **Researchers** – analysing seismic activity trends.
* **Insurance companies** – assessing regional risks.

This pipeline ensures stakeholders have **clean, enriched, and always up-to-date data** for informed decision-making.

---

## ⚙️ Solution Overview

We use Microsoft Fabric services to implement the **Medallion Architecture**:

1. **Bronze Layer** – Ingest raw data from the USGS Earthquake API (GeoJSON).
2. **Silver Layer** – Clean & structure data into **Delta tables** (time, magnitude, location, etc.).
3. **Gold Layer** – Enrich with **country codes** (reverse geocoding) and **significance classifications**.
4. **Power BI Dashboard** – Create interactive reports with maps, slicers, and KPIs.
5. **Data Factory Orchestration** – Automate ingestion & processing on a **daily schedule**.

---

## 🏗️ Architecture Diagram

![Medallion Architecture](images/architecture.png)

![Workflow](images/orchestration.png)
---

## 🚀 Features

* Automated **daily ingestion** of earthquake events.
* **JSON → Delta tables** transformation using PySpark.
* Reverse geocoding to enrich data with **country codes**.
* **Significance classification** (Low, Moderate, High).
* Interactive **Power BI dashboard** with maps, KPIs & slicers.
* End-to-end automation via **Fabric Data Factory**.

---

## 📂 Project Structure

```
earthquake-pipeline/
│── notebooks/
│   ├── Bronze-Layer-Processing.ipynb   # Fetch raw API data
│   ├── Dilver-Layer-Processing.ipynb   # Transform JSON → structured tables
│   ├── Gold-Layer-Processing.ipynb    # Add country codes & classifications
│── images/
│   ├── architecture.png
│   ├── orchestration.json
│── README.md

```

---

## 🔑 Setup Instructions

### 1. Environment Setup

* Create a Microsoft **Work/School account**.
* Sign in to [Microsoft Fabric](https://app.fabric.microsoft.com/).
* Create a **Workspace** and a **Lakehouse**.

### 2. Bronze Layer (Raw Data)

* Create a **PySpark Notebook**.
* Fetch earthquake data using:

  * API: [USGS Earthquake API](https://earthquake.usgs.gov/fdsnws/event/1/)
* Save raw JSON in **Lakehouse Files**.

### 3. Silver Layer (Transformation)

* Load JSON into a Spark DataFrame.
* Extract required attributes (time, magnitude, location).
* Handle missing values & convert timestamps.
* Write output as **Silver Delta Table**.

### 4. Gold Layer (Enrichment)

* Install Python package: `reverse_geocoder`.
* Add **country codes** based on lat/lon.
* Add **significance classification**:

  * `<100 = Low`
  * `100–499 = Moderate`
  * `>=500 = High`
* Save as **Gold Delta Table**.

### 5. Power BI Dashboard

* Connect Power BI to the **Gold Table** via Fabric Semantic Model.
* Create visuals:

  * **Map** → Country (location), Max Significance (bubble size), Classification (legend).
  * **Slicers** → Date Range, Significance.
  * **KPIs** → Total Events, Maximum Significance.

### 6. Data Factory Orchestration

* Create a **Pipeline** in Data Factory.
* Add notebooks in sequence: **Bronze → Silver → Gold**.
* Pass **dynamic dates**:

  * Start Date: `@formatDateTime(addDays(utcnow(), -1), 'yyyy-MM-dd')`
  * End Date: `@formatDateTime(utcnow(), 'yyyy-MM-dd')`
* Schedule **daily refresh**.

---

## 📊 Example Insights

* Daily **earthquake frequency by country**.
* **Magnitude vs significance** analysis.
* **Severity trend over time**.
* **High-risk regions visualised on map**.

---

## 🛠️ Tech Stack

* **Microsoft Fabric** (Lakehouse, Data Factory, Power BI)
* **PySpark** (ETL & transformation)
* **reverse_geocoder** (location enrichment)
* **USGS Earthquake API** (data source)

---


---

## 🙌 Credits

* **Puneeth Kumar Amudala** – Project design & implementation
* **Microsoft Fabric** – Data platform services
* **USGS Earthquake API** – Open seismic data provider
* **reverse_geocoder** – Python package for geolocation enrichment


## 🙏 Acknowledgement  

Special thanks to **AI Luke** for the detailed walkthrough and guidance on this project.


## ✅ Summary

This project delivers a **scalable and automated earthquake monitoring system**:

* End-to-end pipeline from raw ingestion to Power BI insights.
* Clean, enriched, and **daily refreshed** dataset.
* Visualisation layer for decision-makers to quickly interpret seismic activity.
* Built using the **Medallion Architecture** for reliability and scalability.
