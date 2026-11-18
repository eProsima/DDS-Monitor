.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _bottom_panels:
.. _pro_bottom_panel:

#############
Bottom Panels
#############

Three panels sit at the bottom of the *DDS Monitor Pro* window: alert notifications, a problem
summary, and a live entity counter.

.. _pro_alert_messages_panel:
.. _pro_alert_messages_panel_layout:

Alert Messages Panel
====================

The alert messages panel is in the collapsible section at the bottom of the application
window.
It lists the alerts triggered by the application in a tree structure, grouped by the name of the
alert rule that produced them.
Messages are shown with the most recent entries at the bottom.
Each entry shows the alert message and the timestamp of when the alert was triggered.

.. figure:: /rst/figures/screenshots/alert_messages_panel_pro.png
    :align: center

.. _pro_problem_panel:
.. _pro_problem_summary:

Problem Summary
===============

The *Problem Summary* is a collapsible section at the bottom of the main panel.
It lists all detected problems per entity, including data samples lost, incompatible QoS between
endpoints, and missed DataWriter deadlines.
Where applicable, the problem entry includes a link to the relevant documentation.

Entities with reported problems also display a warning or error icon next to their name in the
:ref:`Domain View <pro_domain_view>`.

.. thumbnail:: /rst/figures/screenshots/problem_detail_pro.png
    :align: center

.. _entity_summary_bar:
.. _pro_status_bar:

Entity Summary Bar |Pro|
========================

The *Entity Summary Bar* is a compact counter strip in the bottom status bar of the window.
It shows the total number of the four main DDS entity types discovered across all active monitors,
so you can read them without opening any panel.

The bar shows four counters inline:

* |participant| - total number of DomainParticipants discovered.
* |datawriter| - total number of DataWriters discovered.
* |datareader| - total number of DataReaders discovered.
* |topic| - total number of distinct DDS Topics discovered.

All four values aggregate across every active monitor tab and update automatically as entities are
discovered or removed.
When the **Show Proxy Entities** option is enabled in the **View** menu, a blue asterisk appears
after the counters to show that proxy entities are included in the totals.

Hovering over the counter strip shows a tooltip that lists the four values under the heading
*Entities discovered*, with each entity type written out by name (*Participants*, *Writers*, *Readers* and *Topics*).
When proxy entities are visible and at least one proxy entity of a given type exists, the tooltip
shows the proxy count in parentheses next to the total for that type.

The status bar also shows:

- A dot and a text that say what is being monitored: *Not monitoring* (gray dot); *Monitoring · Domain 0*
  (green dot), which names up to two monitors, or *Monitoring · 3 monitors* when there are more; and
  *Recording playback* in :ref:`offline mode <offline_mode>`.
- At the right end, while the MCP server runs, the MCP chip: the name assistants know this window by
  and the connected assistant.
  Click it to open the AI Assistants window (see :ref:`pro_mcp_chip`).

.. figure:: /rst/figures/screenshots/status_bar_pro.png
    :align: center
