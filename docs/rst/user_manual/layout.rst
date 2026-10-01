.. include:: ../exports/alias.include

.. _layout:

######
Layout
######
This section describes the Graphical User Interface (GUI) of the *DDS Monitor* application: its main menus and
windows, and where to find each button and piece of information.
The screenshot below shows *DDS Monitor* running.

.. thumbnail:: /rst/figures/screenshots/App_run.png
    :align: center

.. _application_menu_layout:

Application Menu
================
This menu contains all the options of the application, in four groups:

- **File**: General purpose buttons.
- **Edit**: Specific buttons with application functionality.
- **View**: Window layout configuration.
- **Help**: Useful links for getting application information or support.

.. figure:: /rst/figures/screenshots/application_menu.png
    :align: center

These buttons are explained in the section :ref:`application_menu`.

.. _shortcuts_bar_layout:

Shortcuts Bar
=============
This horizontal bar has shortcuts to the main operations of the application.
You can configure it in the *View* tab of the application menu.

.. figure:: /rst/figures/screenshots/shortcuts_bar.png
    :align: center

How to configure this bar is explained in the section :ref:`shortcuts_bar`.

.. _left_sidebar_layout:

Explorer Panel
==============
This panel shows the entities discovered by the monitor, in interactive lists that you can expand or collapse.
Click an entity to see its information in this same panel.

The number of subpanels can change.
The available subpanels are the :ref:`dds_panel_layout`, the :ref:`physical_panel_layout`,
the :ref:`logical_panel_layout` and the :ref:`info_panel_layout`.
Each subpanel shows the discovered entities of one kind.
The kinds of entities and their categories are described in :ref:`entities`.

To show or hide subpanels, use the ``...`` button in the upper bar of the panel and
select them.
To resize this sidebar, drag its border.
To hide the whole left sidebar, click *Hide Left sidebar* in the *View* menu.

For more information about what is an entity and how they are organized refer to :ref:`entities`.
For more information about what it means to select an entity refer to :ref:`selected_entity`.

.. figure:: /rst/figures/screenshots/explorer_panel.png
    :align: center
    :scale: 50 %

.. _dds_panel_layout:

DDS Panel
---------
This subpanel shows the :ref:`dds_entities` of the monitor.
These entities are the DDS *DomainParticipant*, the DDS *DataReader* and *DataWriter*, and the transport *Locators* that
each entity is using.
This subpanel shows only the DDS entities related to the currently selected entity,
so some DDS entities discovered by the monitor may not appear in it at a given moment
(see :ref:`selected_entity` for further details).

.. figure:: /rst/figures/screenshots/dds_panel.png
    :align: center

These entities and how to interact with them are explained in the section :ref:`dds_panel`.

.. _physical_panel_layout:

Physical Panel
--------------
This subpanel shows the physical entities discovered by the monitor.
There are three kinds of physical entities: *Host*, *User* and *Process*.
They describe the machine and the context where an application using
*Fast DDS* is running.
These entities and how to interact with them are explained in the section :ref:`physical_panel`.

.. figure:: /rst/figures/screenshots/physical_panel.png
    :align: center

.. _logical_panel_layout:

Logical Panel
-------------
This subpanel shows the abstract entities of a DDS communication network discovered by the monitor:
*Domain* and *Topic*.
They are abstract partitions of a DDS network. Only entities in the same *Domain* can communicate
with each other, by publishing or subscribing in the same *Topic*.
These entities and how to interact with them are explained in the section :ref:`logical_panel`.

.. figure:: /rst/figures/screenshots/logical_panel.png
    :align: center

.. _info_panel_layout:

Entity Info Panel
-----------------
This subpanel shows information about the last entity clicked, in two tabs.
The ``info`` tab has its general information, and
the ``Statistics`` tab has a summary of its main statistical data.

.. _info_subpanel_layout:

Info Panel
^^^^^^^^^^
This panel shows the main information of the last entity clicked.
The information depends on the kind of entity: for a *DDS Entity* it shows
the *QoS*, while for a *Process* it shows its *process id*.

.. figure:: /rst/figures/screenshots/Info_panel.png
    :align: center

This information is explained in the section :ref:`info_panel`.

.. _statistics_panel_layout:

Statistics Panel
^^^^^^^^^^^^^^^^
This panel shows a summary of the main statistical data of the last entity clicked.

.. figure:: /rst/figures/screenshots/statistics_panel.png
    :align: center

This information is explained in the section :ref:`statistics_panel`.

.. _alerts_panel_layout:

Alerts Panel
============

This panel shows the alerts you have created to monitor specific events in the DDS network.

.. figure:: /rst/figures/screenshots/alert_panel.png
    :align: center

This information is explained in the section :ref:`alerts_panel`.

.. _alert_list_layout:

Alert List
----------

This panel lists the alerts you have created to monitor specific events in the DDS network.
To create an alert, click the |create_alert| button in the Shortcuts Bar or the
*+* symbol in the upper right corner of the panel.
To remove an alert, right-click it and select the remove option.

.. _alert_data_layout:

Info
----

This panel shows the configuration values of the alert selected in the *Alert List*, including the
alert name, its domain, the values of host, user and topic of the monitored entities, its threshold
or the duration of the alert.

.. _monitor_status_panel_layout:

Monitor Status Panel
====================

This panel shows data about the monitored entities and the current state of the application.
It has two subpanels, the :ref:`status_panel_layout` and the
:ref:`log_panel_layout`. To switch between them, click the name of the subpanel you want to see.

To resize this sidebar, drag its border.
To hide the whole left sidebar, click *Hide Left sidebar* in the *View* menu.

.. _status_panel_layout:

Status Panel
------------

This panel shows data about the current state of the application:

- Entities is the number of entities being monitored in the user application.

- Domains lists the *Domains* that have been initialized in the Monitor.

.. figure:: /rst/figures/screenshots/status_panel.png
    :align: center

This information is explained in detail in the section :ref:`status_panel`.

.. _log_panel_layout:

Log Panel
---------

This panel shows the callbacks the application has received for events in the monitored DDS network.
You can clear them with the :ref:`clear_log` button.
A callback may refer to:

- The discovery of a new Entity in the DDS network.

- The reception of new data related to any of the entities that are being monitored.

.. figure:: /rst/figures/screenshots/log_panel.png
    :align: center

This information is explained in detail in the section :ref:`log_panel`.

.. _issues_panel_layout:

Issues Panel
============

This panel lists the error events of the application.
In the current version, the application reacts to these events:

- Attempt to start a new monitor while another one is already active (the free version supports only one).

.. figure:: /rst/figures/screenshots/issues_panel.png
    :align: center

This information is explained in detail in the section :ref:`issues_panel`.

.. _alert_messages_panel_layout:

Alert Messages Panel
====================

This panel lists the alert events the application has detected, based on the alerts you have created.
They are shown as a tree, with the most recent alerts at the bottom.

.. figure:: /rst/figures/screenshots/alert_messages_panel.png
    :align: center

.. _main_panel_layout:

Main Panel
==========
The central window has multiple tabs for different views.
It also has a collapsed menu with the problems detected on the DDS entities.
It can show the data charts you have configured, called *Chartbox*.
It can also show a domain graph of the physical, logical and DDS entities of a domain,
which shows how endpoints connect through the topics and the physical hierarchy of the entities.

.. figure:: /rst/figures/screenshots/main_panel.png
    :align: center

How to create a chart is explained in the section :ref:`chart_panel`.

.. _chartbox_layout:

Chartbox
--------
These windows in the main panel hold *series* (*data configurations*) that show a specific data type for
one or several entities over a time interval, with different accumulative operations on the data.

To create a new *Chartbox*, go to *Chart View* in the default tab of the Main Panel and click the *Create new chart*
button.
You can then add, remove or modify series in the new *Chartbox*.

You can move *Chartboxes* within the *Chart View* tab.
To move one, click its title and drag it to the new location
inside the main panel.
The other *Chartboxes* rearrange automatically.

.. thumbnail:: /rst/figures/screenshots/chartbox.png
    :align: center

How to create a chart is explained in the section :ref:`chart_panel`.

.. _create_new_series_layout:

Create Series Dialog
^^^^^^^^^^^^^^^^^^^^
This dialog appears every time you create a new Chartbox, or add a new series from the Chartbox menu
*Series->Add series*.

.. figure:: /rst/figures/screenshots/Create_series_historical.png
    :align: center

    Create historical series dialog

.. figure:: /rst/figures/screenshots/Create_series_dynamic.png
    :align: center

    Create real-time series dialog

How to configure a new series is explained in :ref:`historic_series` for historic data and
:ref:`dynamic_series` for dynamic data.

.. _domain_graph:

Domain View
-----------
This view in the main panel shows the connections between DataWriters and DataReaders that belong to the same
DDS Domain.
Each endpoint is drawn inside its physical entities (see :ref:`entities` relationship), and connected
to the topic it publishes on or subscribes to.

.. thumbnail:: /rst/figures/screenshots/domain_graph.png
    :align: center

Click any entity to see its detailed information in the :ref:`info_panel`.
Right-click an entity to change its alias or to filter the problems to show only that entity's problems.
For topics, the right-click menu can also filter the domain graph so that only the entities related to the selected
topic are shown.

The right-side configuration panel |Pro| has per-entity visibility controls for the graph.
Individual topics, hosts, users, processes, participants, writers, and readers can be shown or hidden
by alias, with bulk *Show All* and *Hide All* actions.
See :ref:`domain-graph` for details.

.. _problem_summary:

Problem summary
---------------

This collapsible section shows all the collected problems per entity.
Examples are DataReader samples lost, incompatible QoS between endpoints, or the DataWriter deadline missed
counter.

Entities that have reported a problem show a warning or an error icon next to the entity name, depending on
the severity of the problem.
The entity representation in the domain graph may also display that icon.

.. thumbnail:: /rst/figures/screenshots/problem.png
    :align: center
