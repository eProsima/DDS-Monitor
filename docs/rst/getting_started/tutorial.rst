.. include:: ../exports/alias.include
.. include:: ../exports/roles.include

.. _start_tutorial:

################
Example of usage
################

This example shows how to monitor a DDS network with *DDS Monitor* and explains the application features and
configurations.

.. _fastdds-with-statistics:

*******************************
Fast DDS with Statistics module
*******************************

To show *DDS Monitor* monitoring a real DDS network, this tutorial creates a simple DDS network with the
:code:`hello_world` example of the *Fast DDS* repository.

To run this minimal DDS scenario, in which each entity publishes its statistical data, follow these steps:

#. Compile *Fast DDS* library with CMake option :code:`COMPILE_EXAMPLES` to build the examples
   (:code:`-DCOMPILE_EXAMPLES=ON`).
#. Have *DDS Monitor* installed or a working environment with *Fast DDS*, *Fast DDS Statistics Backend* and
   *DDS Monitor* built.
#. Use the environment variable :code:`FASTDDS_STATISTICS` to activate the statistics writers in the DDS execution (see
   following section).

For more information about the Statistics configuration, see
`Fast DDS statistics module <https://fast-dds.docs.eprosima.com/en/latest/fastdds/statistics/statistics.html>`_.
For information about installing the Monitor and its dependencies, see
:ref:`installation_manual_linux` or :ref:`developer_manual_installation_sources_linux`.

.. _hello_world_example:

Hello World Example
===================

This tutorial uses the *Fast DDS* :code:`hello_world` example to create the DDS network to monitor.
The commands below run this network.
The tutorial does not start with this network running: it is executed once the monitor has started.
This order does not change the Monitor behavior, but it changes the data and information the application shows.

#.  Execute a *Fast DDS* :code:`hello_world` **subscriber** with statistics data active.

    .. code-block:: bash

        export FASTDDS_STATISTICS="HISTORY_LATENCY_TOPIC;NETWORK_LATENCY_TOPIC;\
        PUBLICATION_THROUGHPUT_TOPIC;SUBSCRIPTION_THROUGHPUT_TOPIC;RTPS_SENT_TOPIC;\
        RTPS_LOST_TOPIC;HEARTBEAT_COUNT_TOPIC;ACKNACK_COUNT_TOPIC;NACKFRAG_COUNT_TOPIC;\
        GAP_COUNT_TOPIC;DATA_COUNT_TOPIC;RESENT_DATAS_TOPIC;SAMPLE_DATAS_TOPIC;\
        PDP_PACKETS_TOPIC;EDP_PACKETS_TOPIC;DISCOVERY_TOPIC;PHYSICAL_DATA_TOPIC;\
        MONITOR_SERVICE_TOPIC"

        ./build/fastdds/examples/cpp/hello_world/hello_world subscriber

    where the :code:`subscriber` argument creates a *DomainParticipant* with a *DataReader* in the topic
    :code:`hello_world_topic` in *Domain* :code:`0`.

#.  Execute a *Fast DDS* :code:`hello_world` **publisher** with statistics data active.

    .. code-block:: bash

        export FASTDDS_STATISTICS="HISTORY_LATENCY_TOPIC;NETWORK_LATENCY_TOPIC;\
        PUBLICATION_THROUGHPUT_TOPIC;SUBSCRIPTION_THROUGHPUT_TOPIC;RTPS_SENT_TOPIC;\
        RTPS_LOST_TOPIC;HEARTBEAT_COUNT_TOPIC;ACKNACK_COUNT_TOPIC;NACKFRAG_COUNT_TOPIC;\
        GAP_COUNT_TOPIC;DATA_COUNT_TOPIC;RESENT_DATAS_TOPIC;SAMPLE_DATAS_TOPIC;\
        PDP_PACKETS_TOPIC;EDP_PACKETS_TOPIC;DISCOVERY_TOPIC;PHYSICAL_DATA_TOPIC;\
        MONITOR_SERVICE_TOPIC"

        ./build/fastdds/examples/cpp/hello_world/hello_world publisher --samples 0

    where the :code:`publisher` argument creates a *DomainParticipant* with a *DataWriter* in the topic
    :code:`hello_world_topic` in *Domain* :code:`0`.
    The :code:`--samples 0` argument makes this process publish until it is stopped with :code:`Ctrl+C`.
    The example writes a message every tenth of a second (its :code:`100` milliseconds period is fixed in
    the example code).

The environment variable :code:`FASTDDS_STATISTICS` activates the statistics writers for a *Fast DDS*
application execution.
The *DomainParticipants* created with this variable set report the statistical data of themselves and their
sub-entities.

See the
`Fast DDS documentation <https://fast-dds.docs.eprosima.com/en/latest/fastdds/statistics/dds_layer/topic_names.html>`_
for the available statistical topics.

**************************
DDS Monitor Execution
**************************

This section walks through a complete *DDS Monitor* execution on a real DDS network.

Initial Window
==============

The Monitor starts with no DDS entities running.
The *DDS Monitor* initial window is shown first.
Press :code:`Start monitoring!` to enter the application and start monitoring.

.. thumbnail:: /rst/figures/screenshots/main.png
    :align: center

Initiate monitoring
===================

Once in the application, the first dialog asks for a domain to monitor.
Monitoring a domain means listening in that domain for DDS entities that are running and reporting statistical data.
See section :ref:`monitor_domain` for more information.

You can first press :code:`Cancel` to look around the monitor and check its configurations, but no entities or data
are shown because no domain is being monitored.
You can always return to the :ref:`initialize_monitoring` dialog from :ref:`application_menu_file`.

Initialize monitoring in **domain 0** and press :code:`OK`.

.. thumbnail:: /rst/figures/screenshots/usage_example/Init_domain.png
    :align: center

Add physical and logical panels
===============================

By default, the Monitor only displays the DDS panel, which lists the DDS entities with their configuration and
available statistics information.
To open the logical and physical panels, click the :code:`···` button in the top right corner of the
:ref:`left_panel` and add all the panels.

.. thumbnail:: /rst/figures/screenshots/usage_example/Add_panels.png
    :align: center

The whole application window is now visible.
The left sidebar shows a single entity: the domain you have just initiated.
Once a domain is initiated, it is set as :ref:`selected_entity`, so its information is shown in the
:ref:`info_panel_layout`.

For details on how the information is divided and where to find it, see :ref:`index_user_manual`.

Execute subscriber
==================

Now run the first DDS entity of the network, a *DomainParticipant* with one *DataReader* in
topic :code:`hello_world_topic` in domain :code:`0`, following the steps in :ref:`hello_world_example`.
Once the subscriber is running, the window updates and new information appears in the left sidebar.

.. thumbnail:: /rst/figures/screenshots/usage_example/Execute_subscriber.png
    :align: center

The number of discovered entities has increased.
There is now a *DomainParticipant* called :code:`RTPSParticipant`, holding a *DataReader* called
:code:`hello_world_topic_0.0.1.4`.
This *DataReader* has a locator, which is the *Shared Memory Transport* locator.
That is because the Monitor and the *DomainParticipant* run on the same host, so they communicate using
the `Shared Memory Transport (SHM) protocol
<https://fast-dds.docs.eprosima.com/en/latest/fastdds/transport/shared_memory/shared_memory.html>`_.

A *Host* now exists as well, with a *User* and a *Process* where :code:`RTPSParticipant` is running.
The *DomainParticipant* reports this information because :code:`PHYSICAL_DATA_TOPIC` is activated.
There is also a new *Topic* :code:`hello_world_topic` under *Domain* :code:`0`.

Clicking any entity name selects it and shows its specific information, such as name, backend id, QoS, etc.
Double-clicking an entity expands or collapses its child entities.

.. thumbnail:: /rst/figures/screenshots/usage_example/Information_subscriber.png
    :align: center

Execute publisher
=================

Next, run a publisher in topic :code:`hello_world_topic` in domain :code:`0`,
following the steps in :ref:`hello_world_example`.
Once the publisher is running, new entities appear:
a new *DomainParticipant*, also called :code:`RTPSParticipant`, with a *DataWriter*
:code:`hello_world_topic_0.0.1.3`.
If this publisher runs on the same *Host* and *User*, there is also a new *Process* that represents the process where
this new :code:`RTPSParticipant` is running.

.. thumbnail:: /rst/figures/screenshots/usage_example/Information_publisher.png
    :align: center

Domain View
===========

With both the publisher and the subscriber running, you can check the configuration of the new DDS network.
Click *Domain View* in the :ref:`chart_panel_index` to open the Domain display. In
this tab, a graph shows the structure of the network: the single Host contains the single User,
which contains both Processes. Each Process is related to one of the Participants, either the publisher
or the subscriber. The vertical line represents the Topic. The publisher contains the DataWriter, shown as an arrow
that feeds into the Topic, and the subscriber contains the DataReader, shown as an arrow coming from the Topic.

.. thumbnail:: /rst/figures/screenshots/usage_example/Domain_view.png
    :align: center

In this view you can filter by Topic: right-click the Topic name and choose *Filter topic graph* to open the
filtered graph in a new Tab. You can also see the IDL representation of any Topic: right-click the Topic name and
choose *Data type IDL view*.
This opens a new Tab with the IDL, which can be copied and pasted.

.. thumbnail:: /rst/figures/screenshots/usage_example/IDL_img_tutorial.png
    :align: center

These Tabs are not used again, so click the *X* to close all Tabs and return to the
:code:`New Tab` view.

Summary of Statistical Data
===========================

The :ref:`statistics_panel_layout` shows the main information retrieved by each entity.
This panel shows a summary of the data retrieved by the clicked entity.
Here, only the data that the entities are publishing appears. The other *DataKinds*, related to topics not in use,
remain without data.

.. thumbnail:: /rst/figures/screenshots/usage_example/Summary.png
    :align: center

.. _change_alias:

Change entity alias
===================

You can change the name of any entity.
Change the names of the *Publisher* and *Subscriber* *DomainParticipants*, and of the *DataReader*
and *DataWriter*, to make them easier to identify. To do so, right-click the entity name and select **Change alias**.

.. thumbnail:: /rst/figures/screenshots/usage_example/Alias_dialog.png
    :align: center

Set the new alias for these entities.
From now on, the monitor uses this name everywhere.

.. note::

    This changes the alias of the entity inside the monitor only. It does not affect the real DDS network.

Create Historic Series Chart
============================

This section plots the data reported by a DDS network.

Data Count Plot
---------------

First, click *Chart View* in the :ref:`chart_panel_index` to open the graph display. Then, go to
*Edit->Display Historical Data*. In the Dialog that opens, choose the topic whose collected data you want
to see. This tutorial uses :code:`DATA_COUNT`.

.. thumbnail:: /rst/figures/screenshots/usage_example/New_series_data_count.png
    :align: center

A new Dialog then asks you to configure the series to display.
For :code:`DATA_COUNT`, the data belongs to the *DataWriter*, so choose this entity in the
:code:`Source Entity Id:` checkbox.
:code:`Number of bins` is the number of points in which the data is stored.
This example uses :code:`20` bins.
With :code:`Default initial timestamp` as the :code:`Start time`, the initial timestamp is the time at
which the monitor was executed.
Using :code:`Now` in :code:`End time` gets all the data available until the moment the chart is created.
For :code:`Statistic kind`, use :code:`SUM` to get the amount of data sent in each time interval.

.. thumbnail:: /rst/figures/screenshots/usage_example/Data_count_configuration.png
    :align: center

Clicking :code:`Add` creates the series in the main window without closing the dialog.
This makes it easy to create a new series similar to the one already created.
Keep all the settings but change :code:`Number of bins` to :code:`0`.
The value :code:`0` shows all the different *datapoints* that the writer has stored.
:code:`Statistic kind` has no effect when :code:`Number of bins` is :code:`0`.
Then click :code:`Add & Close`. Both series are now shown in the :code:`DATA_COUNT`
window.

.. thumbnail:: /rst/figures/screenshots/usage_example/Data_count_chart.png
    :align: center

In the new chart, the blue series shows the total amount of data packages sent in each time
interval.
The green series shows that the publisher sends this data periodically.

Latency Plot
-------------

Next, plot the latency between these *DomainParticipants*.
First, go to *Edit->Display Historical Data*.
In the Dialog that opens, choose the topic whose collected data you want to see.
Here, choose :code:`FASTDDS_LATENCY`.
It has this name because it represents the time elapsed between the user calling the :code:`write` function
and the reader in the other endpoint receiving the data in the user callback.
Network latency has its own topic, :code:`NETWORK_LATENCY`. However, these endpoints neither store
nor publish this type of data, so it cannot be monitored.

A new Dialog then asks you to configure the series to display.
For :code:`FASTDDS_LATENCY`, the data relates to two entities.
Choose both *DomainParticipants*. This gives all the latency between the
*DataWriters* of the first participant and the *DataReaders* of the second one.

Use the same bins, start time, and end time configuration parameters as in the previous example.

.. thumbnail:: /rst/figures/screenshots/usage_example/Latency_configuration.png
    :align: center

For :code:`Statistic kind`, use several values to get more than one series of statistical data.
Change the :code:`Statistic kind` and click :code:`Add` for each one to create a series per kind.
This example uses these statistic kinds:

* :code:`MEDIAN` (blue series)
* :code:`MAX`  (green series)
* :code:`MIN` (yellow series)
* :code:`STANDARD_DEVIATION` (purple series)

.. thumbnail:: /rst/figures/screenshots/usage_example/Latency_chart.png
    :align: center

The series name, color, axes, and other chart properties can be changed as mentioned in :ref:`chartbox`.

.. _tutorial_create_dynamic_series:

Create Dynamic Series Chart
===========================

This section plots data of a running DDS network in real-time.

Periodic Latency Plot
---------------------

This plot shows the FastDDS latency between the publisher and the subscriber in real-time.
First, click |dynamic_chart|.
In the Dialog that opens, choose the topic whose collected data you want to see.
Here, choose :code:`FASTDDS_LATENCY`.
Set a :code:`Time window` of 1 minute, so the chart shows the data of the last minute of the network.
Finally, set an :code:`Update period` of 5 seconds.
The chart then queries for new data every 5 seconds and retrieves and displays it.

.. thumbnail:: /rst/figures/screenshots/usage_example/New_dynamic_series_latency.png
    :align: center

A new Dialog then asks you to configure the series to display.
For :code:`FASTDDS_LATENCY`, the data relates to two entities.
In this example, choose the *Host*.
This retrieves the latency measured in the communication between the entities of this host and itself.
Here, that is the latency between the two participants, but the same approach can filter latency between two
specific hosts or collect all the latency in the same domain.

For :code:`Statistic kind`, use several values to get more than one series of statistical data.
Change the :code:`Statistic kind` and click :code:`Add` for each one to create a series per kind.
This example uses these statistic kinds:

* :code:`MEAN` (blue series)
* :code:`MAX` (green series)
* :code:`MIN` (yellow series)

.. thumbnail:: /rst/figures/screenshots/usage_example/Dynamic_latency_configuration.png
    :align: center

This chart updates every 5 seconds, displaying the data collected by the monitor within the last 5 seconds.
The axes update periodically, so zooming and moving the chart are not available in this kind of chart while
it is running.
The *play/pause* button stops the axis update so you can zoom and move along the chart.
Pausing the chart does not stop new points from appearing, because the data update still happens every 5 seconds.

.. thumbnail:: /rst/figures/screenshots/usage_example/Dynamic_latency_chart.png
    :align: center

Latency DataPoints
------------------

Real-time charts can also show every *DataPoint* received from the monitored DDS
entities (similar to :code:`bins 0` in historic series).
To see this data in real-time, add a new series to the same chartbox in *Series->Add series*.
Choose the *Host* again as source and target and choose :code:`RAW DATA` as :code:`Statistic kind`.

A new purple series now represents each of the
*DataPoints* sent by the DDS entities and collected by the monitor in the last 5 seconds.
It shows how the :code:`Statistic kind` works:
the :code:`MEAN`, :code:`MAX` and :code:`MIN` in each interval are calculated from these *DataPoints*.

.. thumbnail:: /rst/figures/screenshots/usage_example/Dynamic_all_latency_chart.png
    :align: center

Dynamic series are configurable, like historic series.
The label and color of each series can be changed, and the chart can zoom in and out and move along the axis
while paused.

Set alert to watch events
============================

Alerts watch for specific events in the monitored DDS network. To create one, first click
the *Alerts* tab (marked with a bell icon) in the left panel to open the Alerts view. This tab lists
all the defined alerts.

.. thumbnail:: /rst/figures/screenshots/usage_example/alert_panel_pre.png
    :align: center

Click the *+* button to create a new alert. A dialog opens where you can configure the alert.

.. thumbnail:: /rst/figures/screenshots/usage_example/alert_dialog.png
    :align: center

In this dialog, you set the name of the alert, its type, the domain to monitor and the conditions for triggering the alert.

All alerts filter the triggering entities using the fields `host`, `user` and `topic`. If any of these fields is left empty
or set to the `ALL` option, all entities match that part of the filter. The filter is a simple equality check between strings,
not a regular expression. An entity must meet all 3 conditions to match the alert filter.

If the alert type is *NEW_DATA*, the alert triggers when a positive `DATA_COUNT` is received from any entity that matches the fields
`host`, `user` and `topic`.

If the alert type is *NO_DATA*, the alert triggers when a `PUBLICATION_THROUGHPUT` message is received from any entity that matches
the fields `host`, `user` and `topic` and its value is lower than `threshold`.

If a timeout period is defined, the alert sends a timeout message with this periodicity. `NEW_DATA` alerts don't support timeout because
they are event-driven. However, you can set a more relaxed polling time to collect timeout messages in the `Edit->Alerts Configuration` option
of the upper menu.

If a script is provided, it is executed every time the alert is triggered. The script must have executable permissions in the
host OS.

Once set up, the alert appears in the list of alerts, and its metadata is shown below it when clicked.

.. thumbnail:: /rst/figures/screenshots/usage_example/alert_panel_post.png
    :align: center

To remove an alert, right-click it and choose the **Remove Alert** option.

.. _pro_features_tutorial:

**************************
DDS Monitor |Pro|
**************************

*DDS Monitor Pro* includes all the features of the open-source edition, and everything
in the previous sections of this tutorial works the same way in Pro.
The sections below cover the features exclusive to *DDS Monitor Pro*.

These features need a richer DDS network than the minimal ``hello_world`` example.
The main scenario in this tutorial uses the *eProsima Shapes Demo*, a graphical application that
publishes and subscribes to colored geometric shapes on named DDS topics (``Square``, ``Circle``,
``Triangle``).
Each shape sample has four fields: ``color`` (a string), ``x``, ``y``, and ``shapesize``
(integers), which suit live charts, spy views, and scatter plots.
A separate scenario at the end of this section demonstrates the :ref:`image_pane`.

.. _shapes_demo_scenario:

Shapes Demo Scenario
====================

*eProsima Shapes Demo* is available at `https://github.com/eProsima/ShapesDemo
<https://github.com/eProsima/ShapesDemo>`_.
Follow the build and installation instructions in that repository before continuing.
The network used in this tutorial needs two instances.

#. Open a terminal, source the *eProsima Shapes Demo* installation, and launch the first
   instance:

   .. code-block:: bash

       source ~/shapes_demo_ws/install/setup.bash
       ShapesDemo

   In the Shapes Demo GUI, go to **Options → Participant Configuration** and make sure the
   **Active statistics** toggle is enabled (it is on by default) so the participant reports
   statistical data to the monitor.
   Then click **Publish** and create a **Square** publisher.
   Click **Publish** again and create a **Circle** publisher.

#. Open a second terminal and launch a second instance:

   .. code-block:: bash

       source ~/shapes_demo_ws/install/setup.bash
       ShapesDemo

   In this second GUI, make sure **Active statistics** is enabled the same way under
   **Options → Participant Configuration**.
   Then click **Subscribe** and create a **Square** subscriber.

The DDS network now has three active endpoints on domain :code:`0`: a Square publisher and a
Circle publisher in the first instance, and a Square subscriber in the second.
Keep both Shapes Demo windows open throughout the tutorial.

.. thumbnail:: /rst/figures/screenshots/shapes_demo_pro.png
    :align: center

.. _pro_monitor_launch:

DDS Monitor Pro Execution
================================

Start *DDS Monitor Pro*.
The start screen appears; press **Start monitoring!** to enter the main interface.

.. figure:: /rst/figures/screenshots/main_pro.png
    :align: center

Initiate Monitoring
===================

Once in the application, the **Initialize Monitor** dialog opens.
The Shapes Demo processes are running on domain :code:`0`.
Enter :code:`0` in the **DDS Domain** field and click **OK**.

.. figure:: /rst/figures/screenshots/init-monitor_pro.png
    :align: center

The monitor starts discovering entities.
After a few seconds the **Explorer Panel** on the left shows the participants, writers, and reader
created by the two Shapes Demo instances.
Open all sub-panels by clicking the :code:`···` button in the top-right corner of the Explorer
Panel.
The topics ``Square`` and ``Circle`` appear in the Logical panel under domain :code:`0`, and the
host, users, and two processes appear in the Physical panel.

.. figure:: /rst/figures/screenshots/explorer_pro.png
    :align: center

Explore the Domain View
=======================

Click **Domain View** in the main panel selector, or go to **Add → Add Domain View**, to see
the DDS network as an interactive graph.

.. figure:: /rst/figures/screenshots/domain_pro.png
    :align: center

The graph shows both Shapes Demo processes as boxes inside the host.
Each process contains its participant.
The ``Square`` topic line runs vertically, with a DataWriter arrow from the first process feeding
into it and a DataReader arrow from the second process coming out of it.
The ``Circle`` topic line shows only a DataWriter arrow from the first process; it has no
subscriber yet, so no reader arrow appears.

Right-click the ``Square`` topic line and choose **Data type IDL view** to open an IDL pane
showing the ``ShapeType`` definition with its ``color``, ``x``, ``y``, and ``shapesize``
fields.
Close the IDL pane once you have inspected it.

.. figure:: /rst/figures/screenshots/domain_idl_pro.png
    :align: center
    :width: 300px

Right-click the ``Square`` topic line and choose **Filter topic graph** to open a filtered view
showing only the entities connected to that topic.
A new tab opens with the Square publisher and subscriber. The Circle publisher is not shown
because it is not related to the Square topic.
Close the filtered tab and return to the full domain view.

.. figure:: /rst/figures/screenshots/filter_topic_pro.png
    :align: center
    :width: 400px

Next, try the visibility controls.
Click the |gear| button in the Domain View pane header.
The configuration panel opens on the right and shows **DOMAIN GRAPH** at the top.
The panel lists all entities grouped into seven collapsible sections: **TOPICS**, **HOSTS**,
**USERS**, **PROCESSES**, **PARTICIPANTS**, **DATAWRITERS**, and **DATAREADERS**.
Each section header shows a visible/total count.

**Hiding a process and its descendants**

Expand the **PROCESSES** section.
The two Shapes Demo processes are listed by their process ID or alias.
Clear the checkbox next to one of them.
That process disappears from the graph immediately, along with everything it contained:
its participant, the participant's DataWriter or DataReader, and the locators associated with
them.
This is the container behavior: hiding a parent entity hides all its descendants automatically.
Re-check the process to bring all its entities back at once.

**Hiding and showing individual topics**

Expand the **TOPICS** section.
Both ``Square`` and ``Circle`` are listed.
Clear the checkbox next to ``Circle``.
The Circle topic line vanishes from the graph along with its DataWriter arrow; the ``Square``
part of the graph is unaffected.
Re-check ``Circle`` to restore it.

When the list is long, use the **Filter entities...** search box at the top of the panel to find
an entity by name.

**Showing metatraffic**

By default metatraffic is hidden.
Go to **View → Hide/Show Metatraffic** to make it visible.
Many new topic lines and endpoints appear in the graph: the internal statistics topics produced
by the statistics module.
Toggle the same menu item again to hide metatraffic.

.. figure:: /rst/figures/screenshots/statistics_filter_pro.png
    :align: center

To restore all manually hidden entities at once, use the **ACTIONS** button in the configuration
panel and choose **Show All Entities**.

Topics Panel
============

Click the |topic_icon| icon in the vertical icon bar on the far left of the window to open the
**Topics Panel**.
It lists all discovered topics: ``Square`` and ``Circle``, together with the statistics
metatraffic topics produced by the *Fast DDS* statistics module.

Click the small arrow next to ``Square`` to expand it.
The fields of ``ShapeType`` are listed: ``color``, ``x``, ``y``, and ``shapesize``.
The numeric fields ``x``, ``y``, and ``shapesize`` are interactive leaf nodes: drag one onto an
open chart to add a new series, or right-click it to plot immediately.

.. figure:: /rst/figures/screenshots/topics_square_pro.png
    :align: center
    :width: 400px

Spy a Topic
===========

Right-click ``Square`` in the **Topics Panel** and select **Spy topic data**.
A Topic Spy pane opens and immediately starts receiving live samples from the Square
publisher.

.. figure:: /rst/figures/screenshots/spy_square_pro.png
    :align: center
    :width: 400px

Use the |play| / |pause| button in the pane header to pause or resume the live feed without
closing the pane.
While paused, the last received sample stays visible for inspection.

Split Panes
===========

*DDS Monitor Pro* can hold several views side by side in the same monitor tab.
With the Spy pane open, split it to place a chart next to it.

Click the **...** (three-dots) button in the Spy pane header and hover over **Split right**.
A submenu lists all available pane types. Select **Topic Chart** to open a new
chart pane to the right of the Spy pane.

.. figure:: /rst/figures/screenshots/resize_pro.png
    :align: center
    :width: 470px

Drag the vertical divider between the panes to resize them as needed.
The configuration panel opens automatically with the creation form for the new chart.

Up to six panes can be open in a single tab at the same time.

Plot a Topic Chart
==================

With the new chart pane open next to the Spy pane, configure it to track the Square's
position.
The configuration panel shows the **NEW TOPIC CHART** creation form at the top.

The **PLOT MODE** row has two buttons, **Time Series** and **XY Chart**, that switch
this pane between the two chart types.
Make sure **Time Series** is selected, then fill in the form:

* **DOMAIN**: :code:`Domain 0`.
* **TIME WINDOW**: :code:`60` seconds (``00`` d ``00`` h ``01`` m ``00`` s), so the last minute of
  data is visible.
* **ADVANCED**: leave **Max points** at :code:`500`.
* Click **Create Topic Chart**.

The chart is created and the configuration panel switches to **TIME SERIES CHART**.
Under **CHART NAME**, type ``Square Position`` to label this chart.

Click **Add Series** in the **SERIES** section.
The inline form expands: type ``Square`` in the **Filter topics** box.
Select ``Square`` and wait for the first sample to arrive. The field list then shows
``color``, ``x``, ``y``, and ``shapesize``.
Click ``x`` and then click **Add Series** (or double-click ``x``) to add it.
Repeat and add ``y`` as a second series.

.. figure:: /rst/figures/screenshots/topic_time_series_pro.png
    :align: center

The chart now shows both the horizontal and vertical position of the square updating live as the
shape bounces around the canvas.
Under **DISPLAY**, enable **Show legend** to see the series names alongside their line colors.

You can also add series without using the configuration panel:

* **From the Topics Panel** - expand ``Square`` in the **Topics Panel** and drag the ``shapesize``
  leaf directly onto the chart; a third series appears immediately.
* **From the Spy pane** - right-click the ``x`` field in the Spy pane and select **Plot field**
  to open a new chart for that field, or drag any numeric leaf from the sample tree onto an
  already-open chart to add it as a new series.

Click |resize| **Reset View** in the chart header at any time to return both axes to their
default range after zooming or panning.

Plot an XY Chart
================

A Time Series chart shows each value changing over time.
To see the shape's trajectory, with ``x`` plotted against ``y``, switch to XY Chart mode.

Click |gear| in the ``Square Position`` chart header to open the configuration panel.
Click the **XY Chart** button in the **PLOT MODE** row.
The chart clears and the settings update for XY mode.

Under **PANE SETTINGS**, keep **Domain** at :code:`Domain 0` and click **Apply & Reset Chart**.
Under **DISPLAY**, set **Max points** to :code:`150` to keep the scatter plot readable.

Click **Add XY Series** in the **SERIES** section:

* Under **X AXIS**, select the ``Square`` topic and choose ``x`` as the **X Field**.
* Under **Y AXIS**, select the ``Square`` topic and choose ``y`` as the **Y Field**.
* Click **Add XY Series**.

.. figure:: /rst/figures/screenshots/xy_pro.png
    :align: center

The scatter plot shows every position where the shape has been during the last :code:`150` samples.
As the Shapes Demo keeps running, new points appear and old ones drop off once the buffer is full.
Because the shape bounces between the edges of the canvas, the point cloud outlines the boundaries
of the Shapes Demo window as a rectangle.

When X and Y values come from different topics, each new X sample is paired with the most recent
Y value, so you can plot correlations between any two numeric fields in the same domain.

Create a Custom Series
======================

Besides plotting topic fields directly, *DDS Monitor Pro* can plot a series computed from a
JavaScript formula that combines one or more topic fields with your own constants.
This example plots the Square's distance from the origin, computed live from its ``x`` and ``y`` fields.

Open the **Custom Series** panel by clicking the |custom_series| icon in the vertical icon bar on the
far left of the window, then click the |plus| button to create a new series.
The formula editor opens in a central tab.

Fill in the editor as follows:

* Under **SERIES NAME**, type ``Square distance``.
* Under **DATA SOURCES**, select **Domain 0** and topic ``Square``, pick the ``x`` field, type ``x``
  in **As var**, and click **Add Binding**. Repeat for the ``y`` field with the variable name ``y``.
* Under **GLOBAL VARIABLES**, add a variable named ``scale`` with the value ``0.1``.
* Under **JAVASCRIPT FUNCTION BODY**, write a formula that returns the scaled distance from the
  origin:

  .. code-block:: javascript

      return Math.sqrt(x * x + y * y) * scale;

Click **Save & Exit**.
The new series appears in the **Custom Series** panel.

.. figure:: /rst/figures/screenshots/custom_series_editor_tutorial_pro.png
    :align: center

Open a Topic Chart (or reuse the ``Square Position`` chart) and drag the ``Square distance`` row from
the **Custom Series** panel onto the chart, or right-click the row and choose **Plot on chart**.
The computed series is plotted live with any other series and updates as new ``Square`` samples
arrive.

.. figure:: /rst/figures/screenshots/custom_series_chart_tutorial_pro.png
    :align: center

Custom series definitions can be exported to a ``.json`` file with the |file_up| button in the panel
(or **File → Export Custom Series...**) and imported later with |file_down|, independently of the
workspace.

Statistics Charts
=================

Besides raw topic values, *DDS Monitor Pro* can visualize pre-computed DDS statistics.
This section adds a live publication throughput chart for the Square publisher.

Click |dynamic_chart| in the shortcuts toolbar, or go to **Add → Add Statistics Chart**.
The configuration panel opens the creation form for the new chart: **NEW REAL-TIME CHART** from the
toolbar button, or **NEW STATISTICS CHART** from the menu (the latter adds a **CHART TYPE** selector;
choose *Live (real-time)*).
Fill in the form:

* **DATA KIND**: choose :code:`PUBLICATION_THROUGHPUT`.
* **TIME WINDOW**: :code:`120` seconds (``00`` d ``00`` h ``02`` m ``00`` s, the default).
* **UPDATE PERIOD**: :code:`5` seconds (the default).
* Click **Create Real-Time Chart**.

The chart pane opens and the configuration panel switches to **STATISTICS CHART LIVE**.
A real-time chart is created without series, so add one now.
Click **Add Series** in the **SERIES** section.
The inline form expands with a **Source** selector.
Choose the Square publisher participant as the source entity.
Select :code:`MEAN` for **Statistic** and click **Add Series**.

.. figure:: /rst/figures/screenshots/statistics_charts_pro.png
    :align: center

The series appears in the chart and updates every five seconds, showing the mean publication
throughput of the Square publisher over time.
Under **CHART NAME**, rename this chart to ``Throughput`` to make it easy to identify later.

Under **AXES**, enable **Lock Y axis** to keep the vertical scale stable.
Under **ACTIONS**, click **Export to CSV** at any time to save the chart data to a file for
offline analysis.

Enable and Disable Statistics
=============================

To save resources, *DDS Monitor Pro* only collects a statistic while something is using it.
Creating the throughput chart in the previous section automatically enabled the
``PUBLICATION_THROUGHPUT`` reader.
The **Enable / Disable Statistics** panel shows which statistics readers are active and lets you
control them.

Click the |enable_statistics| icon in the vertical icon bar on the far left of the window to open the
panel.
Each statistic is listed with a toggle.
The ``PUBLICATION_THROUGHPUT`` reader shows an information marker indicating it is active only because
the throughput chart needs it. If you delete that chart, the reader is removed again automatically.

Alerts create statistics readers the same way. Create one and watch its reader appear:

#. Click the |create_alert| icon in the shortcuts toolbar, or the **+** button in the
   :ref:`Alerts Panel <pro_alerts_panel>`, to open the alert creation form.
#. Set an **Alert kind** of ``NEW_DATA`` (fires when new data is published on a topic), set the
   **Topic** filter to ``Square``, and give the alert a name.
#. Click **Add Alert**.

The ``NEW_DATA`` alert monitors the ``DATA_COUNT`` statistic reported by the DataWriters of the
topic, so creating it automatically enables the ``DATA_COUNT`` reader.
Return to the **Enable / Disable Statistics** panel and note that ``DATA_COUNT`` now appears active
with an information marker, like ``PUBLICATION_THROUGHPUT`` did for the chart. It stays only
as long as the alert exists.
See :ref:`pro_alerts_panel` for the full alert configuration reference.

Toggle a statistic on to keep its reader active permanently, even when no chart or alert uses it, so
its data is always available.
Toggle it off to stop collecting that statistic entirely.
See :ref:`statistics_readers_panel` for the full behavior, including which readers alerts create.

Publish Topic Data
==================

The *Publisher Pane* lets you inject custom DDS samples directly from the monitor, without
writing any code.
This section publishes a new ``Square`` shape that appears in the Shapes Demo subscriber window.

Right-click ``Square`` in the **Topics Panel** and select **Publish topic data**.
A Publisher Pane opens and the configuration panel shows **PUBLISHER** at the top.

The **CURRENT TOPIC** section shows the topic name (``Square``), the domain (:code:`Domain 0`),
the resolved type name (``ShapeType``), the publisher status, and a samples-sent counter.

Click **Apply & Reset** to attach the publisher to the ``Square`` topic.
The pane body fills with an auto-generated form with one row per field in ``ShapeType``.
Click **Randomize** in the **ACTIONS** section of the configuration panel to fill all fields
with random valid values automatically.

.. figure:: /rst/figures/screenshots/publish_pro.png
    :align: center

Click **Publish** (the blue button at the bottom of the pane body), or **Publish once** in the
**ACTIONS** section of the configuration panel, to send a single sample.
The samples-sent counter in **CURRENT TOPIC** increments to :code:`1`.
A shape with the randomized color, size, and position appears in the Shapes Demo instance that
has the Square subscriber for the duration of one message lifetime.

To publish a continuous stream, enable **Publish continuously** in the **CONTINUOUS** section of
the configuration panel and set **Interval** to :code:`100` milliseconds.
The shape stays refreshed at the same position for as long as continuous mode is active.
Click the toggle again to stop publishing.

Register a Data Type
====================

The *Register Type* view lets you supply a data type from its IDL so it can be used on topics whose
type was never discovered on the network, for example *Safe DDS* topics.
This example uses the ``ShapeType`` already on the network as a starting point to register a new type.

Open **Add → Add Type Registration**.
A Register Type pane opens.

#. In the **SELECT AN EXISTING TYPE OR START FROM SCRATCH** dropdown, choose ``ShapeType``.
   Its IDL loads into the editor.
#. In the **REGISTER AS** field, change the name to a new one, for example ``MyShapeType``.
   Because this name is not a struct in the loaded IDL, the type is registered under it as an
   alias of ``ShapeType``.
#. Click **Save**. The pane reports that the type was registered successfully.

.. figure:: /rst/figures/screenshots/register_type_tutorial_pro.png
    :align: center

The registered type is now available on every monitored domain and can be paired with any topic
name.
Although there is no topic using ``MyShapeType`` in this tutorial, you could now publish it on any
topic from the :ref:`Publisher Pane <publisher_pane>` shown in the previous section, and the publisher
form would be built automatically from the registered type.
See :ref:`register_type` for the full workflow, including uploading IDL files with ``#include``
directives.

Add a Second Monitor
====================

*DDS Monitor Pro* can run several
independent monitors in the same window, each watching a different DDS environment.
The next section displays a live image topic, so this step runs an image publisher on a
**separate domain** (:code:`1`) and adds a second monitor tab for it.

.. note::

    This tutorial does not ship an image publisher. Any DDS application that publishes an image-typed
    topic works, such as a ROS 2 node publishing ``sensor_msgs/msg/Image`` or a *Fast DDS* application
    using the *eProsima Fast DDS* image types. A ready-to-use IDL for the latter is available in the monitor
    repository at `resources/idl/FastDdsImage.idl
    <https://github.com/eProsima/DDS-Monitor/blob/main/resources/idl/FastDdsImage.idl>`_; generate
    a type from it with *Fast DDS Gen* and publish frames on a topic in domain :code:`1`.
    See :ref:`image_pane` for the full list of supported image schemas.
    The exact domain does not matter: any domain other than :code:`0` keeps this scenario separate
    from the Shapes Demo network.

#. Start your image publisher on domain :code:`1`, publishing frames on an image topic.

#. In *DDS Monitor Pro*, open the **File** menu and select **Initialize DDS Monitor**.
   The initialization dialog appears.
   Enter :code:`1`, and click **OK**.

When you click the Domain View icon, a window asks you to choose a domain. Select domain :code:`1`.
A second tab labeled with domain :code:`1` appears in the main panel area alongside the first.

.. figure:: /rst/figures/screenshots/2_monitors_pro.png
    :align: center

The Explorer Panel, entity lists, and the **Topics Panel** switch to show the entities from the
second domain.
The image topic appears in the **Topics Panel** and the image publisher's
participant is listed in the Explorer Panel.
Click back to the domain :code:`0` tab in the logical panel and everything returns to the Shapes Demo network instantly.

Each monitor runs independently: entity discovery and data collection continue in the
background whichever tab is visible.

View Live Image Data
====================

The *Image Pane* renders live image frames from a DDS topic directly inside the monitor.
The image publisher started in the previous section is already running on domain :code:`1`
and sending frames on the topic.

In the **Topics Panel**, right-click on the image topic and select **Open image view**.
A new Image Pane opens subscribed to that topic and the configuration panel shows **IMAGE DISPLAY** at
the top.

Alternatively, go to **Add → Add Image Display**. In the **NEW IMAGE DISPLAY** form, select
**Domain 1** under **DOMAIN**, pick your image topic under **IMAGE TOPIC** (the list shows only the
image topics), and click **Create Image Display**.
To switch an open Image Pane to another topic later, use its **CHANGE TOPIC** section and click
**Apply & Reset**.

.. figure:: /rst/figures/screenshots/image_tutorial_pro.png
    :align: center

The pane starts displaying frames as soon as the first one arrives.
A metadata strip at the bottom of the pane shows the frame resolution, encoding, and a running
total frame count.

Use the |play| / |pause| button in the pane header to pause the stream.
When paused, the last received frame stays visible so you can inspect it.

Under **ACTIONS** in the configuration panel, click **Save Screenshot** to save the current frame
as a PNG file, or **Copy Screenshot** to copy it to the clipboard.

Map a Custom Image Topic
========================

The Image Pane recognizes the standard ROS 2 and *eProsima Fast DDS* image types automatically.
When a topic carries image data under a non-standard type (different field names, or a byte buffer
with no width/height/encoding fields), you can still render it by mapping its fields manually.

.. note::

    This step is optional and only applies when you have a topic whose type is **not** one of the
    recognized image schemas. To try it out, take the ``resources/idl/FastDdsImage.idl`` type from
    the previous section and rename its fields (for example ``width`` → ``cols``, ``height`` →
    ``rows``, ``encoding`` → ``color_format``, ``step`` → ``line_size``, ``data`` → ``pixels``), then
    publish a topic with that modified type. The monitor will no longer auto-detect it as an image,
    which is the case this mapping is for.

Open a new Image Display (**Add → Add Image Display**).
In the **NEW IMAGE DISPLAY** form, if the image topic does not appear under **IMAGE TOPIC**, select it
under **CONFIGURE A CUSTOM TOPIC** instead and click **Configure as image topic**.
The **CONFIGURE IMAGE TOPIC** panel opens.

.. figure:: /rst/figures/screenshots/custom_image_mapping_pro.png
    :align: center

Choose the **Visualization Mode** (**Raw image** or **Compressed image**) and map each slot to a field
of the topic type.
For a raw image whose type names its fields ``cols``, ``rows``, ``color_format``, ``line_size``, and
``pixels`` instead of the standard names, map **Width** → ``cols``, **Height** → ``rows``,
**Encoding** → ``color_format``, **Step / row stride** → ``line_size``, and **Pixel data (bytes)** →
``pixels``.
Each slot's dropdown lists only fields of a compatible data type, and when the type has no suitable
field you can enable the **Fixed value** switch to supply a constant instead.

Click **Save mapping**.
The topic becomes selectable under **IMAGE TOPIC**; select it and click **Create Image Display** to
render it just like a standard image topic.
See :ref:`image_pane_custom_topic` for the full mapping reference.

Stop Monitoring a Domain
========================

The image topic on domain :code:`1` has been inspected, so that monitor is no longer needed.
*DDS Monitor Pro* can stop monitoring a specific domain without closing its panes or
affecting the other monitors.

Go to **File → Stop Monitor** and select domain :code:`1` from the submenu.
Monitoring of domain :code:`1` stops: its entities are no longer tracked and its tab and panes remain
open but become inactive, while the Shapes Demo monitor on domain :code:`0` keeps running.
This is the reverse of *Initialize DDS Monitor* and frees resources from a domain that
is no longer of interest.
See :ref:`pro_stop_monitor` for details.

Save and Restore a Workspace
==============================

*DDS Monitor Pro* saves the complete session state, including monitors, pane layouts, charts, and
alert rules, to a workspace file and restores it exactly on the next launch.

Click the |save| button at the right end of the tab bar, or go to
**File → Save Workspace as...**.
A file dialog opens (the |save| button only asks for a file the first time; after that it saves
to the same file).
Navigate to a suitable folder, type a name such as ``shapes_tutorial``, and click **Save**.
The file is written with the ``.fdmw`` extension.

To verify that the restore works, go to **File → Load Workspace...** and select the
``shapes_tutorial.fdmw`` file.
All monitor tabs, pane layouts, chart series, chart settings, alert rules, sidebar state, theme,
and toolbar visibility are restored exactly as they were.
Each monitor reopens in a waiting state and populates as the Shapes Demo processes are rediscovered.

.. note::

    The statistics database is not stored in the workspace file.
    Entity discovery and data collection restart fresh on load; panes populate as DDS traffic is
    received after the workspace is applied.

Switch Theme
============

*DDS Monitor Pro* ships with **Light** and **Dark** themes.
Every part of the interface (panels, charts, icons, dialogs, the title bar, and the menu bar)
switches instantly when the theme is changed, with no restart required.

Go to **View → Theme** and select **Dark**, or use the |moon| / |sun| toggle at the right end of the
tab bar, next to the |save| button.

.. figure:: /rst/figures/screenshots/dark_image_pro.png
    :align: center

The entire application switches to the dark palette immediately.
Charts use the same ten-color series palette in both themes, so existing series stay
distinguishable.
Node and edge colors in the Domain View adapt automatically. Entity status colors (green for alive,
yellow for degraded, red for error) stay fixed so their meaning does not change.

To revert, go to **View → Theme** and select **Light**.

The active theme is included in the workspace file and is restored the next time the
``shapes_tutorial.fdmw`` workspace is loaded.

Inspect a Recording (Offline Mode)
==================================

*DDS Monitor Pro* can open a previously captured DDS recording and inspect it with full
playback control instead of connecting to a live network.
Use it to analyze an issue after it happened or to share a captured session with a
colleague.

.. note::

    This tutorial does not produce a recording. To obtain one, capture a DDS session with
    `eProsima DDS Record & Replay <https://dds-recorder.readthedocs.io/en/latest/>`_, which saves DDS
    traffic to an ``.mcap`` database. For example, record the Shapes Demo network used earlier in
    this tutorial and then open the resulting file here. *DDS Monitor Pro* opens ``.mcap`` files
    and SQLite ``.db`` recordings.

Go to **File → Open Recording...** and select a recording file (an ``.mcap`` or SQLite ``.db``
file).

.. note::

    Opening a recording never interrupts your live session.
    Because a monitor is already running in this window, the recording opens in a **new, independent
    monitor application**, and the live Shapes Demo monitor keeps running.
    You now have two separate monitor applications open at once, and closing one does not close the
    other.

A **Select recording range** dialog appears first; click **Use full recording** to load the whole
capture, or pick a sub-range and click **Apply range**.

.. figure:: /rst/figures/screenshots/offline_range_pro.png
    :align: center

A playback bar appears at the bottom of the window with the recording name, the absolute start time
and duration, a scrubbable timeline, play/pause, back/forward, a loop toggle, and a speed control.
Drag the timeline (or left-drag directly on a chart plot) to move the playback cursor; the charts,
spy, and image panes all update to show the data at that point.
On a Topic Chart, each series' value at the cursor is shown next to its entry in the legend, so
as you scrub, the legend reads out the value of every series at the current playback point.

.. figure:: /rst/figures/screenshots/offline_pro.png
    :align: center

See :ref:`offline_mode` for the full list of playback controls and which panes are available while
inspecting a recording.
