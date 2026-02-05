# AI Handgun Detection Device

## Gun Safety in America: Motivation & Context
Gun violence remains a critical public safety issue in the United States, with particularly devastating impacts in school and educational environments. Firearms are now among the leading causes of death for children and adolescents in the U.S., surpassing many other unintentional and health-related causes. In recent years, the nation has experienced a troubling number of mass shooting events, including multiple high-profile school shootings that have resulted in loss of life, long-term trauma, and widespread community disruption.

Schools are uniquely vulnerable due to high population density, predictable schedules, and limited real-time threat awareness. While no single technology can fully prevent gun violence, early detection and rapid alerting systems can play a meaningful role in reducing response times and improving situational awareness for administrators, security personnel, and first responders.

This project is motivated by the need for proactive, automated threat detection—systems that operate continuously, do not rely on human vigilance alone, and can provide immediate alerts when a potential firearm threat is identified. The goal is not surveillance, but risk mitigation through early warning.

## Project Overview
This project implements an embedded handgun detection and alert system using computer vision, motion sensing, and cloud-based AI inference. The device continuously monitors an environment for motion, analyzes camera input only when activity is detected, and determines whether a handgun is present. When a threat is identified, the system escalates alerts through multiple channels, including on-device indicators, audible alarms, email notifications, and smartphone alerts.

The system is designed as a finite-state machine, ensuring predictable behavior, efficient use of resources, and clear transitions between operational modes such as idle monitoring, motion detection, analysis, alerting, and reset.

### System Behavior
#### Boot & Initialization
1. Upon power-up, the device initializes hardware peripherals and network connectivity.
2. The blue status LED flashes slowly during startup.
3. The LCD displays: "Turning On"
4. Once initialized, the PIR motion sensor continuously monitors for movement.
#### No Motion Detected
1. The first green LED remains ON.
2. LCD displays: Detecting Motion...
3. Camera and AI inference remain inactive to conserve resources.
#### Motion Detected
1. The first red LED turns ON.
2. LCD displays: Motion Detected.
3. The USB camera is activated.
4. A frame is captured and sent to a pretrained cloud-based AI model.
5. The AI Model returns how confident it is that a handgun is present
#### No Handgun Detected
1. The second green LED turns ON.
2. LCD displays: No Handgun Detected.
3. System returns to monitoring for motion
#### Handgun Detected
1. The second red LED turns ON.
2. The active buzzer is enabled.
3. LCD displays: Alert: Handgun Detected!.
4. A 30-second video recording begins.
5. A smartphone notification is sent via Pushover.
6. The recorded video is emailed to a predefined list of recipients.
7. The device remains in this state until the user pushes the reset button
#### Reset Button / Manual Override
A physical pushbutton acts as the reset button
By pressing it at any time, the following occurs
1. Cancels video recording and notifications if in progress.
2. Disables buzzer and alert LEDs.
3. LCD displays: Resetting.
4. System returns to monitoring for motion
#### Error Handling
If an error occurs at any time, the Blue LED rapidly flashes and the LCD Display will display the error message

### Security and Ethical Considerations
- No continuous recording occurs without motion detection
- Video is only recorded upon confirmed threat detection
- No biometric identification is performed
- System is intended for controlled environments and research use

### Intended Use and Future Improvements
#### This project demonstrates applied skills in:
- Embedded systems engineering
- Computer vision integration
- Cloud API communication
- State-machine-based software design
- Human-centered alert systems
#### Potential future enhancements include:
- Edge-based inference
- Multi-camera support
- Encrypted video transmission
- Admin dashboard integration

#### GPIO Pin Mapping
This project uses BCM GPIO numbering. Pin assignments are defined in `config.json`
and match the provided KiCad schematic exactly.

## Summary
This project showcases a full-stack embedded AI system that bridges hardware, software, and cloud intelligence to address a real-world safety challenge. It is intended as a technical demonstration, research platform, and portfolio artifact for employers and collaborators interested in embedded AI, security systems, and applied computer vision.

