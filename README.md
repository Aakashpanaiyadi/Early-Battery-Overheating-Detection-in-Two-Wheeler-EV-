

# Early Battery Overheating Detection in Two-Wheeler EV 

##  Project Introduction
This project is an early-warning diagnostic system designed to detect battery overheating in electric two-wheelers before it happens. While traditional systems only react after a battery gets hot, this solution runs a live electric scooter simulation on an ESP32 to predict thermal stress. By monitoring riding patterns (like aggressive acceleration) and estimating rider weight in real time, it catches rapid temperature rises early and sends live alerts to a dashboard before any battery damage occurs

---

## System Components (Hardware & Software)

### Hardware Layer

The project utilizes an embedded hardware setup to simulate and process vehicle diagnostics in real time:

* **ESP32 MCU**: Acts as the main simulation and diagnostic core.


* **Potentiometer 1**: Simulates the rider's throttle input from 0% to 100% (connected to GPIO 34).


* **Potentiometer 2**: Simulates the total rider payload/load ranging from 40 kg to 150 kg (connected to GPIO 35).


* **Potentiometer 3**: Simulates changing ambient temperatures from 30°C to 50°C (connected to GPIO 32).


* **USB Serial Interface**: Streams telemetry data to a computer at a 115200 baud rate.



### Software Layer

The system runs multi-layered software operations divided between the micro-controller firmware and a desktop application:

* **Simulation Core (`sim_step`)**: Runs an internal physics simulation modeling vehicle dynamics, battery performance, and heat generation.


* **Feature Extraction Engine**: Groups real-time data into 60-second windows to evaluate 14 statistical metrics regarding throttle, speed, and current stability.


* **Pattern Diagnosis Code (`diagnose_window`)**: A rule-based scoring engine that categorizes behavior into Aggressive Acceleration (AA) or Sustained High Speed (SHS).


* **Payload Estimator**: Evaluates steady-state driving parameters to calculate rider weight and detect vehicle overloading.


* **Live Dashboard UI**: A Python-based Tkinter desktop application that visualizes speed, state of charge (SoC), battery temperature, behavioral confidence trends, and predictive thermal warning banners.

## System Workflow

The project operates through a structured pipeline that repeats continuously during operation:

1. **Hardware Input Reading**: The ESP32 continuously reads the manual knobs (potentiometers) simulating throttle behavior, rider weight, and outside temperature.

2. **Drivetrain Simulation**: The inputs feed into the live powertrain model, computing how fast the scooter moves and how much heat the battery produces under that specific demand.

3. **Parallel Diagnostics processing**:
* **Behavior Analysis**: The system monitors the driver over 1-minute windows, scoring features to check if the rider is heavily accelerating or speeding continuously.

* **Weight Analysis**: Over 5-minute intervals, the system looks for stable, steady cruising periods to isolate and calculate the actual weight of the rider.

4. **Combined Reporting & Alerting**: Every 5 minutes, a master diagnosis report is generated. If the combined behavior shows aggressive tendencies paired with an elevated temperature rise rate, the software triggers immediate visual alerts (Advisories or Warnings) on the instrument cluster dashboard before battery cells degrade.


# OUTPUT


<img width="1150" height="532" alt="image" src="https://github.com/user-attachments/assets/d29067c8-a40f-4e4e-80cc-6934f062e9f6" />

