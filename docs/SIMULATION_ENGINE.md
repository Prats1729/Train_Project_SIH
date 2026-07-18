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