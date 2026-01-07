# AEE 479 - Aerospace Engineering (Aeronautics) Capstone

This repository contains the controls software for our capstone project in AEE 479 at Arizona State University. The system is part of an unmanned aircraft system (UAS) designed for a hypothetical U.S. Army surveillance, request for propsal, featuring a carrier aircraft deploying smaller payload aircraft. This code focuses on the payload aircraft's flight controller, enabling hover-to-forward flight transitions via tilt-rotors, attitude stabilization, and remote piloting.

## Key Mission

24-hour low-altitude (50 ft) data collection over 1020 nm range, with telemetry relay to the carrier.

## Features

IMU Integration: Uses MPU6050 for 6DOF attitude estimation via Madgwick filter.
PID Control: Stabilizes roll, pitch, and yaw in angle mode; tunable gains for hover stability.
Radio Input: PWM receiver handling for throttle, aileron, elevator, rudder, and tilt control.
Actuator Mixing: Custom mixer for left/right main motors, rear EDF, and tilt servos; supports transition fading.
Failsafe: Throttle cut and default values on signal loss.
Loop Rate: Regulated at 2000 Hz for consistent filtering.

## Hardware Requirements

Arduino Mega 2560 (or compatible).
MPU6050 IMU (I2C).
PWM receiver (e.g., Spektrum/Futaba).
Servos: 2x tilt (e.g., HS-645MG).
ESCs/Motors: 2x main brushless, 1x rear EDF (OneShot125 compatible).
Pins: Defined in code (e.g., ch1Pin=2 for throttle).

## Setup

Install Arduino IDE.
Add libraries: Wire, SPI, PWMServo, Servo, MPU6050 (from jrowberg/i2cdevlib).
Upload controller.ino to Arduino.
Calibrate IMU on flat surface (automatic on boot).
Tune PID gains (e.g., Kp_roll_angle=0.2) via serial monitor.

## Usage

Power on: LED blinks indicate startup/IMU calibration.
Arm via radio (channel 5 >1500 μs disables throttle cut).
Control: Throttle (ch1), Aileron (ch2), Elevator (ch3), Rudder (ch4), Tilt switch (ch6).
Monitor via serial (500000 baud): Uncomment print functions for debugging (e.g., printRollPitchYaw()).
Safety: Ensure failsafe values (e.g., channel_1_fs=1000) and test in open area.

## Reference

Full design document located at `documentation/reports/AEE-479-final-report.pdf`.

## Acknowledgments

This project was developed as part of the [AEE 479 - Design of Autonomous Aircraft Systems](https://catalog.apps.asu.edu/catalog/courses/courselist?campusOrOnlineSelection=A&catalogNbr=479&subject=AEE&term=2261) course, at [Arizona State University](https://engineering.asu.edu). Problem statements and materials are attributed to the course instructors.

**Collaborators**: Cole Parker, McKenna Samuelson, Dallas Perkins, Matthew Zamora, Jonathan Gonsalves, Evan Coronado, Abhigya Raval, and Max Donnelly

**Special thanks** to [Professor Fred Garrett](https://search.asu.edu/profile/1809552)
