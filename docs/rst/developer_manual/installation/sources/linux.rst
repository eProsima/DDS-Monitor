.. _developer_manual_installation_sources_linux:

###############################
Linux installation from sources
###############################

This page explains how to install the *eProsima DDS Monitor application* from sources, including the required
`Qt` installation.

.. _fastdds_lib_sl:

Dependencies installation
=========================

*DDS Monitor* depends on *eProsima Fast DDS* library, *eProsima Fast DDS Statistics Backend* library, Qt and
certain Debian packages.
This section explains how to install the *eProsima Fast DDS* dependencies and requirements in a Linux
environment from sources.
The following packages are installed:

- ``foonathan_memory_vendor``, an STL compatible C++ memory allocator library.
- ``fastcdr``, a C++ library that serializes according to the standard CDR serialization mechanism.
- ``fastdds``, the core library of eProsima Fast DDS.
- ``fastdds_statistics_backend``, a C++ library with a simple API for interacting with data
  from the *Fast DDS* statistics module.

First, meet the :ref:`Requirements <requirements>` and :ref:`Dependencies <dependencies>` detailed below.
Then follow either the :ref:`colcon <colcon_installation>` or the
:ref:`CMake <cmake_installation>` installation instructions.

.. _requirements:

Requirements
------------

Installing *eProsima DDS Monitor* from sources in a Linux environment requires the following tools:

* :ref:`cmake_gcc_pip_wget_git_sl`
* :ref:`colcon_install` [optional]
* :ref:`gtest_sl` [for test only]


.. _cmake_gcc_pip_wget_git_sl:

CMake, g++, pip, wget and git
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

These packages provide the tools required to install *eProsima Fast DDS* and its dependencies from the command line.
Install CMake_, `g++ <https://gcc.gnu.org/>`_, pip_, wget_ and git_ using the package manager of the appropriate
Linux distribution. For example, on Ubuntu use the command:

.. code-block:: bash

    sudo apt install cmake g++ pip wget git


.. _colcon_install:

Colcon
^^^^^^

colcon_ is a command line tool based on CMake_ for building sets of software packages.
Install the ROS 2 development tools (colcon_ and vcstool_) with the following command:

.. code-block:: bash

    pip3 install -U colcon-common-extensions vcstool

.. note::

    If this fails due to an Environment Error, add the :code:`--user` flag to the :code:`pip3` installation command.


.. _gtest_sl:

Gtest
^^^^^

Gtest is a unit testing library for C++.
By default, *eProsima DDS Monitor* does not compile tests.
You can activate them with the corresponding
`CMake options <https://colcon.readthedocs.io/en/released/reference/verb/build.html#cmake-options>`_
when calling colcon_ or CMake_.
For more details, see the :ref:`cmake_options` section.
For the Gtest installation process, see the
`Gtest Installation Guide <https://github.com/google/googletest>`_.

.. _dependencies:

Dependencies
------------

When installed from sources in a Linux environment, *eProsima Fast DDS* has the following dependencies:

* :ref:`asiotinyxml2_sl`
* :ref:`openssl_sl`
* :ref:`eprosima_dependencies`
* :ref:`qt_installation`

.. _asiotinyxml2_sl:

Asio and TinyXML2 libraries
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Asio is a cross-platform C++ library for network and low-level I/O programming with a consistent
asynchronous model.
TinyXML2 is a simple, small and efficient C++ XML parser.
Install these libraries using the package manager of the appropriate Linux distribution.
For example, on Ubuntu use the command:

.. code-block:: bash

    sudo apt install libasio-dev libtinyxml2-dev

.. _openssl_sl:

OpenSSL
^^^^^^^

OpenSSL is a toolkit for the TLS and SSL protocols and a general-purpose cryptography library.
Install OpenSSL_ using the package manager of the appropriate Linux distribution.
For example, on Ubuntu use the command:

.. code-block:: bash

   sudo apt install libssl-dev

.. _eprosima_dependencies:

eProsima dependencies
^^^^^^^^^^^^^^^^^^^^^

If the system already has *Fast DDS* `3.0.0` or later and *Fast DDS Statistics Backend* installed,
source these libraries when building the *DDS Monitor* with the command:

.. code-block:: bash

    source <fastdds-installation-path>/install/setup.bash

Otherwise, download the *Fast DDS* project from sources and build it together with *DDS Monitor* using colcon,
as explained in section :ref:`colcon_installation`.


.. _qt_installation:

Qt 6.4
^^^^^^^

Building *DDS Monitor* requires Qt 6.4.
To install this Qt version, see the `Qt Downloads <https://www.qt.io/download>`_ website.

.. note::

    During the installation steps, make sure the *Qt Charts* component is checked.


.. _colcon_installation:

Colcon installation
===================

#.  Create a :code:`DDS-Monitor` directory and download the :code:`.repos` file used to install
    *eProsima DDS Monitor* and its dependencies:

    .. code-block:: bash

        mkdir -p ~/DDS-Monitor/src
        cd ~/DDS-Monitor
        wget https://raw.githubusercontent.com/eProsima/DDS-Monitor/main/dds_monitor.repos
        vcs import src < dds_monitor.repos

    .. note::

        If *Fast DDS* is already installed in the system, you do not need to download and build
        every dependency in the :code:`.repos` file.
        Download and build only the *DDS Monitor* project, after sourcing its dependencies.
        See section :ref:`eprosima_dependencies` for how to source the *Fast DDS* and
        *Fast DDS Statistics Backend* libraries.

    To build the project, you must specify the path to the Qt 6.4 :code:`gcc_64` installation.
    With the standard Qt installation, this path is similar to :code:`/home/<user>/Qt/6.4.2/gcc_64`.

#.  Build the packages:

    .. code-block:: bash

        colcon build --cmake-args -DQT_PATH=<qt-installation-path>

.. note::

    Since colcon_ is based on CMake_, you can pass CMake configuration options to the :code:`colcon build`
    command. For the specific syntax, see the
    `CMake specific arguments <https://colcon.readthedocs.io/en/released/reference/verb/build.html#cmake-specific-arguments>`_
    page of the colcon_ manual.


.. _cmake_installation:

CMake installation
==================

.. Warning::

    Only use this installation method if the colcon_ installation method is not suitable for your needs.

This section explains how to compile *eProsima DDS Monitor* with CMake_, either
:ref:`locally <local_installation_sl>` or :ref:`globally <global_installation_sl>`.

.. _local_installation_sl:

Local installation
------------------

#.  Create a :code:`DDS-Monitor` directory where to download and build *eProsima DDS Monitor* and its dependencies:

    .. code-block:: bash

        mkdir ~/DDS-Monitor

#.  Clone the following dependencies and compile them using CMake_.

    * `Foonathan memory <https://github.com/foonathan/memory>`_

      .. code-block:: bash

          cd ~/DDS-Monitor
          git clone https://github.com/eProsima/foonathan_memory_vendor.git
          mkdir foonathan_memory_vendor/build
          cd foonathan_memory_vendor/build
          cmake .. -DCMAKE_INSTALL_PREFIX=~/DDS-Monitor/install -DBUILD_SHARED_LIBS=ON
          cmake --build . --target install

    * `Fast CDR <https://github.com/eProsima/Fast-CDR.git>`_

      .. code-block:: bash

          cd ~/DDS-Monitor
          git clone https://github.com/eProsima/Fast-CDR.git
          mkdir Fast-CDR/build
          cd Fast-CDR/build
          cmake .. -DCMAKE_INSTALL_PREFIX=~/DDS-Monitor/install
          cmake --build . --target install

    * `Fast DDS <https://github.com/eProsima/Fast-DDS.git>`_

        .. code-block:: bash

            cd ~/DDS-Monitor
            git clone https://github.com/eProsima/Fast-DDS.git
            mkdir Fast-DDS/build
            cd Fast-DDS/build
            cmake .. -DCMAKE_INSTALL_PREFIX=~/DDS-Monitor/install -DCMAKE_PREFIX_PATH=~/DDS-Monitor/install
            cmake --build . --target install

    * `Fast DDS Statistics Backend <https://github.com/eProsima/Fast-DDS-statistics-backend.git>`_

      .. code-block:: bash

          cd ~/DDS-Monitor
          git clone https://github.com/eProsima/Fast-DDS-statistics-backend.git
          mkdir Fast-DDS-statistics-backend/build
          cd Fast-DDS-statistics-backend/build
          cmake .. -DCMAKE_INSTALL_PREFIX=~/DDS-Monitor/install -DCMAKE_PREFIX_PATH=~/DDS-Monitor/install
          cmake --build . --target install

#.  Once all dependencies are installed, install *eProsima DDS Monitor*:

    .. code-block:: bash

        cd ~/DDS-Monitor
        git clone https://github.com/eProsima/DDS-Monitor.git
        mkdir DDS-Monitor/build
        cd DDS-Monitor/build
        cmake .. \
            -DCMAKE_INSTALL_PREFIX=~/DDS-Monitor/install \
            -DCMAKE_PREFIX_PATH=~/DDS-Monitor/install \
            -DQT_PATH=<qt-installation-path>
        cmake --build . --target install


.. note::

    By default, *eProsima DDS Monitor* does not compile tests.
    You can activate them by downloading and installing `Gtest <https://github.com/google/googletest>`_
    and building with CMake option ``-DBUILD_TESTS=ON``.


.. _global_installation_sl:

Global installation
-------------------

To install *eProsima DDS Monitor* and its dependencies system-wide instead of locally, remove all the flags that
appear in the configuration steps of :code:`Fast-CDR`, :code:`Fast-DDS`, :code:`Fast-DDS-Statistics-Backend`, and
:code:`DDS-Monitor`, and change the flags in the configuration step of :code:`foonathan_memory_vendor` to the
following:

.. code-block:: bash

    -DCMAKE_INSTALL_PREFIX=/usr/local/ -DBUILD_SHARED_LIBS=ON

.. _run_app_colcon_sl:

Run an application
==================

To run the *eProsima DDS Monitor* application, source the *Fast DDS* and *Fast DDS Statistics Backend* libraries
and run the executable installed in :code:`<install-path>/dds_monitor/bin/dds_monitor`
(colcon) or :code:`<install-path>/bin/dds_monitor` (CMake):

.. code-block:: bash

    # If built has been done using colcon, all projects could be sourced as follows
    source install/setup.bash
    ./install/dds_monitor/bin/dds_monitor

Make sure this file has execute permissions.

.. include:: ../../../installation/includes/running_as_root.rst

.. External links

.. _colcon: https://colcon.readthedocs.io/en/released/
.. _CMake: https://cmake.org
.. _pip: https://pypi.org/project/pip/
.. _wget: https://www.gnu.org/software/wget/
.. _git: https://git-scm.com/
.. _OpenSSL: https://www.openssl.org/
.. _Gtest: https://github.com/google/googletest
.. _vcstool: https://pypi.org/project/vcstool/
