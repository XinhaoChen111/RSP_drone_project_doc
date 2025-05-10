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

**MAVProxy Commands:**

In the MAVProxy terminal:

.. code-block:: bash

   mode guided
   arm throttle
   takeoff 5
   velocity x y z
   mode land

**ROS 2 Commands:**

In a new terminal:

.. code-block:: bash

   ros2 service call /ap/mode_switch ardupilot_msgs/srv/ModeSwitch "{mode: 4}"
   ros2 service call /ap/arm_motors ardupilot_msgs/srv/ArmMotors "{arm: true}"
   ros2 service call /ap/experimental/takeoff ardupilot_msgs/srv/Takeoff "{alt: 4}"

Available Topics
----------------

Some relevant topics:

.. code-block:: bash

   ros2 topic echo ap/imu/experimental/data
   ros2 topic echo ap/pose/filtered
