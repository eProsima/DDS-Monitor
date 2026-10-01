.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _workspace:
.. _workspace_saving:
.. _workspace_restoring:
.. _workspace_what_is_saved:

################################
Workspace Save and Restore |Pro|
################################

*DDS Monitor Pro* can save the complete visual state of a monitoring session to a file and
reload it in a later session, so you can resume where you left off without reconfiguring
monitors, layouts, charts, and alerts.

Saving a Workspace
==================

To save the current workspace, do one of the following:

- Click the |save| button at the right end of the tab bar.
- Press **Ctrl+S**.
- Go to **File -> Save Workspace as...**.

**Save Workspace as...** always opens a file dialog to choose the destination folder and file name.
The |save| button and **Ctrl+S** save directly to the current workspace file (the last one saved or
loaded), and only open the file dialog when no workspace file has been chosen yet.
An existing file at the selected path is overwritten.
Saving is not available in :ref:`offline mode <offline_mode>`.
The workspace is saved as a JSON file with the ``.fdmw`` (*DDS Monitor Workspace*) extension.

Restoring a Workspace
=====================

To load a saved workspace, click **File** in the menu bar and choose **Load Workspace...**

A file dialog opens. Select the ``.fdmw`` file you want to load. The application validates the file before
applying it and shows an error for malformed files. Unknown properties in the file are ignored, so
workspace files from newer versions open in older builds without failing. Values outside valid ranges
are clamped or ignored instead of stopping the load.

When loading, the following data is cleared before the workspace is applied: DDS entity lists, alert
status information, status logs, issues, problems found, and alert messages. Monitors then start
fresh and the rest of the workspace state is rebuilt on top of them.

.. note::

    If a saved workspace references a DDS domain or Discovery Server that is not reachable at load time, that monitor opens in a waiting state and its panes populate as entities are discovered.

The statistics backend is always reset on load.
Entities are resolved by type and name instead of by entity IDs, which are volatile and change between
runs, so workspaces stay portable across runs.

What Gets Saved
===============

The workspace file stores the complete visual state of the application, grouped as follows.

**Application settings**

* Theme selection (light or dark). A workspace without a saved theme follows the operating system
  color scheme.
* Show or hide proxy entities, inactive entities, and metatraffic.
* :ref:`ROS 2 Demangling <ros2_demangling>` state (reverted or applied).
* Toolbar visibility and which buttons are shown in the shortcuts toolbar.
* Left sidebar visibility and which buttons are shown in it.
* Alerts polling time and scheduler configuration.
* The active :ref:`statistics readers <statistics_readers_panel>`, so the same statistics are
  collected when the workspace is reloaded.

**Left sidebar**

* The selected icon and the active sub-category within it (for example, the Log tab inside
  :ref:`Monitor Status <pro_status_panel>`).
* Width ratio of the left sidebar.
* All configured alert rules.

**Bottom bar**

* Whether the bottom bar is open, collapsed, or fully closed.
* Its height ratio.
* The selected sub-tab (Problems or Alerts).
* The problem that is currently being filtered.

**Main panel**

* All open monitor tabs, the selected tab, and the tab order.
* Each monitor is identified by its type and connection parameters: domain number for regular monitors,
  Discovery Server locator for DS monitors, and the XML profile file path for XML-configured monitors. All
  three monitor types are restored on load.
* Created entity aliases within each :ref:`domain view <pro_domain_view>`.
* Active topic filter applied to each :ref:`domain graph view <pro_domain_graph>`.
* Entity visibility settings (shown/hidden per alias) for each :ref:`domain graph view <pro_domain_graph>`.

:ref:`Statistics Charts <pro_chart_view>`

For each statistics chart pane:

* Data kind, time window, update period, and maximum data points.
* For each series: source and target entity (resolved by type and name), statistics kind, label, color,
  visibility, max data points, and whether cumulative mode was active.
* Chart name, legend visibility, pause state, expand state, and whether data points are shown.
* Y-axis settings (and X-axis settings for historic charts).

:ref:`Image Panes <image_pane>`

* The subscribed topic name and domain number.
* Whether the pane was active (streaming) or paused when saved. On load, the pane reconnects by topic
  name and domain, because the topic entity ID is volatile.
* Any :ref:`custom image topic mappings <image_pane_custom_topic>` defined in the session (the mode
  and the field-path or fixed-value mapping for each configured topic). Mappings are restored globally
  and re-validated against each topic's type when it is next used, so custom-mapped image panes reopen
  correctly even before their topic is rediscovered.

:ref:`Spy Panes <dockable_spy_pane>`

* The subscribed topic and domain.
* Whether the pane was paused or running.

:ref:`Topic Charts <topic_charts>`

For each topic chart pane:

* Domain, time window, and maximum data points.
* For each series: topic name, field path, max data points, label, color, and visibility.
* Chart name, legend visibility, pause state, expand state, and whether data points are shown.
* Y-axis lock and range (X-axis lock and range are not saved).

:ref:`Custom Series <custom_series_panel>`

* All :ref:`custom series <custom_series_panel>` defined in the session, including each series' name,
  its data-source bindings, global variables, and JavaScript formula. Custom series are saved with the
  workspace whether or not they are plotted on any chart. They can also be exported to and imported
  from a separate ``.json`` file, independently of the workspace.

:ref:`Publisher Panes <publisher_pane>`

* The target topic name and domain number. On load, the pane resolves the topic from this stable pair
  instead of the volatile entity identifier.
* The complete map of form values entered by the user, keyed by field path. Values are captured at
  save time, so unpublished edits are kept. The element count of every variable-length sequence and
  map, and the active branch of every union, are also saved, so the form reopens in the same shape.
* The per-field slider minimum and maximum bounds for every numeric scalar field.
* The continuous-mode toggle state and the configured interval in milliseconds.

:ref:`IDL Panes <dockable_idl_pane>`

* The topic name and domain being viewed, so the pane reopens showing the same
  type definition on load.

:ref:`Register Type Panes <register_type>`

* The IDL contents and the type name it is registered under, so the pane reopens with the same
  definition on load.
* Registered type definitions are also restored to the backend when the workspace is loaded, so
  types registered before saving stay available for spying, publishing, and charting during the
  session, even for topics that are not yet discovered.

:ref:`Pane layouts <dockable_panes>`

* The full split tree for each monitor tab, including the type of every pane, its position, and the
  width and height ratios of all dividers.
