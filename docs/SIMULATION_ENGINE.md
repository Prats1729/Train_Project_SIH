# SimPy Discrete-Event Simulation Engine

## Overview
The simulation engine executes train movements through track sections, junctions, and station platforms using discrete-event simulation principles. Time advances instantaneously between events, allowing 24-hour railway schedules to be simulated in seconds.

## Environment Initialization (`simulation/env.py`)
The `run_simulation()` function orchestrates:
- SimPy `Environment` instance creation.
- Instantiation of Station resources representing physical platforms.
- Spawn schedules for train entities based on synthetic timetables.
- Real-time logging of arrival, dwell, dispatch, and departure events.
\n
### Train Agent Lifecycle
Each train entity models a realistic train service transitioning through discrete states:
1. **Scheduled**: Train is queued for generation based on timetable departure time.
2. **Approaching**: Train enters the inbound block signal territory.
3. **Platform Request**: Train signals the Station Controller requesting a platform berth.
4. **Dwelling**: Train occupies platform; passengers embark/disembark (configurable dwell time).
5. **Cleared Departure**: Outbound track block is acquired; train departs section.
\n
## Station Resource Modeling (`simulation/station.py`)
Stations are modeled as finite-capacity multi-server queues using `simpy.Resource`:
- **Platform Resources**: Each platform acts as a mutually exclusive server.
- **Queueing Discipline**: First-Come, First-Served (FCFS) for baseline; priority-weighted AI dynamic queue for AI mode.
- **Berthing Constraints**: Trains cannot occupy a platform longer than their designated dwell plus clearing margin.
\n
### Headway Safety Envelopes
To enforce railway safety regulations:
- Minimum Headway Distance: Trains must maintain a minimum time separation of $T_{headway}$ (typically 3 minutes) when traversing the same block section.
- Deceleration Profiles: Approaching trains encounter caution signals, throttling speed according to braking distance curves.
\n
## Stochastic Perturbation Modeling

Real railway delays exhibit heavy-tailed distributions rather than pure Gaussian noise. The simulator models arrival perturbations using Weibull and Log-Normal probability density functions:

$$f(x; \lambda, k) = \frac{k}{\lambda} \left(\frac{x}{\lambda}\right)^{k-1} e^{-(x/\lambda)^k}$$

Where shape parameter $k = 1.3$ models the skewness typical of railway operational delays (many small delays, infrequent severe delays).
\n
### Train Priority Classes & Overtaking Dynamics

Trains are classified into four operational priority tiers:
1. **Tier 1 (Vande Bharat / Rajdhani Express)**: Highest speed profile ($130\text{ km/h}$), absolute right-of-way.
2. **Tier 2 (Mail / Express)**: Standard passenger speed profile ($110\text{ km/h}$).
3. **Tier 3 (Passenger / EMU Shuttle)**: High stop frequency, lower priority.
4. **Tier 4 (Freight / Goods)**: Heavy axle load, lower acceleration ($75\text{ km/h}$ max speed), holds in loop sidings during overtakes.
\n
## Train Dynamics & Speed Profiling

Train movements incorporate physical acceleration, cruising, and braking regimes:
- **Tractive Acceleration**: Approximated by constant acceleration $a = 0.5\text{ m/s}^2$ up to cruising velocity $v_{max}$.
- **Service Braking**: Deceleration $d = -0.6\text{ m/s}^2$ approaching caution signals or platform stops.
- **Dwell Time Calculation**:
  $$t_{dwell} = t_{base\_dwell} + \Delta t_{passenger\_density}$$
\n