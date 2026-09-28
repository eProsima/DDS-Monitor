.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _pro_alerts_panel:
.. _pro_alerts_panel_layout:

############
Alerts Panel
############

The alerts panel is located on the left side of the application window and allows the user to define
conditions to monitor and receive notifications about specific events in the DDS network.
It consists of two sections:

.. figure:: /rst/figures/screenshots/alert_panel_pro.png
    :align: center

.. _pro_alerts_list_panel:
.. _pro_alert_list_layout:

Alerts List
===========

Displays the list of alerts defined by the user.
Alerts are created using the |create_alert| button in the Shortcuts Bar or the **+** button in the
upper-right corner of the panel.
Selecting an alert highlights it and shows its details in the :ref:`pro_alert_info_panel`.
Right-click an alert to remove it.

.. _pro_alert_info_panel:
.. _pro_alert_data_layout:

Alert Info
==========

Displays the configuration of the alert currently selected in the Alerts List, including its
domain, host, id, kind, name, time between triggers, topic, and user.

For alert event notifications, see :ref:`pro_alert_messages_panel`.

.. _pro_alert_configuration_panel:

Alert Configuration
===================

The **Configuration** tab in the lower section of the Alerts Panel provides an integrated form for
creating and editing alert rules without opening a separate dialog.

.. figure:: /rst/figures/screenshots/alert_configuration_pro.png
    :align: center

The |help| button is available at the right side of the Configuration tab header.
Clicking it opens a contextual popover with a short description of the pane and tips.

The form contains the following fields:

- **Alert kind** - selects the DDS metric to monitor. The currently supported kinds are
  ``NO_DATA`` (fires when a topic stops receiving data) and ``NEW_DATA`` (fires when new data is
  published on a topic).
- **Alert name** - a human-readable label for the alert rule. It is generated automatically from the
  selected kind and entity, but can be overridden manually.
- **Domain** - the DDS domain to monitor. Only domains currently being monitored are listed.
- **Host / User / Topic** - optional entity filters that narrow the scope of the alert to a specific
  host, user process, or topic. Each filter can be set from the discovered entities or entered
  manually using the override toggle.
- **Threshold** - the numeric value that triggers the alert when the metric crosses it. The units
  shown next to the field depend on the selected alert kind.
- **Time between alerts (ms)** - the minimum interval between two consecutive firings of the same
  alert rule, in milliseconds.
- **Alert timeout (ms)** - how long the alert can go without receiving any sample of its metric
  before it reports a timeout message (*Alert <name> timed out*), in milliseconds.
- **Script** - an optional path to a script executed when the alert fires.

Click **Add Alert** to add a new alert rule, or **Save Changes** to update an existing one after
selecting it in the Alerts List.

.. _pro_alert_kind_no_data:

NO_DATA
-------

The ``NO_DATA`` alert kind monitors the **subscription throughput** of a topic endpoint and fires
when the data flow drops below a defined rate.

- **Underlying statistic**: ``SUBSCRIPTION_THROUGHPUT`` - the bytes per second received by a
  subscription endpoint on the monitored topic.
- **Trigger condition**: fires as soon as a reported throughput sample is **less than** the
  configured threshold (subject to the time between alerts). Independently, if no throughput sample
  is received for the alert timeout, a timeout message is reported.
- **Typical use**: detect that a publisher has stopped publishing or that a topic has gone silent
  unexpectedly.

The following fields are active for ``NO_DATA``:

- **Threshold** - the minimum acceptable throughput in **bytes/sec**. The alert fires when the
  measured rate falls below this value. The default is ``500.0`` bytes/sec.
- **Alert timeout (ms)** - how long (in milliseconds) the alert can go without receiving any
  throughput sample before it reports a timeout message. Use this to detect a subscription that
  stops reporting statistics entirely.
- **Time between alerts (ms)** - minimum interval between two consecutive firings of the same rule.
- **Host / User / Topic** - narrow the monitored subscription to a specific entity.
- **Script** - optional script path executed when the alert fires.

.. _pro_alert_kind_new_data:

NEW_DATA
--------

The ``NEW_DATA`` alert kind monitors the **data sample count** sent by a topic endpoint and
fires as soon as new data is published.

- **Underlying statistic**: ``DATA_COUNT`` - the cumulative number of DATA/DATAFRAG sub-messages
  sent by a DataWriter on the monitored topic.
- **Trigger condition**: fires whenever a matching DataWriter reports a ``DATA_COUNT`` sample
  greater than zero (subject to the time between alerts).
- **Typical use**: detect the first publication of data on a topic that is expected to be idle, or
  confirm that a specific publisher has resumed sending.

The following fields are active for ``NEW_DATA``:

- **Time between alerts (ms)** - minimum interval between two consecutive firings of the same rule.
  Use a larger value to avoid repeated notifications on a high-frequency topic.
- **Host / User / Topic** - narrow the monitored publisher to a specific entity.
- **Script** - optional script path executed when the alert fires.

The **Threshold** and **Alert timeout** fields are not configurable for ``NEW_DATA``: the alert uses
a fixed greater-than-zero comparison on the reported count, so it triggers on every new ``DATA_COUNT``
report regardless of the data value.
