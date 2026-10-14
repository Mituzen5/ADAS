# ADAS
ADAS: Advanced Driver Assistance System

Zone-Based Automatic Vehicle Speed Controller with Vehicle-to-Vehicle Communication

Project Category: Automotive Safety, Embedded Systems, Intelligent Transportation
Project Type: Hardware Prototype and Future ADAS Framework
Primary Focus: Overspeed prevention in sensitive zones and reduction of road-safety risks
Platform: Arduino-based embedded system
Communication: 433 MHz RF for zone signaling; ESP32/Wi-Fi concepts for future V2V communication

---

1. Abstract

Road accidents remain a major public-safety concern, with overspeeding, human error, delayed reactions, and inadequate awareness of road conditions contributing to dangerous situations. Conventional road-safety measures, including traffic signs and speed-limit boards, depend heavily on drivers noticing and following instructions.

Our project proposes an Advanced Driver Assistance System (ADAS) focused on a zone-based automatic vehicle speed controller. The system identifies predefined road zones, such as school zones, hospital zones, college areas, and traffic-sensitive locations, and sends a wireless signal to a vehicle-mounted receiver.

The receiver uses an HT12D decoder to interpret signals transmitted through an RF communication system. An Arduino processes the received zone information, controls a motor driver connected to a demonstration motor, and displays relevant information on an I2C LCD.

The objective is to demonstrate how vehicles could automatically respond to designated speed restrictions instead of depending entirely on driver compliance. Additional planned capabilities include rain-condition warnings, manual override, continuous speed monitoring, and vehicle-to-vehicle (V2V) communication.

The project represents a prototype of a broader intelligent vehicle-safety system. Real-world deployment would require calibrated speed measurement, automotive-grade hardware, secure communication, safety validation, and integration with a vehicle's control systems.

Keywords: ADAS, automatic speed control, Arduino, HT12E, HT12D, RF communication, road safety, V2V communication, embedded systems.

---

2. Introduction

Road transportation is essential for everyday life, but it also involves risks caused by human behavior, vehicle limitations, and changing road conditions.

Drivers may exceed speed limits in sensitive areas, overlook warning signs, fail to anticipate hazards, or react too late to unexpected situations. These risks are particularly important near schools, hospitals, colleges, construction areas, and congested roads.

Traditional speed-limit systems communicate restrictions through signs and signals. Although these measures are important, they generally require the driver to recognize the warning and take appropriate action.

Our project introduces an electronic approach to this problem. Instead of relying only on visual signs, a designated road zone transmits information wirelessly to a vehicle-side system. The vehicle's controller interprets the received information and adjusts the demonstration motor's permitted operation according to the configured zone.

The project also establishes a foundation for future features that could improve communication between vehicles and increase awareness of environmental hazards.

2.1 What is ADAS?

Advanced Driver Assistance Systems are technologies designed to support safer driving by helping drivers detect hazards, understand road conditions, and respond to potentially dangerous situations.

Examples of ADAS functions in modern vehicles include:

- Forward collision warnings.
- Lane-departure warnings.
- Blind-spot monitoring.
- Adaptive cruise control.
- Automatic emergency braking.
- Driver attention monitoring.

Our project focuses primarily on zone-based speed restriction, with V2V communication and environmental warnings considered as extensions to the wider system.

2.2 Project Vision

To develop a modular, affordable educational prototype demonstrating how wireless zone information and embedded control can support intelligent vehicle-speed management and road-safety awareness.

---

3. Problem Statement

Conventional road-speed management has several limitations:

1. Dependence on driver compliance: A driver may ignore or fail to notice a speed-limit sign.
2. Overspeeding in sensitive areas: Excessive speed near schools, hospitals, and crowded intersections can increase accident risk.
3. Delayed response: Drivers may not reduce speed sufficiently before entering a restricted area.
4. Limited vehicle-to-vehicle awareness: Vehicles may not automatically share useful information about breakdowns, diversions, or nearby hazards.
5. Changing environmental conditions: Rain and reduced visibility can require additional caution.
6. Fragmented safety functions: Speed management, hazard alerts, and vehicle communication may operate as separate functions rather than as parts of a coordinated system.

Core problem

How can a vehicle receive information about a predefined road zone and automatically limit its permitted operation according to the applicable speed restriction, while also providing a foundation for additional road-safety features?

---

4. Objectives

The primary objectives of the project are:

- To design a wireless, zone-based speed-control prototype.
- To demonstrate communication between a zone transmitter and a vehicle receiver.
- To decode received zone information using the HT12D.
- To process the received information through an Arduino.
- To control a demonstration motor through a motor driver.
- To display system or zone information on an I2C LCD.
- To demonstrate how predefined restrictions can prevent unrestricted motor operation.
- To explore vehicle-to-vehicle communication for hazard and road-condition alerts.
- To investigate environmental warnings, including rain detection.
- To develop a modular platform that can be expanded with additional sensors and controllers.

4.1 Success criteria

The prototype should demonstrate that:

- A valid zone signal can be received and interpreted.
- The controller selects the corresponding configured restriction.
- The motor output responds to the selected restriction.
- The LCD communicates the relevant system state.
- Invalid, missing, or inconsistent signals can be identified as conditions requiring safe handling.

Actual vehicle speed measurement in km/h is a separate requirement and must not be inferred solely from motor output.

---

5. Proposed Solution

The proposed system consists of two main parts: a zone-side transmitter and a vehicle-side controller.

5.1 Zone-side transmitter

The transmitter represents a predefined road zone. It sends an encoded wireless signal identifying the configured zone or restriction.

For example, a school-zone demonstration may use a configured limit of 20 km/h as a conceptual reference. The exact value is illustrative and should be set according to the relevant road rules in a real implementation.

5.2 Vehicle-side receiver

The vehicle-side prototype receives the RF transmission through a compatible receiver and HT12D decoder. The Arduino processes the decoded output and applies the corresponding control logic.

The Arduino then commands a motor driver connected to the demonstration motor. The LCD provides information about the controller's current state.

5.3 System-level operation

1. The zone transmitter sends its configured signal.
2. The RF receiver captures the transmission.
3. The HT12D decodes the transmitted information.
4. The Arduino reads the decoded outputs.
5. The firmware determines the applicable restriction.
6. The controller commands the motor driver according to its programmed rules.
7. The LCD displays the relevant system state.
8. When a different valid zone signal is received, the controller updates its response according to the implemented logic.

The system demonstrates the principle of automated restriction. It does not, by itself, establish a certified road-vehicle speed limiter.

---

6. System Architecture

6.1 Block diagram

       PREDEFINED ROAD ZONE
                 |
                 v
          Zone Transmitter
              HT12E
                 |
                 v
          433 MHz RF Link
                 |
                 v
          RF Receiver Module
                 |
                 v
           HT12D Decoder
                 |
                 v
             Arduino
           /         \
          v           v
    Motor Driver    I2C LCD
          |
          v
    Demonstration
         Motor

  Future extensions:
  Rain Sensor | Speed Sensor | ESP32/V2V
  Ultrasonic Sensor | Driver Monitoring

6.2 Main functional modules

Module| Responsibility
Zone transmitter| Sends configured zone information
RF communication link| Transfers information wirelessly
HT12E encoder| Encodes the transmitter-side digital inputs
HT12D decoder| Decodes compatible received data
Arduino| Executes the control logic
Motor driver| Controls the demonstration motor
I2C LCD| Displays system information
Optional sensors| Supply environmental or vehicle-state information
Future ESP32 communication module| Supports development of V2V messaging

The exact modules and connections depend on the final hardware assembly.

---

7. Hardware Components

7.1 Arduino microcontroller

The Arduino acts as the central controller. It reads the decoded zone signals, evaluates the programmed restrictions, controls the motor driver, and updates the display.

Its main responsibilities are:

- Reading digital input states.
- Selecting the corresponding zone configuration.
- Applying control rules.
- Sending commands to output devices.
- Reporting relevant system states.

7.2 HT12E encoder

The HT12E is an encoder IC used to encode digital input information for compatible RF transmission arrangements.

In this project, it represents the transmitter-side encoding stage for communicating predefined zone information.

7.3 HT12D decoder

The HT12D is a decoder IC designed to recover encoded digital information from a compatible transmitter and receiver arrangement.

The Arduino uses the decoder's output pins as inputs to determine which zone information has been received.

The HT12D is not itself a radio transmitter or receiver; it operates alongside the RF modules.

7.4 RF transmitter and receiver

The prototype uses a nominal 433 MHz RF communication arrangement to transmit zone information wirelessly.

The actual communication range and reliability depend on the modules, antennas, interference, supply voltage, surroundings, and installation.

The prototype must not assume that a received signal proves the vehicle is physically inside a specific road zone. A practical system needs zone-entry detection, distance estimation, or another suitable localization mechanism.

7.5 Motor driver

The motor driver interfaces the Arduino's low-power control signals with the demonstration motor.

It allows the firmware to command motor operation according to the selected restriction.

The motor driver's exact model, current capacity, and wiring should be documented from the components actually used.

7.6 DC demonstration motor

The motor represents a simplified vehicle propulsion system. Its operation changes in response to the controller's commands.

Important: The rotational behavior of a small DC motor is not equivalent to a vehicle traveling at a measured road speed. Actual km/h control requires suitable speed sensing, calibration, and a validated control strategy.

7.7 I2C LCD

The I2C LCD provides a simple interface for communicating system status.

Possible display information includes:

- Active zone or zone code.
- Configured restriction.
- Received-signal status.
- Motor-control status.
- Sensor warning status, when implemented.

The exact messages depend on the final firmware.

7.8 Power supply and wiring

The Arduino, RF modules, decoder, LCD, and motor driver must receive power within their specified operating limits.

The motor supply must be suitable for the motor driver and motor. Grounds and signal connections must follow the actual circuit design, and motor-current paths should be kept separate from sensitive signal paths where appropriate.

The final repository should include a verified circuit diagram and a pin-mapping table matching the assembled prototype.

---

8. Software and Development Environment

The prototype is based on embedded programming with Arduino-compatible firmware.

Software components

- Arduino IDE for editing, compiling, and uploading firmware.
- Arduino programming language, based on C/C++.
- "Wire.h" for I2C communication.
- "LiquidCrystal_I2C.h" for the I2C LCD, where supported by the installed library.
- Firmware logic for interpreting zone inputs and controlling outputs.

Software responsibilities

The firmware performs the following operations:

1. Initializes the input and output pins.
2. Initializes the LCD.
3. Reads the decoded zone inputs.
4. Determines the active zone or control state.
5. Applies the configured restriction.
6. Sends the appropriate motor-driver commands.
7. Updates the LCD.
8. Handles changes in received signals according to the implemented logic.

The exact firmware version, library version, board selection, and upload settings should be recorded in the repository to support reproducibility.

---

9. Zone-Based Speed-Control Logic

The central feature is the ability to associate a received zone signal with a predefined control rule.

9.1 Example zone configuration

Zone| Example configured limit| Intended purpose
School zone| 20 km/h| Encourage lower speeds near schools
Hospital zone| 20 km/h| Support cautious movement in sensitive areas
College zone| Configurable| Apply a locally appropriate restriction
Traffic-sensitive zone| Configurable| Reduce permitted speed where appropriate
Normal zone| Configurable| Apply the ordinary configured operating policy

These values are examples for demonstrating the concept, not a claim that one speed limit applies to every location. Actual limits must follow local regulations and road-specific requirements.

9.2 Control principle

The intended control principle is that the controller should not permit operation above the configured restriction when a valid restricted-zone state is active.

Conceptually:

Read zone information
        |
        v
Validate the received state
        |
        v
Select the applicable restriction
        |
        v
Determine the permitted motor command
        |
        v
Apply the motor-driver command
        |
        v
Update the LCD

A production implementation would compare a measured vehicle speed with the applicable limit and regulate propulsion accordingly.

The current demonstration motor can show a change in commanded operation, but it cannot establish a real road-speed limit unless speed feedback and calibration have been implemented.

9.3 Safety considerations

The controller should account for:

- No valid zone signal.
- Unexpected combinations of decoder outputs.
- Conflicting or rapidly changing zone information.
- RF interference or communication loss.
- Power interruption or microcontroller reset.
- Failure of a sensor or actuator.

A safe response must be explicitly designed and tested. The prototype should not claim that it always defaults to a safe speed unless that behavior is implemented and verified.

---

10. RF Communication: Working Principle

The RF link transfers digital information between the zone transmitter and vehicle-side receiver.

Transmission sequence

1. The transmitter-side input configuration represents a zone code.
2. The HT12E encodes the relevant digital inputs.
3. The RF transmitter broadcasts the encoded signal.
4. The RF receiver detects the transmission.
5. The HT12D decodes the received information.
6. The Arduino reads the resulting digital outputs.
7. The controller applies the configured zone logic.

Advantages

- Wireless communication without a physical connection to the vehicle.
- Relatively simple educational implementation.
- Low-complexity hardware architecture.
- Demonstration of the relationship between communication and embedded control.

Limitations

- Range may be limited or inconsistent.
- Interference can affect reception.
- Basic RF signaling does not automatically authenticate the transmitter.
- A decoded signal does not establish the vehicle's exact position.
- The signal does not inherently measure the vehicle's speed.
- Communication loss and invalid messages require deliberate handling.

A real deployment would require a more robust communication design, message validation, appropriate cybersecurity, and a reliable method of determining zone boundaries.

---

11. Vehicle-to-Vehicle Communication (V2V)

Vehicle-to-vehicle communication is a planned extension of the broader ADAS concept.

V2V allows vehicles to exchange information that may help drivers or vehicle controllers respond to road conditions and potential hazards.

11.1 Proposed use cases

Emergency or breakdown alerts: A vehicle experiencing a breakdown could communicate a warning to nearby vehicles.

Road construction and diversions: Vehicles could exchange information about construction areas or route changes.

Turn-intention notifications: A vehicle could communicate an intended turn or maneuver to improve awareness.

Hazard notifications: A vehicle could report a detected road hazard to other vehicles in the vicinity.

Assistance requests: A vehicle could transmit a request for help following a breakdown or other incident.

11.2 Proposed communication approach

An ESP32 and Wi-Fi-based arrangement may be explored for an educational V2V demonstration. The software would define message formats, sender identification, event types, timestamps, and receiving behavior.

A conceptual message could contain:

Message type: ROAD_HAZARD
Sender ID: VEHICLE_01
Event: ROAD_CONSTRUCTION
Location: Example coordinates
Timestamp: Example timestamp
Status: ACTIVE

The values above are illustrative, not messages verified from the current prototype.

11.3 Important distinction

The 433 MHz zone-signaling link and the proposed ESP32/Wi-Fi V2V link are separate communication functions. They should not be described as a single implemented communication system unless they have actually been integrated and tested.

V2V functionality remains a planned extension unless a working implementation is included in the final build.

---

12. Environmental Awareness: Rain Detection

Rain detection is another proposed extension to the ADAS system.

Wet roads can reduce available tire grip and increase stopping distances. Rain can also reduce visibility, depending on its intensity and the surrounding conditions.

A rain sensor could provide an environmental warning to the controller.

Proposed operation

1. A rain sensor detects a change associated with wet conditions.
2. The controller reads the sensor output.
3. The system identifies the condition according to a configured threshold.
4. A warning or cautious-driving indication is displayed.
5. The system may communicate the warning through an appropriate alert interface.

A rain sensor alone cannot accurately determine a safe vehicle speed. A real implementation would need additional information about vehicle speed, road conditions, visibility, tires, and other relevant factors.

The rain sensor should therefore be documented as a warning or experimental input unless automatic speed-control behavior has actually been implemented and validated.

---

13. Other Potential ADAS Extensions

The system can be expanded through additional modules, subject to hardware availability and integration testing.

13.1 Continuous speed monitoring

A suitable wheel-speed sensor or other validated speed-measurement method could provide feedback to the controller.

This would enable the system to compare measured speed against the configured limit.

13.2 Ultrasonic obstacle detection

An ultrasonic sensor, p
