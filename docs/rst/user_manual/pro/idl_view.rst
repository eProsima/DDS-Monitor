.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _dockable_idl_pane:

################
Topic Type (IDL)
################

A *Topic Type (IDL)* pane displays the Interface Definition Language (IDL) type description for a selected
DDS topic in a scrollable, selectable monospace text view.
When a topic is not yet discovered, the pane waits and loads the IDL automatically once the topic
becomes available.

.. thumbnail:: /rst/figures/screenshots/idl_pro.png
    :align: center

.. _pro_idl_opening:

Opening a Topic Type (IDL) Pane
===============================

To open a new Topic Type (IDL) pane, do one of the following:

* Right-click a topic in the :ref:`topics_panel`, the :ref:`pro_logical_panel`, or the :ref:`Domain View <pro_domain_view>` and
  choose **Data type IDL view**.
* Use **Add → Topic Type (IDL)** in the application menu bar.
* Click the three-dots button in the header of any existing pane, choose **Split right** or
  **Split down**, and select **Topic Type (IDL)** to open a new Topic Type (IDL) pane alongside the current
  one, or choose **Replace panel** to replace the current pane with a Topic Type (IDL) pane.

.. _pro_idl_title_bar:

Pane Header Controls
====================

* The header shows the type name of the topic followed by "(IDL)".
* |copy| **Copy IDL** - copies the full IDL text to the clipboard.
* |question| **Help** - opens a contextual help panel with usage tips and a link to this documentation page.
* |expand_square| **Expand** / |collapse_square| **Collapse** - maximizes or minimizes the pane; click again to restore the previous
  layout.
* |gear| **Panel Settings** - opens the :ref:`right_pane_config` sidebar for this pane.
* |three_dots_menu| **Split** - opens the split menu, for opening a new pane to the right or below.
* |cross| **Close** - closes the pane.

.. _pro_idl_text_area:

Text Area Interactions
======================

* Select text with the mouse or keyboard.
* Right-clicking opens a context menu with **Copy** (copies the selection, or the full IDL if nothing
  is selected) and **Select All**.

When the type of the topic was discovered by name only, without its definition, the pane says **IDL
not available**: register the type in a :ref:`Type Registration <register_type>` pane to complete it.

.. _ros2_demangling:

ROS 2 Demangling
================

ROS 2 wraps its type names in a mangled format when publishing over DDS (for example,
``std_msgs::msg::dds_::String_`` instead of
``std_msgs/msg/String``).
*DDS Monitor* can reverse this mangling to show the original ROS 2 type name and a clean IDL
representation that is directly usable with *Fast DDS Gen*.

When demangling is active, a badge reading **ROS 2 Demangling applied** appears in the upper-right
corner of the Topic Type (IDL) pane of a ROS 2 topic. It means the displayed IDL is not the raw on-the-wire representation.

Demangling is enabled by default and applies to all Topic Type (IDL) panes at once.
To toggle it, use:

- **View → Revert ROS 2 Demangling** to show the raw representation.
- **View → Perform ROS 2 Demangling** to restore the clean representation.

The same toggle is also in the **DISPLAY** section of the right-side configuration panel for any
open Topic Type (IDL) pane.

.. _pro_idl_config:

Right-Side Configuration Panel |Pro|
====================================

When the :ref:`right_pane_config` sidebar is open for a Topic Type (IDL) pane it shows five sections:

* **TOPIC** - shows the current topic name, monitor, and resolved type name as read-only
  labels.
* **CHANGE TOPIC** - select a different monitor and topic, then apply with **Apply & Reset**, which
  fetches and displays the IDL for the new topic immediately.
* **DISPLAY** - toggle to enable or disable :ref:`ros2_demangling` for the current pane.
  This setting applies to all Topic Type (IDL) panes at once.
* **ACTIONS** - **Copy IDL to Clipboard** to copy the full IDL text, and **Select All** to select it.
* **PANEL ACTIONS** - **Replace panel**, **Split right**, and **Split down** submenus, to replace the
  current pane or open a new pane alongside it.
