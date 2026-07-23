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