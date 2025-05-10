Setup Instructions
==================

This section provides setup instructions for both simulation and real hardware environments.

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

SITL/MAVProxy
-------------

MAVProxy is a UAV ground control station software package. It should be installed and compiled at this point.

Basic commands in the MAVProxy terminal:

.. code-block:: bash

   mode guided
   arm throttle
   takeoff 15

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

MAVROS Installation (Optional)
------------------------------

If MAVROS is required:

.. code-block:: bash

   sudo apt install ros-humble-mavros
   ros2 run mavros install_geographiclib_datasets.sh

Workspace Structure
-------------------

After setup, your workspace should look like:

.. code-block:: text

   drone_workspace
   ├── Micro-XRCE-DDS-Gen
   ├── src
   │   ├── ardupilot
   │   ├── micro_ros_agent
   │   └── RSP_drone_project
