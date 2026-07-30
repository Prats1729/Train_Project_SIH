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
### Delay Prediction Model Specs
- **Algorithm**: `RandomForestRegressor` from `scikit-learn`.
- **Hyperparameters**:
  - `n_estimators`: 100 trees.
  - `max_depth`: 12.
  - `min_samples_split`: 4.
  - `random_state`: 42.
- **Target Variable**: Continuous delay in minutes ($y_{delay} \ge 0$).
- **Inference Latency**: < 5ms per dispatch event to maintain real-time simulation speed.
\n
### Platform Allocation Classifier Specs
- **Algorithm**: `GradientBoostingClassifier` or `RandomForestClassifier`.
- **Target Variable**: Discrete platform index $[0, 1, \dots, N_{platforms}-1]$.
- **Constraint Masking**: Model output probabilities are masked with real-time platform availability to prevent collision assignments.
\n
## Decision Latency & Performance Profiling

In real-world traffic management systems (TMS), dispatch recommendations must compute within sub-second intervals:
- **Single Train Inference Latency**: $2.4\text{ ms} \pm 0.3\text{ ms}$.
- **Batch Rescheduling Latency (50 trains)**: $48\text{ ms}$.
- **Memory Footprint**: Model binaries occupy $< 15\text{ MB}$ RAM, enabling edge deployment on signaling workstation hardware.
\n
### Heuristic Fallback Safety Net
To guarantee operational safety in production:
- If model prediction confidence drops below threshold $\tau = 0.65$, or if the AI controller predicts an already-occupied platform, the system triggers the **Deterministic Safety Fallback Rule**.
- The fallback rule chooses the lowest-indexed platform that is vacant and clear of inbound conflict envelopes.
\n