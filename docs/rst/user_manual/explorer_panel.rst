.. include:: ../exports/alias.include
.. include:: ../exports/roles.include

.. _left_panel:

##############
Explorer Panel
##############

The left sidebar shows the entities known to the application and their information.
The section :ref:`entities` describes the kinds of entities shown and how they connect to each other.

.. _dds_panel:

DDS Panel
=========
This panel shows all the :ref:`dds_entities` the monitor has discovered so far in every monitored
DDS domain or Discovery Server.
When a DDS Monitor entity is selected, it shows only the DDS entities related to it
(see :ref:`selected_entity`).
For example, you can track the DDS entities created by an application running on a specific *Host*,
*User*, or *Process*, or the DDS entities working on a specific DDS domain or publishing or
subscribed to a given *Topic*.
Every entity in this panel is interactive:

- Double-click the Participant name or icon to expand or collapse the list of
  DataWriters/DataReaders of that Participant.
- Double-click the DataReader/DataWriter name or icon to expand
  or collapse the list of Locators of that DataReader/DataWriter.
- Click an entity to set it as *selected*.
  See :ref:`selected_entity` for what selecting an entity means.

.. _physical_panel:

Physical Panel
==============
This panel shows all the :ref:`physical_entities` the monitor has discovered so far.
As in the :ref:`dds_panel`, every entity in this panel is interactive:

- Double-click the Host name or icon to expand or collapse the list of Users of the Host.
- Double-click the User name or icon to expand or collapse the list of Processes of the User.
- Click an entity to set it as *selected*.
  See :ref:`selected_entity` for what selecting an entity means.

.. _logical_panel:

Logical Panel
=============
This panel shows all the monitored :ref:`logical_entities`.
DDS Monitor monitors only the DDS domains you specify (see :ref:`monitor_domain`).
Domains cannot be discovered dynamically and must be predefined, so no other domains appear here.
This panel only updates the information of those domains.
For example, if you are monitoring Domain X
and an application using Fast DDS creates a new DomainParticipant in that domain with a DataWriter publishing in
Topic Y, Topic Y appears in this view under Domain X, the domain of
the discovered DomainParticipant.

As in the :ref:`dds_panel`, every entity in this panel is interactive:

- Double-click the Domain name or icon to expand or collapse the list of Topics of the Domain.
- Click an entity to set it as *selected*.
  See :ref:`selected_entity` for what selecting an entity means.


.. _info_panel:

Info Panel
==========
This panel shows the information of the currently **selected** entity
(see :ref:`selected_entity`).
Some fields are common to all entity kinds, and others depend on
the entity kind:

* **General fields**

  * **name**: internal name of the entity
  * **id**: internal unique id for each entity
  * **kind**: kind of entity (e.g. host)
  * **alive**: if the entity is alive or not
  * **alias**: alias of the entity given by the user
  * **metatraffic**: if the entity is processing metatraffic data or not
  * **status**: status of the entity
  * **discovery_source**: how the entity was discovered ("discovery" if using DDS discovery protocol,
    "proxy" if discovered through statistics messages)

* **Process**

  * **pid**: Process Id in its host

* **Topic**

  * **type_name**: name of the data type of the topic

* **Domain**

  * **domain_id**: The domainId used to identify the DDS domain.

* **Participant**

  * **GUID**: DDS GUID
  * **QoS**: DDS QoS information

* **DataWriter**

  * **GUID**: DDS GUID
  * **QoS**: DDS QoS information

* **DataReader**

  * **GUID**: DDS GUID
  * **QoS**: DDS QoS information


.. _statistics_panel:

Statistics Panel
================
This panel shows a summary of some data types of the currently **selected** entity
(see :ref:`selected_entity`).
The data is collected from all the entities related to the selected one.
It is calculated by accumulating the data of this entity (using a specific `StatisticKind` in
each case) in one bin, from the first to the last data available.
If no entity is selected, the panel shows the data of all the entities in the
application.
The data shown is:

.. list-table::
    :header-rows: 1

    *   - Data Kind
        - Statistic kind
        - Description
    *   - `FASTDDS_LATENCY`
        - `MEDIAN`
        - Median value of Application Latency |br|
    *   - `FASTDDS_LATENCY`
        - `STANDARD_DEVIATION`
        - Standard deviation value of Application Latency |br|
    *   - `PUBLICATION_THROUGHPUT`
        - `MEDIAN`
        - Median value of Publication Throughput |br|
    *   - `PUBLICATION_THROUGHPUT`
        - `STANDARD_DEVIATION`
        - Standard deviation value of Publication Throughput |br|
    *   - `SUBSCRIPTION_THROUGHPUT`
        - `MEDIAN`
        - Median value of Subscription Throughput |br|
    *   - `SUBSCRIPTION_THROUGHPUT`
        - `STANDARD_DEVIATION`
        - Standard deviation value of Subscription Throughput |br|
    *   - `RESENT_DATA`
        - `MEAN`
        - Mean value of Data packages that had to be resent |br|
    *   - `HEARTBEAT_COUNT`
        - `SUM`
        - Total number of `Heartbeat` messages |br|
    *   - `ACKNACK_COUNT`
        - `SUM`
        - Total number of `Acknack` messages |br|
    *   - `NACKFRAG_COUNT`
        - `SUM`
        - Total number of `Nackfrag` messages |br|
    *   - `GAP_COUNT`
        - `SUM`
        - Total number of `Gap` messages |br|
    *   - `DATA_COUNT`
        - `SUM`
        - Total number of `Data` messages |br|
    *   - `PDP_PACKETS`
        - `SUM`
        - Total number of PDP packets sent |br|
    *   - `EDP_PACKETS`
        - `SUM`
        - Total number of EDP packets sent |br|

