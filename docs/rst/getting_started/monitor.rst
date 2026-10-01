.. include:: ../exports/alias.include
.. include:: ../exports/roles.include

.. _monitor_domain:

##############
Monitor Domain
##############

This application tracks the :ref:`entities` that belong to the DDS communication protocol or are related to it.
The DDS communication protocol (see |DDSSpecification|) divides a DDS network into independent
partitions called :ref:`domain_entity`.
Only entities in the same Domain can discover and communicate with each other.
How a Domain is defined depends on the *Discovery Protocol* in use.
This application implements two *Discovery Protocols* that can be used to monitor entities.

Several Domains can be monitored at the same time.
The :ref:`logical_entities` and the :ref:`dds_entities` under a Domain are never shared with other Domains
(except for the special case of the :ref:`locator_entity`).
The :ref:`physical_entities` can be shared between entities in different Domains,
so the same :ref:`host_entity` or :ref:`locator_entity` can be related to entities in several Domains.

To monitor a Domain, use the :ref:`init_monitor_button` button, where you can
manually specify the configuration of a Discovery type.
Once a Monitor is initialized in a Domain, the application starts discovering the entities in that Domain and
collecting their data.
Every newly discovered entity or data is notified as a callback in the :ref:`log_panel`.

.. note::

    The *DDS Monitor* discovers entities through the DDS protocol,
    so discovery is not instantaneous or simultaneous.

.. _simple_discovery_monitor:

Simple Discovery Monitor
========================
The DDS Simple Discovery Protocol (SDP) relies on the discovery of individual entities through multicast communication.
You do not need prior knowledge of the network or its architecture to create a new
monitor that connects with the *Participants* already running in the same network.
To configure this kind of Domain monitoring, you only need the number of the Domain to track.
Additional options can be configured using the *Advanced options* button (see :ref:`monitor_advanced_configuration`).

.. _monitor_advanced_configuration:

Advanced Options
----------------
The *Advanced options* button in the *Initialize Monitor* dialog configures additional parameters.

If you enable any advanced option, the *OK* button is enabled only when all inputs are correct.

The supported advanced options are:

- **Easy Mode**:
  Specifies the IP address of the remote discovery server used in a
  `ROS 2 Easy Mode <https://docs.vulcanexus.org/en/latest/rst/enhancements/easy_mode/easy_mode.html>`_ scenario.
  If you enable this option, enter a valid IPv4 address in the text input.

.. _discovery_server_monitor:

Discovery Server Monitor
========================
The `Discovery Server <https://www.eprosima.com/index.php/products-all/tools/eprosima-discovery-server>`_
discovery protocol is a *Fast DDS* feature that centralizes the discovery phase in a single or a network of
*Discovery Servers*.
It reduces discovery traffic and avoids some problems that can appear with the Simple Discovery Protocol and
multicast.

To configure this type of Domain monitoring, you need one or more Discovery Server network addresses (locators).
In the *Initialize Discovery Server Monitor* dialog, each locator is set in its own row, choosing its
*Transport Protocol* (``UDPv4``, ``UDPv6``, ``TCPv4`` or ``TCPv6``) and entering the *IP* and *Port* where a
Discovery Server is listening.
Rows can be added with the *Add locator row* button and removed with the cross button at the end of each row.
The monitor only needs to connect to one of the specified addresses, because interconnected Discovery
Servers form a redundant network.

For example, to connect to one Discovery Server on localhost listening on port ``11811``, one in the same
local network at ``192.168.1.2:12000`` and a third one in an external network at
``8.8.8.8:12345``, add three ``UDPv4`` rows with those IP and port values.

.. code-block:: console

    "127.0.0.1:11811;192.168.1.2:12000;8.8.8.8:12345"

To learn how to launch a Discovery Server, see the
`Discovery Server CLI tutorial <https://fast-dds.docs.eprosima.com/en/latest/fastddscli/cli/cli.html#discovery>`_.

.. _add_monitor_using_dds_xml_profiles:

DDS XML Profile configured Monitor
==================================

The *DDS Monitor* can configure and initialize monitoring from DDS XML profiles.
These profiles define the configuration of DDS entities, such as DomainParticipants, Topics, and QoS settings.

To add a monitor using DDS XML profiles:

1. **Prepare the XML Profiles File**:
   Create or edit an XML file that contains the configuration for the DDS entities.
   The file must include the profiles for the DomainParticipants and other entities you want to monitor.
   See the `Fast DDS documentation <https://fast-dds.docs.eprosima.com/en/stable/fastdds/xml_configuration/xml_configuration.html>`_
   for details on how to structure the XML profiles.

2. **Load the XML Profiles File**:
    Click *File -> Initialize DDS Monitor with Profile* button in the *DDS Monitor* application menu.

3. **Upload the XML File**:
   In the dialog that appears, select the XML file you prepared in step 1.
   The application parses the file and loads the profiles it defines.

4. **Select the Profile**:
   After the XML file loads, a list of available profiles appears.
   Choose the profile you want to use for monitoring.
