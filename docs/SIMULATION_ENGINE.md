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
### Junction Routing & Switch Clearances
At station approaches, points and track switches require mechanical clearance envelopes:
- **Route Setting Time**: 15 seconds required for switch motorized throw and interlocking verification.
- **Switch Locking**: A set route remains locked until the rear bogie of the train clears the fouling point track circuit.
\n
### Passenger Exchange Dwell Modeling
Dwell times scale with station passenger footfall and train capacity:
$$t_{dwell} = t_{door\_open} + \max\left(\frac{N_{alighting}}{r_{alight}}, \frac{N_{boarding}}{r_{board}}\right) + t_{dispatch\_bell}$$

Where:
- $r_{alight} \approx 1.2\text{ passengers/door/sec}$.
- $r_{board} \approx 0.8\text{ passengers/door/sec}$.
\n
### Multi-Track Section Overtaking Protocol
When high-priority Express trains approach low-priority Freight trains:
1. Distance-to-confluence check: AI detects if trailing Express is within 15 km.
2. Signal loop entry: Preceding Freight is routed into siding loop line at kilometer marker 24.
3. Express through clearance: Main line aspect remains clear green.
4. Freight re-entry: Freight resumes journey once the Express clears the forward block.
\n
## Synthetic Timetable Generator

The generator creates realistic daily train patterns:
- **Morning Peak Window (07:00 - 10:30)**: High frequency suburban shuttles and intercity expresses (headway 4-6 mins).
- **Midday Lull (11:00 - 15:30)**: Lower passenger frequency, allocated freight slots.
- **Evening Peak Window (16:30 - 20:30)**: Secondary passenger rush hour.
- **Night Window (21:00 - 05:00)**: Long-distance mail/express and bulk freight haulage.
\n
## Four-Aspect Signalling Emulation

The simulator emulates modern Indian Railways four-aspect automatic color-light signalling:
1. **Green (Clear)**: Train proceeds at maximum authorized line speed ($v_{max}$).
2. **Double Yellow (Attention)**: Train prepares to reduce speed to pass the next signal at restricted speed.
3. **Yellow (Caution)**: Train decelerates to enter the platform or prepares to stop at the next red aspect.
4. **Red (Danger)**: Train must stop completely before the signal footprint.
\n
### Terminal Rake Turnaround Mechanics
At terminus platforms, rolling stock requires mandatory turnaround procedures:
- Locomotive decoupling or cab changeover ($15-20\text{ minutes}$).
- Safety inspection and air brake continuity test ($10\text{ minutes}$).
- Water refilling and cabin cleaning ($20-30\text{ minutes}$).
The simulator respects these minimum turnaround bounds before re-dispatching trains as outbound services.
\n
### Track Geometry & Gradient Resistance
Train tractive effort is influenced by ruling gradients and curvature:
$$F_{resistance} = F_{rolling} + F_{gradient} + F_{curve} + F_{aero}$$
- **Gradient Resistance**: $R_g = 9.81 \cdot M_{train} \cdot \sin(\theta)$.
- **Curvature Resistance**: Empirical formula $R_c = 0.0004 \cdot D \cdot M_{train}$.
These resistances are incorporated into section traversal time calculations.
\n