.. _ros_jazzy:

#################################
Monitor Tutorial with ROS 2 Jazzy
#################################

This section shows how to install and deploy some ROS 2 Jazzy nodes and monitor them with DDS Monitor.

Installation
============

Follow the :ref:`installation_manual_linux` or the :ref:`installation_manual_windows` in this
documentation to install DDS Monitor. You also need a ROS 2 Jazzy installation.

Execution
=========

This tutorial creates a simple DDS network with one :code:`talker` and one :code:`listener` from the ROS 2 demo nodes.

Execute DDS Monitor
------------------------

Start DDS Monitor by running the executable file created in the installation process.
Once DDS Monitor is running, start a monitor in domain :code:`0` (default domain).

.. thumbnail:: /rst/figures/screenshots/usage_example/Init_domain.png
    :align: center

Execute ROS 2 demo nodes with statistics
----------------------------------------

Running ROS 2 nodes with statistics requires two configuration settings:

- The middleware must be Fast DDS, which is the default (it can also be set through an environment variable).
- To activate the publication of statistical data, Fast DDS needs an environment variable listing the
  kinds of statistical data to report.

To run the nodes, run each of the following commands in a different terminal:

.. code-block:: bash

    export FASTDDS_STATISTICS="HISTORY_LATENCY_TOPIC;NETWORK_LATENCY_TOPIC;\
    PUBLICATION_THROUGHPUT_TOPIC;SUBSCRIPTION_THROUGHPUT_TOPIC;RTPS_SENT_TOPIC;\
    RTPS_LOST_TOPIC;HEARTBEAT_COUNT_TOPIC;ACKNACK_COUNT_TOPIC;NACKFRAG_COUNT_TOPIC;\
    GAP_COUNT_TOPIC;DATA_COUNT_TOPIC;RESENT_DATAS_TOPIC;SAMPLE_DATAS_TOPIC;\
    PDP_PACKETS_TOPIC;EDP_PACKETS_TOPIC;DISCOVERY_TOPIC;PHYSICAL_DATA_TOPIC;\
    MONITOR_SERVICE_TOPIC"

    ros2 run demo_nodes_cpp listener

.. code-block:: bash

    export FASTDDS_STATISTICS="HISTORY_LATENCY_TOPIC;NETWORK_LATENCY_TOPIC;\
    PUBLICATION_THROUGHPUT_TOPIC;SUBSCRIPTION_THROUGHPUT_TOPIC;RTPS_SENT_TOPIC;\
    RTPS_LOST_TOPIC;HEARTBEAT_COUNT_TOPIC;ACKNACK_COUNT_TOPIC;NACKFRAG_COUNT_TOPIC;\
    GAP_COUNT_TOPIC;DATA_COUNT_TOPIC;RESENT_DATAS_TOPIC;SAMPLE_DATAS_TOPIC;\
    PDP_PACKETS_TOPIC;EDP_PACKETS_TOPIC;DISCOVERY_TOPIC;PHYSICAL_DATA_TOPIC;\
    MONITOR_SERVICE_TOPIC"

    ros2 run demo_nodes_cpp talker

Remember to source your `ROS 2 installation
<https://docs.ros.org/en/jazzy/Installation/Alternatives/Ubuntu-Development-Setup.html#setup-environment>`_
before every :code:`ros2` command.

Monitoring network
------------------

Two new Participants appear in the :ref:`dds_panel_layout`.

.. thumbnail:: /rst/figures/screenshots/jazzy_tutorial/Participants.png
    :align: center

Domain View
^^^^^^^^^^^

To inspect the structure of the DDS network, open the *Domain View* in the :ref:`chart_panel_index`.
This tab shows a graph of the network: the single Host contains the single User,
which contains both Processes, each with a number of DataReaders and DataWriters. The graph also shows a
number of Topics, drawn as vertical gray lines, related to the code of the listener and talker. Only one of them,
:code:`rt/chatter`, relates two entities, a DataWriter and a DataReader. This is the Topic
used to exchange information.

.. thumbnail:: /rst/figures/screenshots/jazzy_tutorial/Domain_Graph.png
    :align: center

*Right-click* a Topic name in the *Domain View* to see several options, such as filtering the graph by that Topic
(*Filter topic graph*). Clicking the
:code:`rt/chatter` Topic shows the entities exchanging information.

.. thumbnail:: /rst/figures/screenshots/jazzy_tutorial/Topic_filter.png
    :align: center

To see the IDL representation of a Topic, right-click
the Topic name and choose *Data type IDL view*. This opens a new Tab with the IDL, which you can
copy and paste. For ROS 2 topics, the IDL representation is demangled by default (you can undo this in
*View->Revert ROS 2 Demangling*).

.. thumbnail:: /rst/figures/screenshots/jazzy_tutorial/IDL_img_jazzy2.png
    :align: center

Alias
^^^^^

Participants in ROS 2 are named :code:`/` by default.
To tell them apart, change the alias of each Participant (see :ref:`change_alias`), either
from the :ref:`left_panel` or from the Domain View panel, by *right-clicking* the entity.
The :code:`talker` is the one with a :code:`chatter` writer, and the :code:`listener` the one with a
:code:`chatter` reader. This Tab is not needed anymore, so click the *X* to return to the
:code:`New Tab` view.

.. thumbnail:: /rst/figures/screenshots/jazzy_tutorial/Alias_new.png
    :align: center

Statistical data
^^^^^^^^^^^^^^^^

To show statistical data about the communication between the :code:`talker` and the :code:`listener`,
open the *Chart View* and follow the steps to :ref:`tutorial_create_dynamic_series` and plot this statistical data
in a real time chart.

.. thumbnail:: /rst/figures/screenshots/jazzy_tutorial/Statistics.png
    :align: center

Introspect metatraffic topics
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

By default, DDS Monitor hides the topics used for sharing metatraffic and their related endpoints,
so the network is easier to inspect.
These are the topics ROS 2 uses for discovery and configuration, such as :code:`ros_discovery_info`,
and the ones Fast DDS uses to report statistical data.

To see these topics in the monitor, click the *View->Show Metatraffic* menu button
(see :ref:`hide_show_metatraffic`).
The logical panel then shows these topics, and the Readers and Writers associated with them appear under their
Participants.

.. thumbnail:: /rst/figures/screenshots/jazzy_tutorial/Metatraffic.png
    :align: center

Video Tutorial
==============

A `video tutorial <https://www.youtube.com/watch?v=OYibnUnMIlc>`_ walks through the steps
described in this section.
