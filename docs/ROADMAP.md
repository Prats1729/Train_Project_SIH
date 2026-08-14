# Project Roadmap & Future Enhancements

## Phase 1: Prototype MVP (SIH 2024 Core) - Completed
- [x] Dual-track discrete-event simulation engine with SimPy.
- [x] Static rule-based Baseline Controller.
- [x] Scikit-learn Random Forest delay prediction.
- [x] Streamlit web interface with real-time progress indicators.
- [x] KPI metrics: punctuality, average delay, throughput.

## Phase 2: Enhanced Dispatcher & Resiliency (Current)
- [x] Platform allocation classifier with dynamic conflict masking.
- [x] Disaster Mode failure simulation (track section blockages).
- [x] Decision audit telemetry and Gantt chart visualization.
\n
## Phase 3: Deep Reinforcement Learning (DRL) Controller (Planned)
- [ ] Migrate dispatching policy from supervised learning to Deep Q-Networks (DQN) / Proximal Policy Optimization (PPO).
- [ ] Formulate Markov Decision Process (MDP) with reward function balancing punctuality, energy savings, and safety margins.
- [ ] Gym/Gymnasium environment wrapper around the SimPy simulation core.
- [ ] Benchmarking DRL policies against mixed-integer linear programming (MILP) solvers.
\n
## Phase 4: Multi-Station Network Topology
- [ ] Expand simulation from single section/station to multi-station divisional corridors.
- [ ] Model interlocking junctions, loop lines, and diamond crossings.
- [ ] Simulate bi-directional single line sections with dynamic passing loops.
- [ ] Automatic token block section signalling protocols.
\n
## Phase 5: Real-World Indian Railways Timetable Ingestion
- [ ] Ingest National Train Enquiry System (NTES) and GTFS transit feeds.
- [ ] Support realistic train compositions: Rajdhani, Shatabdi, Vande Bharat, goods trains.
- [ ] Calibrate delay distributions against historical zonal delay data.
- [ ] Support seasonal weather impact modeling (dense fog speed restrictions).
\n
## Phase 6: Wayside Edge Computing Deployment
- [ ] Containerize AI Controller into lightweight Docker containers (< 100MB).
- [ ] Optimize models with ONNX Runtime for deployment on NVIDIA Jetson / Raspberry Pi wayside edge nodes.
- [ ] Support MQTT / OPC-UA protocols for direct hardware PLC interfacing.
\n
## Telemetry Streaming via WebSockets (Phase 5 Extension)
- [ ] Implement an asynchronous WebSocket broadcaster in `simulation/env.py`.
- [ ] Broadcast real-time GeoJSON train coordinates to an interactive Leaflet/Mapbox front-end.
- [ ] Enable multiplayer dispatcher mode where human controllers compete against the AI agent.
\n
## 3D Digital Twin Visualization (Phase 6 Extension)
- [ ] Integrate Three.js / WebGL 3D rendering pipeline for the station yard.
- [ ] Animate procedural 3D train models along track curves according to SimPy event timestamps.
- [ ] Realistic camera presets: Signal Tower perspective, Driver Cab view, Drone Overview.
\n