# Clock Alarm Application (UML HSM Project)

## Overview
This project implements a clock alarm application using a hierarchical state machine (HSM), modeled with the QM modeling tool and programmed in C++ for an Arduino board. The primary objective is to design a reliable and responsive timekeeping system that provides real-time clock functionality with customizable alarm settings. Leveraging the advantages of hierarchical state machines, the project efficiently manages different modes (clock setting, alarm setting) and transitions between them, ensuring error handling and user convenience.

The application’s design follows key principles of state-based programming, providing structured, event-driven logic that simplifies complex behaviors. This design choice enhances maintainability and scalability, making it a practical example of modern embedded systems design.

## Features
- **Clock Display**: Real-time clock display with adjustable 12-hour/24-hour formats.  
- **Alarm Functionality**: Set and activate/deactivate an alarm.  
- **Error Handling**: Aborts incorrect entries and returns to previous settings.  
- **Snapshot Feature**: Retains current time while modifying settings.  

## Hardware Components
- Arduino board  
- LCD display  
- Two buttons  
- Optional buzzer  
- Potentiometer (for contrast adjustment)  

### Buttons
- **SET/CLOCK_SET**: Enters clock set mode.  
- **OK/ALARM_SET**: Confirms selections and sets the alarm.  

## Application States and Transitions

### States
- **Ticking State (Initial)**: Displays the current time.  
- **Clock Setting State**: Modify time settings.  
- **Alarm Setting State**: Set and manage the alarm.  

### Events and Transitions
- **From Ticking**:  
  - **Press SET**: Transition to Clock Setting.  
  - **Press OK**: Transition to Alarm Setting.  
- **In Clock Setting or Alarm Setting**:  
  - **Abort (both buttons)**: Return to Ticking without saving.  
  - **Save (OK)**: Return to Ticking with saved settings.  
- **Alarm Notification**:  
  - Triggered by **ALARM** event.  
  - **OK** dismisses the alarm and returns to the previous state (history state).  

## Implementation Structure

### Main Attributes
- `current_time`: Tracks real-time clock value.  
- `temp_time`: Temporary time for setting mode.  
- `alarm_time`: User-set alarm time.  
- `alarm_status`: Alarm ON/OFF.  
- `time_mode`: 12-hour/24-hour display preference.  

### Signals
- `SET`: Enter clock setting.  
- `OK`: Confirm settings or dismiss alarm.  
- `ABRT`: Abort operation.  
- `ALARM`: Alarm trigger.  
- `TICK`: Updates display periodically.  

## Building the Model in QM
1. **Folder Setup**: Create a folder `qm` for model files.  
2. **New Model**: Use QM to create a `ClockAlarm` project.  
3. **Package**: Add a package `HSMs` with stereotype components.  
4. **Class Definition**: Define `Clock_Alarm` class inheriting `QHsm`.  
5. **Attributes**: Add `current_time`, `temp_time`, and others as needed.  

### Directories and Files
- Add `ClockAlarm_SM.cpp` and `ClockAlarm_SM.h`.  
- Generate Code.  

### Drawing the State Machine
#### State Hierarchy
- `Clock` superstate containing:  
  - `Ticking`  
  - `Settings` superstate:  
    - `Clock_Setting`  
    - `Alarm_Setting`  
  - `Alarm Notification`  
    - Add `Alarm_Notify` state.  
    - Transition back to `Clock` history state on OK.  

### Using History States
- Define a deep history for the `Clock` state.  
- Save the state machine.  

## Visuals
- **QM Model Diagram**  
  ![SM_of_Clock_Alarm](https://github.com/user-attachments/assets/948e1807-5e0c-491d-a675-a0a62879e8a1)

- **Device Image**  
![IMG_4670](https://github.com/user-attachments/assets/8a110ea9-7f6b-43f6-9a63-bf869aa2d96f)


## Summary
This project demonstrates a robust hierarchical state machine implementation for a clock and alarm system. The application features real-time clock updates, error handling, and alarm notifications, making it a comprehensive example of state-driven design. The project ensures scalability, maintainability, and efficient resource utilization by using structured state transitions and modular code design. These attributes are particularly beneficial for embedded system developers aiming to build responsive, user-friendly interfaces.
