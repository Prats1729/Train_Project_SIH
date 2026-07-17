# System Architecture & Design Overview

## Executive Summary
The AI-Powered Train Traffic Control Simulator is a high-fidelity discrete-event simulation engine engineered to evaluate and maximize railway section throughput, punctuality, and incident resilience. Built for the Smart India Hackathon (SIH), it pits standard static rule-based railway scheduling against an adaptive AI-driven dispatching controller.

## Core Architectural Layers
The system is divided into three primary decouple layers:
1. **Simulation Layer (`simulation/`)**: Discrete-event execution powered by SimPy.
2. **Intelligence Layer (`ai/`)**: Feature engineering, delay prediction, and platform allocation classifiers.
3. **Visualization & Analytics Layer (`dashboard/`)**: Interactive Streamlit GUI, KPI telemetry, and scenario comparisons.
\n
### High-Level Component Flow Diagram
```mermaid
graph TD
    A[Streamlit User Controls] -->|Simulation Parameters| B[Simulation Environment]
    B --> C[Station & Track Resources]
    B --> D[Train Agents]
    D -->|State & Telemetry| E{Traffic Controller}
    E -->|Baseline Heuristics| F[Rule-Based Dispatcher]
    E -->|Delay Predictions| G[AI Model Manager]
    G --> H[Platform Allocation Classifier]
    H -->|Optimized Assignment| B
    B --> I[KPI Metrics Engine]
    I --> J[Streamlit Analytics Dashboard]
```
\n