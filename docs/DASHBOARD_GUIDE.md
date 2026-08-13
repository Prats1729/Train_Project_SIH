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
## What-If Scenario Analysis Workflow

The simulator allows dispatchers and planners to test hypothetical operating scenarios:
1. **Platform Capacity Sizing**: Compare throughput when adding a 4th or 5th platform to Station B.
2. **Speed Restriction Impact**: Evaluate punctuality collapse under temporary $30\text{ km/h}$ speed restrictions.
3. **Traffic Mix Sensitivity**: Assess the impact of increasing freight proportion from 10% to 40% on passenger punctuality.
\n
## Troubleshooting Common Dashboard Issues

- **Streamlit Port Collision**: If port `8501` is occupied, launch with `streamlit run app.py --server.port 8502`.
- **Session State Cache Reset**: Click the 'R' key in browser or use the sidebar cache clear button to re-initialize model parameters.
- **Memory Consumption with Large Train Counts**: For runs exceeding 200 trains, run headless or increase browser RAM allocation.
\n
## Telemetry Export Capabilities

The dashboard supports exporting full simulation run artifacts:
- **CSV Log Export**: Complete tabular logs of train arrival, departure, and delay metrics.
- **JSON Decision Telemetry**: Structured JSON array of all AI controller allocation decisions.
- **KPI Summary Report**: Plain-text and markdown export summarizing comparative punctuality gains.
\n
## Disaster Mode Alerts & Incident Telemetry

When Disaster Mode is engaged:
- **Visual Alert Banner**: A prominent warning banner appears at the top of the dashboard.
- **Incident Telemetry Box**: Displays failed block ID, failure duration, and number of impacted train paths.
- **Mitigation Statistics**: Displays real-time delta of trains rerouted by AI vs stuck under baseline rule.
\n
### Dashboard Theming & Visual Aesthetics
The dashboard uses custom CSS styling injected via `st.markdown(..., unsafe_allow_html=True)`:
- High contrast dark mode tailored for railway operational display screens.
- Color-coded KPI chips: Green for punctuality $> 85\%$, Yellow for $70-85\%$, Red for $< 70\%$.
- Styled metric cards with subtle box shadows and border radiuses.
\n
## Live Simulation Execution Feedback

During long simulation runs with large train batches, `app.py` delivers dynamic user feedback:
- Separate progress bars for Baseline and AI simulation passes.
- Dynamic status spinner indicating KPI calculation and Plotly figure generation.
- Clear error notification dialogs if invalid configurations are supplied.
\n
## Multi-Run Scenario Comparison & Reporting

The dashboard provides a dedicated comparative tab:
- Side-by-side comparison of up to 5 experimental runs with different configurations.
- Automatic Delta Calculation: Percentage improvement in punctuality and delay reduction.
- One-click export of comparison tables to Microsoft Excel (`.xlsx`) format.
\n