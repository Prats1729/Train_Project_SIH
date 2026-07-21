# AI Controller & Machine Learning Dispatching

## Overview
The AI Controller (`ai/model.py` and `simulation/ai_controller.py`) acts as an intelligent traffic dispatcher. Rather than relying on rigid static rules, it continuously evaluates section telemetry, predicts upcoming train arrival delays, and dynamically reassigns platforms to minimize total system delay.

## Machine Learning Architecture
The AI subsystem integrates two predictive engines:
1. **Delay Prediction Regressor**: Estimates expected minutes of delay based on current travel time, upstream congestion, and priority class.
2. **Platform Allocation Classifier**: Evaluates candidate platforms and outputs optimal platform assignment probabilities.
\n