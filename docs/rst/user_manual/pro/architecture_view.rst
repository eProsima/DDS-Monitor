.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _pro_architecture_view:

#######################
Architecture View |Pro|
#######################

The *Architecture View* is bound to one topic. It lists the topic's DataWriters under **PUBLISHERS**
and its DataReaders under **SUBSCRIBERS**, draws the connections between them, and describes the
selected writer-reader pair in the *Connection Inspector*: its QoS side by side, its traffic, and what
each endpoint reports about the connection.

Everything in this view describes connection state, which is not the same as sample delivery: two
endpoints can be matched and reported and still not exchange data.
The connection reports come from the *Fast DDS* Monitor Service of the monitored applications, and the
traffic figures from their statistics (see :ref:`statistics_readers_panel`).

.. thumbnail:: /rst/figures/screenshots/architecture_view_pro.png
    :align: center

.. _pro_architecture_view_opening:

Opening an Architecture View
============================

Open an Architecture View in any of these ways:

* Right-click a topic in the :ref:`topics_panel`, the :ref:`pro_logical_panel` or the Domain View and
  choose **Show architecture view**.
* Right-click a DataWriter or DataReader in the Explorer or the Domain View and choose **Show
  architecture view**. The view opens on the endpoint's topic with the endpoint selected.
* In the Domain View, double-click a topic or an endpoint, or use |architecture| **Open topic
  architecture** (see :ref:`pro_domain_view_selection`).
* Use **Add → Architecture View** in the menu bar (in a new tab), or click **+** at the end of the tab
  strip and choose the **Architecture View** tile in the view selector.

When an Architecture View of the topic is already open, its tab comes to the front instead.

A view opened from the **Add** menu or the view selector has no topic yet. It shows a **New Architecture
View** placeholder, and the **NEW ARCHITECTURE VIEW** panel opens on the right: choose the **MONITOR**
and the **TOPIC**, then click **Open topic**. **Cancel** in the panel, or |cross| in the placeholder,
discards the view and brings back the view selector.
Once a topic is chosen, the tab stays bound to it.

.. _pro_architecture_view_toolbar:

Toolbar
=======

The first row shows **Architecture overview · <topic>**, the type of the topic, the monitor, and the
number of writers and readers. Right-click the title for the topic menu (see
:ref:`pro_domain_view_menus`). The buttons are:

* |minus| **Zoom out (-)**, **Reset zoom (0)** (the zoom percentage) and |plus| **Zoom in (+)**, as
  in the Domain View.
* |resize| **Fit every endpoint** picks the zoom that fits the longer column in the view.
* |question| **Help** opens the help of the view.

The second row has:

* **Search endpoints…**, which keeps the endpoints whose name, participant, host, process or GUID
  matches the text.
* **Connections**, which chooses the connections drawn:

  * **Selected endpoints** - the connections of the selected endpoints (see
    :ref:`pro_architecture_view_selection`).
  * **All connections** - every writer to every reader. When the topic has more than 2000 possible
    connections, the view does not draw them and says **Too many connections to draw. Search to narrow
    the endpoints.**
  * **Incompatible QoS** - only the connections with a reported QoS incompatibility.

* **Layout**, which chooses how the endpoints are arranged:

  * **Topic links** - writers on the left, readers on the right, with the connections between them.
  * **Deployment** - the same endpoints grouped by host and process. Endpoints whose host or process is
    not known are grouped under **Unknown**.

.. _pro_architecture_view_selection:

Selecting Endpoints
===================

* Click a DataWriter to see every reader it connects to, or a DataReader to see every writer that
  reaches it.
* Select a writer and a reader to narrow the graph to that one connection. The Connection Inspector
  then describes the pair.
* Click a selected card again to release it.

The view opens with the first DataWriter selected, unless it was opened on an endpoint.
Right-click an endpoint for its context menu (see :ref:`pro_domain_view_menus`).

Each card shows whether the endpoint is a **DataWriter** or a **DataReader**, its name and a badge with
the state of its connection to the selected endpoint. A red badge names the incompatible QoS policies.
Hover a card for the endpoint's name, GUID and participant.
Endpoints that are no longer alive stay in the view, faded.

The legend under the graph explains the lines:

* **Reported link** (solid) - the endpoints report this connection.
* **Unconfirmed pair** (gray, dashed) - an endpoint reported its connections but did not list this peer.
  This is unconfirmed, not broken: the other end may not run the *Fast DDS* Monitor Service.
* **QoS incompatible** (red, dashed) - an incompatible QoS is reported for this pair.
* **No report** (amber, dashed) - no connection report is available.

.. _pro_architecture_view_inspector:

Connection Inspector
====================

The **CONNECTION INSPECTOR** on the right side of the view shows the selected pair as
``<writer> → <reader>`` with a state badge, or **No pair selected**. Drag its left edge to resize it.
|copy| **Copy everything (Overview, QoS and Evidence)** copies the content of its three tabs to the
clipboard.

The state badge says what the reports establish about the pair, for example **Connection reported ·
both endpoints**, **Connection reported · writer only**, **QoS incompatible**, **Conflicting reports**,
**Not reported** or **Unknown · no reports available**.

**Overview**
    A summary of what the reports show, then:

    * **COMMUNICATION** - **Delivery mode**, **Observation coverage** (which endpoints have reported)
      and **Last observed change**.
    * **TRAFFIC** - **Fast DDS latency**, **Publication throughput** and **Subscription throughput**,
      as medians over the last 30 seconds. **Not measured** means that there is no sample for that
      statistic, usually because it is not enabled.
    * **IDENTITY** - **Writer GUID** and **Reader GUID**.

**QoS**
    The **OFFERED VS REQUESTED** table compares, policy by policy, what the writer offers and what the
    reader requests: **Reliability**, **Durability**, **Deadline**, **Liveliness**, **Ownership**,
    **Destination order**, **Latency budget**, **Presentation**, **Partition**, **Lifespan** and
    **Data sharing**. A row is highlighted in red only when an endpoint reports that policy as
    incompatible for this exact pair, and its |link| button opens the compatibility rule of the policy.

**Evidence**
    * **MONITOR SERVICE REPORTS** - whether the writer's report lists the reader, and the reader's
      report lists the writer. An endpoint whose application does not enable the *Fast DDS* Monitor
      Service has no report.
    * **REMOTE-SPECIFIC QOS REPORT** - the **Incompatible policy** an endpoint reports against this
      pair.
    * **WRITER-REPORTED LOCATORS** - the **Delivery mode** and the **Used** and **Announced** locators.

.. _pro_architecture_view_qos_incompatibility:

Showing a QoS Incompatibility
=============================

To find and show the pair behind a QoS incompatibility:

#. In the Domain View, choose **Incompatible QoS** in the hierarchy selector to list the endpoints that
   report one.
#. Double-click one of them. The Architecture View of its topic opens with that endpoint selected.
#. Choose **Incompatible QoS** under **Connections**. Only the incompatible connections remain, drawn as
   red dashed lines.
#. Select the DataWriter and the DataReader at the two ends of a red line. Their badges name the
   incompatible policy.
#. Open the **QoS** tab of the Connection Inspector. The highlighted row shows what the writer offers
   and what the reader requests for the incompatible policy.

.. _pro_architecture_view_offline:

Recordings and Stopped Monitors
===============================

With a recording open (see :ref:`offline_mode`), the view shows the DataWriters the recording holds, with
their QoS and the host, process and participant they ran in. A recording holds no DataReaders and no
Monitor Service reports, so there are no connections to show, and the header says **evidence
unavailable**.

When you stop the monitor of an Architecture View, the view says so and stops updating. Start that
monitor again to restore it, or close the tab.
