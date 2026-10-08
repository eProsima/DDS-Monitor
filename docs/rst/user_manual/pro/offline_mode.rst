.. include:: ../../exports/alias.include
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

Use **File → Open Recording...** (or the **Open a recording instead...** link in the *Initialize
Monitor* dialog) to select a recording file. Two formats are supported:

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

* **Apply range** commits the selected range.
* **Use full recording** loads the entire recording.
* **Cancel** (or pressing *Escape* / closing the dialog) cancels opening the recording.

.. _offline_mode_transport_bar:

The Playback Bar
================

The playback bar is only visible in offline mode. It has the following controls.

**Recording information (left)**
    A *RECORDING* label, the recording file name (hover to see the full path), and the recording's
    absolute start time and total duration.

**Timeline (center)**
    A scrubber showing the current position (``MM:SS``) and the recording length. Drag the scrubber to
    move the playback cursor; hovering shows the absolute time at that point. Below the scrubber:

    * **Jump to start** - moves the cursor to the beginning.
    * **Back 5 seconds** (*-5s*) and **Forward 5 seconds** (*+5s*).
    * A round **play / pause** button.
    * A **loop** toggle - repeats playback continuously; the tooltip reads *Looping on* when active.

**Speed (right)**
    A *SPEED* control showing the current playback rate. Click it to choose from ``0.1x``, ``0.25x``,
    ``0.5x``, ``1x``, ``2x``, ``4x``, and ``8x``.

    A |help| button opens a contextual help panel with a link to this documentation page.

You can also move the playback cursor directly on a recording chart: left-drag on the plot to move the
cursor, and right-click to read the nearest point's value. On :ref:`Topic Charts <topic_charts>`, the
chart legend shows each series' value at the cursor position next to its entry, and these values
follow the playback point as you scrub.

.. _offline_mode_panes:

What Works Offline
==================

Time Series and XY Charts show the active recording range.
Event Charts plot up to 500 change events per lane; larger lanes ask for an event-range selection.
Spy and image panes show the last sample at or before the
playback cursor (and appear empty before the first sample arrives). The following panes and panels are
available offline: :ref:`Topic Charts <topic_charts>`, :ref:`Spy Topic Views <dockable_spy_pane>`,
:ref:`Topic Type Views (IDL) <dockable_idl_pane>`, :ref:`Image Panes <image_pane>`, :ref:`Register Type View <register_type>`, :ref:`Custom Series <custom_series_panel>` and :ref:`Workspace <workspace>` save and load.

The following are **not** available while inspecting a recording. Their controls are either hidden or
disabled with the tooltip *Unavailable in offline mode (inspecting a recording)* (*Unavailable in
offline mode* in the view selector of an empty tab):

* :ref:`Statistics Charts <pro_chart_view>`.
* :ref:`Publisher Panes <publisher_pane>`.
* The :ref:`Enable / disable statistics <statistics_readers_panel>` and :ref:`Alerts
  <pro_alerts_panel>` sidebar panels (their icons are hidden).
* Live monitoring actions in the application menu.
