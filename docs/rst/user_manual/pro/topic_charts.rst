.. include:: ../../exports/alias.include
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

Choose **Time Series**, **Event Chart**, or **XY Chart** from the **Plot Mode** dropdown in the
:ref:`right_pane_config` sidebar when creating or replacing a topic chart. **Time Series** is the
default. Selecting a different mode on an existing chart opens a replacement form; the pane and its
series are replaced only after confirming **Replace pane with ...**. **Cancel** returns to the
existing chart.

Time Series and XY Charts plot numeric fields (integers, floats, or doubles). Event Charts also
support strings, booleans, and enums, plus numeric custom series. Struct and array fields cannot
be plotted as a whole; expand them to reach their scalar leaf fields. Dropping a non-numeric field
onto a Time Series chart displays a warning; select **Event Chart** to track its changes.

.. toctree::
    :hidden:

    /rst/user_manual/pro/time_series
    /rst/user_manual/pro/event_charts
    /rst/user_manual/pro/xy_charts
