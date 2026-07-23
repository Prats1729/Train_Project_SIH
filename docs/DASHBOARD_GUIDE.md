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