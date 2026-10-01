.. include:: ../exports/alias.include
.. include:: ../exports/roles.include

.. _selected_entity:

###############
Selected Entity
###############

The application stores one entity as the **last entity clicked** and uses it to decide what information to display.
In the DDS Monitor, an entity is any element the monitor can track (see :ref:`entities`).
Click any entity in any of the :ref:`left_sidebar_layout` panels to make it the *Selected Entity* for the whole
application.
Selecting an entity has these effects on the application view:

- The clicked entity keeps a blue background until another entity is clicked or the Selected
  Entity is restored.
- The :ref:`info_subpanel_layout` shows information about this entity, such as *QoS* or specific
  entity settings.
- The :ref:`statistics_panel_layout` lists a general summary of the data stored for this entity.
- If the selected entity is a DDS Monitor entity belonging to the Physical or Logical Entities group,
  the entities displayed in :ref:`dds_panel` are only those *related* to this entity.
  Therefore, clicking one of the :ref:`dds_entities` does not update the :ref:`dds_panel`.
  The relations between entities are described in the :ref:`entities` section.


Deselect Entity
---------------
To change the current *Selected Entity*, click another entity in the :ref:`left_sidebar_layout`.
To deselect it, use the *Refresh* button (:ref:`refresh_button`).
With no entity selected, the application view changes as follows:

- The :ref:`dds_panel` lists all DDS entities in every Domain monitored by DDS Monitor,
  so you can see any DomainParticipant, DataWriter and DataReader regardless of the physical entity
  or the DDS logical entity they belong to.
- The information shown in the :ref:`info_panel_layout` becomes a brief summary of the current state of the application.
