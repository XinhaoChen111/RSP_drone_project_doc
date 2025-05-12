Simulation Guide
================

This section walks through launching the simulation with Gazebo and ArduPilot SITL.

Build the ROS2 Packages
-----------------------

Use `colcon` to build the core packages:

.. code-block:: bash

   colcon build --packages-select x4_description x4_bringup x4_interfaces x4_gazebo x4_bringup

Launch Simulation
-----------------

Start Gazebo with SITL and ROS2 bridges:

.. code-block:: bash

   ros2 launch x4_bringup x4_startup.launch.py

This starts:
- Gazebo Fortress
- ArduPilot SITL
- MAVProxy terminal
- MAVROS

Send MAVProxy commands in the console:

.. code-block:: bash

   mode guided
   arm throttle
   takeoff 5

Send MAVROS ROS2 commands in a new terminal

.. code-block:: bash

   Arm throttle: ros2 service call /mavros/cmd/arming mavros_msgs/srv/CommandBool "{value: true}"
   Set Mode: ros2 service call /mavros/set_mode mavros_msgs/srv/SetMode "{base_mode: 0, custom_mode: 'GUIDED'}"
   Takeoff: ros2 service call /mavros/cmd/takeoff mavros_msgs/srv/CommandTOL "{min_pitch: 0.0, yaw: 0.0, latitude: 0.0, longitude: 0.0, altitude: 3.0}"
   Land: ros2 service call /mavros/cmd/land mavros_msgs/srv/CommandTOL "{min_pitch: 0.0, yaw: 0.0, latitude: 0.0, longitude: 0.0, altitude: 0.0}"

