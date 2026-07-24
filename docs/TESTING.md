# Testing & Verification Guide

## Testing Philosophy
Railway simulation systems require strict verification because invalid state transitions can produce unphysical artifacts like phantom collisions or deadlock starvation.

## Test Suite Layout
- `tests/test_simulation.py`: Verifies SimPy train processes, headway invariants, and queue states.
- `tests/test_ai_model.py`: Validates model inference bounds, feature scaling, and input validation.
- `tests/test_kpi.py`: Verifies mathematical correctness of KPI calculation formulas.
- `tests/test_edge_cases.py`: Stresses zero-delay, 100% saturation, and single-platform scenarios.
\n