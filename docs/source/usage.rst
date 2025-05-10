Usage
=====

This page explains how to operate the drone in simulation and real hardware using ROS2 and MAVProxy.

ROS2 Services
-------------

Switch to Guided mode:

.. code-block:: bash

   ros2 service call /ap/mode_switch ardupilot_msgs/srv/ModeSwitch "{mode: 4}"

Arm the drone:

.. code-block:: bash

   ros2 service call /ap/arm_motors ardupilot_msgs/srv/ArmMotors "{arm: true}"

Takeoff:

.. code-block:: bash

   ros2 service call /ap/experimental/takeoff ardupilot_msgs/srv/Takeoff "{alt: 4}"

Available Topics
----------------

Echo IMU data:

.. code-block:: bash

   ros2 topic echo /ap/imu/experimental/data

Echo local pose:

.. code-block:: bash

   ros2 topic echo /ap/pose/filtered
