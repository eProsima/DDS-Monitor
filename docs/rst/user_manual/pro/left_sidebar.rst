.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _pro_left_sidebar:

############
Left Sidebar
############

The left sidebar holds several panels, opened from the icon bar on the left edge of the window.
Each icon switches the sidebar to the corresponding panel, and hovering an icon shows its tooltip.
Hide the sidebar with the last button of the icon bar, |panel_left_close| **Hide Sidebar**
(|panel_left_open| **Show Sidebar** while it is hidden), or resize it by dragging its border.

.. figure:: /rst/figures/screenshots/icon_bar_pro.png
    :align: center

- |explorer| :ref:`Explorer Panel <pro_left_panel>` (*DDS Entities Explorer*) - shows all DDS entities discovered
  by the monitor in collapsible, interactive lists organized by DDS, Physical, Logical, and
  Info/Statistics sub-panels.
- |topic| :ref:`Topics Panel <topics_panel>` |Pro| (*Topics Explorer*) - topic-centered view with text
  filtering, expandable field trees, and direct actions (Spy, Chart, Data Table, Publish, IDL) for any topic.
- |custom_series| :ref:`Custom Series Panel <custom_series_panel>` |Pro| (*Custom Series*) - define, edit, and manage
  user-defined data series computed from a JavaScript formula.
- |enable_statistics| :ref:`Enable / Disable Statistics Panel <statistics_readers_panel>` |Pro| - control which
  statistics DataReaders are active, so only the statistics you need are collected.
- |record| :ref:`Recording Configurations Panel <pro_left_sidebar_recordings>` |Pro|
  (*Recording Configurations*) - saved recording configurations, each one ready to start a recording.
- |alert| :ref:`Alerts Panel <pro_alerts_panel>` - define threshold-based alert rules and view their status
  and configuration details.
- |status| :ref:`Monitor Status Panel <pro_status_panel>` (*Monitor Status*) - live entity counts, active
  domains, and a scrollable log of DDS network events.
- |issues| :ref:`Issues Panel <pro_issues_panel>` (*Issues*) - operational error events reported by the
  application.

.. note::

    The *Alerts*, *Recording Configurations* and *Enable / Disable Statistics* panels are hidden in
    :ref:`offline mode <offline_mode>` while inspecting a recording.

Two icons can show a dot:

- The |alert| bell, when alerts have fired that you have not looked at yet in the **Alerts** tab of the
  :ref:`bottom panel <bottom_panels>`.
  Its tooltip then says how many, for example *Alerts (3 new)*.
- The |record| icon, while a :ref:`recording <pro_recording>` is running.

.. _pro_left_sidebar_headers:

Panel Headers
=============

Every panel starts with a header that shows its name in capitals and a |question| **Help** button.
Click it to open a short description of the panel with some tips and an **Open Documentation** link
to the matching page of this manual.
Some sections and tabs inside the panels have a |question| button of their own.

.. _pro_left_sidebar_recordings:

Recording Configurations Panel |Pro|
====================================

The *Recording Configurations* panel (header **RECORDINGS**) keeps named recording setups: the files to
write, their format and the topics to record. The workspace saves them.
Click |plus| to create one, and the record button of a configuration to start recording with it; click
it again to stop.
See :ref:`pro_recording_configurations` for the panel and :ref:`pro_recording` for recording in general.

.. toctree::
    :hidden:

    /rst/user_manual/pro/explorer_panel
    /rst/user_manual/pro/topics_panel
    /rst/user_manual/pro/custom_series_panel
    /rst/user_manual/pro/statistics_readers_panel
    /rst/user_manual/pro/alerts_panel
    /rst/user_manual/pro/status_panel
    /rst/user_manual/pro/issues_panel
