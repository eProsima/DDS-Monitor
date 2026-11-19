.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _topic_charts:

##################
Topic Charts |Pro|
##################

*Topic Charts* plot live data published on any user-defined DDS topic, using the raw values from
incoming samples instead of pre-computed DDS statistics metrics.

Three chart types are available in live monitoring and offline recordings:

* :ref:`Time Series Charts <time_series>` |Pro| plot one or more numeric fields against time as samples
  arrive, with support for multiple series, per-series color and visibility controls, and pause/resume.

* :ref:`Event Charts <event_charts>` |Pro| track string, numeric, boolean, and enum field values as
  colored intervals in separate timeline lanes, with duration tooltips and recorded change navigation.

* :ref:`XY Charts <xy_charts>` |Pro| plot two numeric fields against each other as a real-time scatter
  chart, for phase-space or correlation analysis of any pair of numeric fields within the same
  DDS domain.

.. _topic_charts_plot_mode:

Choose **Time Series**, **Event Chart**, or **XY Chart** from the **PLOT MODE** dropdown in the
:ref:`right_pane_config` sidebar when creating or replacing a topic chart. **Time Series** is the
default. Selecting a different mode on an existing chart opens a replacement form; the pane and its
series are replaced only after confirming **Replace pane with ...**. **Cancel** returns to the
existing chart.

.. _topic_charts_fields:

Time Series and XY Charts plot numeric fields (integers, floats, or doubles), as well as
:ref:`Custom Series <custom_series_panel>`. Time Series Charts also take booleans (plotted as 1 or 0)
and enums (plotted by their numeric value). Event Charts also support strings, booleans, and enums.
Struct and array fields cannot be plotted as a whole; expand them to reach their scalar leaf fields.
Dropping a non-numeric field onto a Time Series chart displays a warning; select **Event Chart** to
track its changes.

A custom series can return a number, a text, or a boolean. Event Charts show any of them.
Time Series and XY Charts plot its numbers, and its booleans as 1 or 0. While it returns text, they
plot nothing for it and its legend entry says so.

.. _topic_charts_creating:

Creating a Topic Chart
======================

The three kinds of chart share one creation form.

.. figure:: /rst/figures/screenshots/config_new_topic_chart_pro.png
    :align: center
    :width: 330px

* **PLOT MODE** - the kind of chart: **Time Series** (the default), **Event Chart**, or **XY Chart**.
  The header and the button of the form follow it: **NEW TOPIC CHART** and **Create Topic Chart**,
  **NEW EVENT CHART** and **Create Event Chart**, or **NEW XY CHART** and **Create XY Chart**.
* **MONITOR** - the monitor whose topics the chart reads. It is already selected when only one monitor
  is running. Hidden in offline mode.

.. _topic_charts_reading:

Reading the Samples
===================

To read the field values, the monitor creates its own DataReader for each plotted topic while the chart
is open, so it joins the domain as a subscriber of that topic.

If the monitor cannot create that DataReader, the chart shows **Unable to read "<topic>"** with the
reason, and a **Retry** button that tries again.

.. toctree::
    :hidden:

    /rst/user_manual/pro/time_series
    /rst/user_manual/pro/event_charts
    /rst/user_manual/pro/xy_charts
