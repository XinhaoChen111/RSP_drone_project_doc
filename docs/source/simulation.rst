Simulation Guide
================

This section walks through launching the simulation with Gazebo and ArduPilot SITL.

Build the ROS2 Packages
-----------------------

Use `colcon` to build the core packages:

.. code-block:: bash

   colcon build --packages-select x4_description x4_bringup x4_interfaces x4_gazebo

Launch Simulation
-----------------

Start Gazebo with SITL and ROS2 bridges:

.. code-block:: bash

   ros2 launch x4_bringup x4_startup.launch.py

This starts:
- Gazebo Fortress
- ArduPilot SITL
- Micro XRCE DDS Bridge
- MAVProxy terminal (optional)

Send MAVProxy commands in the console:

.. code-block:: bash

   mode guided
   arm throttle
   takeoff 5
