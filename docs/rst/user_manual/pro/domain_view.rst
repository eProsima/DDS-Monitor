.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _pro_domain_view:
.. _pro_domain_graph:

###########
Domain View
###########

The *Domain View* shows all entities belonging to the same DDS domain as an interactive graph.
It lists the deployment hierarchy of the domain on the left (hosts, users, processes,
participants and their endpoints) and the topics of the domain across the top.
A line joins each DataWriter or DataReader row to the column of the topic it publishes to or receives
from.
Arrows run from a DataWriter to its topic, and from a topic to its DataReaders.

A line means only that the endpoint is on that topic, not that a writer and a reader matched or that
data flows between them. To check a connection, open the :ref:`Architecture View <pro_architecture_view>`
of the topic.

.. thumbnail:: /rst/figures/screenshots/domain_graph_pro.png
    :align: center

.. _pro_domain_view_opening:

Opening a Domain View
=====================

Open a Domain View in any of these ways:

* Use **Add → Domain View** in the menu bar. The view opens in a new tab.
* Click **+** at the end of the tab strip and choose the **Domain View** tile in the view selector.

With one monitor running, the view opens on its domain. With several, the **Select DDS Domain** dialog
asks which one to show. With none, the **Initialize Monitor** dialog opens first (see
:ref:`pro_initialize_dialogs`).

.. _pro_domain_view_toolbar:

Toolbar
=======

The first row of the toolbar shows **Domain overview · <domain>** and these buttons:

* |minus| **Zoom out (-)** and |plus| **Zoom in (+)** change the size of the graph between 50 % and
  150 %. The zoom percentage between them is **Reset zoom (0)**: click it to go back to 100 %.
* |resize| **Fit diagram** picks the zoom that shows the whole graph.
* |gear| **Configure graph visibility** opens the visibility panel (see
  :ref:`pro_domain_view_visibility`).
* |refresh| **Refresh graph** reloads the graph.
* |question| **Help** opens the help of the view, with a link to this page.

The second row narrows what the graph shows:

* The **Search entities or topics…** box keeps the entities and topics whose name, application, process
  id or topic matches the text.
* The hierarchy selector chooses how much of the hierarchy is drawn:

  * **Full hierarchy** - hosts, users, processes, participants and endpoints.
  * **Hosts only** - one collapsed row per host.
  * **Participants** - the hosts and their participants, without users and processes.
  * **Incompatible QoS** - only the endpoints that report an incompatible QoS, with the entities that
    contain them. When no endpoint reports one, the view says **No incompatible QoS**.

While a search, a topic focus or hidden entities narrow the graph, a line under the toolbar says so,
with **Show all topics** to drop the topic focus and **Clear filters** to drop the search, the focus and
the hidden entities.

.. _pro_domain_view_graph:

Reading the Graph
=================

The header of the entity column counts the hosts, participants, writers and readers shown, and has
|expand_all| **Expand all entities** and |collapse_all| **Collapse all entities**.
A domain with more than 500 endpoints opens with its participants collapsed, and the header then reads
**ENTITIES · COLLAPSED**.
Drag the right edge of the entity column to make it wider or narrower.

Each row shows the entity's icon and name. Depending on what the monitor knows, a row also shows:

* the logo of the DDS vendor and of the application;
* |issues| when the entity reports a warning and |error| when it reports an error (see
  :ref:`pro_problem_panel`);
* |proxy| for a proxy entity (see :ref:`pro_domain_view_proxies`);
* for a host, user, process or participant, the number of endpoints it contains.

Hover a row for its kind, name, vendor, application and process id.

The **DOMAIN TOPICS** header counts the topics shown. Each topic card shows the topic name (a ROS 2
namespace goes on a line of its own above the name) and the number of writers (**W**) and readers
(**R**) on it.

When you collapse a row, the lines of the endpoints it contains become one dashed stem per topic,
labeled with the number of writers and readers it stands for (for example ``2W 1R``).

.. _pro_domain_view_selection:

Selecting Entities and Topics
=============================

Clicking any entity in the graph selects it; its details appear in the
:ref:`pro_info_panel` in the Explorer Panel.

* Click an endpoint to highlight the endpoints on the other side of its topic: the writers that reach a
  reader, or the readers a writer reaches. Click a topic to highlight everything on it. Click the same
  item again, or press :kbd:`Esc`, to clear the selection.
* Double-click a topic to open its :ref:`Architecture View <pro_architecture_view>`. Double-click an
  endpoint to open the Architecture View of its topic with that endpoint already selected.
  Double-click a host, user, process or participant to show its details in the Explorer.
* Hover a topic card and click |architecture| **Open topic architecture** to open its Architecture View.

While something is selected, a bar at the bottom of the view shows its name. For a topic or an endpoint
the bar has two buttons, which act on the topic (for an endpoint, the topic it is on):

* |filter_full| **Focus topic** shows only that topic, its endpoints and the entities that contain
  them. The focus also shows in the visibility panel, as that topic being the only one checked.
* |architecture| **Open topic architecture** (**Architecture** on a narrow view) opens the topic's
  Architecture View.

|cross| **Clear selection** clears the selection.

.. _pro_domain_view_keys:

Keyboard
========

.. list-table::
    :header-rows: 1

    *   - Key
        - Action
    *   - :kbd:`/` or :kbd:`Ctrl+K`
        - Move to the search box.
    *   - :kbd:`Esc`
        - Clear the search, then the topic focus, then the selection.
    *   - :kbd:`↑` :kbd:`↓`
        - Move between rows.
    *   - :kbd:`←` :kbd:`→`
        - Collapse or expand the current row.
    *   - :kbd:`Enter` or :kbd:`Space`
        - Select the current row.
    *   - :kbd:`+` :kbd:`-`
        - Zoom in or out.
    *   - :kbd:`0`
        - Reset the zoom to 100 %.

.. _pro_domain_view_menus:

Context Menus
=============

Right-clicking an entity opens a context menu with the following actions:

- **Show architecture view** - DataWriters and DataReaders only: opens the
  :ref:`Architecture View <pro_architecture_view>` of the endpoint's topic with this endpoint selected.
- **View info** - selects the entity and shows the **Info** tab of the **Entity Info** section, opening
  the Explorer and that section if they are hidden.
- **Change alias** - opens a dialog to assign a custom display name to the entity.
  The alias is used throughout the application.
- **View Problems** - filters the Problem Summary panel to show only issues related to this entity.

Right-clicking a topic opens a context menu with **Change alias** and **View problems** plus the
following actions:

- **Show architecture view** - opens the :ref:`Architecture View <pro_architecture_view>` of this topic.
- **Data type IDL view** - opens a :ref:`dockable_idl_pane` showing the full IDL type definition
  for the topic. For ROS 2 topics the IDL is shown demangled by default; see
  :ref:`ros2_demangling` for details.
- **Set alert** - opens the :ref:`pro_alerts_panel` with the alert creation form pre-filled for this
  topic.
- **Open Data Table** - opens a :ref:`Data Table <pro_data_table>` pane reading this topic.
- **Spy topic data** - opens a :ref:`dockable_spy_pane` for this topic.
- **Publish topic data** - opens a :ref:`publisher_pane` for this topic.
- **Chart topic data** - opens a :ref:`time_series` chart for this topic.
- **Open image view** - opens an :ref:`image_pane` for this topic (only shown for topics with a
  recognized image schema or a custom image mapping).

.. _pro_domain_view_metatraffic:

Metatraffic
===========

Metatraffic entities (*Fast DDS* statistics topics, ROS discovery topics, and their associated
endpoints) are hidden from the graph by default.
While hidden, they do not appear in the domain view or entity lists at all.

To show metatraffic in the graph, go to **View -> Hide/Show Metatraffic**.
When visible, metatraffic topics and their endpoints appear in the domain graph like any other
entity and can be interacted with in the same way.

.. _pro_domain_view_visibility:

Visibility |Pro|
================

You can show or hide individual entities in the graph without removing them from the monitor,
using the right-side configuration panel for the Domain View.

Click the |gear| button in the Domain View toolbar to open the configuration panel.
Each entity type (Topics, Hosts, Users, Processes, Participants, DataWriters, DataReaders) is
listed in its own collapsible section with a checkbox per entity alias.
Clear a checkbox to hide that entity; the entity remains listed and can be restored at any time.
Hiding a container entity (such as a Host or Process) also hides all its descendants: child
entities cannot remain visible as orphan nodes in the graph.
Hiding a topic also hides its DataWriters and DataReaders.

See :ref:`domain-graph` for the full description of the visibility control panel.

.. _pro_domain_view_proxies:

Routed Domains and Proxy Entities
=================================

When multiple monitors are active (see :ref:`multiple_monitors`), each monitor tab shows its own
independent domain graph.
Entities from one domain are not shown in another domain's graph unless they are explicitly
bridged or proxied.

Proxy entities are entities from other domains whose statistics messages are reaching the current
monitor's domain.
This happens, for example, when a *Fast DDS Router* is routing traffic from a different DDS domain
into the monitored domain: the remote entities appear as proxy entities in the graph of the local
domain.
To show or hide them, go to **View -> Hide/Show Proxy Entities**.
When visible, proxy entities appear in the graph and entity lists and their data can be charted.

.. _pro_domain_view_offline:

Recordings and Stopped Monitors
===============================

With a recording open (see :ref:`offline_mode`), the view is titled **Recording overview** and shows the
DataWriters the recording holds. A recording holds no DataReaders, so no topic shows a receiving side,
and the **Incompatible QoS** scope has nothing to show.

When you stop monitoring the domain of a Domain View, the view says so and stops updating. Monitor the
domain again to restore it, or close the tab.
