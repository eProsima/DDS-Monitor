.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _right_pane_config:

###################################
Right-Side Pane Configuration |Pro|
###################################

The *Right-Side Pane Configuration* panel is a sidebar that slides in from the right edge of the
workspace.
For chart, spy, IDL, image, and publisher panes, you use it to create new panes and edit the settings
of existing ones without opening a separate dialog.
When a Domain Graph tab is active, clicking the |gear| button opens the same sidebar with a dedicated
visibility control panel for managing which entities are displayed in the graph
(see :ref:`domain-graph`).

.. _right_pane_config_opening:

Opening the Panel
=================

Open the configuration panel in any of these ways:

* Click the |gear| button in the header of any existing pane to open the panel configured for that pane.
* Click a pane placeholder (a pane still being created) to return to its creation form.
* Use a context menu action that targets the panel, such as opening a new pane from the split menu on
  any pane header. The panel then opens programmatically.

To close the panel, click the **✕** button in its header.

.. _right_pane_config_layout:

Panel Layout
============

The panel has a fixed header at the top that is always visible when a pane is selected or a creation
flow is active.

**Header bar**

Shows the label *PANEL CONFIGURATION* and a close button on the right.

Below the header, the content area shows the configuration form specific to the open pane type and its
current mode.

.. _right_pane_config_modes:

Creation vs. Configuration Mode
================================

The panel works in one of two modes, depending on how it was opened.

In **creation mode**, the panel shows a wizard-style form for a pane type that does not yet exist. You
select the monitor, topic, and other required parameters, then confirm to create the pane. Creation forms
include a cancel button that discards the flow without affecting the workspace layout.

In **configuration mode**, the panel shows the live settings for an already-open pane.
Most settings apply as soon as you change them. The ones that rebuild the pane, such as its monitor, its
topic, or the chart type of a statistics chart, apply only when you click **Apply & Reset** or
**Apply & Reset Chart**, so you can change several of them first. Rebuilding a chart removes its series.

.. _right_pane_config_by_type:

Configuration by Pane Type
===========================

Each pane type shows a different set of sections in the configuration panel. The page of each pane
documents its sections in detail; the summaries below link to those pages.

.. _statistics_chart_config:

Statistics Chart
----------------

See :ref:`pro_chart_view` for the full statistics chart documentation.

The configuration panel for a statistics chart covers:

* Chart name editing.
* Chart type and data kind (plus the time range for historical charts), applied together with
  **Apply & Reset Chart**.
* Series list with per-series controls for label, color, visibility, max data points, and removal.
* An inline add-series form with entity and statistic selection.
* Time window, and X-axis and Y-axis locking with explicit minimum and maximum.
* Display toggles for the legend and data points, plus the update period and maximum data points for
  real-time charts.
* Pause/resume toggle.
* Actions with replace-split submenus, show and hide, and screenshot options.

.. figure:: /rst/figures/screenshots/config_stats_pro.png
    :align: center
    :width: 330px

.. _image-pane:

Image Display
-------------

See :ref:`image_pane` for the full image pane documentation.

The configuration panel for an image pane covers:

* A read-only **TOPIC** section showing the current topic name and domain.
* A **CHANGE TOPIC** section listing only image-compatible topics, with an **Apply & Reset** button.
* A **CUSTOM IMAGE TOPICS** section to map a non-standard topic as an image (see
  :ref:`image_pane_custom_topic`).
* A **PLAYBACK** toggle to start or stop the frame stream.
* A read-only **STATUS** indicator (Streaming, Waiting for frames, Paused, or Error).
* A **LAST ERROR** section visible only when a decode error has occurred.
* A **FRAME INFO** section showing resolution, encoding, and frame count once frames arrive.
* Actions with split submenus and screenshot options.

.. figure:: /rst/figures/screenshots/config_image_pro.png
    :align: center
    :width: 330px

.. _spy-pane:

Topic Spy
---------

See :ref:`dockable_spy_pane` for the full spy pane documentation.

The configuration panel for a spy pane covers:

* Monitor and topic selection with **Apply & Reset** to switch the subscription.
* Playback toggle to start or stop the live data feed.
* Actions to expand or collapse the sample tree, clear it, and copy the last sample as JSON.
* PANEL ACTIONS with replace-split submenus.

.. figure:: /rst/figures/screenshots/config_spy_pro.png
    :align: center
    :width: 330px

Time Series Topic Chart
-----------------------

See :ref:`topic_charts` for the full topic chart documentation.

The configuration panel for a topic chart covers:

* The **PLOT MODE** dropdown for choosing Time Series, Event Chart, or XY Chart.
* Chart name editing.
* Monitor selection, applied with **Apply & Reset Chart**.
* Series list with per-series controls for label, color, visibility, max data points, and removal.
* An inline add-series form with topic and numeric field selection. Click **Add Series** to expand it.
  Select a topic, wait for the first sample to arrive so fields are populated, then pick a field and
  confirm with **Add Series** or double-click the field.
* Time window, and X-axis and Y-axis locking with explicit minimum and maximum.
* Display toggles for the legend, data points, and the running (pause/resume) mode, plus the maximum
  data points.
* Actions with replace-split submenus, show and hide, and screenshot options.

.. figure:: /rst/figures/screenshots/config_topic_pro.png
    :align: center
    :width: 330px

.. _right_pane_config_event_charts:

Event Charts
------------

See :ref:`event_charts` for the full event chart documentation.

The configuration panel for an event chart covers:

* The **PLOT MODE** dropdown for choosing Time Series, Event Chart, or XY Chart.
* Chart name editing.
* Monitor selection, applied with **Apply & Reset Chart** (live mode only).
* Series list with per-series controls for label, visibility, max data points (live mode only),
  and removal.
* An inline add-series form with topic and scalar field selection, or a custom series.
  Click **Add Series** to expand it. Select a topic, then pick a field and confirm with **Add Series**
  or double-click the field. In live mode, fields are populated after the first sample arrives. In offline
  mode, a series with more than 500 change events opens the **Select change events** dialog first.
* Time window and X-axis locking with explicit minimum and maximum (live mode only).
* Display toggles for the legend and the running (pause/resume) mode, and the maximum number of change
  events per series, up to 500 (live mode only).
* Actions with replace-split submenus, show and hide and screenshot options.

.. figure:: /rst/figures/screenshots/config_event_pro.png
    :align: center
    :width: 330px

XY Topic Charts
---------------

See :ref:`xy_charts` for the full XY charts documentation.

The configuration panel for XY charts covers:

* The **PLOT MODE** dropdown for choosing Time Series, Event Chart, or XY Chart.
* Chart name editing.
* Monitor selection, applied with **Apply & Reset Chart**.
* Series list with per-series controls for label, color, visibility, max data points, and removal.
* An inline add-series form for selecting an X topic and field and a Y topic and field independently.
  Click **Add XY Series** to expand it. X and Y values may come from the same or different topics.
* X-axis and Y-axis locking with explicit minimum and maximum.
* Display toggles for the legend, connecting lines, and the running (pause/resume) mode, plus the
  maximum data points.
* Actions with replace-split submenus, show and hide, and screenshot options.

.. figure:: /rst/figures/screenshots/config_xy_pro.png
    :align: center
    :width: 330px

.. _publisher-pane:

Topic Publisher
---------------

See :ref:`publisher_pane` for the full publisher pane documentation.

The configuration panel for a publisher pane covers:

* A read-only **CURRENT TOPIC** section showing the topic name, monitor, resolved type name, publisher
  status, and number of samples sent.
* A **CHANGE TOPIC** section with monitor and topic selection and an **Apply & Reset** button that
  rebuilds the dynamic-type form for the new topic.
* A **CONTINUOUS** section with a **Publish continuously** toggle and an **Interval** spin box in
  milliseconds (minimum 50 ms).
* An **ACTIONS** section with **Publish once**, **Reset**, and **Randomize** buttons.
* PANEL ACTIONS with replace-split submenus.

.. figure:: /rst/figures/screenshots/config_publish_pro.png
    :align: center
    :width: 330px

.. _idl-pane:

Topic Type (IDL)
----------------

See :ref:`dockable_idl_pane` for the full IDL pane documentation.

The configuration panel for an IDL pane covers:

* A read-only **TOPIC** section showing the current topic name, domain, and resolved type name.
* A **CHANGE TOPIC** section with monitor and topic selection and an **Apply & Reset** button.
* A **DISPLAY** toggle for ROS 2 demangling.
* Actions with replace-split submenus and copying option.

.. figure:: /rst/figures/screenshots/config_idl_pro.png
    :align: center
    :width: 330px

.. _pro_right_pane_config_data_table:

Data Table
----------

Headed **DATA TABLE**: **TABLE NAME**, **DISPLAY**, **COLUMNS**, **ADD COLUMNS**, **FILTERS**,
**ACTIONS** and **PANEL ACTIONS**. A Data Table has no creation form: it opens with this panel, where
you add its topics and columns. See :ref:`pro_data_table_config`.

.. _pro_right_pane_config_type_registration:

Type Registration
-----------------

Headed **TYPE REGISTRATION**, the panel only has **PANEL ACTIONS**: the IDL source, the type name, and
the registration are all handled inside the pane. See :ref:`register_type`.

.. _pro_right_pane_config_architecture:

Architecture View
-----------------

An Architecture View tab, which shows which DataReaders receive from which DataWriters of one topic,
uses the panel to choose that topic (see :ref:`pro_architecture_view_opening`). The panel is headed
**NEW ARCHITECTURE VIEW** until a topic is chosen, and **ARCHITECTURE VIEW** afterwards:

* **SCOPE** - the current topic and its monitor.
* **MONITOR** (live only) - the monitor whose topics are listed.
* **TOPIC** - the topic to show. Only the topics of the selected monitor, or of the recording in offline
  mode, are listed.
* **ACTIONS** - **Open topic**, which becomes **Apply topic** once the view shows a topic (it also
  clears the selected pair), and **Cancel**.

.. figure:: /rst/figures/screenshots/config_architecture_pro.png
    :align: center
    :width: 330px

.. _domain-graph:

Domain Graph
============

When a Domain Graph tab is active, click the |gear| button to open the right-side panel.
It shows a dedicated visibility control panel instead of the pane-type configuration described above.
Toggling a checkbox takes effect immediately, with no apply step.

See :ref:`pro_domain_view` for the full Domain View documentation.

The panel lists all entities discovered in the domain, grouped into seven collapsible sections:
**TOPICS**, **HOSTS**, **USERS**, **PROCESSES**, **PARTICIPANTS**, **DATAWRITERS**, and **DATAREADERS**.
Each section shows the alias of every discovered entity of that kind alongside a checkbox and a
visible/total count in the section header.

.. figure:: /rst/figures/screenshots/config_domain_pro.png
    :align: center
    :width: 330px

The panel covers:

* A **search field** at the top that filters all sections simultaneously. Sections with no matching
  aliases collapse automatically while the filter is active.
* **Per-entity checkboxes** to show or hide individual entities by alias. Unchecked entities are
  removed from the graph but remain listed so they can be restored at any time.

.. note::

   Visibility is controlled by alias, not by internal entity identifier. If two or more entities of
   the same kind share the same alias, toggling that entry hides or shows all entities that carry
   that alias simultaneously.

* **Collapsible sections** that can be expanded or collapsed by clicking the section header.
* An **ACTIONS** section with two bulk buttons:

  * **Show All Entities** - makes every entity of every kind visible.
  * **Hide All Entities** - hides every entity of every kind at once.

When all entities of a given kind are hidden and a new entity of that kind is discovered later (for
example after enabling metatraffic visibility or after a new participant joins), the new entity
inherits the hidden state automatically. If at least one entity of that kind is
visible, newly discovered ones appear visible by default. Manual checkbox selections are preserved
across model refreshes and are never overridden by this rule.

When a topic is focused in the graph, the **TOPICS** section shows that topic as the only one checked.
Checking another topic turns the focus into ordinary visibility settings.

.. _pro_right_pane_config_axes:

Locking the Axes
================

The **AXES** section of a chart sets what part of the data the chart shows.
**Lock Y axis** and **Lock X axis** fix the visible range of that axis, so new data no longer moves it or
changes its scale. Turning a lock on fills its minimum and maximum fields with the current range, which you
can then edit:

* On a time axis, **X min** and **X max** take a local date and time in ``yyyy-MM-dd hh:mm:ss`` format.
  The fields refuse characters that cannot form a valid date and time, so a month 13 or a minute 77
  cannot be typed.
* On a value axis, the fields take a number, with a dot or a comma as the decimal separator.

A value applies when you press **Enter** or leave the field. The **Time window** field of a live chart
applies the same way.
The minimum must be lower than the maximum: a range that is not is not applied, and a message below the
fields says why (for example *X min must be earlier than X max.*) while the fields return to the current
range. The two values are never swapped.

While the X axis of a live chart is locked, its **Time window** field is disabled and shows the span of
the locked range. Turning a lock off lets the axis follow the data again.
The |pause| / |play| button in the pane header locks or unlocks both axes at once. **Reset Zoom**, like
|resize| **Reset View** in the pane header, unlocks both axes and returns them to their default range.
