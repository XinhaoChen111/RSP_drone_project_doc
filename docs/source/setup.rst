Setup Instructions
==================

This section provides setup instructions for both simulation and real hardware environments. everything runs on Ubuntu 22.04 using ROS2 Humble.

Prerequisites
-------------

Install Gazebo Fortress: https://gazebosim.org/docs/fortress/install/

Install ROS2 Humble: https://docs.ros.org/en/humble/Installation.html

Workspace Setup
---------------

Assuming your workspace is named `drone_workspace`:

.. code-block:: bash

   cd ~/drone_workspace
   mkdir src && cd src

ArduPilot Setup
---------------

Refer to the official ArduPilot documentation for detailed instructions:

https://ardupilot.org/dev/docs/building-setup-linux.html

Clone the ArduPilot repository:

.. code-block:: bash

   git clone -b Copter-4.5 --recurse-submodules https://github.com/ArduPilot/ardupilot.git
   cd ardupilot
   Tools/environment_install/install-prereqs-ubuntu.sh -y
   . ~/.profile

Compile ArduPilot for SITL:

.. code-block:: bash

   ./waf configure --board sitl
   ./waf copter

Add ArduPilot tools to PATH:

.. code-block:: bash

   export PATH=$PATH:$HOME/ardupilot/Tools/autotest
   export PATH=/usr/lib/ccache:$PATH
   . ~/.bashrc

Test the installation:

.. code-block:: bash

   cd ardupilot/ArduCopter
   sim_vehicle.py -v copter --console --map -w

ArduPilot for ROS 2
-------------------

Refer to the official ArduPilot ROS 2 integration documentation:

https://ardupilot.org/dev/docs/ros2.html

Import ROS 2 packages:

.. code-block:: bash

   cd ~/drone_workspace
   vcs import --recursive --input https://raw.githubusercontent.com/ArduPilot/ardupilot/master/Tools/ros2/ros2.repos src
   sudo apt update
   rosdep update
   source /opt/ros/humble/setup.bash
   rosdep install --from-paths src --ignore-src -r -y

NOTE: May have to change ardupilot back to Copter-4.5 after vcs import

Micro XRCE DDS Gen Setup
------------------------

Install Java Runtime Environment:

.. code-block:: bash

   sudo apt install default-jre

Clone and build Micro XRCE DDS Gen:

.. code-block:: bash

   cd ~/drone_workspace
   git clone --recurse-submodules https://github.com/ardupilot/Micro-XRCE-DDS-Gen.git
   cd Micro-XRCE-DDS-Gen
   ./gradlew assemble
   echo "export PATH=\$PATH:$PWD/scripts" >> ~/.bashrc
   source ~/.bashrc
   microxrceddsgen -help

Build the workspace:

.. code-block:: bash

   cd ~/drone_workspace
   colcon build --packages-up-to ardupilot_sitl

Gazebo Plugin Installation
--------------------------

Refer to the official ArduPilot Gazebo plugin documentation:

https://github.com/ArduPilot/ardupilot_gazebo/tree/fortress

Install dependencies:

.. code-block:: bash

   sudo apt install rapidjson-dev libignition-gazebo6-dev

Clone and build the plugin:

.. code-block:: bash

   git clone https://github.com/ArduPilot/ardupilot_gazebo -b fortress
   cd ardupilot_gazebo
   mkdir build && cd build
   cmake .. -DCMAKE_BUILD_TYPE=RelWithDebInfo
   make -j4

Configure environment variables:

.. code-block:: bash

   echo 'export IGN_GAZEBO_SYSTEM_PLUGIN_PATH=$HOME/ardupilot_gazebo/build:${IGN_GAZEBO_SYSTEM_PLUGIN_PATH}' >> ~/.bashrc
   echo 'export IGN_GAZEBO_RESOURCE_PATH=$HOME/ardupilot_gazebo/models:$HOME/ardupilot_gazebo/worlds:${IGN_GAZEBO_RESOURCE_PATH}' >> ~/.bashrc

MAVROS Installation
------------------------------

https://github.com/mavlink/mavros/blob/ros2/mavros/README.md

.. code-block:: bash

   sudo apt install ros-humble-mavros
   ros2 run mavros install_geographiclib_datasets.sh

NOTE: May need some permissions to run install_geographiclib_datasets.sh

Workspace Structure
-------------------

After setup, possible workspace should look like:

.. code-block:: text

   drone_workspace
   ├── Micro-XRCE-DDS-Gen
   ├── src
   │   ├── ardupilot
   │   ├── micro_ros_agent
   │   └── RSP_drone_project


Make sure to use rosdep install all missing packages for the drone_project that you may be missing. Most of the packages are pretty standard. Once everything is done you can run 

.. code-block:: bash

   colcon build

in the drone_workspace to build all of the packages and dont forget to source ROS2 and setup.bash.

