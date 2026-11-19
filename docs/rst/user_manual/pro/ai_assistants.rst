.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _pro_ai_assistants:

###################
AI Assistants |Pro|
###################

*DDS Monitor Pro* has an MCP server. MCP (Model Context Protocol) is the protocol AI assistants use to call
outside tools. While the server is on, an assistant such as Claude Code, Codex or another MCP client running on
the same computer can read what the monitor sees and work in the monitor's window: open and arrange views,
record, open recordings and, if you allow it, publish.
You ask in your own words, for example why a DataReader receives no data, and the assistant answers from the
monitor's data and opens the views that show the answer.

Apart from the assistant, there is nothing to install. The assistant starts the monitor's own executable with
``--mcp``, and that process connects to the monitor window you have open.

To use it:

#. Install an MCP client, such as Claude Code or Codex, on the computer that runs the monitor.
#. Start monitoring (or open a recording), then choose **AI → Enable MCP Server**
   (see :ref:`pro_ai_assistants_enable`).
#. Add the monitor to your assistant once, from **AI → Connect Assistants**, and restart the assistant
   (see :ref:`pro_ai_assistants_connect`).
#. Ask your assistant about your DDS system.

.. _pro_ai_assistants_capabilities:

What an Assistant Can Do
========================

A connected assistant can:

* Inspect the monitored system: hosts, users, processes, participants, topics, DataWriters and DataReaders,
  their QoS, each topic's data type (its fields and its IDL), the connections and locators each endpoint reports,
  the statistics collected, and what the :ref:`Problems <pro_problem_panel>` panel, the
  :ref:`Issues <pro_issues_panel>` panel and the alerts report.
  It can also take a screenshot of the monitor window, and read what an open Topic Spy, Image Display,
  Event Chart or Data Table pane shows.
* Explain problems, such as endpoints that do not match or samples that are lost, from a DDS reference built
  into the monitor (see :ref:`pro_ai_assistants_knowledge`).
* Work in the monitor window: start and stop monitors, open the Domain View and the Architecture View,
  Statistics Charts, Topic Charts, XY Charts, Event Charts, Topic Spy, Topic Type (IDL), Image Display and
  Data Table panes, arrange them in tabs, open the side panels and the Panel Configuration, switch statistics
  readers on and off, register types, and create alerts and custom series.
* Record the monitored domains to MCAP or SQLite files, and manage recording configurations
  (see :ref:`pro_recording`).
* Open a recording and move through it (see :ref:`offline_mode`).
* Publish samples on the DDS network, and run programs or write files at a path it chooses, only after you
  allow it (see :ref:`pro_ai_permissions`).

The assistant makes its changes in *plans*: up to 20 changes in one request, which the monitor checks all
together before it applies any of them. The result looks and behaves as if you had made the changes yourself,
and it is saved with the workspace in the same way.

.. _pro_ai_assistants_examples:

Example Requests
----------------

* *"Which applications publish and subscribe to RobotStatus? One of the readers gets no data: why, and how do I
  fix it?"* The assistant lists the topic's writers and readers, finds the QoS policy that stops them from
  matching, explains it from the DDS reference, and can open the Architecture View on that writer and reader.
* *"Show me the latest RobotStatus sample, and under it an Event Chart of the robot's state, mode and emergency
  stop."* The assistant opens a Topic Spy and an Event Chart in one tab and places the chart under the spy, as
  in the figure below.
* *"Is the latency between the two ShapesDemo applications on Square normal? Show me a chart of it."* The
  assistant reads the latency statistics, compares them with what the reference says, and opens a Statistics
  Chart.
* *"Open the recording robots.mcap in my home folder and tell me when robot_2 went into FAULT."* The assistant
  opens the recording, charts the ``state`` field and moves the playback to that change.

.. thumbnail:: /rst/figures/screenshots/ai_arranged_tab_pro.png
    :align: center

.. _pro_ai_assistants_knowledge:

The DDS Reference
-----------------

The monitor gives assistants its own reference material for their explanations and recommendations: it
describes what Fast DDS does, defaults included. Each section says which Fast DDS
releases and editions it applies to, and names the Fast DDS Pro features that solve a problem. It covers:

* How a DataWriter and a DataReader match (QoS compatibility).
* Reliability, history and acknowledgments.
* Durability, liveliness, ownership, deadlines, instances and filters.
* Discovery.
* Transports: shared memory, UDP, TCP and the Fast DDS Pro network options.
* Throughput, latency and large data.
* Types: matching, evolution, representation and keys.
* DDS Security.
* What each statistic measures, and what each entity status reports.
* Running Fast DDS applications: configuration, ROS 2, statistics and logs.
* Writing and building a Fast DDS application in C++: XML profiles, Fast DDS-Gen and CMake.
* Fast DDS Pro and Safe DDS.
* Recording to MCAP and SQLite files.
* The monitor's own menus and panels, including the text of every **?** help button.
* Step-by-step playbooks for common questions, worked examples, and which view shows each kind of finding.

.. _pro_ai_assistants_enable:

Enabling the MCP Server
=======================

The **AI** menu is in the menu bar, next to the other menus, once you leave the start screen (by starting a
monitor, loading a workspace or opening a recording).

.. figure:: /rst/figures/screenshots/ai_menu_pro.png
    :align: center

* **Enable MCP Server** switches the server on. The entry then reads **Disable MCP Server**, which switches it
  off and disconnects every client.
* **Connect Assistants** opens the **AI Assistants** window on its **Connect** page.
* **Assistant Activity** opens the **AI Assistants** window on its **Activity** page.
* **Undo Last Assistant Change** closes the tabs and panes that the last assistant change opened
  (see :ref:`pro_ai_assistants_undo`). It is disabled when there is nothing to undo.

The server is off every time the monitor opens. It is not saved in workspaces or settings: loading a workspace
neither starts it nor stops it. It also works in offline mode, so an assistant can inspect a recording.

If the server cannot start, the **AI Assistants** window opens on its **Connect** page and says why.

.. _pro_ai_assistants_window:

The AI Assistants Window
========================

**AI → Connect Assistants**, **AI → Assistant Activity** and a click on the :ref:`MCP chip <pro_mcp_chip>` open
the **AI Assistants** window. It does not block the monitor: you can keep working while it is open.

Its top part shows the server:

* **MCP server is on** or **MCP server is off**, with a switch that starts and stops the server, as the
  **AI** menu does.
* While the server runs, **Serving as Monitor 1 · domain 0**: the name assistants know this window by, and what
  it monitors. **Copy name** copies the name, for when an assistant asks which monitor to use
  (see :ref:`pro_ai_assistants_several_monitors`).
* While the server runs, the two permission switches (see :ref:`pro_ai_permissions`).
* While the server runs, each connected client, with *Connected since <time>* and a **Disconnect** button, or
  *No assistant is connected yet.*

**Disconnect** closes that client's connection. The client then stays disconnected until you restart the server
in the client: in Claude Code, run ``/mcp`` and reconnect ``dds-monitor``; restart other clients. To disconnect
every client at once, switch the server off.

Below are two pages, **Connect** and **Activity**. **Close** closes the window.

.. _pro_ai_assistants_connect:

Connecting an Assistant
=======================

You connect each client once. The **Connect** page has a card for **Claude Code**, one for **Codex** and one for
**Other MCP clients**. You can use it whether the server is on or off.

.. figure:: /rst/figures/screenshots/ai_assistants_connect_pro.png
    :align: center

The **Claude Code** and **Codex** cards show whether the client has the monitor:

* **Added**: the client has a ``dds-monitor`` server that starts this monitor. **Remove** removes that entry and
  changes nothing else in the client.
* **Not added**: **Add to Claude Code** (or **Add to Codex**) adds it.
* **Needs update**: the client's ``dds-monitor`` entry starts a different file, for example a monitor installed
  in another place, or an AppImage you have moved since. **Update** replaces it with this monitor.
* **Not installed**: the monitor cannot find the client's command-line program (``claude`` or ``codex``). Install
  the client; the card notices it while the window is open, without restarting the monitor.
* **Checking…**: the monitor is asking the client.

The monitor looks for ``claude`` and ``codex`` on the ``PATH`` and in the folders they usually install to, so it
also finds them when you start the monitor from a desktop shortcut or the Start menu.

**Add to Claude Code**, **Add to Codex**, **Update** and **Remove** run the client's own command line. The
monitor never edits a client's configuration files itself. If the command fails, the card shows the client's
message under it.

* Claude Code: the monitor is added for every project (user scope). Adding first removes any ``dds-monitor``
  entry (``claude mcp remove --scope local dds-monitor``, then with ``--scope user``), then runs the command
  shown on the card.
* Codex: the monitor is added to Codex's configuration, for every project. Adding first runs
  ``codex mcp remove dds-monitor``, then the command shown on the card.

After adding or updating, restart the client so that it loads the server.

Each card also shows its command in a box, with a |copy| button to copy it and run it yourself in a terminal.
The path in it is the monitor you are running: its executable or, when you run the AppImage, the AppImage file.
On Linux the path is in single quotes; on Windows it is in double quotes, which both ``cmd`` and PowerShell
accept. For example:

.. code-block:: bash

    # Claude Code, Linux
    claude mcp add --scope user dds-monitor -- '/path/to/dds_monitor' --mcp

    # Claude Code, Windows
    claude mcp add --scope user dds-monitor -- "C:\path\to\dds_monitor.exe" --mcp

    # Codex, Linux
    codex mcp add dds-monitor -- '/path/to/dds_monitor' --mcp

    # Codex, Windows
    codex mcp add dds-monitor -- "C:\path\to\dds_monitor.exe" --mcp

The **Other MCP clients** card is for Claude Desktop, Cursor, VS Code and other clients that read their MCP
servers from a configuration file. It shows the entry to add to that file:

.. code-block:: json

    {"mcpServers":{"dds-monitor":{"args":["--mcp"],"command":"/path/to/dds_monitor"}}}

On Windows the path is written with doubled backslashes, as JSON needs (``"C:\\path\\to\\dds_monitor.exe"``).
VS Code takes the same entry under ``"servers"`` in its ``mcp.json``, instead of ``"mcpServers"``.

Under its command, the **Claude Code** card links to **Install Claude Code** and **Using MCP servers in Claude
Code**, and the **Codex** card to **Install Codex** and **Using MCP servers in Codex**. They open the client's own
documentation for your operating system.

.. _pro_ai_assistants_connection:

How the Connection Works
------------------------

The client starts ``dds_monitor --mcp`` itself whenever it needs the monitor; you do not run it. In this mode the
monitor opens no window and starts no DDS participant: it connects the client to the monitor window that has its
server on.

You can start the client before or after the monitor. Until a monitor window has its server on, the assistant is
told to ask you to choose **AI → Enable MCP Server**.

When the monitor restarts, or when you switch the server off and on, there is nothing to do in the client:
switch the server on again and the assistant's next request reaches the window. The assistant is told that the
monitor restarted, and reads it again before it changes anything. Only a client you disconnected with
**Disconnect** needs a restart (see :ref:`pro_ai_assistants_window`).

After you update or move the monitor, restart the client. If the monitor is now at another path, first open
**AI → Connect Assistants** and press **Update** on the card that shows **Needs update**.

.. _pro_ai_assistants_activity:

Following What an Assistant Does
================================

The **Activity** page lists what assistants have done in this window, newest first. Its tab shows how many
entries there are, as in **Activity · 12**.

.. figure:: /rst/figures/screenshots/ai_assistants_activity_pro.png
    :align: center

Each entry shows the time, a colored dot, the client's name, what it did and, for a call, how long it took.

* A burst of reads of the same kind is one entry with a count, such as *Claude Code · Listed entities ×3*.
* A change, such as *Claude Code · Changed the monitor · 3 operation(s)*, lists each operation under it, with a
  |tick| or a |cross|: what it opened or changed, in which tab, and for a failed operation, why. A sample the
  assistant published is shown, shortened. Past six lines, *+N more* shows the rest when you hover over it.
* A refused request, such as *Plan refused · 1 operation(s)*, shows the monitor's reason, for example a
  permission that is off.
* The list also shows clients connecting and disconnecting, and the server starting and stopping or failing to
  start.

The dot is green when everything went well, amber when some operations of a change failed, and red when all of
them failed or the request was refused. Events, such as a client connecting or the server stopping, have a hollow
dot. A server that fails to start has a red one.

The page keeps the last 50 entries while the monitor runs. They are not written to any file. The type IDL,
custom series code and file contents an assistant sends are not shown.

.. _pro_ai_assistants_undo:

Undoing an Assistant's Change
-----------------------------

**Undo last change**, at the top of the **Activity** page, and **AI → Undo Last Assistant Change** close the tabs
and panes that the last assistant change opened, whichever client made it. Your undo is listed in the activity as
*You · Undo of the last assistant change*.

Undo has limits:

* It only closes the tabs and panes that change opened. Settings, renamed or moved tabs, monitors, alerts,
  custom series, registered types and published samples stay as they are, and tabs or panes the change closed
  are not reopened. A tab that showed the view selector before the change put a pane in it shows the view selector
  again.
* It goes back one change only.
* It only works while no tab or pane has been opened, closed, moved, docked, arranged or renamed since, by you or
  by an assistant. Otherwise **Undo last change** and the menu entry are disabled.

An assistant can also undo its own last change, with the same limits.

.. _pro_mcp_chip:

The MCP Chip in the Status Bar
==============================

While the server runs, the status bar at the bottom of the window shows an **MCP** chip at its right end.

.. figure:: /rst/figures/screenshots/mcp_chip_pro.png
    :align: center

Its label says the name of the window and who is connected:

* **MCP · Monitor 1**: no client is connected.
* **MCP · Monitor 1 · Claude Code**: one client is connected.
* **MCP · Monitor 1 · 2 clients**: several clients are connected.

Its dot is gray with no client connected and green with a client connected. It turns red when the last change an
assistant made had a failure in it, and goes back with the next change that has none. While a client is
connected, the chip has a blue outline, and it lights up for a moment each time an assistant changes something.

Hover over the chip to see the window's name and domains, the connected clients and the last change. Click it to
open the **Activity** page.

The chip is hidden while the server is off, and also when the status bar has no room for it. The **AI** menu is
still there.

.. _pro_ai_permissions:

Permissions
===========

Switching the server on lets any MCP client run by your user account on this computer read the monitor and
arrange its workspace, with no further question from the monitor. What reaches past the monitor needs one of two
more switches, shown in the **AI Assistants** window while the server runs:

**Let assistants publish on the DDS network**
    *Publisher panes, samples and workspaces that start them. Other applications act on what is sent.*
    This covers opening a :ref:`Topic Publisher <publisher_pane>` pane, which creates a DataWriter at once,
    publishing samples, continuous publishing, moving a Topic Publisher to another topic, and loading a workspace.
    Starting a monitor or registering a type also needs it when Topic Publisher panes are waiting for that domain
    or for a type, because they would then start publishing.

**Let assistants run programs and write files through the monitor**
    *Alert scripts, and exports, dumps, recordings and workspaces written or loaded at a path the assistant
    chooses.*
    This covers an alert that runs a script, exporting charts, Data Tables or custom series, dumping statistics,
    the Scheduler's dump settings, recording to a folder the assistant chooses, saving the workspace to a path it
    chooses, and loading a workspace.

Both switches are off every time the server starts, and go off when you switch the server off. Only you can turn
them on: assistants have no operation for them.

Without them, an assistant can still read everything, open, arrange and close views, start and stop monitors,
stop a Topic Publisher, save your workspace to its own file (as **Save Workspace** does), record to your home
folder (the default) or to the folder of a saved recording configuration, create alerts without a script, create
custom series, and open recordings, XML profile files and custom series files. Custom series code runs inside the monitor, with no access
to files, the network or other programs, and each call is stopped after 100 ms.

When a request needs a switch that is off, the monitor refuses the whole plan and names the switch. The assistant
should then ask you. If you agree, turn the switch on and tell the assistant to go on. For example, *"Publish a
Square sample with color ORANGE at x 50, y 50"* is refused until **Let assistants publish on the DDS network** is
on.

These switches only cover what an assistant does through the monitor. What the assistant does with its own tools,
such as running commands or editing files, follows the client's own settings, and the client may also ask you
before each tool call.

.. _pro_ai_assistants_several_monitors:

Several Monitor Windows
=======================

Each window with its server on gets a short name, **Monitor 1**, **Monitor 2** and so on: the lowest number that
no other serving window uses. Each window shows its name in its MCP chip and, next to the domains it monitors, in
its **AI Assistants** window (**Serving as Monitor 2 · domain 1**). A window keeps its name when you switch its
server off and on, unless another window has taken it meanwhile.

* With one window serving, the assistant uses it.
* With several windows serving, the assistant cannot choose one itself. It asks you which one to use, and every
  request but the connection check is refused until you answer. Tell it the name, such as *Monitor 2*, or just
  *2*. **Copy name** in the **AI Assistants** window copies it. Your choice lasts for the assistant's session while
  that window serves; if the window closes or stops its server, the assistant asks again.

A recording opened from a window that has already monitored opens in a new window (see :ref:`offline_mode`),
whose server is off. Switch it on in that window if you want an assistant to use it; the assistant then asks you
which window to use.

.. _pro_ai_assistants_privacy:

Privacy and Safety
==================

* Only MCP clients run by your user account on this computer can connect: the server opens no network port. The
  monitor itself does not connect to any AI service.
* Whatever an assistant reads through the server goes to the MCP client, which sends it to the AI model provider
  it uses, under that provider's terms. This can include host, user and process names, topic and type names, QoS,
  IDL, statistics, sample values, file paths and screenshots of the monitor window. Do not switch the server on
  while you monitor a system whose details you may not share with that provider.
* The monitor does not ask before each client or call: switching the server on is your consent. While it is on,
  any MCP client started under your user account can connect, so switch it off when you are done.
* Names and values that come from the DDS network, such as topic and type names, aliases and sample values, reach
  the assistant as data, not as instructions. This lowers the risk that text published on the network steers an
  assistant, but cannot rule it out. If it happens, the permission switches limit what the assistant can do
  through the monitor.
* The name shown for a client in the **AI Assistants** window and in the MCP chip is the name the client gives
  itself. The monitor does not check it.
* So that clients can find it, a serving window writes a small file in a folder of your user account. The file
  holds the window's name and the domain numbers it monitors, but no topic names or file paths.

.. _pro_ai_assistants_limitations:

Known Limitations
=================

* Clients must run on the same computer, under the same user account. At most 8 clients can be connected at a
  time; one more is refused with a message asking to close a session you no longer use.
* When several topics share a name (one per type), the views an assistant opens on that name show the first one
  discovered, and the assistant is told which. It cannot open a view of the others.
* An assistant cannot publish on a domain with a type that only another domain's applications carry. The monitor
  refuses the request and says why.
* Leave the monitor window visible when an assistant checks its work on screen: a screenshot of a minimized or
  covered window can show old charts.
* While a recording is open, what the monitor disables for a recording is also refused to assistants, such as
  publishing, alerts and starting monitors. A recording holds no statistics.
* Undo only closes tabs and panes, one change back (see :ref:`pro_ai_assistants_undo`).
* The **Activity** page keeps only the last 50 entries of the current session (see
  :ref:`pro_ai_assistants_activity`).
