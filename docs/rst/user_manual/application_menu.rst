.. include:: ../exports/alias.include

.. _application_menu:

################
Application Menu
################

This section describes the operations available in the *DDS Monitor* application menu.

.. _application_menu_file:

File
====

.. note::
    The free version of *DDS Monitor* supports only **one active monitor** at a time.
    Initializing a second monitor shows an error message.

.. _init_monitor_button:

Initialize DDS Monitor
----------------------

Starts monitoring a new DDS network.
The monitor discovers the entities of this network automatically, and builds and displays their connections,
their configuration and the statistical data they report, so you can query them later.

Section :ref:`monitor_domain` explains what monitoring a domain means in the
context of the application.

This button opens a dialog that asks for the DDS Domain number, between 0 and 232.
The monitor then starts in that DDS domain and discovers its entities automatically.

.. note::
    If the monitor cannot be initialized in the selected Domain, an error message appears
    and an issue is added to the :ref:`issues_panel`. Select ``Retry`` to
    choose a different Domain.

Initialize Discovery Server Monitor
-----------------------------------

Starts monitoring a new DDS network.
The monitor discovers the entities of this network automatically, and builds and displays their connections,
their configuration and the statistical data they report, so you can query them later.

Section :ref:`monitor_domain` explains what monitoring a domain means in the
context of the application.

This button opens a dialog where you add one or more Discovery Server
locators to connect to. In each locator row, choose a transport protocol (``UDPv4``, ``UDPv6``,
``TCPv4`` or ``TCPv6``) from a dropdown and enter the **IP** and **Port** in separate fields.
You can add or remove locator rows freely before starting the monitor.

*DDS Monitor* then connects to the Discovery Servers listening on those addresses
and gets all the discovery information of the entities connecting through them.

.. note::
    If the monitor cannot be initialized with the given *Discovery Server* locators, an error message
    appears and an issue is added to the :ref:`issues_panel`. Select ``Retry`` to
    set different locators.

.. _init_monitor_with_profile_button:

Initialize DDS Monitor with Profile
------------------------------------

Starts monitoring a new DDS network using a *Fast DDS* XML profile to configure the monitor's own
DomainParticipant (e.g. to set a custom transport, discovery configuration, or other QoS).
This button opens a dialog where you select a previously loaded DDS profile from a dropdown, or upload new
XML profile files. The DDS Domain to monitor comes from the selected profile, so you do not enter it manually.

Export Charts to CSV
--------------------

Export all the data displayed in the current DDS Monitor session to a CSV file.
The format of the generated CSV file is described in section :ref:`export_data`.

.. _dump_button:

Dump
----

Dump the information from the database to a JSON file.
The format of the generated JSON file is described in section :ref:`export_data`.

.. _dump_clear_button:

Dump and clear
--------------

Same as **Dump**, but also clears the statistics data of all the entities.

Quit
----

Close the application.

.. _edit_menu:

Edit
====

.. _display_historic_data_button:

Display Historical Data
-----------------------
Create a new historic *Chartbox* in the :ref:`chart_panel_index`.
How to configure a historic *Chartbox* is explained in the section :ref:`historic_series`.

.. _display_dynamic_data_button:

Display Real-Time Data
----------------------
Create a new dynamic *Chartbox* in the :ref:`chart_panel_index`.
How to configure a dynamic *Chartbox* is explained in the section :ref:`dynamic_series`.

.. _create_alert_menu_button:

Create Alert
------------
Opens the *Add alert* dialog, the same one opened by the |create_alert| button in the :ref:`shortcuts_bar`.
In this dialog you select the alert kind, name, domain, host, user and topic to watch, as well as the
threshold, the time between alerts, the alert timeout and, optionally, a script to execute when the alert triggers.
See section :ref:`alerts_panel` for more information.

.. _clear_inactive_entities:

Delete inactive entities
------------------------

Removes all the inactive entities from the database.

.. _delete_statistics_data:

Delete statistics data
----------------------

Clears the statistics data of all the entities.

.. _schedule_delete:

Scheduler Configuration
-----------------------

Opens a dialog where you create a schedule to dump the database to a file, remove old data and/or remove
inactive entities at a specified interval.

.. _alerts_configuration:

Alerts Configuration
--------------------

Opens a dialog where you edit the notification and alert system settings.

.. _refresh_button:

Refresh
-------
Resets the clicked entity and the entity models, for when an entity is missing from the display.

.. _clear_log:

Clear Log
---------
Clears the callbacks log.

.. _clear_issues:

Clear Issues
------------
Clears the issues log.

.. _view_menu:

View
====

Hide/Show Proxy Entities
------------------------
Proxy entities are entities from other domains whose statistics reach the monitor's domain.
This button hides or reveals the proxy entities currently detected by the monitor. They are hidden by default.
When they are shown, you can access their data. When they are hidden, they are not available anywhere in the
application, so you cannot plot charts with their data.

Hide/Show Inactive Entities
---------------------------
This button hides or reveals the currently inactive entities detected by the monitor.
When they are shown, you can access their data. When they are hidden, they are not available anywhere in the
application, so you cannot plot charts with their data.

.. _hide_show_metatraffic:

Hide/Show Metatraffic
---------------------
Entities used for sharing metatraffic data are not shown by default.
These include the Fast-DDS Statistics module topics, the topics ROS uses for metatraffic data exchange, and the
endpoints bound to these topics.
As with inactive entities, hidden metatraffic entities are not available anywhere in the application.
This button shows or hides the metatraffic entities detected by the monitor.

Revert/Perform ROS 2 Demangling
-------------------------------
By default, ROS 2 types are demangled to recover the original type name and IDL representation in IDL view, which
improves compatibility with FastDDS Gen IDL use. Demangled IDLs in IDL view show a sign in the corner.
When this feature is disabled, ROS 2 types are shown as the monitor receives them. This button
reverts or performs the demangling.

Dashboard Layout
----------------
Changes the size of the chart boxes displayed in the :ref:`chart_panel_index` of the application.
There are three mutually exclusive layouts:

* |dashboard_layout_1| **Large**: A single full-screen chart is displayed.
* |dashboard_layout_2| **Medium**: Two chart boxes per row.
* |dashboard_layout_3| **Small**: Three chart boxes per row.

Hide/Show Shortcuts Toolbar
---------------------------
Hides the upper shortcuts toolbar if visible, or reveals it otherwise.

Customize Shortcuts Toolbar
---------------------------
Shows or hides each shortcut button in the shortcut toolbar.

Hide/Show Left sidebar
----------------------
Hides the left sidebar if visible, or reveals it otherwise.

Customize Left Sidebar
----------------------
Shows or hides each panel in the :ref:`left_panel`.

Help
====

Documentation
-------------

Link to this documentation.

Release Notes
-------------

Link to the `Releases <https://github.com/eProsima/DDS-Monitor/releases>`_ section of the
`GitHub DDS Monitor repository`_.

Join Us on LinkedIn
-------------------
Link to `eProsima LinkedIn account <https://www.linkedin.com/company/eprosima>`_.

Search Feature Requests
-----------------------
Link to the `Issues`_ section of the `GitHub DDS Monitor repository`_.

Report Issue
------------
Link to create a new Issue in the `Issues`_ section of the `GitHub DDS Monitor repository`_.

About
-----
General information of the currently running *DDS Monitor* application.

.. _GitHub DDS Monitor repository: https://github.com/eProsima/DDS-Monitor
.. _Issues: https://github.com/eProsima/DDS-Monitor/issues
