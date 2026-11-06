.. include:: ../exports/alias.include

.. _installation_manual_linux:

#########################
DDS Monitor on Linux
#########################

The *DDS Monitor* application is available on the `eProsima <https://www.eprosima.com/>`_ website in the
`Downloads <https://www.eprosima.com/index.php/downloads-all>`_ section.

There are two ways to run the monitor application on Linux:

- Through the *DDS Monitor* installer.
- Using the *AppImage* format, a portable format of the application.

*DDS Monitor* installer
============================

The installer installs the *DDS monitor* application together with all its dependencies.
Run the ``eProsima_DDS-Monitor-<DDS-Monitor-Version>-Linux.run`` executable
(you might need to make the file executable first by running
``chmod +x eProsima_DDS-Monitor-<DDS-Monitor-Version>-Linux.run``)
and follow its instructions to install the program in a directory on the system.

.. figure:: /rst/figures/installer_linux.png
    :align: center

*DDS Monitor* portable format
==================================

*eProsima* also distributes a portable version of the *DDS Monitor* for Linux in AppImage format.
Download it from the
`eProsima Downloads website <https://www.eprosima.com/index.php/downloads-all>`_ and run the downloaded
file to launch the monitor.
The file is named ``eProsima_DDS-Monitor-<DDS-Monitor-Version>-Linux.AppImage``.


.. warning::

    If these files do not run, check that they have executable permissions.

.. include:: includes/running_as_root.rst
