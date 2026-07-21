# AI Controller & Machine Learning Dispatching

## Overview
The AI Controller (`ai/model.py` and `simulation/ai_controller.py`) acts as an intelligent traffic dispatcher. Rather than relying on rigid static rules, it continuously evaluates section telemetry, predicts upcoming train arrival delays, and dynamically reassigns platforms to minimize total system delay.

## Machine Learning Architecture
The AI subsystem integrates two predictive engines:
1. **Delay Prediction Regressor**: Estimates expected minutes of delay based on current travel time, upstream congestion, and priority class.
2. **Platform Allocation Classifier**: Evaluates candidate platforms and outputs optimal platform assignment probabilities.
\n
## Feature Engineering Pipeline (`ai/features.py`)
The model consumes engineered features derived from real-time simulation state:
- `scheduled_arrival`: Planned arrival time in minutes from epoch.
- `priority`: Numeric priority tier (1 = Freight, 2 = Passenger, 3 = Superfast).
- `dwell_time`: Expected station dwell duration.
- `upstream_delay`: Accumulated delay at preceding block signals.
- `active_occupancy_ratio`: Proportion of occupied platforms at target station.
- `time_of_day_sin`/`time_of_day_cos`: Cyclical temporal encoding.
\n