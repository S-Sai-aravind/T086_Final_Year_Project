# T086_Final_Year_Project
# AI-Powered Snapshot Lifecycle Management and Storage Optimization System

An intelligent Azure VM snapshot management system that combines workload telemetry, XGBoost-based workload risk prediction, cost optimization, snapshot lifecycle decisions, and deterministic safety controls to determine when snapshots should be created and when retained snapshots can be deleted.

---

## 📌 Project Overview

Traditional VM snapshot management commonly relies on fixed snapshot intervals or manually configured policies. A fixed interval may create unnecessary snapshot overhead during low workload periods while providing insufficient protection during periods of high data-change activity.

This project proposes a risk-adaptive snapshot lifecycle management system for Azure Virtual Machines.

The system:

1. Collects VM workload telemetry.
2. Performs feature engineering on workload data.
3. Uses an XGBoost model to estimate future workload/data-change risk.
4. Converts the predicted risk into a risk parameter.
5. Uses a cost optimization model to determine an optimal snapshot interval.
6. Compares the current snapshot age with the calculated interval.
7. Produces a `CREATE` or `WAIT` decision.
8. Evaluates snapshot retention using `KEEP` or `DELETE`.
9. Applies a deterministic safety gate for high and extreme workloads.
10. Displays workload, risk, decisions, interval, and cost information through a Streamlit dashboard.

---

## 🎯 Objectives

- Develop an intelligent snapshot creation mechanism for Azure VMs.
- Reduce unnecessary snapshot operations during low-risk workloads.
- Provide stronger protection during high workload/data-change periods.
- Incorporate recovery policies such as RPO, RTO, and criticality.
- Optimize snapshot intervals using a cost-based mathematical model.
- Provide deterministic safety overrides for extreme workloads.
- Manage both snapshot creation and snapshot retention.
- Provide a professional dashboard for monitoring and demonstration.

---

## 🏗️ System Architecture

```text
                    ┌──────────────────────────┐
                    │    Azure VM / Monitor    │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Telemetry & Feature       │
                    │ Engineering               │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ XGBoost Workload Risk     │
                    │ Prediction                │
                    └────────────┬─────────────┘
                                 │
                         Predicted Risk
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Cost Optimization         │
                    │ & Interval Calculation    │
                    └────────────┬─────────────┘
                                 │
                            Optimal T*
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Snapshot Decision Engine  │
                    │                           │
                    │ CREATE / WAIT             │
                    │ KEEP / DELETE             │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Deterministic Safety Gate│
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Azure Snapshot Storage    │
                    └──────────────────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │ Streamlit Dashboard      │
                    └──────────────────────────┘
