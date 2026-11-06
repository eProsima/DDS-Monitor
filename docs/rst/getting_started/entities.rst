.. include:: ../exports/alias.include

.. _entities:

########
Entities
########

The *DDS Monitor* tracks the activity of a set of *Entities* and stores the connections and data exchanged
between them to present them to the user.
These entities are DDS communication entities, or physical elements related to DDS entities.

The following diagram shows the kinds of entities the monitor tracks.
Each arrow is a direct connection between two kinds of entities (not a 1:n in every case).
Entities (or types of entities) without a direct relationship are still related indirectly through
intermediate entities.
For example, a *DomainParticipant* is related to its *User* through its *Process*.

.. _fig_entities_diagram:

.. figure:: /rst/figures/entities_diagram.svg

.. _dds_entities:

DDS Entities
============

These are the DDS entities that manage the communication: the *DomainParticipants*,
*DataWriters* and *DataReaders*.
Each *DataReader/DataWriter* has one or more associated *Locator* entities.
*Locators* are the network addresses through which *DataReaders/DataWriters* communicate in a DDS network.

For more information about each entity, see the |DDSSpecification| or the |FastDDSDocs|.

.. _participant_entity:

DomainParticipant
-----------------
*DomainParticipant* is the main entity in the DDS protocol.
It groups a collection of *DataReaders/DataWriters*, and manages the whole DDS Discovery of other
*DomainParticipants* and *DataReaders/DataWriters* within the DDS Domain to which it belongs.
Refer to `DomainParticipant Fast DDS Documentation
<https://fast-dds.docs.eprosima.com/en/latest/fastdds/dds_layer/domain/domainParticipant/domainParticipant.html>`_
for a more detailed explanation of the *DomainParticipant* entity in DDS.

Each *DomainParticipant* communicates under a single *Domain*
(see :ref:`logical entities <logical_entities>` section), so each *DomainParticipant* is directly connected to the
*Domain* in which it operates. As the :ref:`entities diagram <fig_entities_diagram>` shows, *DomainParticipant*
entities are contained within a *Process*. A system process (the *Process* entity) runs an application using
*Fast DDS*, which instantiates *DomainParticipants*. The same applies to the *DataReaders* and *DataWriters*
created by a *DomainParticipant* in that *Process*. A *Process* therefore contains every DDS entity that the
*Fast DDS* application running in it has instantiated.

.. _datawriter_entity:

DataWriter
----------
*DataWriter* is the DDS entity responsible for publishing data.
Each *DataWriter* is directly contained within a single *DomainParticipant*.
A *DataWriter* is also associated with the *Topic* it publishes under, so each *Topic* contains all the
*DataWriters* publishing under it.

Each *DataWriter* is therefore directly connected to the *DomainParticipant* it belongs to
and the *Topic* under which it publishes.
A *DataWriter* is also associated with one or more *Locators*, representing the physical communication
channels it uses to send data.

.. _datareader_entity:

DataReader
----------
*DataReader* is the DDS entity responsible for subscribing to data.
As with the *DataWriter*, each *DataReader* is directly contained within a single *DomainParticipant*.
A *DataReader* is also associated with the *Topic* it is subscribed to,
so each *Topic* contains all the *DataReaders* subscribed to it.
Each *DataReader* is therefore directly connected to the *DomainParticipant* it belongs to,
and to the *Topic* to which it is subscribed.

.. _locator_entity:

Locator
-------
*Locator* represents the physical address and port that a *DataReader/DataWriter* uses to send and/or receive data.
It belongs to the physical division of the entities, as every *Locator* belongs to a single *Host*
(see section :ref:`physical_entities`).
However, the monitor treats it as a *DDS Entity* to keep the entity connections simpler and easier
to understand.

A *Locator* is connected to one or more *DataReaders/DataWriters*. It is related to a *Host*
through those *DataReaders/DataWriters*, their *DomainParticipant*, and that *DomainParticipant*'s
*Host*.

.. _logical_entities:

Logical Entities
================

.. _domain_entity:

Domain
------
*Domain* is a logical abstraction in the DDS protocol that divides the DDS network into partitions.
Each *Domain* is completely independent and unaware of any others.
This logical partition depends on the chosen discovery protocol.

With the *Simple Discovery Protocol* (the default discovery protocol in *Fast DDS*), the *Domain* is a number
(domain ID), and every DDS entity in that *Domain* discovers the rest of the entities deployed on it.
With *Discovery Server*, the partition is defined by the *Discovery Server*
or *Discovery Servers Net* the monitor connects to. See the
`Fast DDS documentation <https://fast-dds.docs.eprosima.com/en/latest/fastdds/discovery/discovery_server.html>`_ for
more information about this feature.
Each entity connected to a *Discovery Server* on the same network knows all other entities it needs to
communicate with.

In the monitor, this entity is related to the *DomainParticipants* that communicate under this same *Domain*,
and the *Topics* created in this *Domain*.

.. _topic_entity:

Topic
-----
*Topic* is an abstract DDS entity that represents the communication channel between publishers and subscribers.
Every *DataReader* subscribed to a *Topic* receives the publications of every *DataWriter*
publishing under the same *Topic*.

In the monitor, this entity is directly connected to the *Domain* it belongs to,
and to the *DataReaders/DataWriters* communicating under that *Topic*.

.. _physical_entities:

Physical Entities
=================

.. _host_entity:

Host
----
*Host* is the physical (or logical, e.g. Docker) machine where one or more DDS *Processes*
are running.
This entity is directly connected to the *Users* running in this *Host*.

.. _user_entity:

User
----
*User* is each user that runs in a *Host*.

This entity is directly connected to the *Host* it belongs to, and to the *Processes* running
under this *User*.

.. _process_entity:

Process
-------
*Process* is each process running an application using *Fast DDS*. A *Process* can
run more than one *DomainParticipant*, and those *DomainParticipants* do not need to be related to
each other, or even be under the same *Domain*.

This entity is directly connected to the *User* it belongs to, and to the *Participants* running within it.

Proxy Entities
================

.. _proxy_entities:

If the monitor receives statistics from a writer that does not belong to any monitored domain, the entities associated
with that data are treated as *Proxy entities*. These entities may contain limited information, because the monitor
infers them from the received statistics messages instead of discovering them directly. They have the field
``discovery_source`` set to ``proxy``, while entities discovered through DDS discovery protocols have the value
``discovery``. You can show or hide these entities with the "Hide/Show Proxy entities" option in the View Menu
(see :ref:`view_menu`), and you can also use them in the statistics charts.
