# Testing & Verification Guide

## Testing Philosophy
Railway simulation systems require strict verification because invalid state transitions can produce unphysical artifacts like phantom collisions or deadlock starvation.

## Test Suite Layout
- `tests/test_simulation.py`: Verifies SimPy train processes, headway invariants, and queue states.
- `tests/test_ai_model.py`: Validates model inference bounds, feature scaling, and input validation.
- `tests/test_kpi.py`: Verifies mathematical correctness of KPI calculation formulas.
- `tests/test_edge_cases.py`: Stresses zero-delay, 100% saturation, and single-platform scenarios.
\n
## Simulation Unit Test Specifications

### 1. Headway Enforcement Test
- **Objective**: Ensure two trains on the same track maintain $\ge 3$ minutes headway.
- **Assertion**: $\min(t_{departure, i+1} - t_{departure, i}) \ge t_{headway}$.

### 2. Platform Exclusivity Test
- **Objective**: Verify no two trains occupy the same platform concurrently.
- **Assertion**: For all time intervals, $\sum \text{Occupants}(P_k) \le 1$.
\n
### KPI Mathematical Invariant Tests
- **Punctuality Range**: $0 \le \text{Punctuality} \le 100$.
- **Delay Non-negativity**: Average delay must always be $\ge 0.0$.
- **Throughput Conservation**: Total cleared trains cannot exceed total scheduled trains.
- **Capacity Bounds**: Platform utilization percentage cannot exceed 100% over the simulation duration.
\n
## Stress Testing & Bottleneck Scenarios

### High Density Congestion Stress Test
- **Input**: 150 trains injected into a 24-hour simulation window across 3 platforms.
- **Evaluation**: Verify simulation completes without unhandled exceptions or infinite event loops.
- **Pass Criteria**: All 150 train entities transition to `Departed` state within finite simulation time.
\n
### Single Platform Bottleneck Test
- **Input**: Simulate station with `platforms_b = 1` and 20 trains.
- **Evaluation**: Verifies that the queueing system degrades gracefully and queues strictly in FIFO order under the baseline controller, while prioritizing Tier 1 trains under the AI controller.
\n
## Continuous Integration (CI) Workflow

Our CI pipeline executes on every pull request to `main`:
1. **Linting**: Checks compliance with `flake8` and `black --check`.
2. **Type Checking**: Validates type signatures with `mypy`.
3. **Simulation Sanity**: Runs 10 deterministic test simulations across various platform configurations.
4. **KPI Verifier**: Confirms output metrics are within valid bounds.
\n
## Regression Testing Framework

Whenever `AIManager` model code or feature engineering logic is modified:
- `tests/test_model_regression.py` validates that MAE on the canonical test partition does not exceed $4.2\text{ minutes}$.
- Verifies that model serialization via `pickle` or `joblib` produces bit-compatible inference outputs.
\n