.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _time_series:

##############################
Time Series Topic Charts |Pro|
##############################

A *Time Series Topic Chart* plots the live values of one or more numeric fields from DDS topics over time.
Each series tracks one numeric field from one DDS topic and updates in real time as samples arrive.

Fields that are integers, floats, doubles, booleans (as 1 or 0), or enums (by their numeric value) can be
plotted, as well as :ref:`Custom Series <custom_series_panel>`.
Struct and array fields cannot be plotted directly but can be expanded to reach their numeric leaf fields.

.. thumbnail:: /rst/figures/screenshots/topic_time_series_pro.png
    :align: center

.. _time_series_creating:

Opening a Time Series Topic Chart
=================================

There are several ways to open a new Time Series Topic Chart pane:

* Right-click a topic in the :ref:`topics_panel`, the :ref:`pro_logical_panel`, or the :ref:`Domain View <pro_domain_graph>` and choose
  **Chart topic data**. Built-in and statistics Fast DDS topics cannot be charted, so this option is
  disabled for them.

* Use **Add → Topic Chart** in the application menu bar.

* Click **+** at the end of the tab strip and choose the |topic_chart| **Topic Charts** tile in the view
  picker; when the chart opens, select **Time Series** from the **PLOT MODE** dropdown in the
  configuration panel.

* Click the three-dots button in the header of any existing pane to open the split menu, then choose
  **Split right** or **Split down** and select **Topic Chart** to open a new chart alongside the current
  pane, or choose **Replace panel** to replace the current pane with a Time Series Topic Chart.

* Right-click a numeric field in the :ref:`topics_panel`, or a numeric value in a
  :ref:`Topic Spy <dockable_spy_pane>` or in the sample details of a :ref:`Data Table <pro_data_table>`,
  and choose **Plot on Time Series**. The chart opens with that field as its first series. The option is
  disabled for values that are not numbers or booleans.

* Right-click a custom series in the :ref:`Custom Series panel <custom_series_panel>` and choose
  **Plot on Time Series**. The option is disabled while the series has only returned text.

.. _time_series_series:

Managing Series
===============

**Adding a series:**

* Click **Add Series** in the **SERIES** section to expand the series creation form. Select a topic from
  the filtered list and then pick a numeric leaf field. Fields only appear after the first DDS sample has
  arrived on that topic. Click **Add Series** to confirm, or double-click a field to add it immediately.

* Select a custom series in the **Custom Series** part of the same form and click **Add Custom Series** to
  track its calculated value.

* Drag a numeric field leaf from an open :ref:`Topic Spy <dockable_spy_pane>`, or from the sample details of
  a :ref:`Data Table <pro_data_table>`, and drop it onto the chart.
  The field is added as a new series immediately.

* Drag a numeric field leaf from the :ref:`topics_panel` on the left sidebar and drop it onto an existing
  chart. The field must belong to a topic on the same domain as the chart.

* Drag a custom series from the :ref:`Custom Series <custom_series_panel>` panel and drop it onto the chart.

A custom series that returns text is accepted, since it may return numbers later. While its result is
text, nothing is plotted for it and its legend entry shows the text after the name, as in
``non-numeric: "LOW"``. A custom series that returns a boolean is plotted as 1 or 0, and its legend entry
shows ``true`` or ``false``.

**Editing a series:**

Right-clicking a series entry in the legend opens a context menu with the following options:

* **Rename series** opens a dialog to give the series a custom display name shown in the legend.
* **Change color** opens a color picker to assign a custom line color.
* **Hide series** / **Display series** toggles the series visibility on the chart without removing it.
* **Set max data points** sets how many recent data points this series retains in memory.
* **Remove series** removes the series from the chart permanently.

The same options are available from the **SERIES** section of the :ref:`right_pane_config` sidebar, where
each series has a row with a color swatch, rename, visibility toggle, and remove button.

**Bulk actions:**

The **ACTIONS** section of the :ref:`right_pane_config` sidebar provides:

* **Show All Series** makes every hidden series visible at once.
* **Hide All Series** hides all series without removing them.
* **Clear Chart** removes all series and resets the chart.

.. _time_series_controls:

Chart Header Controls
=====================

The chart header has these buttons, from left to right:

* |resize| **Reset View** returns both axes to their default range after any manual zooming or panning.

* |legend_fill| **Show Legend** / |legend| **Hide Legend** shows or hides the legend listing all active series and their colors.

* |pause| / |play| **Lock / Resume chart scroll** locks both the X and Y axes so the chart stops
  auto-scrolling while data keeps flowing in. The button shows |pause| while at least one axis is still
  auto-scrolling and switches to |play| once both are locked. Clicking it again unlocks both axes and
  resumes auto-scroll. Data reception is unaffected; to pause ingestion use the **Running** toggle in the
  sidebar.

* |question| **Help** opens a contextual help panel with a description of the chart, usage tips, available
  interactions, and a link to this documentation page.

* |expand_square| / |collapse_square| maximizes or minimizes the pane; click again to restore the previous layout.

* |gear| **Panel Settings** opens the :ref:`right_pane_config` sidebar for this chart.

* The three-dots button opens the split menu to open a new pane to the right or below the current one.

* |cross| **Close** closes the pane.

.. _time_series_interaction:

Interactive Chart Controls
==========================

The chart area supports these mouse and keyboard interactions:

* **Click on a data point** to show its exact value.
* **Scroll wheel** to zoom the X axis in and out.
* **Ctrl + scroll wheel** to zoom the Y axis in and out.
* **Shift + drag** to zoom into a selected area.
* **Ctrl + click and drag** to scroll (pan) the axes without zooming.

.. _time_series_config:

Right-Side Configuration Panel
===============================

Opening the :ref:`right_pane_config` sidebar for a Time Series Topic Chart (via the |gear| button)
shows the following sections:

* **PLOT MODE** - a dropdown with **Time Series**, **Event Chart**, and **XY Chart**. Selecting
  another mode opens a replacement form; confirm **Replace pane with ...** to replace the chart
  and its series, or **Cancel** to return to the existing chart.
* **PANE SETTINGS** - monitor selection, applied with **Apply & Reset Chart**.
* **CHART NAME** - rename the chart title shown in the pane header.
* **DISPLAY** - toggles for legend, data points, and running (pause/resume ingestion), and the
  **Max points** setting.
* **SERIES** - list of active series with per-series controls; **Add Series** button to expand the
  inline series creation form (topic series or custom series).
* **AXES** - time window (applied with its own apply button), lock Y axis or X axis to a fixed
  range; **Reset Zoom**.
* **ACTIONS** - show/hide all series, clear chart, save and copy screenshot, and export to CSV.
* **PANEL ACTIONS** - split and replace submenus.

See :ref:`right_pane_config` for the full configuration panel reference.
