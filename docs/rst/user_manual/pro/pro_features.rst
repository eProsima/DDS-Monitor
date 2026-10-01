.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _pro_features:

######################
DDS Monitor |Pro|
######################

*DDS Monitor Pro* is the commercial edition of *eProsima DDS Monitor*.
It extends the open-source version with more advanced monitoring features, a richer interface, and
tools for production deployments.

.. note::

    All features described in this section are exclusive to *DDS Monitor Pro*.

In addition to the features of *DDS Monitor Basic*, it includes the following Pro features:

* :ref:`Dockable Panes <dockable_panes>` |Pro|: Charts, Topic Spy and Topic Type (IDL) panes open as
  panes you can move and split freely, instead of fixed tab views.

* :ref:`Dark Mode and Theming <theming>` |Pro| with light and dark palettes applied across the whole
  application, including panels, charts, icons, and dialogs.

* :ref:`Multiple Monitor Support <multiple_monitors>` |Pro| to observe several DDS Domains, Discovery
  Servers, or XML-configured environments side by side in the same workspace.

* :ref:`Offline Mode <offline_mode>` |Pro| for opening a captured DDS recording (MCAP or SQLite) and
  inspecting it with playback controls to scrub, play, pause, loop, and change speed through the
  recorded timeline.

* :ref:`Domain Removal <pro_stop_monitor>` |Pro| to stop monitoring a specific domain at any time, keeping all existing panes and charts open in an inactive state.

* :ref:`Workspace Save and Restore <workspace>` |Pro| to save the full workspace state to a file and
  reload it in a future session, preserving tab layouts, pane configurations, chart settings, alert rules,
  and tab order.

* :ref:`Topics Panel <topics_panel>` |Pro|, a topic navigation panel in the left sidebar
  with text filtering, expandable field trees, and context actions for opening Spy or Topic Chart panes.

* :ref:`Custom Series <custom_series_panel>` |Pro| for defining data series computed from a JavaScript
  formula that binds one or more topic fields to variables, then plotting the result on a topic chart.

* :ref:`On-Demand Statistics Readers <statistics_readers_panel>` |Pro| for controlling which
  statistics DataReaders are active, so only the statistics you ask for are collected.

* :ref:`Alert Configuration Pane <pro_alert_configuration_panel>` |Pro|, a form in the left
  sidebar for creating and editing alert rules inline instead of in a separate dialog.

* :ref:`Entity Summary Bar <entity_summary_bar>` |Pro| showing live counters for every type of monitored
  DDS entity at the bottom of the window, where they are always visible.

* :ref:`Image Pane <image_pane>` |Pro| for rendering live image data from DDS topics inside the
  monitor, with automatic detection of ROS 2 ``sensor_msgs`` and *eProsima Fast DDS* image types, plus
  manual field mapping for arbitrary topics.

* :ref:`Topic Time Series Charts <topic_charts>` |Pro| for plotting live numeric values from any DDS topic as a
  time-series chart, with support for multiple series, field selection, and pause/resume controls.

* :ref:`Event Charts <event_charts>` |Pro| for tracking string, numeric, boolean, and enum values as
  colored intervals in live samples and recordings, with separate field lanes and change navigation.

* :ref:`XY Topic Charts <xy_charts>` |Pro| for plotting two numeric DDS topic fields against each other as a
  real-time scatter chart, for phase-space or correlation analysis of any pair of numeric fields
  within the same DDS domain.

* :ref:`Publisher Pane <publisher_pane>` |Pro| for publishing user-defined samples on any discovered DDS
  topic, with a form built automatically from the topic's dynamic type and support for one-shot and
  continuous publishing.

* :ref:`Register Type <register_type>` |Pro| for registering a user-supplied data type from its IDL,
  optionally under a custom name, so it can be used for spying, publishing, and charting on topics
  whose type was never discovered on the network.

* :ref:`Right-Side Pane Configuration <right_pane_config>` |Pro| for creating and editing all pane types
  from an inline configuration sidebar, including statistics charts, topic charts, spy panes, IDL panes, and
  image panes, without opening separate dialogs.
