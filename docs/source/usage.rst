Usage Guide
===========

This section provides instructions on how to use the simulation and control the drone.

Building the Repository
-----------------------

To compile the repository:

.. code-block:: bash

   colcon build --packages-select x4_description x4_bringup x4_interface x4_gazebo

Launching the Simulation
------------------------

To launch the Gazebo simulation with ArduPilot support:

.. code-block:: bash

   ros2 launch x4_bringup x4_startup.launch.py

This command starts Gazebo and ArduPilot with SITL and a Micro ROS bridge to ROS 2 commands. It also launches a MAVProxy terminal for communication.

Controlling the Drone
---------------------

**MAVROS Commands**

In a new terminal:

.. code-block:: bash
   Arm Throttle: ros2 service call /mavros/cmd/arming mavros_msgs/srv/CommandBool "{value: true}"
   
   Set Mode: ros2 service call /mavros/set_mode mavros_msgs/srv/SetMode "{base_mode: 0, custom_mode: 'GUIDED'}"
   
   Takeoff: ros2 service call /mavros/cmd/takeoff mavros_msgs/srv/CommandTOL "{min_pitch: 0.0, yaw: 0.0, latitude: 0.0, longitude: 0.0, altitude: 3.0}"
   
   Land: ```ros2 service call /mavros/cmd/land mavros_msgs/srv/CommandTOL "{min_pitch: 0.0, yaw: 0.0, latitude: 0.0, longitude: 0.0, altitude: 0.0}"``
   
   Local Waypoint (Relative to Home): ros2 topic pub /mavros/setpoint_position/local geometry_msgs/msg/PoseStamped "{header: {frame_id: 'map'}, pose: {position: {x: 5.0, y: 5.0, z: 3.0}, orientation: {w: 1.0}}}"

These are just some examples but full documentation can be found here.


**MAVProxy Commands:**

In the MAVProxy terminal:

.. code-block:: bash

   mode guided
   arm throttle
   takeoff 5
   velocity x y z
   mode land

**ROS 2 DDS Commands:**
(Not active by default)
In a new terminal:

.. code-block:: bash

   ros2 service call /ap/mode_switch ardupilot_msgs/srv/ModeSwitch "{mode: 4}"
   ros2 service call /ap/arm_motors ardupilot_msgs/srv/ArmMotors "{arm: true}"
   ros2 service call /ap/experimental/takeoff ardupilot_msgs/srv/Takeoff "{alt: 4}"

Available Topics
----------------

Some relevant DDS topics:

.. code-block:: bash

   ros2 topic echo ap/imu/experimental/data
   ros2 topic echo ap/pose/filtered
