.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _pro_chart_view:
.. _pro_chartbox_layout:

#################
Statistics Charts
#################

A *Statistics Chartbox* plots pre-computed DDS metrics (such as latency, throughput, and packet
counts) collected from the monitored DDS network.
Where :ref:`Topic Charts <topic_charts>` work with raw values published on user-defined topics,
Statistics Charts show the statistical summaries computed by the *Fast DDS* statistics module.

Two chart modes are available:

* **Historical** - displays data over a user-specified past time range, using a fixed time window
  and an aggregation operation (mean, median, standard deviation, etc.).
* **Real-time** - updates continuously as new statistical samples arrive, scrolling the time axis
  forward as the session progresses.

Multiple series from different entities can be overlaid on the same chart.

Opening a Statistics Chart
==========================

To create a new Statistics Chartbox:

* Use **Add → Add Statistics Chart** in the application menu.
* Click the |historical_chart| button for a historical chart or |dynamic_chart| for a real-time
  chart in the shortcuts bar.
* Click the **Statistics Charts** tile in the view selector shown in a tab that has no panes open.
* Click the three-dots button in any pane header, choose **Split right** or **Split down**, and
  select **Statistics Chart** from the pane-type menu, or choose **Replace panel** to replace the
  current pane with a Statistics Chart.

.. thumbnail:: /rst/figures/screenshots/statistics_charts_pro.png
    :align: center

.. _pro_create_new_series_layout:

Series Management
=================

**Adding a series:**

A historical chart is created together with its first series, chosen in the creation form (see
:ref:`below <pro_statistics_chart_creation>`); a real-time chart is created empty.
To add further series, click **Add Series** in the **SERIES** section of the
:ref:`statistics_chart_config` sidebar to expand the inline series creation form.
Each series tracks one data kind for one or more entities over the configured time window.

**Editing a series:**

Right-clicking a series name in the legend opens a context menu with the following options:

* **Rename series** - assign a custom display name.
* **Change color** - open a color picker to assign a custom line color.
* **Hide series** / **Display series** - toggle visibility without removing the series.
* **Set max data points** (real-time charts only) - limit how many data points this series retains
  in memory.
* **Remove series** - permanently delete the series from the chart.
* **Export to CSV** - export only this series to a CSV file.

**Bulk actions:**

The **ACTIONS** section of the :ref:`statistics_chart_config` sidebar provides:

* **Show All Series** - reveal every hidden series.
* **Hide All Series** - hide every series at once.
* **Save Screenshot** / **Copy Screenshot** - save the chart as an image or copy it to the clipboard.
* **Export to CSV** - export every series in this chart to a CSV file.

Chart Header Controls
=====================

The Chartbox toolbar has these actions, from left to right:

* |resize| **Reset View** - returns both axes to their default range, fitting all visible data.

* |legend| **Show Legend** / **Hide Legend** shows or hides the legend listing all active series and their colors.

* |play| / |pause| **Lock / Resume chart scroll** (real-time charts only) - freezes or resumes the
  time-axis scroll.
  While paused, data keeps arriving but the view stays fixed, so you can zoom and pan over
  historical data.

* |help| **Help** - opens a contextual help panel with usage tips and a link to this
  documentation page.

* |maximize_square| / |minimize_square| - maximizes or minimizes the pane; click again to restore the previous
  layout.

* |gear| **Panel Settings** - opens the :ref:`statistics_chart_config` sidebar for this chart.

* The three-dots button opens the split menu to open a new pane to the right or below, or to
  replace the current pane.

* |cross| **Close** - removes the chart from the workspace.

Interactive Chart Controls
==========================

The chart area supports these mouse and keyboard interactions:

* **Click a data point** to display an info box showing its exact timestamp and value.
* **Scroll wheel** to zoom the X axis in and out.
* **Ctrl + scroll wheel** to zoom the Y axis in and out.
* **Shift + drag** to zoom into a selected area.
* **Ctrl + click and drag** to scroll (pan) the axes without zooming.
* **Escape** hides the data point info box.

Right-Side Configuration Panel |Pro|
====================================

.. _pro_statistics_chart_creation:

When a new Statistics Chart is created, the sidebar shows a creation form headed
**NEW STATISTICS CHART** (from the Add menu, with a **CHART TYPE** selector for *Live (real-time)* or
*Historical*):

* A real-time chart is configured with **DATA KIND**, **TIME WINDOW**, **UPDATE PERIOD**, and
  **ADVANCED** (max points), and is created with **Create Real-Time Chart**. Series are added
  afterwards.
* A historical chart is configured with **DATA KIND**, **SOURCE ENTITY**, **TARGET ENTITY**,
  **STATISTIC KIND**, the time range, and the **SERIES LABEL** of its first series, and is created with
  **Create Historical Chart**.

Once the chart exists, the :ref:`statistics_chart_config` sidebar (opened via the |gear| button),
headed **STATISTICS CHART LIVE** or **STATISTICS CHART HISTORICAL**, shows the following sections:

* **Pane Settings** - change the chart type, data kind, and related settings, then click
  **Apply & Reset Chart** to rebuild the chart with them.
* **Chart Name** - rename the chart title shown in the pane header.
* **Display** - toggles for legend, data points, and running (pause/resume ingestion); for real-time
  charts also the update period and max points.
* **Series** - list of active series with per-series controls; **Add Series** button to expand
  the inline form for selecting the source, target, and statistic.
* **Axes** - time window, lock Y axis or X axis to a fixed range; **Reset Zoom**.
* **Actions** - show/hide all series, export to CSV, save and copy screenshot.
* **Panel Actions** - split and replace submenus.

See :ref:`right_pane_config` for the full configuration panel reference.
