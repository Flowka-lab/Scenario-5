
# Demand Planning App

A lightweight demand planning application designed to support forecasting, scenario analysis, and planner decision-making through a simple, modular workflow.

---

## Overview

This application provides a structured demand-planning flow, starting from statistical baseline forecasts and progressing through manual adjustments, exception handling, and scenario comparison.  
It is built as an MVP with clarity, extensibility, and performance in mind.

The project is intentionally generic and does not expose any client-specific logic, data, or business rules.

---

## Core Objectives

- Provide a reliable baseline demand forecast
- Enable planners to enrich forecasts with business insight
- Highlight exceptions and focus areas
- Compare multiple demand scenarios
- Support publish and review workflows

---

## Key Features

- **Baseline Demand Forecast**
  - Statistical forecast generation using historical demand data
  - Configurable forecast horizon and granularity

- **Manual Forecast Adjustment**
  - Planner overrides at SKU / location / time level
  - Full traceability of adjustments

- **Exception-Driven Focus**
  - Identification of anomalies, spikes, drops, and forecast deviations
  - Prioritization of items requiring attention

- **Scenario Comparison**
  - Side-by-side comparison of multiple forecast versions
  - Impact analysis across time and dimensions

- **Demand vs Capacity View**
  - High-level comparison between demand and available capacity
  - Early detection of potential supply constraints

- **Publish & Share**
  - Final forecast validation and publishing
  - Versioning and historical tracking

---

## Architecture (High Level)

- Modular backend services for data processing and forecasting
- Relational database for historical data, forecasts, and audit logs
- Web-based UI for planners and analysts
- API-first design to support future integrations

---

## Data Principles

- Separation between raw data, calculated forecasts, and user overrides
- Full auditability of forecast runs and changes
- Support for multi-SKU, multi-location, time-series data

---

## Security & Confidentiality

- No real customer data included
- No proprietary algorithms or parameters exposed
- Designed to be safely shared as a public reference MVP

---

## Intended Audience

- Demand planners
- Supply-chain analysts
- Product and solution architects
- Teams exploring modern demand-planning workflows

---

## Roadmap (Indicative)

- Advanced forecasting models
- Hierarchical forecasting and reconciliation
- Integration with supply and inventory systems
- Automation and AI-assisted planning features

---

## License

This project is shared for demonstration and educational purposes only.  
All sensitive logic and data remain private and out of scope.
