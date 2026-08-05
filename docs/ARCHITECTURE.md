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
## Mathematical Formulation of Section Throughput

Section capacity $C$ over time window $T$ is governed by:
$$C = \frac{T}{h_{avg} + t_{clear}} \cdot \eta_{platform}$$

Where:
- $h_{avg}$: Weighted average minimum headway across train categories.
- $t_{clear}$: Turnaround and switch-lock release time between departures.
- $\eta_{platform}$: Platform utilization efficiency factor.

The AI controller maximizes $\eta_{platform}$ by eliminating idle platform gaps caused by cascading delays.
\n
## Controller Paradigm Comparison

| Feature | Baseline Heuristic Controller | AI-Powered Controller |
| :--- | :--- | :--- |
| **Platform Assignment** | Fixed timetable pre-assignment | Dynamic predicted availability |
| **Delay Response** | Reactive First-Come First-Served | Predictive proactive re-routing |
| **Priority Handling** | Static FIFO queueing | Dynamic priority-weighted penalty function |
| **Deadlock Mitigation** | Timeout backoff heuristic | Lookahead path conflict detection |
| **Incident Recovery** | Linear propagation of delays | Fast localized absorption |
\n
## Deadlock Prevention & Conflict Resolution

In dense railway networks, mutual waiting conditions (train A holding block 1 waiting for block 2, while train B holds block 2 waiting for block 1) cause deadlocks.

### Prevention Strategy
1. **Hierarchical Resource Ordering**: Block sections are ordered strictly along travel vectors.
2. **Lookahead Windowing**: Trains cannot enter a critical junction zone unless the destination block and platform are reserved.
3. **Deadlock Detection Timeout**: The simulation detects if two agents remain stationary for $> 15$ simulation minutes and triggers preemptive AI re-routing.
\n
## Disaster Mode & Resiliency Architecture

Disaster Mode simulates high-stress operational contingencies:
- **Track Failure**: An entire platform or incoming track block is taken offline abruptly.
- **Signal Disruption**: Manual caution speeds imposed across critical sections ($15\text{ km/h}$ limit).
- **Controller Reaction**:
  - Baseline controller queues all approaching trains, causing cascading gridlock.
  - AI controller anticipates the blockage, diverts trains to secondary loop tracks, and reschedules low-priority freight to hold at upstream loops.
\n
## Delay Propagation Physics & Knock-on Effect Modeling

Primary delays (e.g., rolling stock faults, track maintenance) frequently trigger secondary "knock-on" delays across adjacent services:
- **Headway Propagation**: A delayed train forces following trains to encounter amber/red aspects, triggering reactive braking.
- **Platform Occupation Starvation**: If train $A$ overstays its platform dwell, train $B$ must hold in the outer loop, blocking the main through-line.
- **AI Dampening Effect**: By proactively assigning train $B$ to an alternate siding before it reaches the outer signal, the AI controller prevents the through-line from locking.
\n
### Mathematical Formulation of Buffer Time ($B_{margin}$)
To absorb minor perturbations, timetables incorporate schedule recovery margins:
$$B_{margin} = t_{scheduled\_dwell} - t_{minimum\_dwell}$$

When primary delay $D_{primary} \le B_{margin}$, the delay is fully absorbed within the station dwell. When $D_{primary} > B_{margin}$, the unabsorbed delay propagates downstream:
$$D_{downstream} = \max(0, D_{primary} - B_{margin})$$
\n
## Subsystem Modular Decomposition

The codebase decouples concerns cleanly across python packages:
```
Train_Project_SIH/
├── ai/                     # Machine learning models & feature extraction
│   ├── features.py         # Tabular feature transformation
│   └── model.py            # Model training & inference wrapper (AIManager)
├── simulation/             # Discrete-event engine core
│   ├── env.py              # SimPy environment loop & runner
│   ├── station.py          # Station & platform resource representation
│   ├── train.py            # Train agent behavior & state machine
│   ├── controller.py       # Baseline heuristic controller
│   └── ai_controller.py    # AI-guided dynamic dispatch controller
├── dashboard/              # Streamlit front-end
│   ├── ui.py               # Layout components & parameter sidebar
│   ├── kpi.py              # Statistical KPI aggregation
│   ├── graphs.py           # Plotly charts (Gantt, histograms)
│   └── tables.py           # Decision tables & audit viewer
├── app.py                  # Main application entry point
```
\n