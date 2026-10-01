.. include:: ../exports/alias.include
.. include:: ../exports/roles.include

.. _chart_panel_index:

##########
Main Panel
##########

The central panel has tabs for multiple views, and a collapsed menu that reports the
problems detected on the DDS entities.

The main feature of *DDS Monitor* is plotting the monitored data in the *Chart View*.
DDS entities have different types of data (called *DataKind*) that you can visualize by configuring
a *Chart*.
For example, a chart can show the mean, median and standard deviation of the latency between two machines (*Hosts*)
running *Fast DDS* applications over two hours, in intervals of ten minutes.

*DDS Monitor* can also show the detected entities in a graph.
The *Domain view* shows all entities that belong to the same DDS Domain and the hierarchy of the
physical and DDS entities (the DataWriters or DataReaders that belong to a DomainParticipant, the
DomainParticipants that run on the same Process, the Processes that a User is running, and the Users that are on a
Host).
Each level is drawn as a box that contains the entities below it.
Arrows show the connections between endpoints that publish or subscribe to a Topic.
For a publication, the arrow goes from the DataWriter to the Topic; for a subscription, it goes from the Topic to
the DataReader.

.. thumbnail:: /rst/figures/screenshots/shapes_domain.png
    :align: center

Filtering the graph by Topic shows only the entities whose endpoints publish in, or subscribe to, the selected
Topic. The filtered graph opens in a new Tab.

.. thumbnail:: /rst/figures/screenshots/shapes_topic.png
    :align: center

From the *Domain view* you can also open the data type IDL of each Topic,
and inspect its live data with a :ref:`Spy Topic View <spy_view>` via the **Spy topic data**
right-click option.

.. thumbnail:: /rst/figures/screenshots/IDL_img.png
    :align: center

Right-clicking the IDL view opens a context menu with options to copy the selected text from the
IDL to the clipboard (or the full IDL if nothing is selected), select the full text, or copy the title to the
clipboard. For a ROS 2 type, the type IDL and name are shown demangled by default, and a sign in the
upper-right corner of the IDL view says so. View->Revert ROS 2 Demangling reverts the demangling and shows the
IDL of the type as received by the monitor. View->Perform ROS 2 Demangling applies the demangling again.

.. thumbnail:: /rst/figures/screenshots/IDL_demangled_context_menu.png
    :align: center

Problems reported by DDS entities are grouped by entity in the Problem Summary section at the bottom of the
layout. Each problem counter describes the problem and, in some cases, links to the relevant documentation.

.. thumbnail:: /rst/figures/screenshots/problem_detail.png
    :align: center

*DDS Monitor Pro* adds further pane types for visualizing live topic data:

* :ref:`Topic Charts <topic_charts>` |Pro| for plotting live numeric values from any DDS topic as a :ref:`Time Series Topic Chart <time_series>`, including :ref:`XY Charts <xy_charts>` for scatter plots of one field against another.
* :ref:`Dockable Spy Pane <dockable_spy_pane>` |Pro| turns the :ref:`Spy Topic View <spy_view>` into a freely positionable, splittable pane that can be opened multiple times at once.
* :ref:`Image Pane <image_pane>` |Pro| for rendering live image data from DDS topics directly in the workspace.

.. toctree::
    :maxdepth: 2

    /rst/user_manual/chart_panel/chart_panel
    /rst/user_manual/chart_panel/historic_series
    /rst/user_manual/chart_panel/dynamic_series
    /rst/user_manual/chart_panel/chartbox
    /rst/user_manual/chart_panel/problem_summary
