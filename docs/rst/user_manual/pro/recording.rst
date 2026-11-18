.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _pro_recording:

###############
Recording |Pro|
###############

*DDS Monitor Pro* can record the DDS data it monitors to files.
It writes the same MCAP and SQLite files as
`eProsima DDS Record & Replay <https://dds-recorder.readthedocs.io/en/latest/>`__, and you do not
need to deploy a recorder, because the monitor is already subscribed to the system.
Use a recording to keep a problem that comes and goes, to compare one test run with the next, or to
share data with a colleague or with eProsima support.
Open it later in the monitor with **File → Open Recording...** (see :ref:`offline_mode`), or publish
it again with eProsima DDS Replayer.

There are two ways to record:

* **File → Start Recording...** records what is on screen, after a few choices in a dialog.
  See :ref:`pro_start_recording`.
* The **Recording Configurations** panel keeps saved setups with every recording option, and starts
  any of them with one click. The configurations are saved with the :ref:`workspace <workspace>`.
  See :ref:`pro_recording_configurations`.

One recording runs at a time, and only live monitors can be recorded: while the window shows a
recording, recording is not available.

.. _pro_start_recording:

Starting a Recording
====================

**File → Start Recording...** records the samples of the topics shown in Topic Spy, Topic Chart
(Time Series, Event Chart and XY Chart), Data Table and Image Display panes, in every monitored domain,
while the recording runs.
The topics follow the panes: a pane you open during the recording adds its topic from then on, and
closing the last pane of a topic stops recording its samples.
:ref:`Topic Publisher <publisher_pane>` panes do not count.
The files also describe every other topic the monitors discovered, with its type and no samples.
With no pane open, the recording describes the topics but holds no samples, so open the panes of
the topics you want before you start.

To start a recording:

#. Start monitoring one or more domains (see :ref:`pro_initialize_monitoring`).
#. Open a pane for each topic to record, for example a :ref:`Topic Spy <dockable_spy_pane>` or a
   :ref:`Topic Chart <topic_charts>`.
#. Select **File → Start Recording...**.
#. Choose the folder, the file name and the format, then click |record| **Start**.

**Start Recording...** is disabled while a recording is in progress, when no monitor is running, and
in :ref:`offline mode <offline_mode>`. Its tooltip says which applies.

.. figure:: /rst/figures/screenshots/start_recording_dialog_pro.png
    :align: center

The **Start Recording** dialog has these fields:

**Folder**
    The folder where the files are written. It must be a full path to an existing folder that you can
    write to; the monitor does not create it. Type it, or choose it with **Browse...**.
    It starts as your home folder and keeps the last folder you used until the monitor closes.

**File name**
    The name of the files, without extension and without a folder. The default name starts with the
    date, time and time zone, such as ``2026-11-18_10-30-00_CET_recording``.
    See :ref:`pro_recording_files` for the names of the files written.

**Format**
    **MCAP** (the default), **SQLite**, or **MCAP and SQLite**, which writes one file of each format
    with the same data.

**MCAP compression**
    Shown when MCAP is selected. The algorithm (**None**, **LZ4** or **Zstd**, the default) and the
    level (**Fastest**, **Fast**, **Default**, **Slow** or **Slowest**).
    **Zstd** writes the smallest files, **LZ4** compresses fastest and uses the least CPU, which suits
    high data rates, and **None** uses no CPU and writes the largest files.
    A slower level makes smaller files for more CPU time. The level is disabled with **None**.

**SQLite data format**
    Shown when SQLite is selected. How each sample is stored in the database:

    * **CDR and JSON** (the default): both representations, so the file can be replayed and read.
    * **CDR**: the serialized sample, as it was sent. eProsima DDS Replayer can replay it.
    * **JSON**: readable by any tool without the type definition. eProsima DDS Replayer cannot replay
      a database with JSON data only.

**Advanced options**
    Click it to show **ROS 2 types (store ROS 2 topic and type names demangled)**.
    With it, the files store the types as ROS 2 message definitions instead of OMG IDL, and the ROS 2
    topic and type names demangled (``rt/chatter`` is stored as ``/chatter``), for ROS 2 tools.
    See :ref:`pro_recording_compatibility` before you use it with SQLite.

The |question| button in the dialog header opens a short help on recording.
Under the fields, **Create Configuration** closes the dialog and opens a new recording configuration
in the :ref:`Recording Configurations panel <pro_recording_configurations>`, for more options and to
keep them for later recordings.

**Start** stays disabled while the folder or the file name is not valid, and a message under the
fields says why:

* The folder is empty, is not a full path, does not exist, is not a folder, or cannot be written to.
  The check repeats every second while the message is shown, so creating the folder clears it.
* The file name contains ``/`` or ``\`` (on Windows also ``:``, ``*``, ``?``, ``"``, ``<``, ``>``
  or ``|``). The field takes at most 100 characters.

If the recording cannot start, for example because the disk has less free space than the safety
margin, the dialog stays open with the reason under the fields.

.. _pro_recording_in_progress:

While Recording
===============

While a recording runs, a **REC** indicator at the right end of the menu bar shows its elapsed time
and the number of samples recorded so far, for example ``REC 01:24 · 3120 samples``.
Hover over it to see the recording configuration used (if any), the files being written and the
number of samples lost, if any. Click it to stop the recording.
The |record| icon of the **Recording Configurations** panel in the left icon bar also shows a red
dot.

.. thumbnail:: /rst/figures/screenshots/recording_window_pro.png
    :align: center

A monitor started during a recording joins it, for what the recording covers: it gets its own files,
or joins the single file of a configuration that records all domains in one file.
Stopping a monitor ends its part of the recording, and the recording ends when its last monitor
stops.

While the recording runs, each file is named ``<name>.tmp~``, and it takes its final name when the
recording stops. SQLite files receive the samples as they arrive. MCAP files receive them one
compressed chunk at a time, so at a low data rate an MCAP file can stay almost empty for a while.
Use the files once the recording has stopped: only then are they complete.

.. _pro_stop_recording:

Stopping a Recording
====================

To stop the recording, do one of the following:

* Select **File → Stop Recording**.
* Click the **REC** indicator in the menu bar.
* Click the |stop| button of the configuration being recorded in the
  :ref:`Recording Configurations panel <pro_recording_configurations>`.

While the files are closed, the indicator reads **Saving recording...** and **Stop Recording** is
disabled.

A recording also stops by itself when a file reaches the maximum size of its configuration, when the
free disk space falls below the safety margin, or when its last monitor stops.
A full file ends the whole recording, with all its files. Files are not rotated or overwritten.

.. _pro_recording_summary:

When the recording ends, the **Recording finished** dialog summarizes it:

* The number of samples and topics recorded, and the duration, for example
  *1520 samples of 4 topics recorded in 63 s.*
* The samples that could not be recorded, if any (samples that arrived faster than the disk could
  take them, or that failed to be written).
* The files written. Click |copy| next to a file to copy its path.
* Why the recording stopped by itself, when it did, or the error that ended it.

.. figure:: /rst/figures/screenshots/recording_summary_pro.png
    :align: center

Quitting the monitor or loading a workspace stops the recording, so the monitor asks first:

* Quitting (**File → Quit** or closing the window) asks *A recording is running. Quitting will stop
  it.* Click **Stop Recording and Quit** to stop the recording and quit, or **Cancel** to keep
  recording.
* Loading a workspace in the same window asks *A recording is running. Loading the workspace will
  stop it.* Click **Stop Recording and Load** or **Cancel**.
  A workspace saved from a recording opens in a new window, so it does not stop the recording (see
  :ref:`offline_mode_workspaces`).

.. _pro_recording_configurations:

Recording Configurations
========================

A recording configuration keeps every recording option under a name, so a recording made more than
once (each test run, every night) is started with one click.
Configurations also offer what the dialog does not: chosen topics or whole domains, a single file
for all domains, file size limits, the timestamp format and the safety margin.

Open the panel with the |record| icon (tooltip *Recording Configurations*) in the left icon bar.
The icon is hidden in :ref:`offline mode <offline_mode>`.
The panel has a header (**RECORDINGS**, with |question| and |plus| **Add Recording Configuration**),
the **RECORDING CONFIGURATIONS** list, and the **Info** and **Configuration** tabs of the selected
configuration. Drag the divider between the list and the tabs to resize them.

.. figure:: /rst/figures/screenshots/recording_configurations_pro.png
    :align: center

The |question| button next to the **Configuration** tab opens a help on the configuration options.

Managing Configurations
-----------------------

* To create a configuration, click |plus| in the panel header, **New configuration** in an empty
  list, or **Create Configuration** in the **Start Recording** dialog.
  The new configuration is named *Recording* (*Recording 2*, *Recording 3*... if the name is
  taken), writes to your home folder and takes the defaults of eProsima DDS Recorder.
  Fill in the **Configuration** tab and click **Add Configuration**.
* Click a configuration in the list to see its settings in the **Info** tab and edit them in the
  **Configuration** tab. Click it again to deselect it.
* To change a configuration, edit it in the **Configuration** tab and click **Save Changes**.
  The tab confirms with *Configuration saved successfully.*, or says in red why the configuration
  cannot be saved.
* To copy a configuration, right-click it and select **Duplicate**. The copy is named
  *<name> (copy)*.
* To delete a configuration, right-click it, select **Delete**, and confirm with **Delete** in the
  **Delete Recording Configuration** dialog. This cannot be undone.

While a configuration is being recorded, it cannot be deleted, and saving changes to it shows *Stop
the recording before changing its configuration.*

The configurations are saved with the :ref:`workspace <workspace>`, and loading a workspace replaces
them with its own.

.. _pro_recording_configuration_options:

Configuration Options
---------------------

The **Configuration** tab groups the options in sections. Sizes are in MB of 1,000,000 bytes.

**NAME**
    **Name** - the name in the list. It must be unique.

**OUTPUT**
    * **Folder** - where the files are written: a full path to an existing folder you can write to.
      Type it or choose it with **Browse...**.
    * **File name** - the name of the files, without extension (at most 100 characters).
    * **Timestamp format** - the ``strftime`` format of the timestamp that precedes the file name,
      computed when the recording starts. The default, ``%Y-%m-%d_%H-%M-%S_%Z``, makes names that
      sort by time.
    * **Use local time** - the timestamp in the machine's local time instead of UTC.
    * **Files** - an example of the names of the files a recording started now would write, or why
      the timestamp format is not valid.
    * **Safety margin (MB)** - the free disk space kept in the folder. The recording does not start
      with less, and stops when the free space falls below it. Minimum 10 MB, the default.
    * **Format** - **MCAP**, **SQLite**, or **MCAP and SQLite**.

**MCAP** (shown when MCAP is selected)
    * **Compression** - the algorithm and level, as in the :ref:`dialog <pro_start_recording>`.
    * **Force compression** - compresses every chunk, even when compression does not make it smaller.
      Otherwise such a chunk is written uncompressed.
    * **Log publish time** - each message's MCAP log time is the source timestamp set by the writer
      instead of the reception time, for tools that order the data by publication time.
    * **Max file size (MB)** with **Unlimited** (the default) - the size at which the recording stops.
      At least 0.003 MB.
    * **Size tolerance (MB)** - shown with a size limit: how much is written between checks of the
      real file size against its estimate. At least 1 MB.

**SQLITE** (shown when SQLite is selected)
    * **Data format** - **CDR and JSON**, **CDR** or **JSON**, as in the
      :ref:`dialog <pro_start_recording>`.
    * **Max file size (MB)** with **Unlimited** - at least 0.034 MB.
    * **Size tolerance (MB)** - at least 1 MB.

**TOPICS**
    What to record. See :ref:`pro_recording_topics`.

**ROS 2**
    **ROS 2 types (demangled topic and type names)** - as **ROS 2 types** in the
    :ref:`dialog <pro_start_recording>`.

.. _pro_recording_topics:

Choosing the Topics
-------------------

The **TOPICS** section offers three ways to choose what to record, and they combine:

**Record what is visualized** (on by default)
    Records the topics shown in Topic Spy, Topic Chart, Data Table or Image Display panes while
    recording, in every monitored domain, as **File → Start Recording...** does.

**Whole domains and topics to record**
    Lists each running monitor by its name: *Domain 0* for a domain monitor, *Discovery Server
    <locators>* for a Discovery Server monitor, and the profile name for a monitor started from an
    XML profile. Next to the name, a summary says what is selected (*whole domain*, *2 topics*,
    *no topics*), with *not monitored* added for a monitor of the configuration that is not running
    now. With no monitor running and none in the configuration, it reads *No domain is monitored.*

    * Turn on **Whole domain** to record every topic of that monitor, those discovered later
      included. DDS, ROS 2 and monitor internal topics (such as the Fast DDS statistics topics,
      ``rosout`` or ``parameter_events``) are not recorded.
    * Click the monitor's name to show its topics, filter them with **Filter topics...**, and check
      the topics to record. A chosen topic that is not discovered now is listed as
      *<topic> (not discovered)*, and is recorded once it is discovered.

**All domains in a single file**
    Records every domain in the same file, with one timeline. Topics with the same name in several
    domains are recorded as one topic.

A configuration that records nothing is refused with *Nothing to record: record what is visualized,
a whole domain or some topics.*
The files of a configuration describe only the topics it records.

.. _pro_recording_with_configuration:

Recording with a Configuration
------------------------------

Click the red circle at the right of a configuration in the list to start recording with it.
While it records, the configuration's name turns red with a **REC** label, and the button becomes
|stop|, which stops the recording.
The button is disabled while another recording is in progress, and when no monitor is running.

A recording starts only when a monitor of something it records is running. If it cannot start, the
**Info** tab of the configuration says why.

The **Info** tab shows the settings of the selected configuration. While the configuration is being
recorded, it also shows **RECORDING** with the samples, topics and time so far and the files being
written. After it stops, **LAST RECORDING** keeps the same figures, the samples lost, and the reason
the recording stopped by itself, if it did, until the monitor closes or a workspace is loaded.

.. _pro_recording_files:

Output Files
============

The files are named as follows (``.mcap`` for MCAP, ``.db`` for SQLite):

.. list-table::
    :header-rows: 1

    *   - Recording
        - File names
    *   - **File → Start Recording...**
        - ``<file name>_domain<N>.mcap``, one per monitored domain.
    *   - Configuration
        - ``<timestamp>_<file name>_domain<N>.mcap``, one per domain it records.
    *   - Configuration with **All domains in a single file**
        - ``<timestamp>_<file name>.mcap``.

* ``<N>`` is the DDS domain number.
* If a file with that name already exists, ``_2``, ``_3``... is added to the name, so nothing is
  overwritten.
* **File → Start Recording...** writes a file for every monitored domain, even one with no topic on
  screen, which then describes its topics without samples. A configuration writes no file for a
  domain it records nothing of.
* Each file can be opened or replayed on its own.

**MCAP files** are compact, chunked and compressed, as eProsima DDS Recorder writes them by default.
Other MCAP tools can read them.

**SQLite files** can be queried with any SQLite client.
The ``Messages`` table has a row per sample, with the ``topic``, ``type``, ``key``, ``writer_guid``
and ``sequence_number``, the reception and publication times (``log_time`` and ``publish_time``),
and the sample as ``data_json`` and ``data_cdr``, depending on the data format.
The ``Topics`` and ``Types`` tables describe the topics and their types.
``sequence_number`` numbers the samples within the recording from 0, as DDS Recorder does: it is not
the writer's sequence number, so a gap in it is no sign of a lost sample.
The ``Types`` table also holds the types the recorded types depend on, in rows named
``__dep__/<identifier>``.
A SQLite file takes much more room than an MCAP file of the same data: it is not compressed, and
**CDR and JSON** stores each sample twice.

.. _pro_recording_compatibility:

Compatibility with eProsima DDS Record & Replay
===============================================

The monitor writes its recordings in the formats of
`eProsima DDS Record & Replay <https://dds-recorder.readthedocs.io/en/latest/>`__, and the options
of the dialog and of the configurations have the same meaning as in the DDS Recorder configuration.

* eProsima DDS Replayer replays the MCAP files, with any compression.
* It replays the SQLite files that hold CDR data (**CDR** or **CDR and JSON**). A file with
  **JSON** data only cannot be replayed.
* It cannot replay the ROS 2 topics of a SQLite file recorded with **ROS 2 types**. To read a
  recording with ROS 2 tools and also replay it, record MCAP with **ROS 2 types**.
* The monitor opens recordings made by eProsima DDS Recorder as well as its own.

.. _pro_recording_open:

Opening a Recording
===================

To look at a recording in the monitor, select **File → Open Recording...** and choose its ``.mcap``
or ``.db`` file, whose path you can copy from the **Recording finished** dialog.
It opens in a new window, so the live monitors keep running.
See :ref:`offline_mode` for the range dialog, playback and what works on a recording.
