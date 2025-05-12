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

- **Velocity Control Slider**
  - Set desired drone velocity in the range `[0.0, 10.0]`.
  - Affects both linear and angular velocities.
  
- **Keyboard Command Input**
  - Control the drone using the following keyboard keys:
    - `W`: Move forward
    - `A`: Move left
    - `S`: Move backward
    - `D`: Move right
    - `Q`: Rotate left (yaw)
    - `E`: Rotate right (yaw)
    - `C`: Stop movement
  - The latest key command is shown in the GUI.

- **ROS 2 Publishing**
  - Publishes `geometry_msgs/Twist` messages to:
    ```
    /mavros/setpoint_velocity/cmd_vel_unstamped
    ```

- **Flight Control Buttons**
  - `Arm`: Arms the drone (calls `/mavros/cmd/arming`)
  - `Disarm`: Disarms the drone
  - `Takeoff 15m`: Runs `ros2 run x4_service_scripts mavros_takeoff`
  - `Land`: Runs `ros2 run x4_service_scripts mavros_landing`
  - `Guided`: Switches mode to GUIDED via `/mavros/set_mode`
  - `Loiter`: Switches mode to LOITER via `/mavros/set_mode`

- **Demo**: Executes a demo flight plan

 
