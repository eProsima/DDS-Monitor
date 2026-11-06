.. _ros_section:

###########################
DDS Monitor with ROS 2
###########################

DDS Monitor can monitor and study a ROS 2 network.
It discovers entities in a local network automatically, so you can see the running Participants,
their Endpoints, the Topics each one uses, and the network interfaces they use
to communicate with each other.
You can also receive statistical data from every endpoint in the network, to analyze performance and find
communication problems.

ROS 2 nodes communicate through the DDS communication protocol.
The latest ROS 2 versions support several RMWs (ROS MiddleWare).
To receive statistical data and monitor your network, use Fast DDS as your ROS 2 middleware.

The following sections explain how to use Fast DDS with Statistics in the latest ROS 2 version,
and include a brief tutorial that uses DDS Monitor with ROS 2 in a simple scenario.

.. toctree::
   :maxdepth: 2

   jazzy/jazzy
