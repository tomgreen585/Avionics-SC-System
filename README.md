# SWEN326 - Group Project

## Project Outline

Tasked with developing a new Avionics Flight Management and Control System. The software will be responsible for maintaining flight plans and making corrections to the aircraft's control systems and control surfaces, as well as monitoring systems and providing a UI to the pilots.

## Pilot User Interface Specifications

1. Flight Plan Management:
- Input field for entering waypoints (latitude, longitude, altitude).
- Input fields for speed restrictions and expected times of arrival at each waypoint.
- A submit button to load and activate the flight plan.
- Visual display (map) showing current position, planned route, and waypoints

1. Autopilot Control Panel:
- Buttons to engage/disengage autopilot.
- Controls for manual override: altitude adjustment, speed, heading.
- Indicator lights for autopilot status (engaged, disengaged, fault condition).

1. Sensor Data Display:
- Digital readouts for airspeed, altitude, pitch, roll, yaw, and engine parameters.
- Visual indicators for data update frequency (e.g., colour change or blinking to indicate fresh data).

1. Hazard Alerts:
- Dedicated section of the interface for hazard warnings and mitigation actions.
- Audible and visual alerts for immediate hazards.
- A checklist or action plan for emergency procedures.

## Sensor Data Simulation and Frequency
1. Airspeed Sensor: Simulate data to represent the aircraft's speed relative to the surrounding air. Data format: knots (nautical miles per hour). Update frequency: every second.

1. Altitude Sensor: Simulate barometric and GPS altitude data. Data format: feet above mean sea level (AMSL). Update frequency: every 500 milliseconds.

1. Attitude Sensor: (AKA: Artificial Horizon Indicator) Simulate aircraft's orientation data, including pitch (nose up/down), roll (wing up/down), and yaw (nose left/right). Data format: degrees from the horizon for pitch and roll, magnetic heading for yaw. Update frequency: every 500 milliseconds.

1. Engine Parameters:  Simulate engine thrust and fuel flow. Data format: thrust in pounds-force (lbf). Update frequency: every second. Note: we could also consider issues such as temperature or fuel flow, but we will ignore these for this project due to time issues.

## Control Signal Specifications

1. Autopilot Control Frequency: The system should send control signals to the aircraft’s control surfaces (elevators, ailerons, rudders) and engine control systems at least every 500 milliseconds.

1. Execution Check Parameters: After sending a control signal, the system must verify the execution by reading back the relevant sensor data within 200 milliseconds. Success Criteria: A control signal is considered successfully executed if the sensor data reflects the expected change within a margin of error of ±2% for the control surfaces and ±5% for engine parameters, within 1 second of command issuance. Failure Handling: If the execution check fails, the system must attempt to resend the command up to three times before alerting the pilot to the issue via the user interface.

## Sensor Data Simulation and Value Ranges

1. Airspeed Sensor: Simulate data to represent the aircraft’s speed between 50 to 500 knots. Define operational thresholds and conditions under which values exceed normal operational limits.

1. Altitude Sensor: Simulate barometric and GPS altitude data from -1,000 to 50,000 feet AMSL, with thresholds for rapid changes indicating potential sensor faults.

1. Attitude Sensor: Simulate orientation data within typical operational ranges: Pitch: -30 degrees to 30 degrees, Roll: -60 degrees to 60 degrees, Yaw: -180 degrees to 180 degrees. Identify and manage exceedances through system alerts and corrective actions.

## Hazard Mitigation Strategies

Implement fault detection, fault tolerance, and fail-safe mechanisms to handle abnormal sensor values, ensuring the system can safely manage potential hazards without catastrophic failures.

## Engine Thrust and Flight Dynamics

Engine thrust is the force generated by the aircraft’s engines to propel it forward. This force is critical for achieving and maintaining the aircraft’s velocity during various phases of flight. Thrust is produced by accelerating a mass of air or gas to the rear, propelling the aircraft in the opposite direction according to Newton’s third law of motion.

## Interconnection with Flight Dynamics

1. Speed Control: Thrust is directly proportional to the aircraft’s airspeed. An increase in thrust results in an increase in speed, whereas a decrease in thrust lowers the speed, assuming other factors such as air density and drag do not change. Simulation of airspeed should dynamically respond to changes in thrust, especially in scenarios involving speed adjustments to meet flight plan targets or respond to air traffic control.

1. Altitude Adjustment: Thrust adjustments are necessary for changing altitude. To climb, an aircraft typically increases its thrust; to descend, it reduces thrust. The interplay between speed and pitch (influenced by thrust) is crucial for maintaining or changing altitude, which must be accurately modeled in simulations.

1. Attitude Management: Changes in thrust can alter the aircraft’s pitch—increased thrust can cause the nose to rise (pitch up) and decreased thrust can cause it to lower (pitch down). While roll and yaw are primarily controlled by other surfaces (ailerons and rudders), asymmetric thrust (such as in an engine failure scenario) can significantly impact these attitudes, necessitating simulation scenarios that involve thrust differentials.