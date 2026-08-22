# Changelog

All notable changes to the AI-Powered Train Traffic Control Simulator project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Documentation
- Initialized CONTRIBUTING.md with setup guide and git workflow.
- Initialized CHANGELOG.md tracking system architecture and milestones.
\n
### Documentation (2026-07-17)
- Added core system architecture overview and Mermaid component diagram in `docs/ARCHITECTURE.md`.
- Added Conventional Commits standard to `CONTRIBUTING.md`.
\n
### Documentation (2026-07-20)
- Documented station resource queueing and headway safety constraints in `docs/SIMULATION_ENGINE.md`.
- Added mathematical formulation of section throughput in `docs/ARCHITECTURE.md`.
\n
### Documentation (2026-07-21)
- Created `docs/AI_CONTROLLER.md` detailing ML models, feature engineering, and inference pipelines.
- Added Baseline vs AI comparison matrix in `docs/ARCHITECTURE.md`.
\n
### Documentation (2026-07-23)
- Created `docs/DASHBOARD_GUIDE.md` outlining UI components, layout design, and parameter specs.
\n
### Documentation (2026-07-24)
- Documented mathematical KPI definitions and Plotly visualization modules in `docs/DASHBOARD_GUIDE.md`.
- Initialized `docs/TESTING.md` outlining testing philosophy and test suite layout.
\n
### Documentation (2026-07-27)
- Added headway safety and KPI invariant unit test specifications to `docs/TESTING.md`.
- Initialized `docs/ROADMAP.md` covering Phase 1 milestones and Phase 2 enhancements.
\n
### Documentation (2026-07-29)
- Added Phase 3, 4, and 5 specifications to `docs/ROADMAP.md`.
- Documented deadlock avoidance and disaster mode failure injection in `docs/ARCHITECTURE.md`.
\n
## [0.8.0] - 2026-07-30
### Added
- Stochastic delay perturbation modeling via Weibull distributions in `docs/SIMULATION_ENGINE.md`.
- Train priority classifications and overtaking dynamics in `docs/SIMULATION_ENGINE.md`.
- Real-time decision latency benchmarks and heuristic fallback mechanisms in `docs/AI_CONTROLLER.md`.
- High density stress test and bottleneck verification procedures in `docs/TESTING.md`.
\n
### Documentation (2026-07-31)
- Added What-If scenario workflow and troubleshooting notes in `docs/DASHBOARD_GUIDE.md`.
- Added PR review checklist in `CONTRIBUTING.md`.
- Concluded July documentation sprint with comprehensive architectural and operational coverage.
\n
### Documentation (2026-08-01)
- Documented knock-on delay propagation physics and buffer absorption equations in `docs/ARCHITECTURE.md`.
- Kicked off August technical enhancement and operational verification sprint.
\n
### Documentation (2026-08-03)
- Documented train acceleration dynamics and switch interlocking mechanics in `docs/SIMULATION_ENGINE.md`.
- Documented hyperparameter tuning methodology and cross-validation results in `docs/AI_CONTROLLER.md`.
\n
### Documentation (2026-08-04)
- Documented model retraining lifecycle and classification performance in `docs/AI_CONTROLLER.md`.
- Documented telemetry export capabilities in `docs/DASHBOARD_GUIDE.md`.
- Documented CI pipeline and automated test matrix in `docs/TESTING.md`.
\n
### Documentation (2026-08-05)
- Documented subsystem modular directory tree and interface protocols in `docs/ARCHITECTURE.md`.
- Added passenger exchange dwell models and siding overtaking protocols in `docs/SIMULATION_ENGINE.md`.
- Added Phase 6 wayside edge deployment vision to `docs/ROADMAP.md`.
\n
### Documentation (2026-08-06)
- Documented disaster mode visual alert system and CSS theming in `docs/DASHBOARD_GUIDE.md`.
\n
## [0.9.0] - 2026-08-07
### Added
- Time complexity, memory footprint, and session caching analysis in `docs/ARCHITECTURE.md`.
- Synthetic timetable generation algorithms in `docs/SIMULATION_ENGINE.md`.
- Historical training data schema in `docs/AI_CONTROLLER.md`.
- Headless mock testing utilities and model regression test framework in `docs/TESTING.md`.
\n
### Documentation (2026-08-08)
- Added branch naming and release tagging protocol to `CONTRIBUTING.md`.
\n
### Documentation (2026-08-10)
- Documented platform capacity bounds in `docs/ARCHITECTURE.md`.
- Added four-aspect signalling specifications in `docs/SIMULATION_ENGINE.md`.
- Documented feature importance rankings in `docs/AI_CONTROLLER.md`.
- Documented progress feedback UI in `docs/DASHBOARD_GUIDE.md`.
\n
### Documentation (2026-08-11)
- Added eco-driving traction energy calculations in `docs/ARCHITECTURE.md`.
- Documented terminal rake turnaround cycles in `docs/SIMULATION_ENGINE.md`.
- Added WebSocket real-time telemetry streaming roadmap in `docs/ROADMAP.md`.
\n
### Documentation (2026-08-13)
- Documented gradient resistance and emergency braking profiles in `docs/SIMULATION_ENGINE.md`.
- Documented online learning pipelines in `docs/AI_CONTROLLER.md`.
- Added multi-run Excel export guide in `docs/DASHBOARD_GUIDE.md`.
- Added chaos engineering test specifications in `docs/TESTING.md`.
\n
## [1.0.0] - 2026-08-14
### Added
- Complete system documentation suite covering Architecture, Simulation Engine, AI Dispatcher, Dashboard, Testing, and Roadmap.
- Security hardening and input validation standards in `docs/ARCHITECTURE.md`.
- Station track topologies and layout specifications in `docs/SIMULATION_ENGINE.md`.
- 3D Digital Twin visualization vision in `docs/ROADMAP.md`.
\n
### Documentation (2026-08-15)
- Added comprehensive railway operations glossary to `docs/ARCHITECTURE.md`.
- Added developer quick start FAQ to `CONTRIBUTING.md`.
\n
### Documentation (2026-08-17)
- Documented maintenance engineering blocks in `docs/SIMULATION_ENGINE.md`.
- Added Multi-Layer Perceptron benchmarking analysis to `docs/AI_CONTROLLER.md`.
- Documented accessibility shortcuts in `docs/DASHBOARD_GUIDE.md`.
\n
### Documentation (2026-08-18)
- Documented monsoon and fog perturbation models in `docs/ARCHITECTURE.md`.
- Added locomotive pilot duty constraints to `docs/SIMULATION_ENGINE.md`.
- Formulated reinforcement learning reward function in `docs/AI_CONTROLLER.md`.
- Documented benchmark regression test suite in `docs/TESTING.md`.
\n
### Documentation (2026-08-20)
- Documented mixed-traffic freight balancing in `docs/ARCHITECTURE.md`.
- Documented siding length constraints in `docs/SIMULATION_ENGINE.md`.
- Added multi-objective Pareto analysis in `docs/AI_CONTROLLER.md`.
- Documented Kubernetes deployment architecture in `docs/ROADMAP.md`.
\n
## [1.1.0] - 2026-08-21
### Added
- Level crossing gate models and traction power substation load analysis in `docs/ARCHITECTURE.md`.
- Explainable AI (XAI) with SHAP feature contribution waterfalls in `docs/AI_CONTROLLER.md` and `docs/DASHBOARD_GUIDE.md`.
- Infrastructure fault injection test suite in `docs/TESTING.md`.
- AR Cab Signalling conceptual roadmap in `docs/ROADMAP.md`.
\n
### Documentation (2026-08-22)
- Documented CENELEC SIL-4 fail-safe interlocking principles in `docs/ARCHITECTURE.md`.
- Added wayside Hot Axle Box Detection mechanics in `docs/SIMULATION_ENGINE.md`.
\n