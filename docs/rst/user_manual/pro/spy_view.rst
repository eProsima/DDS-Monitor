.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _dockable_spy_pane:

#########
Topic Spy
#########

A *Topic Spy* pane subscribes to a DDS topic and shows the live data samples published on it in real
time, displaying each incoming sample as an expandable field tree.
Useful for verifying that the expected data is being published and inspecting individual field values
as they arrive.

.. thumbnail:: /rst/figures/screenshots/spy_pro.png
    :align: center

Opening a Topic Spy
===================

There are several ways to open a new Topic Spy:

* Right-click a topic in the :ref:`topics_panel`, the :ref:`pro_logical_panel`, or the :ref:`domain graph <pro_domain_graph>` and
  choose **Spy topic data**.
* Use **Add → Add Topic Spy** in the application menu bar.
* Click the **Topic Spy** tile in the view selector shown in a tab that has no panes open.
* Click the three-dots button in the header of any existing pane, choose **Split right** or
  **Split down**, and select **Topic Spy** to open a new Spy pane alongside the current one,
  or choose **Replace panel** to replace the current pane with a Topic Spy.

Pane Header Controls
====================

* The header shows the name of the topic being spied.
* |play| / |pause| - starts and stops the live subscription without closing the pane.
* |copy| - copies the last received sample as JSON to the clipboard in one click.
* |help| - opens a contextual help panel with usage tips and a link to this documentation page.
* |maximize_square| / |minimize_square| - maximizes/ minimizes the pane; click again to restore the previous
  layout.
* |gear| - opens the :ref:`right_pane_config` sidebar for this pane.
* The three-dots button opens the split menu to open a new pane to the right or below.
* |cross| - stops the subscription and removes the pane.

Right-Side Configuration Panel |Pro|
====================================

When the :ref:`right_pane_config` sidebar is open for a Topic Spy it shows four sections:

* **Pane Settings** - select a different domain and topic, then apply with **Apply & Reset**,
  which restarts the subscription on the new topic immediately.
* **Playback** - toggle to start or stop the live subscription without leaving the sidebar.
* **Actions** - **Expand All** and **Collapse All** to unfold or fold the entire sample tree at once,
  **Clear** to discard all received samples, and **Copy JSON to Clipboard** to copy the last sample.
* **Panel Actions** - **Replace panel**, **Split right**, and **Split down** submenus, to replace the
  current pane or open a new pane alongside it.

You can have several Topic Spy panes open at once, each subscribing to a different or the same topic.

Field Interactions
==================

Individual fields within an expanded sample tree are interactive beyond just reading their values.

**Right-click a numeric leaf field** to open a context menu with a **Plot field** action.
Selecting it opens a new :ref:`Time Series Chart <time_series>` for that field immediately, without
having to navigate the Add menu.

**Drag a numeric leaf field** from the sample tree and drop it onto an existing
:ref:`Time Series Chart <time_series>` to add that field as a new series on the chart.

Both interactions work with any field whose IDL type is an integer, float, or double.
Struct and array fields can be expanded to reach their numeric children but cannot be dragged or
plotted directly.
