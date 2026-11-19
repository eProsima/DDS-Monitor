.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _dockable_spy_pane:

#########
Topic Spy
#########

A *Topic Spy* pane subscribes to a DDS topic and shows the live samples published on it, each as an
expandable field tree.
Use it to check that the expected data is being published and to inspect individual field values
as they arrive.

.. thumbnail:: /rst/figures/screenshots/spy_pro.png
    :align: center

.. _pro_spy_opening:

Opening a Topic Spy
===================

To open a new Topic Spy, do one of the following:

* Right-click a topic in the :ref:`topics_panel`, the :ref:`pro_logical_panel`, or the :ref:`Domain View <pro_domain_view>` and
  choose **Spy topic data**.
* Use **Add → Topic Spy** in the application menu bar.
* Click the three-dots button in the header of any existing pane, choose **Split right** or
  **Split down**, and select **Topic Spy** to open a new Topic Spy alongside the current one,
  or choose **Replace panel** to replace the current pane with a Topic Spy.

.. _pro_spy_title_bar:

Pane Header Controls
====================

* The header shows the name of the topic being spied.
* |play| **Play** / |pause| **Pause** - starts and stops the live subscription without closing the pane.
* |copy| **Copy JSON** - copies the last received sample as JSON to the clipboard.
* |image_view| **View this topic as an image** - opens an :ref:`Image Display <image_pane>` of the
  topic beside the spy. Shown only for topics the Image Display can draw.
* |question| **Help** - opens a contextual help panel with usage tips and a link to this documentation page.
* |expand_square| **Expand** / |collapse_square| **Collapse** - maximizes or minimizes the pane; click again to restore the previous
  layout.
* |gear| **Panel Settings** - opens the :ref:`right_pane_config` sidebar for this pane.
* |three_dots_menu| **Split** - opens the split menu, for opening a new pane to the right or below.
* |cross| **Close** - stops the subscription and removes the pane.

.. _pro_spy_config:

Right-Side Configuration Panel |Pro|
====================================

When the :ref:`right_pane_config` sidebar is open for a Topic Spy it shows four sections:

* **PANE SETTINGS** - select a different monitor and topic, then apply with **Apply & Reset**,
  which restarts the subscription on the new topic immediately.
* **PLAYBACK** - toggle to start or stop the live subscription without leaving the sidebar.
* **ACTIONS** - **Expand All** and **Collapse All** to unfold or fold the entire sample tree at once,
  **Clear** to discard all received samples, and **Copy JSON to Clipboard** to copy the last sample.
* **PANEL ACTIONS** - **Replace panel**, **Split right**, and **Split down** submenus, to replace the
  current pane or open a new pane alongside it.

You can have several Topic Spy panes open at once, each subscribing to a different or the same topic.

.. _pro_spy_sample_tree:

The Sample Tree
===============

While no DataWriter is active on the topic, the pane says **No active writer on this topic yet.
Samples appear when one is discovered.**
When the type of the topic was discovered by name only, without its definition, the pane says **Type
information not available**: register the type in a :ref:`Type Registration <register_type>` pane to
decode its samples.

.. _pro_spy_field_actions:

Field Interactions
==================

Right-click a numeric leaf field to open a context menu with a **Plot on Time Series** action.
It opens a new :ref:`Time Series Chart <time_series>` for that field immediately, without going
through the Add menu.

Drag a numeric leaf field from the sample tree and drop it onto an existing
:ref:`Time Series Chart <time_series>` to add that field as a new series on the chart.

Both interactions work with any field whose IDL type is an integer, float, or double.
Struct and array fields can be expanded to reach their numeric children but cannot be dragged or
plotted directly.

The context menu also has **Plot on Event Chart**, which opens a new :ref:`Event Chart <event_charts>`
with this field. It is available for any single value, text and enumerations included. You can also
drop a leaf field onto an Event Chart, or onto a :ref:`Data Table <pro_data_table>` to add the field as
a column.
