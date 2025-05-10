Interfaces
==========

x4_interface
------------

Handles communication with the physical drone:

- MAVLink protocol implementation
- Telemetry data processing
- Command conversion
- Safety monitoring
- Parameter management
- User interface

User Interface
--------------

A graphical keyboard-based teleoperation interface is included to interact with the drone using the defined actions. It is built with `tkinter` and integrated with ROS 2.

Features:

- **Velocity Control Slider:** Set desired drone velocity in the range `[0.0, 10.0]`.
- **Keyboard Command Input:** Press keys like `W`, `A`, `S`, `D`, `Q`, and `E` to send directional or rotational commands.
- **ROS 2 Publishing:**
  - Publishes command strings to `/drone/keyboardcommands`
  - Publishes velocity values to `/drone/keyboardvelocity`
- **ArduPilot MAVProxy Control Buttons:**
  - **Start MAVProxy**: Runs `mavproxy.py --master=/dev/ttyUSB0 --baudrate 57600`
  - **Mode GUIDED**:
::contentReference[oaicite:1]{index=1}
 
