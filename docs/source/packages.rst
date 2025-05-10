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
