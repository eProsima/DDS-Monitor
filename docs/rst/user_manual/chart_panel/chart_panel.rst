.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _chart_panel:

############
Charts Panel
############

This panel displays the *Chartboxes* and the series the user creates in them.

Chart series
============
A *DataPoint* in a *Chart Series* in the *DDS Monitor* is one item of a specific type of DDS network
monitoring data. Each *DataPoint* has a timestamp and a real value.
The *timestamp* is the moment the data was created, reported, received, etc., depending on the *DataKind*.
The *value* is the real value of this *DataPoint* for this *DataKind* at the moment of the *timestamp*.

For example, each *DataPoint* of the *DataKind* ``DATA_COUNT`` has a timestamp and an integer value.
This value is the number of ``Data packets`` a *DataWriter* sent since the last time that same data was reported.

Chart view
==========
Every *DataKind* is shown the same way inside a *Chartbox*.
Each data series in the chart is a line of its own color (a chart can have none, one or several), with this format:

- The X axis is the timestamp value of the data.
- The Y axis is the real value that is stored in the data.

These values can be integers, doubles or times, but a given *DataKind* always uses the same
value type. Every point in the chart is an accumulated value of the *DataPoints* of one data kind in a
given time range.

Chartbox kinds
==============

A Chartbox can be historic or dynamic.

- The **historic**  Chartbox shows static data accumulated during the monitor execution.
  The data shown is not updated with new data or refreshed if anything changes.
  See :ref:`historic_series` for details.
- The **dynamic** or **real-time** Chartbox shows the new data the monitor collects in real time.
  Its series update over time with the new data received from a DDS network, so the new data is
  displayed in pseudo-real-time.
  See :ref:`dynamic_series` for details.

Common Series parameters
==========================

Some parameters for creating a Chartbox depend on the kind of Chartbox.
The parameters below are common to both kinds.

.. _data_kind_parameter:

Data kind
---------

The *DataKind* is the specific data that the Chartbox represents.
There is one *DataKind* for each kind of data that a Fast DDS network can report.
(By default a DDS network does not report most of this data. In Fast DDS, it must be
configured beforehand to report it periodically.)

.. _series_label_parameter:

Series label
------------
Name of the new series in the Chartbox.
If not set, the default series name follows this rule:
``<cumulative_function>_<source_entity_kind>-<source_entity_id>_<target_entity_kind>-<target_entity_id>``.

.. _source_entity_id_parameter:

Source Entity Id
----------------
The name and *entity Id* of the entity the data is collected from, in the format ``<name>:\<<id>\>``.
The field groups the Ids by entity kind, which makes the required Id easier to find.

Each *DataKind* is related to one entity kind, usually a *DataWriter* or a *DataReader*,
which produces that *DataKind*.
However, you can choose any entity kind as the source.
If the selected entity does not have this type of data, the monitor looks for the entities it contains
that do report this *DataKind*.
For example, to show the number of packets (``DATA_COUNT``) transmitted by a *Host*,
the monitor looks for all the *DataWriters* in that *Host* and reports the total number of packets.

In this ``DATA_COUNT`` example, the monitor finds every *DataWriter* in the *Host*
by finding every *User* in the *Host*, then every *Process* in those *Users*, then every
*DomainParticipant* in those *Processes*, and finally every *DataWriter* in those *DomainParticipants*.
The chart then shows all the data stored by those *DataWriters*, accumulated by the
cumulative function.
See the :ref:`entities` section for more information on how monitor entities are connected.

Some examples (see :ref:`start_tutorial`) help to understand this functionality.

.. _target_entity_id_parameter:

Target Entity Id
----------------

.. note::

    Not every *DataKind* has a target entity, so the dialog only shows this field when the selected *DataKind*
    requires it.

The name and *entity Id* of the entity the data refers to.
This field works like the :ref:`source_entity_id_parameter`.
Some *DataKinds* have a target entity that the data refers to, and this target must be of a specific entity kind.
If you choose an entity of a different kind, the monitor uses the mechanism explained
in :ref:`source_entity_id_parameter`: it searches for the correct entity kind by following the connections
between entities.

For example, to show the *DataKind* ``FASTDDS_LATENCY``, which is reported by a *DataWriter* and targeted to a
*DataReader*, from an entity ``Host_1`` to an entity ``Host_2`` (both of kind *Host*), the monitor collects the
data as follows:

- Get all the *DataWriters* of ``Host_1`` by searching for its *Users*, their *Processes*, their
  *DomainParticipants* and their respective *DataWriters*.
- Get all the *DataReaders* of ``Host_2`` by searching for its *Users*, their *Processes*, their
  *DomainParticipants* and their respective *DataReaders*.
- Get all the data from the *DataWriters* found that refer to the *DataReaders* found inside the interval set.
- Accumulate the data using the *cumulative function*.

Some examples (:ref:`start_tutorial`) help to understand this functionality.

.. _statistics_kind_parameter:

Statistic kind
---------------
When several data points fall in a single time frame, a *cumulative function* merges them into one.
*Statistic kind* sets this function.

The available methods to merge data points into one are:

- *MEAN*: calculate the mean value of all the data points.
- *STANDARD_DEVIATION*: calculate the standard deviation of all the data points.
- *MAX*: returns the *DataPoint* with the maximum value.
- *MIN*: returns the *DataPoint* with the minimum value.
- *MEDIAN*: calculate the median of all the data points.
- *SUM*: calculate the sum of all the data points.
- *RAW DATA*: returns the data points without any operation performed on them.

If the *Number of bins* is ``0``, the *Statistic kind* is not used, because the data is not accumulated.
