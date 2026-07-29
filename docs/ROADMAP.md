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