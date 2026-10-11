# 🎧 Salla Call Center & Customer Operations Intelligence Dashboard

[![Project Status: Under Active Development](https://img.shields.io/badge/Status-Under%20Active%20Development%20%F0%9F%9A%A7-orange?style=for-the-badge)]()
[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![HTML5 & CSS3](https://img.shields.io/badge/HTML5%20%26%20CSS3-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/)
[![Deneb Visual](https://img.shields.io/badge/Deneb%20Visual-8A2BE2?style=for-the-badge&logo=visual-studio-code&logoColor=white)](https://deneb-viz.github.io/)
[![DAX Measures](https://img.shields.io/badge/Advanced_DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)]()
[![Portfolio](https://img.shields.io/badge/Live-Portfolio%20Website-06b6d4?style=for-the-badge&logo=googlechrome&logoColor=white)](https://islamyasser424-design.github.io/portfolio-/)

> **A decision-grade Business Intelligence solution combining Power BI data modeling with custom HTML5 & CSS3 / Deneb visual styling to monitor call center operations, workforce capacity, queue dynamics, and customer satisfaction for the Salla e-commerce ecosystem.**

---

## 📌 Table of Contents
- [📖 Executive Overview](#-executive-overview)
- [🎨 Modern UI & HTML/CSS Integration](#-modern-ui--htmlcss-integration)
- [📊 Key Performance Indicators (KPIs)](#-key-performance-indicators-kpis)
- [🖥️ Planned Dashboard Architecture](#️-planned-dashboard-architecture)
- [📐 Data Model & Star Schema](#-data-model--star-schema)
- [⚙️ Core DAX Formulations](#️-core-dax-formulations)
- [📂 Repository Structure](#-repository-structure)
- [🚀 Project Development Roadmap](#-project-development-roadmap)
- [👤 Author & Connect](#-author--connect)

---

## 📖 Executive Overview

Managing high-volume customer contact centers requires instant operational visibility into queue congestion, agent handling efficiency, and customer sentiment. 

This project delivers an end-to-end **Call Center & Customer Support Operations Intelligence Dashboard** designed specifically for the **Salla** customer experience ecosystem:
* **Real-time Queue Governance:** Tracking call arrival volumes, peak congestion hours, and abandonment rate spikes.
* **Service Level Adherence (SLA):** Monitoring contractual response targets (e.g., 80% of calls answered in < 20 seconds).
* **Agent Workforce Management (WFM):** Benchmarking individual agent throughput, talk vs. hold durations, and after-call work (ACW).
* **Root-Cause Resolution:** Isolating top inquiry drivers (shipping inquiries, payment gateway failures, merchant onboarding blockers) to drive first-contact resolution (FCR).

---

## 🎨 Modern UI & HTML/CSS Integration

A standout architectural differentiator of this project is the integration of **HTML5 & CSS3 inside Power BI** (via custom visuals such as **Deneb** and **HTML Content**):

* **Custom Glassmorphism KPI Cards:** Handcrafted modern metric cards with gradient borders, rounded badges, and subtle drop shadows beyond standard visual constraints.
* **Dynamic SLA Status Badges:** Color-coded HTML tags (🟢 *Compliant*, 🟡 *Warning*, 🔴 *Breached*) dynamically computed via DAX string measures.
* **Micro-Charts & In-Card Progress Bars:** SVG-driven inline progress bars and target completion meters embedded directly into metric cards.
* **Agent Performance Cards:** Sleek modular cards displaying agent portraits, real-time availability status, and individual CSAT scorecards.

---

## 📊 Key Performance Indicators (KPIs)

| Metric | Business Definition | Target Benchmark |
| :--- | :--- | :--- |
| **SLA Adherence (%)** | Percentage of inbound calls answered within the acceptable threshold (≤ 20 sec). | **≥ 80.0%** |
| **Average Handling Time (AHT)** | Composite duration of Talk Time + Hold Time + After-Call Work (ACW). | **< 4.5 mins** |
| **First Call Resolution (FCR)** | Percentage of customer inquiries resolved completely during the initial interaction. | **≥ 75.0%** |
| **Call Abandonment Rate (%)** | Percentage of callers hanging up while waiting in queue before reaching an agent. | **≤ 5.0%** |
| **Customer Satisfaction (CSAT)** | Average rating from post-call automated customer survey (1–5 scale). | **≥ 4.2 / 5.0** |
| **Average Speed of Answer (ASA)** | Average queue waiting duration experienced by callers prior to agent pick-up. | **< 25 secs** |

---

## 🖥️ Planned Dashboard Architecture

### 1. 📞 Page 1: Operations Executive Command Center
* High-level command view for Operations Directors and Support Leads.
* Top-level KPI ribbons (Total Calls, Answer Rate %, SLA %, Average Wait Time, Global CSAT).
* Hourly call volume trends vs. agent capacity lines.
* Status donut breakdowns (Answered, Abandoned, Transferred).

### 2. ⏱️ Page 2: Inbound Queue Dynamics & Peak Flow
* Heatmap matrix analyzing call arrival density by **Hour of the Day** vs. **Day of the Week**.
* Abandonment analysis curves correlating caller wait time with hang-up probability.
* Channel distribution (Voice Telephony, Live Chat, WhatsApp Support escalations).

### 3. 👤 Page 3: Agent Productivity & WFM Scorecards
* Agent-level comparison table with interactive sorting and HTML status badges.
* Talk time vs. Wrap-up time (ACW) efficiency matrix.
* Occupancy rate and schedule adherence tracking.
* Quality assurance audit scores and coaching flags.

### 4. ⭐ Page 4: Customer Sentiment & Resolution Deep Dive
* CSAT rating distributions mapped across customer tiers (Standard Merchants vs. Enterprise Stores).
* Reason-for-call taxonomy breakdown (Order Tracking, Checkout Glitches, Domain Configuration, Billing).
* Repeat caller analysis and escalation pathway inspection.

---

## 📐 Data Model & Star Schema

The project is structured on a normalized **Star Schema** to guarantee high-performance query execution across large telephony datasets:

```
                  ┌──────────────────────┐
                  │      Dim_Date        │
                  └──────────┬───────────┘
                             │ 1
                             │
                             │ *
┌────────────────┐ 1       ┌─┴────────────────────┐       1 ┌──────────────────┐
│   Dim_Agent    ├─────────┤   Fact_CallRecords   ├─────────┤  Dim_CallReason  │
└────────────────┘ *       └─┬────────────────────┘       * └──────────────────┘
                             │ *
                             │
                             │ 1
                  ┌──────────┴───────────┐
                  │      Dim_Queue       │
                  └──────────────────────┘
```

* **Fact_CallRecords:** Telephony transactional logs (Call_ID, Timestamp, Agent_ID, Customer_ID, Queue_ID, Wait_Time_Sec, Talk_Time_Sec, Hold_Time_Sec, ACW_Sec, Status, CSAT_Score).
* **Dim_Agent:** Representative profiles (Agent_ID, Agent_Name, Team_Lead, Shift, Tier, Hire_Date).
* **Dim_Queue:** Queue configurations (Queue_ID, Queue_Name, Priority, SLA_Threshold_Sec).
* **Dim_CallReason:** Inbound issue categorization (Reason_ID, Category, Subcategory, Severity).
* **Dim_Date & Dim_Time:** Granular temporal dimensions supporting intraday hourly/interval slicing.

---

## ⚙️ Core DAX Formulations

Explicit DAX measures engineered for accuracy and governance:

```dax
// Total Inbound Call Traffic
Total Calls = COUNTROWS ( Fact_CallRecords )

// Answered Calls Volume
Calls Answered = 
CALCULATE ( 
    [Total Calls], 
    Fact_CallRecords[Call_Status] = "Answered" 
)

// Abandoned Calls Volume
Calls Abandoned = 
CALCULATE ( 
    [Total Calls], 
    Fact_CallRecords[Call_Status] = "Abandoned" 
)

// Call Abandonment Percentage
Abandonment Rate % = 
DIVIDE ( [Calls Abandoned], [Total Calls], 0 )

// Service Level Agreement Compliance (80/20 standard)
SLA Compliance % = 
VAR WithinThreshold = 
    CALCULATE ( 
        [Calls Answered], 
        Fact_CallRecords[Wait_Time_Sec] <= 20 
    )
RETURN
    DIVIDE ( WithinThreshold, [Total Calls], 0 )

// Average Handling Time in Minutes
Average Handling Time (AHT) = 
VAR TotalHandleSec = 
    SUM ( Fact_CallRecords[Talk_Time_Sec] ) + 
    SUM ( Fact_CallRecords[Hold_Time_Sec] ) + 
    SUM ( Fact_CallRecords[ACW_Sec] )
RETURN
    DIVIDE ( 
        DIVIDE ( TotalHandleSec, [Calls Answered], 0 ), 
        60 
    )

// Customer Satisfaction (CSAT) Average
CSAT Score = 
AVERAGE ( Fact_CallRecords[CSAT_Score] )
```

---

## 📂 Repository Structure

```
SALla-call-center-Dashboard/
├── assets/                          # UI mockups, visual themes, and architecture diagrams
├── data/                            # Sample raw datasets and schema definitions
├── html-templates/                  # Custom HTML & CSS templates for Power BI cards
│   ├── kpi-card-glass.html          # HTML/CSS template for modular KPI metric cards
│   ├── sla-badge.html               # Dynamic SLA status indicator snippet
│   └── agent-scorecard.html         # Agent profile scorecard styling
├── Salla_CallCenter_Analytics.pbix  # Interactive Power BI report (WIP)
└── README.md                        # Project documentation and engineering specification
```

---

## 🚀 Project Development Roadmap

- [x] **Phase 1:** Requirements definition, call center domain KPI modeling & schema architecture.
- [x] **Phase 2:** Repository initialization, metadata configuration & documentation setup.
- [ ] **Phase 3:** Telephony data cleansing, Star Schema normalization & Power Query ETL pipelines.
- [ ] **Phase 4:** DAX calculation repository implementation (SLA, AHT, FCR, Abandonment).
- [ ] **Phase 5:** Custom HTML5/CSS3 UI card engineering & Deneb visual integration.
- [ ] **Phase 6:** Multi-page interactive dashboard build & executive drill-down validation.
- [ ] **Phase 7:** Final publication to portfolio & executive presentation release.

---

## 👤 Author & Connect

* **Islam Yasser** — Data Analyst & Business Intelligence
* 🌐 **Portfolio:** [islamyasser424-design.github.io/portfolio-](https://islamyasser424-design.github.io/portfolio-/)
* 💼 **LinkedIn:** [linkedin.com/in/islam-yasser-55048b378](https://www.linkedin.com/in/islam-yasser-55048b378/)
* 📧 **Email:** [islamyasser424@gmail.com](mailto:islamyasser424@gmail.com)
* 🐙 **GitHub:** [@islamyasser424-design](https://github.com/islamyasser424-design)

---
*⭐ Star this repository to track progress as this dashboard is actively developed!*
