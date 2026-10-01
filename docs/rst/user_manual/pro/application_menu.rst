.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _pro_application_menu:

################
Application Menu
################

The application menu bar gives access to all operations in *DDS Monitor Pro*.
It has five groups: **File**, **Edit**, **Add**, **View**, and **Help**.

.. figure:: /rst/figures/screenshots/application_menu_pro.png
    :align: center

.. _pro_application_menu_file:

File
====

The **File** menu contains actions for starting and stopping monitors, exporting data, saving and
restoring workspaces, and closing the application.

.. _pro_init_monitor_button:

**Initialize DDS Monitor**
    Opens a dialog to start monitoring a DDS Domain by number (0-232).
    The monitor then discovers all DDS entities in that domain and collects their connections,
    configuration, and statistical data in real time.
    See :ref:`monitor_domain` for details.
    Initializing a domain that is already being monitored shows an error and adds an entry
    to the :ref:`pro_issues_panel`; select **Retry** in the error dialog to choose a different domain.

**Initialize Discovery Server Monitor**
    Opens a dialog to start monitoring a DDS network via one or more *Fast DDS Discovery Servers*.
    Enter the server addresses as a semicolon-separated list of ``ip:port`` pairs.
    The monitor connects to the servers and collects all discovery information for the entities
    communicating through them.
    See :ref:`monitor_domain` for full details.
    Starting a monitor on an already-initialized Discovery Server shows an error and an entry in the
    :ref:`pro_issues_panel`.

**Initialize DDS Monitor with Profile**
    Opens a dialog to start monitoring using a DDS XML profiles file.
    Select the XML file and then choose the profile that defines the DDS configuration to use.
    See :ref:`add_monitor_using_dds_xml_profiles` for step-by-step instructions.

.. _pro_open_recording:

**Open Recording...** |Pro|
    Opens a previously captured DDS recording (an ``.mcap`` or SQLite ``.db`` file) for offline
    inspection, without connecting to a live DDS network. A playback bar with timeline controls appears
    at the bottom of the window.
    See :ref:`offline_mode` for details.

.. _pro_stop_monitor:

**Stop Monitor** |Pro|
    Opens a submenu listing every domain currently being monitored.
    Selecting a domain stops monitoring it: its panes and charts remain open but become inactive,
    and the domain is no longer tracked.
    This reverses *Initialize DDS Monitor*. Use it to switch between domains or to free the resources
    of a domain you no longer need.

**Save Workspace as...** |Pro|
    Opens a file dialog to save the current session to a new workspace file.
    The |save| button and **Ctrl+S** save to the current workspace file instead, and only open the
    dialog when no workspace file has been chosen yet.
    Not available in :ref:`offline mode <offline_mode>`.
    See :ref:`workspace` for details, including what gets saved.

**Load Workspace...** |Pro|
    Restores a previously saved session from a ``.fdmw`` file.
    See :ref:`workspace` for details on the restore behavior.

.. _pro_export_custom_series:

**Export Custom Series...** |Pro|
    Saves every defined :ref:`Custom Series <custom_series_panel>` to a ``.json`` file so the
    definitions can be reused in another session or on another machine.

**Import Custom Series...** |Pro|
    Loads :ref:`Custom Series <custom_series_panel>` definitions from a ``.json`` file previously
    written with *Export Custom Series...*.

.. _pro_export_data:

**Export Charts to CSV**
    Exports chart data from the current session to a CSV file.
    There are three export scopes:

    * **Single series** - export from the series context menu inside the Chartbox.
    * **All series in a Chartbox** - click **Export to CSV** in the **ACTIONS** section of the chart's
      :ref:`right_pane_config` sidebar.
    * **All series in all Chartboxes** - export everything at once with this menu item.

    The exported CSV file has this structure:

    .. list-table::
        :header-rows: 3

        *   -
            - <Chartbox name>
        *   - ms
            - <DataKind units>
        *   - UnixTime
            - <Series name>
        *   - <unix_time>
            - <data_value>

.. _pro_dump_button:

**Dump**
    Dumps the full contents of the statistics database to a JSON file without modifying the stored
    data.
    The JSON file holds all entity statistics collected since the session started, so you can keep a
    snapshot of the session for offline analysis or archiving.

.. _pro_dump_clear_button:

**Dump and Clear**
    Same as **Dump**, but also clears all accumulated statistics data for every entity after saving.
    Use it to reset statistics and still keep a record of the session. It suits long-running sessions
    that need periodic snapshots without the in-memory database growing indefinitely.

**Quit**
    Closes the application.

.. _pro_edit_menu:

Edit
====

The **Edit** menu contains actions for managing the data in the current session: cleaning up
entities, clearing statistics, configuring alerts, scheduling maintenance tasks, and resetting the
display.

.. _pro_clear_inactive_entities:

**Delete Inactive Entities**
    Removes all entities that are no longer active from the database.
    Inactive entities are those that have stopped publishing or have been undiscovered.
    Removing them frees memory and cleans up the entity lists.

.. _pro_delete_statistics_data:

**Delete Statistics Data**
    Clears all accumulated statistics data for every entity without removing the entities themselves.
    The entities stay visible, but all their historical statistics are reset.

.. _pro_schedule_delete:

**Scheduler Configuration**
    Opens a dialog to configure a recurring schedule for automatic database dumps, statistics data
    removal, and/or inactive-entity cleanup.
    Use it in long-running monitoring sessions that need periodic housekeeping.

.. _pro_alerts_configuration:

**Alerts Configuration**
    Opens the *Alerts Configuration* dialog to set the **Polling time (ms)**, which is how often
    alert timeouts are checked.
    Alert rules are created and edited in the :ref:`pro_alert_configuration_panel` of the
    left sidebar.

.. _pro_refresh_button:

**Refresh**
    Resets the currently selected entity and rebuilds the entity models from the current database
    state. Also available with the **Ctrl+R** keyboard shortcut.
    Use it if entities seem to be missing from the Explorer Panel or the display looks out of sync.

.. _pro_clear_log:

**Clear Log**
    Clears all entries from the callbacks log in the :ref:`pro_log_panel`.
    Only the log display is cleared; the underlying data is not affected.

.. _pro_clear_issues:

**Clear Issues**
    Clears all entries from the :ref:`pro_issues_panel`.
    The underlying issues are not resolved, only removed from the panel.

.. _pro_add_menu:

Add |Pro|
=========

The **Add** menu opens new panes or views in the workspace.
Each pane can be docked, split, or floated anywhere in the layout.

.. _pro_display_historic_data_button:
.. _pro_display_dynamic_data_button:

**Add Topic Chart** |Pro|
    Opens a new :ref:`Time Series Chart <time_series>` pane that plots raw numeric values from any
    user-defined DDS topic against time, updated live as samples arrive.
    Series from different topics can be overlaid on the same chart.
    XY (scatter) mode is available in the chart configuration.
    See :ref:`topic_charts` for details.

**Add Statistics Chart**
    Opens a new statistics *Chartbox* for plotting pre-computed DDS metrics such as latency,
    throughput, and packet counts.
    Then choose between a historical chart (past time range) or a real-time chart
    (live updates as samples arrive).
    See :ref:`historic_series` for historical configuration and :ref:`dynamic_series` for real-time.

**Add Topic Spy**
    Opens a new :ref:`Dockable Spy Pane <dockable_spy_pane>` that subscribes to a selected DDS topic
    and shows each incoming sample as an expandable field tree in real time.
    Use it to check message content and inspect raw field values as they are published.
    See :ref:`Dockable Pane Workspace <dockable_panes>` for details.

**Add Topic Type (IDL)**
    Opens a pane showing the full IDL type definition of a selected DDS topic, including the complete
    struct hierarchy, field names, and type annotations.
    The IDL text can be copied to the clipboard.
    ROS 2 types are shown demangled by default (toggle with **View → Revert ROS 2 Demangling**).

**Add Image Display** |Pro|
    Opens a new :ref:`Image Pane <image_pane>` that renders live image data streamed over a
    DDS topic inside the monitor.
    It supports ROS 2 ``sensor_msgs`` and *eProsima Fast DDS* image types, and can be configured to
    read image data from an arbitrary topic (see :ref:`image_pane_custom_topic`).
    See :ref:`image_pane` for details.

**Add Topic Publisher** |Pro|
    Opens a new :ref:`Publisher Pane <publisher_pane>` for composing and publishing DDS samples on any
    discovered topic.
    The form is generated from the topic's dynamic type and supports one-shot and
    continuous publishing.
    See :ref:`publisher_pane` for details.

**Add Type Registration** |Pro|
    Opens a new :ref:`Register Type <register_type>` view for registering a user-supplied data type
    from its IDL definition, so it can be used for spying, publishing, and charting on topics whose
    type was never discovered on the network.
    See :ref:`register_type` for details.

**Create Alert**
    Opens the alert creation form in the :ref:`pro_alerts_panel` of the left sidebar, to define a
    new alert rule based on a DDS statistic threshold.
    The new alert appears in the :ref:`pro_alerts_panel` and triggers notifications when the
    configured condition is met.

.. _pro_view_menu:

View
====

The **View** menu controls the visibility and appearance of entities and panels in the application,
including entity filters, sidebar layout, theming, and the shortcuts toolbar.

**Hide/Show Proxy Entities**
    Toggles the display of proxy entities: entities from other DDS domains whose statistics messages
    reach the monitor's domain.
    When hidden, proxy entities are completely unavailable in the application, including in charts.
    Proxy entities are hidden by default.

**Hide/Show Inactive Entities**
    Toggles the display of inactive entities: entities that have been discovered but are no longer
    active in the DDS network.
    When hidden, inactive entities are unavailable in the application, including in charts.

.. _pro_hide_show_metatraffic:

**Hide/Show Metatraffic**
    Toggles the display of metatraffic entities.
    Metatraffic entities include *Fast DDS* Statistics module topics, ROS discovery topics, and all
    endpoints bound to them.
    They are hidden by default.
    When hidden, metatraffic entities are completely unavailable in the application.

**Revert/Perform ROS 2 Demangling**
    By default, ROS 2 type names and IDL representations are demangled to match the original ROS 2
    type definitions and improve compatibility with *Fast DDS Gen*.
    Demangled IDL views are marked with a badge in the corner.
    This option turns demangling on or off for all IDL views.

**Theme** |Pro|
    Opens a submenu with two mutually exclusive entries, **Light** and **Dark**, to switch palettes.
    The selected theme applies to all panels, charts, icons, and dialogs.
    See :ref:`theming` for details.

**Hide/Show Shortcuts Toolbar**
    Hides or reveals the shortcuts toolbar at the top of the window.

**Customize Shortcuts Toolbar**
    Opens a dialog to show or hide each button in the shortcuts toolbar.
    The toolbar has shortcuts to the main functions of the *DDS Monitor Pro* application.

    The icons in the shortcut bar are:

    * |historical_chart| - Display historical data.
    * |dynamic_chart| - Display real-time data.
    * |create_alert| - Open the create alerts panel.
    * |refresh| - Refresh DDS Monitor.
    * |clear_log| - Clear the list of logs.
    * |clear_issues| - Clear the issues panel.

**Hide/Show Left Sidebar**
    Hides or reveals the entire left sidebar.

**Customize Left Sidebar**
    Opens a submenu with checkable entries (**DDS Entities**, **Physical**, **Logical**, and
    **Entity Info**) to show or hide each sub-panel within the :ref:`pro_left_panel`.

Help
====

The **Help** menu has links to documentation, release notes, community resources, and
application information.

**Documentation**
    Opens this documentation in the default browser.

**Release Notes**
    Opens the `Releases <https://github.com/eProsima/DDS-Monitor/releases>`_ page of the
    `GitHub DDS Monitor repository`_ in the default browser.

**Join Us on LinkedIn**
    Opens the `eProsima LinkedIn page <https://www.linkedin.com/company/eprosima>`_ in the default
    browser.

**Request a Feature**
    Opens a prefilled email to eProsima support (``info@eprosima.com``) with the *DDS Monitor Pro*,
    *Fast DDS*, *Fast DDS Statistics Backend* and *Qt* versions and the operating system already
    included, so you can describe a feature request directly to the support team.
    Unlike the open-source application, *DDS Monitor Pro* does not use a public GitHub issue tracker
    for feature requests.

**Report Issue**
    Opens a prefilled email to eProsima support (``info@eprosima.com``) with the *DDS Monitor Pro*,
    *Fast DDS*, *Fast DDS Statistics Backend* and *Qt* versions and the operating system already
    included, so you can report a bug directly to the support team.
    Unlike the open-source application, *DDS Monitor Pro* does not use a public GitHub issue tracker
    for bug reports.

**About**
    Displays a dialog with information about the running *DDS Monitor Pro*
    application, including the version number and license information.

.. _GitHub DDS Monitor repository: https://github.com/eProsima/DDS-Monitor
.. _Issues: https://github.com/eProsima/DDS-Monitor/issues
