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