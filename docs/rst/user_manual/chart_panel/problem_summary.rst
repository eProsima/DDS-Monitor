.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _problem_summary_panel:

#####################
Problem Summary Panel
#####################

This expandable and collapsible section displays all the collected problems per entity, for example
DataReader samples lost, incompatible QoS between endpoints, or the DataWriter deadline missed counter.
Entities that have reported a problem display a warning or an error icon next to the entity name,
depending on the severity of the problem. The entity in the domain graph may also display that icon.

.. thumbnail:: /rst/figures/screenshots/problem.png
    :align: center

Error Messages
==============

Errors are serious issues that prevent DDS entities from communicating.
Entities with these issues display an error icon next to their entity name.
Only one type of error can be reported, :code:`INCOMPATIBLE_QOS`.

- :code:`INCOMPATIBLE_QOS`: Reported when the QoS of the DataWriter and DataReader are incompatible,
  that is, their QoS policies differ in a combination that prevents them from communicating.
  The error message names the entities involved, lists the specific QoS policies that are incompatible,
  and links to the relevant documentation.

Warning Messages
================

Warnings are less severe issues in the communication between DDS entities than errors, but
still require attention. Entities with these issues display a warning icon next to their entity name.
The following warnings can be reported:

- :code:`LIVELINESS_LOST`: Reported when a DataWriter has lost liveliness. It also shows
  the number of times the liveliness has been lost.

- :code:`DEADLINE_MISSED`: Reported when an entity misses a deadline. It also shows the
  number of times a deadline has been missed.

- :code:`SAMPLE_LOST`: Reported when an entity has lost samples. It also shows the number of
  samples lost.
