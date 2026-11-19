# Graph-Based Digital Twin for Multi-Tier Aerospace Supply Chains

**A Topological Network Approach to Predict and Mitigate Non-Conformance Cascade Failures & Bullwhip Effect**

## Overview
Traditional Enterprise Resource Planning (ERP) systems and relational databases (SQL) excel at recording transactional data (purchase orders, lead times, and quality non-conformances), yet they fail to capture structural dependencies across multi-tier aerospace supply chains. 

This repository presents a **Proof of Concept (PoC) Graph-Based Digital Twin** operating in a non-intrusive **Digital Shadow** architecture, developed in **Python**, **SQLite**, and **NetworkX**. The model mirrors relational supply chain records into a weighted directed graph $G = (V, E, W)$ to detect hidden bottlenecks, calculate topological centrality, and simulate cascade failures before they halt Final Assembly Lines (FAL).

## Key Engineering Insights (SQL vs. Graph Topology)
* **Relational Blind Spot (SQL):** When ranking suppliers strictly by lead time, critical sub-tier suppliers with short delivery cycles appear low-risk (`T2_A`, 15-day lead time, 12% non-conformance rate).
* **Topological Risk Discovery (Graph):** By computing **Betweenness Centrality** and downstream cascade dependencies, the Digital Twin reveals that `T2_A` holds the highest systemic risk (**Bullwhip Risk Index: 48.0** vs. **3.0** for top SQL-ranked suppliers), acting as a Single Point of Failure affecting **66% of Tier-1 subassemblies** (`T1_A` and `T1_B`) and halting final aircraft assembly (`OEM`).
* **Digital Shadow & Shadow Supply Detection:** Operating in read-only shadow mode (`0 alterations` to the legacy SQL database), the model detects an unrecorded emergency purchase edge (`T2_A` $\rightarrow$ `T1_C`), escalating the Bullwhip Risk Index from **48.0 to 60.0** and exposing **100% of the aircraft network (4 downstream nodes)** to a single-point cascade failure.
* **Mitigation Simulation:** Introducing a redundant contingency supplier (`T2_C`) isolates the bottleneck and preserves operational continuity without inflating global safety stocks.

## Repository Structure
* `TCC_GemeoDigital_SupplyChain_SQL_Grafos.ipynb` — Complete Google Colab / Jupyter Notebook containing the relational database schema, SQL queries, NetworkX graph modeling, Digital Shadow simulation, and comparative visualizations.
* `grafico_tcc_alta_resolucao.png` — High-resolution (300 DPI) topological comparison between the vulnerable network (Scenario 1) and the mitigated network (Scenario 2).
* `tabela_sql_tcc.xlsx` & `tabela_grafo_tcc.xlsx` — Exported quantitative metrics comparing relational vs. graph-based risk prioritization.

## Quantitative Results Summary

| Node ID | Supplier Name | Betweenness Centrality | Downstream Cascade Nodes | Bullwhip Risk Index |
| :--- | :--- | :---: | :---: | :---: |
| **T2_A** | MicroRivets Brasil (Tier 2) | 0.000 | 3 *(4 in Shadow)* | **48.0** *(60.0 in Shadow)* |
| **T2_B** | AlloySheets Minas (Tier 2) | 0.000 | 2 | **12.0** |
| **T1_A** | WingStructures Corp (Tier 1) | **0.075** | 1 | **6.0** |
| **T1_B** | FuselageSystems Inc (Tier 1) | **0.025** | 1 | **5.0** |
| **T1_C** | AvionicsControl (Tier 1) | 0.000 | 1 | **3.0** |
| **OEM** | Final Assembly Line (Aircraft) | 0.000 | 0 | **0.0** |

## Tech Stack & Methodologies
* **Languages & Libraries:** Python 3, SQL (SQLite), NetworkX, Pandas, Matplotlib.
* **Industrial Engineering Frameworks:** Multi-Tier Supply Chain Management, Production Planning & Control (PCP), Bullwhip Effect Mitigation, Network Science, Digital Shadow & Digital Twins.

## Author
**Eliane Soares Nogueira**  
B.S. in Mathematics | B.S. Candidate in Production Engineering (Class of 2027)  
*Research focus: Aerospace Systems Engineering, Supply Chain Resilience, and Graph-Based Digital Twins.*
