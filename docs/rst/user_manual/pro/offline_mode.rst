.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _offline_mode:

##################
Offline Mode |Pro|
##################

*Offline Mode* lets you open a captured DDS recording and inspect it in the monitor as you would a
live session, with playback control over the recorded timeline.
The monitor reads samples from a recording file instead of a running DDS network, and you can scrub,
play, pause, loop, and change speed through the captured data.

.. thumbnail:: /rst/figures/screenshots/offline_pro.png
    :align: center

.. _offline_mode_opening:

Opening a Recording
===================

Use **File → Open Recording...**, |film| **Open Recording** on the start screen (or the **Open a recording
instead...** link in the *Initialize Monitor* dialog) to select a recording file. Two formats are supported:

* **MCAP** (``.mcap``).
* **SQLite** (``.db``).

While a recording is open, the window title shows ``DDS Monitor Pro | Offline: <filename>`` and a
playback bar appears at the bottom of the window.

Opening a recording never interrupts a live session. If the current window has never started a
monitor, the recording opens in that same window. If a monitor has already been started in it (whether
still active or since stopped), the recording opens in a new, independent monitor
application, and the original live monitor keeps running. The two applications are separate
processes, so you can inspect the recording and keep monitoring at the same time, and closing one does
not close the other.

.. _offline_mode_trim:

Selecting a Range
=================

When a recording opens, a *Select recording range* dialog appears once so you can restrict playback to
a portion of the recording. It has a range slider (in seconds from the recording start),
decimal-second spin boxes, and absolute wall-clock fields (``YYYY-MM-DD HH:MM:SS``, the date being
optional).

.. figure:: /rst/figures/screenshots/offline_range_pro.png
    :align: center

* **Apply range** commits the selected range.
* **Use full recording** loads the entire recording.
* **Cancel** (or pressing *Escape* / closing the dialog) cancels opening the recording.

.. _offline_mode_transport_bar:

The Playback Bar
================

The playback bar is only visible in offline mode. It has the following controls.

**Recording information (left)**
    A *RECORDING* label, the recording file name (hover over it to see the full name when it is cut), and
    the start time and duration of the range loaded.

**Timeline (center)**
    A scrubber showing the current position (``MM:SS``) and the length of the range. Drag the scrubber to
    move the playback cursor; hovering shows the absolute time at that point. Below the scrubber:

    * **Jump to start** - moves the cursor to the beginning.
    * **Back 5 seconds** (*-5s*) and **Forward 5 seconds** (*+5s*).
    * A round **play / pause** button.
    * A **loop** toggle - repeats playback continuously; the tooltip reads *Looping on* when active.

**Speed (right)**
    A *SPEED* control showing the current playback rate. Click it to choose from ``0.1x``, ``0.25x``,
    ``0.5x``, ``1x``, ``2x``, ``4x``, and ``8x``.

    A |question| button opens a contextual help panel with a link to this documentation page.

You can also move the playback cursor directly on a recording chart: left-drag on the plot to move the
cursor, and right-click to read the nearest point's value. On :ref:`Topic Charts <topic_charts>`, the
chart legend shows each series' value at the cursor position next to its entry, and these values
follow the playback point as you scrub.

.. _offline_mode_panes:

What Works Offline
==================

Time Series and XY Charts show the active recording range.
Event Charts plot up to 500 change events per lane; larger lanes ask for an event-range selection.
:ref:`Data Tables <pro_data_table>` list every sample of the range loaded, whatever the playback position.
**Seek playback here**, in the details of a sample, moves playback to that sample. See
:ref:`pro_data_table_offline`.
Spy and image panes show the last sample at or before the
playback cursor (and appear empty before the first sample arrives). The following panes and panels are
available offline: :ref:`Topic Charts <topic_charts>`, :ref:`Topic Spies <dockable_spy_pane>`,
:ref:`Topic Type Views (IDL) <dockable_idl_pane>`, :ref:`Image Displays <image_pane>`, :ref:`Data Tables <pro_data_table>`, :ref:`Type Registration <register_type>`, :ref:`Custom Series <custom_series_panel>` and :ref:`Workspace <workspace>` save and load.

The following are **not** available while inspecting a recording. Their controls are either hidden or
disabled with the tooltip *Unavailable in offline mode (inspecting a recording)* (*Unavailable when
inspecting a recording* in the view selector of an empty tab):

* :ref:`Statistics Charts <pro_chart_view>`.
* :ref:`Topic Publishers <publisher_pane>`.
* The :ref:`Enable / disable statistics <statistics_readers_panel>`,
  :ref:`Recording Configurations <pro_recording_configurations>` and :ref:`Alerts
  <pro_alerts_panel>` sidebar panels (their icons are hidden).
* Recording (**File → Start Recording...**).
* Live monitoring actions in the application menu.

.. _offline_mode_workspaces:

Workspaces in Offline Mode
==========================

You can save a :ref:`workspace <workspace>` while a recording is open, in the same ways as in a live session
(**File → Save Workspace as...**, the |save| button or **Ctrl+S**).
The workspace keeps the tabs, panes and settings, and also the recording:

* The recording file, by its full path and by its path relative to the workspace file.
* The range loaded.
* The playback position, the speed and the loop setting.

It has no monitors, alerts or statistics readers, because a recording's window has none.
Wait until the recording has loaded: until then, saving is refused with *The recording is still loading. Save
the workspace once it has loaded.*

Loading such a workspace (**File → Load Workspace...**, **File → Load Recent Workspace**, or **Load
Workspace** on the start screen) opens its recording again with the saved range, without the range dialog.
Then it rebuilds the tabs and panes and restores the playback position, speed and loop, with playback paused.

The monitor looks for the recording at its saved path, then at its path relative to the workspace file, then
by its file name in the folder of the workspace file.
Keep the recording next to the workspace file to move or share both together.
If the recording is not found, or no longer covers the saved range, an error says so and nothing changes.

Where the recording opens depends on the window you load the workspace from:

* A window that shows the same recording and range applies the workspace in place. If the recording is
  still loading, the load is refused: load the workspace again once it has loaded.
* A window that shows another recording, or the same recording with another range, opens a new window for
  the workspace.
* A live window that has never started a monitor, such as the start screen, opens the recording in that
  window.
* A live window that has started a monitor opens a new window for the recording, and keeps monitoring.

A workspace saved from a live system cannot be loaded while a recording is open. Load it from a window that
is not showing a recording.
The recent workspaces (see :ref:`pro_recent_workspaces`) mark the workspaces saved from a recording with
``[Offline]``.

.. _offline_mode_command_line:

Opening a Recording from the Command Line
=========================================

You can start the monitor directly on a recording with these options:

``--offline <file>``
    Opens the ``.mcap`` or ``.db`` file in offline mode.

``--offline-range <start>:<end>``
    With ``--offline``: the range to load, as its start and end in nanoseconds since the Unix epoch.
    The range dialog is not shown. A range that cannot be read is ignored, and the dialog asks instead.

``--workspace <file>``
    With ``--offline``: a workspace saved from that recording, applied once the recording has loaded.

For example:

.. code-block:: bash

    dds_monitor --offline ~/recordings/2026-11-18_10-30-00_CET_recording_domain0.mcap

The monitor uses these options itself to open a recording in a new window.

.. _offline_mode_making_recordings:

Making Recordings
=================

To record a live DDS system to MCAP or SQLite files with the monitor, see :ref:`pro_recording`.
