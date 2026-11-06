.. _fast_dds_suite:

Fast DDS Suite
==============

This Docker image contains the complete Fast DDS suite:

- :ref:`eProsima Fast DDS libraries and examples <fast_dds_suite_examples>`: *eProsima Fast DDS* is a C++
  implementation of the `DDS (Data Distribution Service) Specification <https://www.omg.org/spec/DDS/About-DDS/>`__,
  a protocol defined by the `Object Management Group (OMG) <https://www.omg.org/>`__.
  The *eProsima Fast DDS* library provides an Application Programming Interface (API) and a communication protocol
  that deploy a Data-Centric Publisher-Subscriber (DCPS) model for efficient and reliable
  information distribution among Real-Time Systems. *eProsima Fast DDS* is predictable, scalable, flexible, and
  efficient in resource handling.

  This Docker Image contains the Fast DDS libraries bundled with several examples that demonstrate
  capabilities of eProsima's Fast DDS implementation.

  You can read more about Fast DDS on the `Fast DDS documentation page <https://fast-dds.docs.eprosima.com/en/latest/>`_.

- :ref:`Shapes Demo <fast_dds_suite_shapes_demo>`: eProsima Shapes Demo is an application in which Publishers and
  Subscribers are shapes of different colors and sizes moving on a board. Each shape has its own topic: Square,
  Triangle or Circle. A single instance of the eProsima Shapes Demo can publish on or subscribe to several topics at
  a time.

  You can read more about this application on the `Shapes Demo documentation page <https://eprosima-shapes-demo.readthedocs.io/>`_.

- :ref:`DDS Monitor <fast_dds_suite_monitor>`: eProsima DDS Monitor is a graphical desktop application
  for monitoring DDS environments deployed using the *eProsima Fast DDS* library. It shows in real
  time the status of publication/subscription communications between DDS entities. You can choose which
  communication parameters to measure (latency, throughput, packet loss, etc.), and record and
  compute in real time statistical measurements on these parameters (mean, variance, standard deviation, etc.).

To load this image into your Docker repository, run from a terminal:

.. code-block:: bash

 $ docker load -i ubuntu-fastdds-suite\ <FastDDS-Version>.tar

Run the Docker container:

.. code-block:: bash

 $ xhost local:root
 $ docker run -it --privileged -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix \
 ubuntu-fastdds-suite:<FastDDS-Version>

From the resulting Bash Shell you can run each feature.

.. _fast_dds_suite_examples:

Fast DDS Examples
-----------------

This Docker container includes a set of binary examples that demonstrate several functionalities of the
Fast DDS libraries. To go to the examples folder from a terminal, type:

.. code-block:: bash

 $ goToExamples

This folder contains all examples, both for DDS and RTPS. The steps to launch one of them follow.

Hello World Example
^^^^^^^^^^^^^^^^^^^

This minimal example performs a Publisher/Subscriber match and starts sending samples.

.. code-block:: bash

 $ goToExamples
 $ cd hello_world/bin
 $ tmux new-session "./hello_world publisher 0 1000" \; \
 split-window "./hello_world subscriber" \; \
 select-layout even-vertical

This example is not limited to the current instance. You can run several instances of this
container and check the communication between them by running the following from each container.

.. code-block:: bash

 $ goToExamples
 $ cd hello_world/bin
 $ ./hello_world publisher

or

.. code-block:: bash

 $ goToExamples
 $ cd hello_world/bin
 $ ./hello_world subscriber

.. _fast_dds_suite_shapes_demo:

Shapes Demo
-----------

To launch the Shapes Demo, run from a terminal:

.. code-block:: bash

 $ ShapesDemo

For eProsima Shapes Demo usage information, see the `Shapes Demo First Steps
<https://eprosima-shapes-demo.readthedocs.io/en/latest/first_steps/first_steps.html>`_.

.. _fast_dds_suite_monitor:

DDS Monitor
----------------

To launch the DDS Monitor, run from a terminal:

.. code-block:: bash

 $ dds_monitor

For eProsima DDS Monitor usage information, see the `DDS Monitor Basic
<https://dds-monitor.docs.eprosima.com/en/latest/rst/user_manual/initialize_monitoring.html>`_.

.. include:: ../../installation/includes/running_as_root.rst
