.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _event_charts:

##################
Event Charts |Pro|
##################

An *Event Chart* shows how the values of DDS topic fields change over time.
Each series is drawn in its own horizontal lane as a sequence of colored intervals: a new interval starts
whenever the value changes, so the chart shows when each change happened and how long each value lasted.
Event Charts work with both live DDS samples and :ref:`offline recordings <offline_mode>`.

Fields that are strings, characters, numbers, booleans, or enums can be plotted, as well as numeric
:ref:`Custom Series <custom_series_panel>`.
Struct and array fields cannot be plotted directly but can be expanded to reach their scalar leaf fields.

.. thumbnail:: /rst/figures/screenshots/event_chart.png
    :align: center

.. _event_charts_creating:

Opening an Event Chart
======================

There are several ways to open a new Event Chart pane:

* Use **Add → Add Topic Chart** in the application menu bar and select **Event Chart** from the
  **Plot Mode** dropdown in the configuration panel.

* Click the **Topic Charts View** button in an empty pane; when the chart opens, select **Event Chart**
  from the **Plot Mode** dropdown in the configuration panel.

* Click the three-dots button in the header of any existing pane to open the split menu, then choose
  **Split right** or **Split down** and select **Topic Chart** to open a new chart alongside the current
  pane, or choose **Replace panel** to replace the current pane. Then select **Event Chart** from the
  **Plot Mode** dropdown.

* Select **Event Chart** from the **Plot Mode** dropdown of an existing Time Series or XY Chart.
  Confirm **Replace pane with Event Chart** to replace the chart and its series, or click **Cancel** to
  return to the existing chart.

In live mode, the creation form also asks for a monitored **Domain** and a **Time Window** (two minutes by
default; it cannot be zero). In offline mode the chart uses the active recording range, so these settings are
hidden. Click **Create Event Chart** to open the pane, then add the fields to track.

.. _event_charts_series:

Managing Series
===============

**Adding a series:**

* Click **+ Add Series** in the **Series** section to expand the series creation form. Select a topic from
  the filtered list and then pick a scalar leaf field. In live mode, fields only appear after the first DDS
  sample has arrived on that topic. In offline mode, fields are read from the recording, and the topic must
  have a type that the monitor can decode. Click **Add Series** to confirm, or double-click a field to add it
  immediately.

* Select a custom series in the **Custom Series** part of the same form and click **Add Custom Series** to
  track its calculated value.

* Drag a string, character, numeric, boolean, or enum leaf field from the :ref:`topics_panel` or from an open
  :ref:`Spy Pane <dockable_spy_pane>` and drop it onto the chart. In live mode, the field must belong to a
  topic on the same domain as the chart.

* Drag a custom series from the :ref:`Custom Series <custom_series_panel>` panel and drop it onto the chart.

In offline mode, a series with more than 500 change events asks which part of the recording to plot before
it is drawn. See :ref:`event_charts_offline`.

**Editing a series:**

Right-clicking a series entry in the legend opens a context menu with the following options:

* **Rename series** opens a dialog to give the series a custom display name shown in the legend and on the
  Y axis.
* **Change color** opens a color picker to assign a custom color to the series in the legend. Interval
  colors are not affected, since they always depend on the value.
* **Hide series** / **Display series** toggles the series visibility on the chart without removing it.
  Hidden series are also removed from the Y axis.
* **Set max data points** sets how many change events this series retains, from 1 to 500. Not available in
  offline mode.
* **Select event range...** chooses which part of the recording the series shows. Only available in offline
  mode; see :ref:`event_charts_offline`.
* **Remove series** removes the series from the chart permanently.

The same options, except **Select event range...**, are available from the **Series** section of the
:ref:`right_pane_config` sidebar, where each series has a row with a color swatch, rename, visibility
toggle, max data points (live mode only), and remove button.

**Bulk actions:**

The **Actions** section of the :ref:`right_pane_config` sidebar provides:

* **Show All Series** makes every hidden series visible at once.
* **Hide All Series** hides all series without removing them.
* **Clear Chart** removes all series and resets the chart.

.. _event_charts_intervals:

Reading the Timeline
====================

* The X axis shows time and the Y axis (**Fields**) lists one lane per visible series.
* A new interval begins when the value changes. Repeated samples with the same value extend the current
  interval.
* Interval colors are assigned from the value itself: equal values share a color across lanes, and a value
  keeps its color whenever it reappears, including after loading a :ref:`workspace <workspace>`.
* The value is written inside the interval when there is enough room. An empty string is shown as
  *(empty string)*.
* A series starts at its first known value and keeps its last known value until the next change, or until
  the current time in live mode or the end of the plotted range in offline mode.
* Missing or unavailable values appear as gaps.

.. _event_charts_controls:

Chart Header Controls
=====================

The chart header provides the following buttons from left to right:

* |resize| **Reset View** returns the time axis to its default range: the configured time window in live
  mode, or the active recording range in offline mode.

* |legend| **Toggle Legend** shows or hides the legend listing all series and their colors.

* |pause| / |play| **Lock / Resume chart scroll** locks the time axis so the chart stops auto-scrolling
  while data keeps flowing in. Clicking it again unlocks the axis and resumes auto-scroll. Data reception is
  unaffected; to pause ingestion use the **Running** toggle in the sidebar. Only available in live mode.

* |help| **Help** opens a contextual help panel with a description of the chart, usage tips, available
  interactions, and a link to this documentation page.

* |maximize_square| / |minimize_square| - maximizes/ minimizes the pane; click again to restore the previous layout.

* |gear| **Panel Settings** opens the :ref:`right_pane_config` sidebar for this chart.

* The three-dots button opens the split menu to open a new pane to the right or below the current one.

* |cross| **Close** closes the pane.

.. _event_charts_interaction:

Interactive Chart Controls
==========================

The following mouse and keyboard interactions are available directly on the chart area:

* **Hover over an interval** to show its series name, value, start and end times, and duration in
  milliseconds.
* **Click or right-click an interval** to keep its tooltip visible; click an empty area to close it.
* **Scroll wheel** to zoom the time axis in and out.
* **Shift + drag** to zoom into a selected time range.
* **Ctrl + click and drag** to scroll (pan) the time axis without zooming.

.. _event_charts_live:

Live Monitoring
===============

Live Event Charts update as DDS samples arrive and scroll over the configured time window.
To read the field values, the monitor subscribes to each plotted topic with its own DataReader while the
chart is open.

* Each series retains up to **500 change events**. Use **Max points** in the sidebar to lower the limit for
  all series, or **Set max data points** for a single series; the allowed range is 1 to 500. Once the limit
  is reached, the oldest events are removed as new changes arrive.
* Events that scroll out of the time window are also removed, but the value at the left edge of the window is
  kept, so the first interval always shows the right value.
* The **Running** toggle in the sidebar pauses or resumes ingestion. While paused, incoming samples are
  discarded; when resumed, the chart continues from the current live data.

Saving a :ref:`workspace <workspace>` keeps the series and their limits, but not the plotted intervals,
which are collected again when monitoring resumes.

.. _event_charts_offline:

Inspecting a Recording
======================

In :ref:`offline mode <offline_mode>`, Event Charts show the recorded intervals within the active playback
range, with a playback cursor shared by all panes. The legend shows each series' value at the cursor.
Moving the cursor backward or forward does not change the plotted intervals.

**Selecting an event range:**

Each series plots at most **500 change events**. When a series has more change events in the recording,
the **Select change events** dialog opens before the series is plotted. Choose where to take the events from
in the **Take events** dropdown:

* **From the recording start, forward**.
* **From the recording end, backward**.
* **From a timepoint, forward**.
* **From a timepoint, backward**.

For a timepoint, enter the local time in ``yyyy-MM-dd HH:mm:ss.zzz`` format, within the range shown in the
dialog. Click **Plot events** to apply the selection.

Each series has its own selection, so series in the same chart may cover different parts of the recording.
Intervals outside a series' selection are not shown.
A series shows no intervals while it waits for its selection. Canceling the dialog at that point removes the
series from the chart.

To change the selection later, right-click the series in the legend and choose **Select event range...**.
Canceling this dialog keeps the current selection.
If the active playback range changes and a selected timepoint falls outside it, the dialog opens again.
Saving a :ref:`workspace <workspace>` keeps each series' selection.

**Navigating between changes:**

The arrow buttons at the top right of the plot go to the **previous** or **next value change** of the
visible series, within their selected event ranges. Each click pauses playback and moves the shared cursor
to that change, so all other panes update to the same time. If the change is outside the visible time range,
the chart scrolls to show it. A button is disabled when there is no change in that direction.

.. _event_charts_config:

Right-Side Configuration Panel
==============================

Opening the :ref:`right_pane_config` sidebar for an Event Chart (via the |gear| button) shows the
following sections:

* **Plot Mode** - a dropdown with **Time Series**, **Event Chart**, and **XY Chart**. Selecting
  another mode opens a replacement form; confirm **Replace pane with ...** to replace the chart
  and its series, or **Cancel** to return to the existing chart.
* **Pane Settings** - domain selection, applied with **Apply & Reset Chart** (live mode only).
* **Chart Name** - rename the chart title shown in the pane header.
* **Display** - toggle for legend; in live mode, also the running toggle (pause/resume ingestion) and
  **Max points** for the event limit of all series.
* **Series** - list of series with per-series controls; **Add Series** button to expand the inline series
  creation form.
* **Axes** - time window, lock X axis to a fixed range (**X min** / **X max**), and **Reset Zoom**
  (live mode only).
* **Actions** - show/hide all series, clear chart, save and copy screenshot.
* **Panel Actions** - split and replace submenus.

Event Charts have no Y-axis range, **Show points** toggle, or **Export to CSV** action.

See :ref:`right_pane_config` for the full configuration panel reference.
