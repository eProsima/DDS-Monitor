.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _event_charts:

##################
Event Charts |Pro|
##################

An *Event Chart* displays changes in DDS topic field values as colored intervals on a timeline.
Each series occupies a separate horizontal lane. This makes it easy to compare states across fields,
see when they changed, and inspect how long each value lasted.

Event Charts support string, numeric, boolean, and enum fields, including scalar fields inside
nested structures. Numeric custom series can also be added as lanes. Event Charts work with both
live DDS samples and offline recordings.

.. figure:: /rst/figures/screenshots/event_chart.png
    :align: center
    :alt: Offline Event Chart with separate userID and message lanes, a value tooltip, change
          navigation arrows, and the Plot Mode dropdown in the configuration panel.

    An Event Chart showing numeric and string fields from the hello_world topic in a recording.

In this example, the upper lane tracks **hello_world / userID** and the lower lane tracks
**hello_world / message**. Each block represents one value, such as **11** or **alpha**.
The vertical cursor marks the current playback time, and the legend shows each lane's value at
that time. The tooltip shows the selected interval's value, start, end, and duration.

.. _event_charts_creating:

Opening an Event Chart
======================

1. Open the Topic Chart creation form, for example from **Add > Add Topic Chart** in the application
   menu or by selecting **Topic Chart** in an empty pane.
2. Select **Event Chart** from the **Plot Mode** dropdown in the
   :ref:`right_pane_config` sidebar. The other options are **Time Series** and **XY Chart**;
   **Time Series** is the default for a new topic chart.
3. In live mode, select a monitored **Domain** and a non-zero **Time Window**. The default window
   is two minutes. Offline charts use the recording's active time range and hide these settings.
4. Confirm **Create Event Chart**, then add the fields to track.

To replace an existing topic or XY chart, open its settings with the |gear| button and select
**Event Chart** from **Plot Mode**. Confirm **Replace pane with Event Chart** to replace the chart
and its existing series. **Cancel** returns to the existing chart.

To add an Event Chart alongside another pane, use **Panel Actions > Split right** or
**Split down**, choose **Topic Chart**, and select **Event Chart** in the creation form.
For other pane types, **Panel Actions > Replace panel > Topic Chart** opens the replacement form.

.. _event_charts_series:

Adding and Managing Lanes
=========================

Click **Add Series** in the configuration sidebar, select a topic and a scalar field, then confirm
**Add Series** or double-click the field. In live mode, fields become available after the first
sample arrives. In offline mode, fields are read from the recording; the topic must have a type
that the monitor can decode.

You can also drag a string, numeric, boolean, or enum leaf field from the :ref:`topics_panel` or
an open :ref:`Spy Pane <dockable_spy_pane>` onto an Event Chart to add a lane directly.
In live mode, the field must belong to the same DDS domain as the chart. Dragging or selecting a
numeric custom series adds its calculated values as another lane.

Use the **Series** section to rename, hide, show, or remove individual lanes. The legend context
menu provides the same actions. **Show All Series**, **Hide All Series**, and **Clear Chart**
apply to the whole chart.

Interval colors are assigned automatically from each value. Equal values share a color across
lanes, and a value keeps its color when it reappears. A series color swatch identifies the lane
in the legend; changing that swatch does not change the value-based interval colors.

.. _event_charts_intervals:

Reading the Timeline
====================

* A new interval begins when a field's value changes. Repeated samples with the same value extend
  the current interval.
* The X axis shows time; the Y axis lists the visible field lanes.
* Labels appear inside intervals when there is enough room. Hover over an interval to see its
  series name, value, start and end times, and duration in milliseconds. Click to keep the
  tooltip visible; click an empty area to dismiss it.
* Missing or unavailable values appear as gaps. A lane begins when its first known value is
  available and retains its last known value until a subsequent change or the plotted range ends.

Use the mouse wheel to zoom the time axis, **Shift + drag** to zoom into a selected area, and
**Ctrl + drag** to pan. **Reset View** restores the default range, and **Toggle Legend** shows
or hides the legend.

.. _event_charts_live:

Live Monitoring
===============

Live Event Charts update as DDS samples arrive and scroll over the configured time window.
The monitor subscribes to each plotted topic with its own DataReader while the chart is open.

Each lane retains up to **500 change events**. **Max points** and the series context menu's
**Set max data points** can lower this limit; the allowed range is 1 to 500. Once the limit is
reached, older events are removed as new changes arrive. Events outside the time window are also
pruned while preserving the state at the window's left edge.

The **Running** toggle controls ingestion. When it is off, incoming samples are discarded;
resuming starts from the current live feed. The header **Lock / Resume chart scroll** control
locks or unlocks the time axis while samples continue to arrive.

.. _event_charts_offline:

Inspecting a Recording
======================

Offline Event Charts show recorded intervals within the active playback range, with a moving
cursor shared by all panes. The legend displays the value at the cursor for each lane. Seeking
backward and forward updates the cursor without consuming or removing recorded intervals.

**Selecting an event range**

Each recorded lane plots at most **500 change events**. When a series exceeds its event limit,
the **Select change events** dialog opens before its intervals are plotted. Choose where to take
events using the **Take events** dropdown:

* **From the recording start, forward**.
* **From the recording end, backward**.
* **From a timepoint, forward**.
* **From a timepoint, backward**.

For a timepoint selection, enter local time in ``yyyy-MM-dd HH:mm:ss.zzz`` format, within the
range displayed by the dialog. Click **Plot events** to apply the selection. Each lane has its
own selection, so lanes in the same chart may cover different portions of the recording.
Intervals outside a lane's selection are not displayed.

To change a lane's selection later, right-click its legend entry and choose
**Select event range...**. Canceling a required selection leaves the lane unplotted until a
range is chosen.

**Navigating between changes**

The arrows at the top right of the plot go to the **previous** or **next value change** among
visible lanes, within their selected event ranges. Hidden lanes are excluded. Each action pauses
playback and seeks the shared cursor to the chosen boundary, updating all other panes to that
time. An arrow is disabled when there is no eligible boundary in that direction.

.. _event_charts_config:

Configuration and Workspace
===========================

The configuration sidebar provides **Plot Mode**, **Chart Name**, **Show legend**, the **Series**
list, and screenshot and bulk actions. Live mode also exposes the domain, time window, event
limit, and **Running** controls. Event Charts use field lanes for the Y axis; numeric Y-axis
bounds and the **Show points** option are not offered. **Export to CSV** is not available for
Event Charts. Use **Save screenshot** or **Copy screenshot** to capture the displayed timeline.

:ref:`Workspace Save and Restore <workspace>` preserves the Event Chart presentation, lane
configuration, visibility, event limits, and offline event-range selections. Live interval history
is collected again when monitoring resumes.
