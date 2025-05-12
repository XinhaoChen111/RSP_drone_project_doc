Package Details
===============

x4_description
--------------

Contains the complete robot description model including:

- URDF/xacro files defining the robot's physical structure
- Mesh files for visualization
- Physical properties (mass, inertia matrices)
- Sensor configurations

x4_gazebo
---------

Responsible for simulation capabilities:

- Ignition Gazebo world files
- Simulation-specific launch files
- Plugin configurations
- Testing scenarios

x4_control
----------

Implements control algorithms for:

- Takeoff sequence
- Stable hover
- Landing sequence
- (Stretch) Waypoint navigation

x4_bringup
----------

Contains launch files to start the system:

- Simulation startup
- Hardware connection
- Configuration management

x4_interface
------------

Handles communication with the physical drone:

- MAVLink protocol implementation
- Telemetry data processing
- Command conversion
- Safety monitoring
- Parameter management
- User interface


x4_service_scripts
------------

Demo scripts for completing high-level actions:
- Takeoff
- Landing
- Waypointing
- Loiter

x4_vision
------------

Vision implementation for X4 drone using Sony RX0 II:
- Stream video from a USB UVC-compatible camera 
- Apply camera intrinsics from calibration
- Detect ArUco tags
- Estimate 3D pose of markers
- Publish detections for precision landing


x4_moveit
------------

High-level Moveit package for flight:
