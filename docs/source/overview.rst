Project Overview
================

The Aurelia X4 Drone Project aims to develop a comprehensive ROS 2-based control system for the Aurelia X4 drone. The system includes visualization in RViz, simulation in Gazebo, and execution of basic flight maneuvers on physical hardware.

Team Members
------------

- Seyi R. Afolayan (Remote PIC)
- Sameer Khan
- James Kaluna
- Xinhao Chen
- Lavinia Kong

Project Objectives
------------------

**Primary Objectives:**

- Develop a comprehensive drone description package with URDF/xacro models (`x4_description`)
- Implement a simulation environment in Gazebo (`x4_gazebo`)
- Develop takeoff and landing capabilities in both simulation and real hardware (`x4_gazebo` and physical hardware)

**Stretch Goals (If Time Permits):**

- Implement basic path planning for autonomous navigation
- Add SLAM capabilities for mapping environments
- Develop pick-and-place functionality

Repository Structure
--------------------

.. code-block:: text

   /RSP_drone_project/src
   ├── x4_description      # URDF/xacro files, meshes, materials
   ├── x4_gazebo           # Simulation environments and launch files
   ├── x4_control          # Flight control algorithms
   ├── x4_interface        # Hardware communication bridge
   ├── x4_vision           # Computer vision with RX0II camera
   └── x4_bringup          # System launch files

Development Practices
---------------------

- **Regular meetings:** Twice per week (to be discussed)
- **Documentation:** ROS 2 style documentation, TODOs via Slack, Milestones tracker via Slack

Components
----------

- Aurelia X4 Standard drone
- 4K Camera
- Gimbal
- Onboard Compute (NVIDIA Jetson Nano)
