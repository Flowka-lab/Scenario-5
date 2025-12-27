
---

# Project Black Swan: Autonomous Supply Chain Resilience Engine

**Version:** 1.0

**Status:** Initial Draft / Functional Design

**Domain:** Automotive Supply Chain (Tier-1)

**Architecture:** Agentic AI (LangGraph + RAG + Graph Theory)

---

## 1. Executive Summary

### 1.1 The Context: "Between Two Sharp Edges"

We operate as a **Tier-1 Automotive Supplier** (e.g., producing Braking Systems, ECUs, or Dashboard Assemblies). We exist in a high-pressure ecosystem:

* **Upstream:** We rely on a complex network of global Tier-2 and Tier-3 suppliers (often in Asia) for raw components (chips, sensors, specialized steel).
* **Downstream:** We serve demanding European OEMs (BMW, Renault, Stellantis) operating on **Just-In-Time (JIT)** and **Just-In-Sequence (JIS)** models.

### 1.2 The Problem

The automotive supply chain is optimized for **Cost and Efficiency**, not **Resilience**.

* **Buffer Stocks:** Measured in hours/days, not weeks.
* **The Cost of Failure:** A missing part stops an OEM assembly line. Penalties range from **€1M to €5M per day**, plus catastrophic reputational damage.
* **The Gap:** When a global disruption occurs (e.g., Suez Canal blockage, supplier fire), human planners take 24-48 hours to assess impact and find alternatives. By then, global air freight capacity is booked, and alternative stock is gone.

### 1.3 The Solution

**"Black Swan"** is an Agentic AI Engine that monitors global risks 24/7, maps them instantly to our specific Bill of Materials (BOM), and **autonomously executes mitigation strategies** (sourcing, logistics switching) before the human team even opens their laptops.

---

## 2. User Persona & Pain Points

| User Persona | Role | Primary Pain Point | What they need |
| --- | --- | --- | --- |
| **The Supply Planner** | Manages material flow for a specific plant. | "I drown in Excel sheets when a crisis hits. I don't know which of 5,000 parts are on the stuck ship." | Instant visibility: "Here is exactly what is at risk." |
| **The Procurement Manager** | Negotiates with suppliers. | "Finding a new supplier takes 2 weeks of emails. I need to find one in 2 hours." | Instant sourcing: Automated RFQs to pre-vetted alternatives. |
| **The Plant Director** | Responsible for P&L. | "Do I pay 10x for Air Freight or stop the line? I need the math." | Cost/Benefit Analysis: "Air freight costs €50k, Line stop costs €1M." |

---

## 3. Functional Architecture

The system is built on a **Multi-Agent Architecture** orchestrated by **LangGraph**. It moves beyond simple "Q&A" to a state-based reasoning engine.

### 3.1 The Agent Team

#### 🕵️ Agent A: The Watchtower (Risk Detection)

* **Responsibility:** Monitors the world for "signals" relevant to our specific supply chain geography.
* **Input:** News APIs (Tavily), Weather Data, Port Congestion Feeds.
* **Logic:** Filters noise. A "Strike in Paris" matters. A "Strike in a local bakery" does not.
* **Trigger:** When a high-confidence event is detected (e.g., "Fire in Renesas Chip Plant"), it wakes up Agent B.

#### 🕸️ Agent B: The Graph Master (Impact Mapping)

* **Responsibility:** The "Brain" that understands relationships.
* **Technology:** **Neo4j (Graph Database)**.
* **Logic:**
* Query: *"The fire is in Naka, Japan. Which of our Tier-2 suppliers are there?"*
* Trace: *"Supplier X makes Chip Y. Chip Y goes into ECU Z. ECU Z goes to BMW Plant Munich."*


* **Output:** A list of **Affected SKUs** and **Revenue at Risk**.

#### 🧮 Agent C: The Strategist (Simulation & Optimization)

* **Responsibility:** The "Quant."
* **Logic:**
* Check **ERP (SQL)** for current inventory of the affected part.
* Calculate **"Time to Starvation"** (When will the line stop?).
* Compare Options:
1. *Wait it out:* (Risk: Line stop).
2. *Expedite Shipping:* (Cost: +500%).
3. *Alternative Supplier:* (Cost: +20%, Lead Time: 3 days).





#### 🤝 Agent D: The Negotiator (Sourcing & Action)

* **Responsibility:** Execution.
* **Technology:** **Vector DB (Pinecone)** for contract search.
* **Logic:**
* Find alternative suppliers for "Automotive Grade Resistors."
* Check their "Approved Vendor List" status.
* **Action:** Draft a text-perfect RFQ (Request for Quotation) and place it in the Human's draft folder or Slack channel for one-click approval.



---

## 4. Technical Stack (The "World Class" Standard)

| Component | Technology | Why this choice? |
| --- | --- | --- |
| **Orchestrator** | **LangGraph** (Python) | Required for cyclic logic (Try -> Fail -> Retry) and "Human-in-the-loop" approval flows. |
| **LLM** | **GPT-4o** / **Claude 3.5 Sonnet** | High reasoning capability for complex supply chain constraints. |
| **Graph DB** | **Neo4j** | Essential for mapping N-Tier dependencies (Supplier -> Part -> Assembly -> OEM). SQL is too rigid for this. |
| **Vector DB** | **Pinecone** / **Chroma** | Stores unstructured PDF contracts, Force Majeure clauses, and Supplier Manuals. |
| **Tools** | **Tavily Search** | AI-optimized search for real-time disruption discovery. |
| **Frontend** | **Streamlit** | Rapid visualization of the "War Room" dashboard. |

---

## 5. The "Golden Scenario" (Walkthrough)

**Scenario:** A container ship carrying **Micro-controllers (MCU-500)** from Taiwan to Rotterdam is blocked due to a geopolitical tension in the Red Sea.

1. **08:00 AM:** `Watchtower Agent` detects news: "Red Sea transit halted for Maersk vessels."
2. **08:02 AM:** `Graph Master` queries Neo4j.
* *Result:* "MCU-500 is on a Maersk vessel. It feeds the 'Dashboard Assembly' for the **Renault Megane**."


3. **08:05 AM:** `Strategist Agent` checks SQL ERP.
* *Inventory:* 3 days of stock on hand.
* *Delay:* 14 days (detour via Africa).
* *Impact:* **Line Down in 72 hours.**


4. **08:07 AM:** `Negotiator Agent` checks Pinecone.
* *Result:* "Supplier B in Turkey has compatible MCUs. Price is +15%."


5. **08:10 AM:** **Human Planner receives a Slack Alert:**
> 🚨 **CRITICAL RISK DETECTED**
> * **Event:** Red Sea Blockage.
> * **Impact:** Renault Line Stop in 72h. Penalty Risk: €2.4M.
> * **Recommendation:** Switch to Supplier B (Turkey). Cost impact: +€15k.
> * **Action:** [Button: Approve PO for Supplier B] [Button: Ignore]
> 
> 



---

## 6. Business Value & KPIs

| KPI | Current Manual Process | "Black Swan" Target |
| --- | --- | --- |
| **Time to Insight** | 24 - 48 Hours | < 15 Minutes |
| **Reaction Speed** | Days (Email pong) | Instant (Automated RFQ) |
| **Decision Basis** | Gut feel / Panic | Data-driven ($ vs. Time) |
| **Data Usage** | Structured only (Excel) | Unstructured (News/PDFs) + Graph |

---

## 7. Future Roadmap (Post-MVP)

* **Phase 2:** Integration with Live Logistics APIs (MarineTraffic, FlightAware) for real-time tracking.
* **Phase 3:** "Green Routing" – Agents that optimize for CO2 impact alongside cost.
* **Phase 4:** Vision capabilities – Allow agents to "read" quality reports or schematics using VLM.

---

*Created by Hamza Salami – AI Supply Chain Architect*
