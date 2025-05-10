Setup Instructions
==================

This page describes how to set up your development environment for the Aurelia X4 Drone Project.

Workspace Preparation
---------------------

Every new terminal should be sourced with the workspace setup:

.. code-block:: bash

   cd <drone_workspace>
   source install/setup.bash

ArduPilot Setup
---------------

Refer to `ArduPilot Setup Guide <https://ardupilot.org/dev/docs/building-setup-linux.html>`_ for full installation instructions. The basic steps:

.. code-block:: bash

   git clone -b Copter-4.5 --recurse-submodules https://github.com/ArduPilot/ardupilot.git
   cd ardupilot
   Tools/environment_install/install-prereqs-ubuntu.sh -y
   . ~/.profile
   ./waf configure --board sitl
   ./waf copter

SITL Test
---------

To launch SITL and test ArduPilot:

.. code-block:: bash

   cd ardupilot/ArduCopter
   sim_vehicle.py -v copter --console --map -w

ROS2 and Micro XRCE DDS Setup
-----------------------------

Install dependencies and clone ArduPilot ROS2 repos:

.. code-block:: bash

   vcs import --recursive --input https://raw.githubusercontent.com/ArduPilot/ardupilot/master/Tools/ros2/ros2.repos src
   rosdep install --from-paths src --ignore-src -r -y

Then install Micro XRCE DDS Generator:

.. code-block:: bash

   git clone --recurse-submodules https://github.com/ardupilot/Micro-XRCE-DDS-Gen.git
   cd Micro-XRCE-DDS-Gen
   ./gradlew assemble

Gazebo Plugin and MAVROS (Optional)
-----------------------------------

.. code-block:: bash

   sudo apt install rapidjson-dev libignition-gazebo6-dev
   git clone https://github.com/ArduPilot/ardupilot_gazebo -b fortress
   cd ardupilot_gazebo
   mkdir build && cd build
   cmake .. -DCMAKE_BUILD_TYPE=RelWithDebInfo
   make -j4
