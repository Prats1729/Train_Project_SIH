# Streamlit Analytics Dashboard Guide

## Overview
The interactive dashboard (`app.py`, `dashboard/ui.py`) provides railway controllers and hackathon evaluators with a visual control deck to configure simulation experiments, simulate real-time traffic, and compare baseline vs AI performance side-by-side.

## UI Layout Structure
- **Sidebar Control Deck**:
  - Number of trains to simulate (10 - 200).
  - Number of platforms per station.
  - Delay probability & severity sliders.
  - Disaster Mode toggle and failure parameters.
- **Main Viewport**:
  - Live execution progress indicators.
  - KPI Summary Metric Cards (Punctuality, Average Delay, Throughput).
  - Interactive charts (Gantt timetable, delay distribution, platform heatmaps).
  - Decision audit log table.
\n
### Configuration Parameter Reference

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `num_trains` | Integer | `50` | Total train trips scheduled in the 24-hour simulation window. |
| `platforms_b` | Integer | `3` | Total available berthing platforms at destination station B. |
| `delay_prob` | Float | `0.30` | Probability of synthetic perturbation injected at departure. |
| `max_delay_minutes` | Integer | `45` | Maximum synthetic delay added to perturbed services. |
| `disaster_mode` | Boolean | `False` | Simulates sudden track failure and emergency bottleneck. |
\n
## Key Performance Indicators (KPIs) (`dashboard/kpi.py`)

The platform calculates four primary quantitative KPIs:
1. **Punctuality Rate (%):**
   $$\text{Punctuality} = \frac{N_{\text{arrival delay} \le 5\text{ min}}}{N_{\text{total trains}}} \times 100$$
2. **Average Arrival Delay (min):**
   $$\bar{D} = \frac{1}{N} \sum_{i=1}^{N} \max(0, t_{actual, i} - t_{scheduled, i})$$
3. **Section Throughput (trains/day):** Total count of safely cleared trains.
4. **Platform Utilization (%):** Total active dwell time divided by total platform operating capacity.
\n
## Visualization Modules (`dashboard/graphs.py`)

- **Timetable String Chart (Gantt)**: Plots train position against simulation time. Slopes reflect train velocities; horizontal segments illustrate dwell times.
- **Delay Delta Histogram**: Compares Baseline vs AI delay distribution, showing how the AI model shifts the distribution toward zero delay.
- **Platform Occupancy Heatmap**: Highlights peak utilization hours to identify bottlenecks before cascading delays occur.
\n
## Decision Audit Log Table (`dashboard/tables.py`)
Each AI dispatch decision is recorded with complete audit metadata:
- `timestamp`: Simulation epoch of decision event.
- `train_id`: Target train identifier (e.g., `TRN_12042`).
- `predicted_delay`: ML forecasted delay in minutes.
- `allocated_platform`: Selected platform berth index.
- `alternative_platforms`: Candidate platforms considered.
- `reason`: Heuristic or probabilistic rationale for the allocation.
\n