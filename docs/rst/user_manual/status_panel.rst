.. include:: ../exports/alias.include
.. include:: ../exports/roles.include

.. _status_panel:

############
Status Panel
############

The status panel in the left sidebar shows settings of the monitored entities and general information about the
state and events of the monitor.

Status SubPanel
===============

This panel shows a short summary of the current state of the *DDS Monitor*:

* *Entities*:

  * *Domains*: The Domains initialized in the Monitor so far.
  * *Entities*: Total number of tracked entities.

.. _log_panel:

Log SubPanel
============

This panel shows the events the application has received.
Events arrive as *callbacks* when new entities join the network or are discovered, or when the DDS network state
changes.
Each callback contains the entities discovered by the Monitor and the time it happened.
You can clear this list with :ref:`clear_log`.
