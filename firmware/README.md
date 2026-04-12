# Firmware and Tuning Architecture

This folder documents the current firmware and software architecture available for `E-01 Drive`.

## Current State

The local workspace used for this GitHub update did not contain the actual embedded firmware source files. Because of that, this repository currently documents the software architecture and tuning workflow, but it does not yet include the controller implementation source code itself.

## Embedded Firmware Role

The intended embedded firmware runs on the ESP32-S3 board and is responsible for:

- reading sensor data from the MPU-6050,
- executing the real-time control loop,
- sending motor commands to the driver stage,
- and displaying status or tuning information on the OLED.

## PID Tuning Goal

The software stack is designed to automatically determine effective PID gains (`Kp`, `Ki`, `Kd`) for the real robot while reducing manual trial-and-error.

The tuning strategy is divided into two phases:

1. `Offline tuning`
   An initial guided tuning session that evaluates response behavior and proposes a baseline set of gains.
2. `Online tuning`
   A follow-up adaptive phase that updates gains when the live system experiences new disturbances or changing conditions.

## Target System

Primary use case: `Self-balancing robot (inverted pendulum style platform)`

Typical variables:

- setpoint: zero tilt,
- state: tilt angle, angular velocity, wheel motion,
- output: motor torque or PWM command.

## Ideal Tuning Flow

1. Run an exploratory hardware test.
2. Measure settling time, overshoot, steady-state error, and stability.
3. Use those results to identify a matching dynamic profile.
4. Propose candidate PID gains.
5. Deploy those gains on hardware.
6. Feed the measured result back into the tuning workflow.

## Approach Evolution

### Initial TD3 Reinforcement Learning Direction

An earlier approach attempted automatic PID tuning with TD3 reinforcement learning across simulated systems. This approach was abandoned because the performance was not reliable enough for practical deployment on the real robot.

### Current Cloud LLM Direction

The current design uses a cloud-hosted LLM as the tuning engine.

In this architecture:

- a FastAPI service manages the tuning session,
- the model receives measured hardware response metrics,
- the model suggests improved PID gains,
- and the history of tested gains and outcomes is stored across iterations.

## Service Endpoints

| Endpoint | Purpose |
| --- | --- |
| `/init_session` | Start a tuning session with a system description |
| `/answer_questions` | Reply to clarifying questions from the tuner |
| `/send_results` | Send trial results and receive the next PID values |
| `/accept` | Accept the current gains as the offline baseline |
| `/start_adaptive` | Begin the online adaptive phase |
| `/breach` | Report a disturbance and request updated gains |

## What Still Needs To Be Added

To complete the source code deliverable for evaluation, the repository should still receive:

- ESP32 firmware source files,
- build instructions,
- dependency details,
- hardware pin mapping,
- calibration steps,
- and the exact protocol between the robot and the tuning backend.
