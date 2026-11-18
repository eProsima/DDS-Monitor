.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _pro_data_table:

################
Data Table |Pro|
################

A *Data Table* pane lists DDS samples as the rows of a table: one row per sample, and one column per topic
member, sample field (timestamp, writer, sequence number, partitions...) or :ref:`custom series
<custom_series_panel>`.
One table can list several topics, from different domains too.
A live table keeps a history of the samples that arrive. With a :ref:`recording <offline_mode>` open, the
table lists the recorded samples instead.

A :ref:`Topic Spy <dockable_spy_pane>` shows only the latest sample of one topic, and
:ref:`Topic Charts <topic_charts>` plot field values over time.
Use a Data Table when you need to read many samples side by side: which writer sent each one, in what
order, with which values, and which samples match a condition.

.. thumbnail:: /rst/figures/screenshots/data_table_pro.png
    :align: center

The common tasks are:

* To see the samples of a topic, right-click the topic in the :ref:`topics_panel` and choose **Open Data
  Table** (see :ref:`pro_data_table_opening`).
* To show more members or sample fields, add columns (see :ref:`pro_data_table_columns`).
* To find samples, type in the search box (see :ref:`pro_data_table_search`) or add filters (see
  :ref:`pro_data_table_filters`).
* To sort the rows of a live table, freeze it, then click a column title (see :ref:`pro_data_table_live`
  and :ref:`pro_data_table_sorting`).
* To read a whole sample, click its row (see :ref:`pro_data_table_details`).
* To keep the rows, export them to a CSV file (see :ref:`pro_data_table_csv`).

AI assistants connected to the monitor's MCP server can also open Data Tables, set them up, read their
rows and export them (see :ref:`pro_ai_assistants`).

.. _pro_data_table_opening:

Opening a Data Table
====================

Open a Data Table in any of these ways:

* Right-click a topic in the :ref:`topics_panel`, the :ref:`Logical Panel <pro_logical_panel>`, the
  :ref:`Domain View <pro_domain_view>` or an :ref:`Architecture View <pro_architecture_view>`, and choose
  **Open Data Table**. The table opens already listing that topic.
* Use **Add → Data Table** in the application menu bar. An empty table opens, in a new tab when the
  current one already has panes, together with its :ref:`Panel Configuration <pro_data_table_config>`.
* Click **+** at the end of the tab strip and choose **Data Table** in the view selector of the new tab.
* Click the |three_dots_menu| button in the title bar of any pane, then choose
  **Replace panel**, **Split right** or **Split down**, and **Data Table**.

A table opened with **Open Data Table** has the columns **Timestamp** and **Topic**, and the first five
members of the topic as columns once the monitor knows the topic's type.
A new empty table has only the **Timestamp** and **Topic** columns, and no topics: add them from its Panel
Configuration, or drag members onto it (see :ref:`pro_data_table_columns`).

While a table has nothing to list, it says why: *Add topics to this table from its configuration panel, or
drag topic members onto it*, *Waiting for samples in the selected sources*, *No samples match this query*,
or *No samples while frozen: resume to show new arrivals*.

To list the samples of a topic, the monitor creates a DataReader for it.
If the reader cannot be created, an *Unable to read "<topic>"* dialog over the table gives the reason.
Click **Retry** to try again, or close the dialog.

.. _pro_data_table_columns:

Adding Topics and Columns
=========================

A table lists the samples of its topics. Every row is one sample of one of those topics, so a member
column shows a value only in the rows of its own topic, and ``-`` in the rows of the other topics.
A topic joins the table when you add one of its members as a column, or with **Add Topic**, and leaves it
when you remove its last member column.

A column is titled ``<topic>.<member>``, such as ``RobotStatus.battery_level``.
A system column is titled with the field name, such as ``writer``, and a custom series column with the
series name.
A table cannot have the same column twice.

To add columns, click the |gear| **Panel Settings** button in the table's title bar, then **Add Columns**
in the Panel Configuration. The **ADD COLUMNS** section opens, with three parts.

**Topic Columns**
    Choose the monitored domain in **Monitor** (live only), then the topic in the topic list (type in
    **Filter topics...** to narrow it). The members of the topic's type are listed below once the type is
    known; until then the list shows *Waiting for members...*. Type in **Filter members...** to narrow
    the list.

    * Select a member and click **Add Column** to add it. If the topic is not in the table yet, it is
      added with the column. Nested members are listed with their path, such as ``position.x``. A
      struct can be a column too: its cell shows how many members it has.
    * Click **Add Topic** to add the selected topic with its first five members as columns. Struct
      and collection members are skipped when picking those five.

    Members already added are grayed out, with the tooltip *Already added as a column*.

**System Columns**
    Fields of the sample itself rather than of its data. Select one and click **Add Column**. See
    :ref:`pro_data_table_system_fields`.

**Custom Series**
    The custom series defined in the :ref:`custom_series_panel` (type in **Filter custom series...** to
    narrow the list). Select one and click **Add Column**. See :ref:`pro_data_table_custom_series`.

.. _pro_data_table_drag:

Dropping Columns onto the Table
-------------------------------

You can also add a column by dropping it onto the table:

* A member of a topic, dragged from the :ref:`topics_panel`, from a :ref:`Topic Spy <dockable_spy_pane>`
  or from the :ref:`sample details <pro_data_table_details>` of a Data Table. Its topic joins the table if
  it is not in it yet, whatever its domain.
* A custom series, dragged from the :ref:`custom_series_panel`.

The table is highlighted when it accepts the drop. It refuses a column it already has.

.. _pro_data_table_collections:

Elements of Sequences and Arrays
--------------------------------

A sequence or array member can be added as a whole, and its cell shows its size, such as
``[3 elements]``.
To add one element, or a member of one element, click **…** next to the collection in the member list.
An **Inspect index** field appears with ``0``, and the list then shows that element (such as
``poses[0]``) and its members.
Type another index to list another element instead.

.. _pro_data_table_system_fields:

System Fields
-------------

.. list-table::
    :header-rows: 1

    *   - Field
        - Shows
    *   - ``timestamp`` (the default **Timestamp** column)
        - Live: the sample's source timestamp, or its reception time when the writer sent no source
          timestamp. Recording: the time the sample was recorded.
    *   - ``topic`` (the default **Topic** column)
        - The name of the sample's topic.
    *   - ``domain``
        - The DDS domain number. Not offered for a recording.
    *   - ``writer``
        - The GUID of the DataWriter that sent the sample. For a recording, only a SQLite recording has it.
    *   - ``sourceTime``
        - The source timestamp the writer gave the sample. For a recording, when the file stores it.
    *   - ``receptionTime``
        - When the monitor received the sample. Live only.
    *   - ``logTime``
        - When the sample was recorded. Recordings only.
    *   - ``sequence``
        - Live: the sample's sequence number. Recording: the number of the sample in the recording, as
          eProsima DDS Recorder numbers them.
    *   - ``identityWriter``, ``identitySequence``
        - The writer GUID and sequence number of the sample identity. They keep the original writer of a
          sample forwarded by another application, while ``writer`` is the one that sent it. Live only.
    *   - ``channel``
        - The MCAP channel of the sample. MCAP recordings only.
    *   - ``partitions``
        - The partitions of the DataWriter that sent the sample, separated by commas. The default
          (empty) partition shows as ``(default)``, and ``Unavailable`` means the partitions are not known.
          The monitor does not read the partitions from a recording, so a recording's table always shows
          ``Unavailable``.

A field a sample does not have shows ``-``, for example ``logTime`` in a live table.

The partitions are read once for each writer the monitor's reader matches.
If a matched writer changes its partitions, the table shows the new ones only after that writer stops
matching and matches again.

.. _pro_data_table_custom_series:

Custom Series Columns
---------------------

A custom series column shows the value of a :ref:`custom series <custom_series_panel>` computed at each
sample of its input topics.
The value can be a number, a string or a boolean, whatever the formula returns.

* The samples of the series' input topics are listed as rows even when those topics are not in the table
  otherwise. Adding the column can therefore add rows.
* Rows of other topics show ``-`` in the column.
* The values are computed over the samples the table holds, oldest first. A formula that keeps state
  between samples starts from the oldest sample in the table.
* Editing or renaming the series updates the column.

If a series cannot be computed, the reason is shown in red under the search box.

.. _pro_data_table_arranging:

Arranging Columns
-----------------

* To hide a column, click the |eye| button next to its name in the **COLUMNS** list of the Panel
  Configuration, or right-click its title in the table and choose **Hide column**. A hidden column shows
  |eye_off| in the list: click it to show the column again. **Show All Columns** and **Hide All Columns**
  in **ACTIONS** act on every column. Search and filters still read hidden columns.
* To reorder the columns, drag a column by its handle in the **COLUMNS** list. With the handle focused,
  the *Up* and *Down* keys move it too. Dragging a column title in the table does not move it.
* To resize a column, drag the right edge of its title in the table. A column is at least 80 pixels wide,
  and the last column takes the remaining width of the table.
* To give every shown column the same width, filling the table, click |move_horizontal| **Space columns
  evenly** in the title bar, or **Space Columns Evenly** in **ACTIONS**. The title bar button is hidden
  while the pane is too narrow for it.
* To remove a column, click |cross| next to it in the **COLUMNS** list, or right-click its title in the
  table and choose **Remove column**. The filters made on the column are removed with it, and so is its
  topic when it was that topic's last column. A table keeps at least one column.

.. _pro_data_table_values:

How Values Are Shown
====================

* An enumeration shows the label of its value, such as ``MOVING``, and is sorted and searched by that
  label.
* A bitmask shows its bits, such as ``00000101``, and is sorted by its numeric value.
* A struct or collection added as a whole shows its size, such as ``{2 members}`` or ``[3 elements]``.
  Inspect it in the :ref:`sample details <pro_data_table_details>`.
* A long collection, such as image data, reaches the table summarized, and its cell ends in
  ``(summarized)``.
* A value the sample does not have shows ``-``, and a JSON null value shows ``null``.
* A cell shows at most 1024 characters. Select it and press *Ctrl+C* to copy it whole.

Timestamps are shown as ``yyyy-MM-dd HH:mm:ss.zzz`` followed by the time zone: ``UTC`` by default, or
the computer's own time zone when **Use local time** is on in the Panel Configuration.
The setting applies to every timestamp the table shows, to the dates and times you type in timestamp
filters, and to the CSV export.

.. _pro_data_table_controls:

Title Bar Controls
==================

The title bar shows the table's name (**Data Table** unless you rename it in **TABLE NAME**) and these
buttons, from left to right:

* |move_horizontal| **Space columns evenly** gives every shown column the same width. Hidden while the
  pane is narrow; the same action is in **ACTIONS**.
* |pause| **Freeze** / |play| **Resume** holds the rows still and lets you sort them (see
  :ref:`pro_data_table_live`). Live only.
* |radio| **Follow newest** keeps the newest sample in view. The button is highlighted while it is on.
  Live only.
* |eraser| **Clear history** removes every sample the table holds. Live only.
* |question| **Help** opens a short description of the pane and tips.
* |expand_square| **Expand** / |collapse_square| **Collapse** shows the pane alone in the tab, and back.
* |gear| **Panel Settings** opens the :ref:`Panel Configuration <pro_data_table_config>` of this table.
* |three_dots_menu| **Panel Actions** opens the **Replace panel**, **Split right** and **Split down**
  menus, each listing the pane types.
* |cross| **Close** closes the pane.

Below the title bar are the search box, with its **Aa** button (see :ref:`pro_data_table_search`), and a
line of counts:

* Live: ``<matching> matching / <retained> retained · <evicted> evicted``, followed while frozen by
  ``· <n> arrivals while frozen``. *Matching* is the number of rows listed after the search and filters,
  *retained* the number of samples in the history, and *evicted* the number of samples dropped by the
  history limits.
* Recording: ``<matching> matching / <retained> retained``, followed by the start and end of the
  recording range that was loaded.

.. _pro_data_table_live:

Live Tables: History, Freeze and Follow Newest
==============================================

A live table lists the samples of its topics that arrive after the topic was added to the table, newest
last.
It keeps a history of them within two limits, set in **DISPLAY** in the Panel Configuration:

* **Max samples**: from 1 to 9999. Default 1000.
* **Max size (MB)**: the memory the kept samples may use, from 1 to 128 MB (1 MB is 1,048,576 bytes).
  Default 128.

When either limit is reached, the oldest samples are evicted first.
Raise the limits to keep more samples to search, sort or export, and lower them to use less memory.
Changing the limits applies at once to the samples already kept.

**Follow newest** is on when a table opens: the view stays on the newest row as samples arrive.
Clicking a row, scrolling the table or dragging its scroll bar stops following, so the rows you are reading
stay where they are.
Click |radio| **Follow newest** to follow again.

**Freeze** keeps the rows on screen as they are, so you can read, search, filter and sort them while samples
keep arriving.
The samples that arrive meanwhile still go into the history, and the count line shows how many arrived.
Click **Resume** to list the history again, in arrival order: a sort chosen while frozen is dropped.
The frozen rows are kept apart from the history, so a frozen table can use up to twice its limits.

**Clear history** (or **Clear Table** in **ACTIONS**) removes every sample the table holds and closes the
sample details.
Only samples arriving after that are listed.
A frozen table stays frozen, now empty, and shows the new samples when you resume it.

.. _pro_data_table_sorting:

Sorting
=======

Click a column title to sort the rows by that column, and click it again to reverse the order.
A chevron in the title of the sorted column shows the direction.

* A live table sorts only while it is frozen. While it runs, it lists the samples in arrival order and a
  click on a title does nothing. Freeze it first, then click the title. Resuming returns to arrival order.
* A recording's table can always be sorted. Sort by **Timestamp** to return to time order.
* Numbers sort by value, enumerations by their label, bitmasks by their value, and text by character
  code, so upper-case letters come before lower-case ones.
* Rows without a value in the column (``-``, ``null`` or a summarized collection) always come last, in
  both directions.

.. _pro_data_table_search:

Searching
=========

Type in the search box under the title bar (*Search all decoded fields, including hidden columns*) to list
only the samples that contain the text.
The search looks in:

* The topic name and, in a live table, the domain number.
* Every member of the decoded sample, whether it is a column or not: member names and values, with
  enumerations by their label.
* The values of the system fields and of the custom series columns.

The search ignores letter case unless you turn on **Aa** (*Case sensitive search*).
Timestamps are not matched as they are displayed: to find samples by time, add a
:ref:`timestamp filter <pro_data_table_filters>`.

.. _pro_data_table_filters:

Filtering
=========

Filters list only the samples whose value in a column passes a condition, for example the samples whose
``state`` is ``FAULT``, or whose ``battery_level`` is at most 50.
Build them in the **FILTERS** section of the Panel Configuration:

#. Choose the column. Every column of the table can be filtered, hidden ones included.
#. Choose the operator. The list depends on the column's type (see the table below).
#. Enter the value: **Value or expression**, **Minimum (optional)** and **Maximum (optional)** for a range,
   or a date in ``yyyy-MM-dd`` and a time in ``HH:mm:ss.zzz`` for a timestamp (the milliseconds are
   optional).
#. Turn on **Case sensitive** if needed. It is offered for **Contains**, **Equals** and **Equals / enum
   label** on text, enumeration and custom series columns.
#. Click **Add filter**.

.. thumbnail:: /rst/figures/screenshots/data_table_filter_pro.png
    :align: center

Each filter is listed under **Add filter** as a short line with its column, operator and value, such as
``RobotStatus.battery_level le 50``.
Click |eye| next to a filter to stop applying it without removing it, and again to apply it again.
Click |cross| to remove it.

All the filters apply together: a row is listed only if it passes every filter that is on.
A filter on a member of a topic applies only to the rows of that topic: rows of the table's other topics are
not affected by it.
Filters on system fields and custom series apply to every row.

.. list-table::
    :header-rows: 1

    *   - Column type
        - Operators
    *   - Text (strings and characters, ``topic``, ``writer``, ``identityWriter``, ``partitions``)
        - **Contains**, **Equals / enum label**, **Regex**
    *   - Number (``domain``, ``sequence``, ``identitySequence``, ``channel`` too)
        - **Equals**, **Numeric range (inclusive)**, **Less than**, **At most**, **Greater than**, **At least**
    *   - Timestamp (``timestamp``, ``sourceTime``, ``receptionTime``, ``logTime``)
        - **Equals**, **Between (inclusive)**, **Before**, **At or before**, **After**, **At or after**
    *   - Enumeration
        - **Equals / enum label**
    *   - Boolean
        - **Boolean**
    *   - Custom series
        - **Equals**, **Contains**, **Regex**, **Numeric range (inclusive)**, **Less than**, **At most**,
          **Greater than**, **At least**, **Boolean**
    *   - Any column
        - **Missing**, **JSON null**

Other columns, such as structs, bitmasks and collections of numbers, offer only **Missing** and
**JSON null**.

How the operators behave:

* **Contains** and **Equals / enum label** compare text, ignoring letter case unless **Case sensitive** is
  on. On a sequence or array of strings, such as ``partitions``, a row passes if any element passes.
* **Regex** matches a regular expression anywhere in the text, ignoring letter case.
* **Equals / enum label** on an enumeration takes the label (``FAULT``) or its numeric value.
* **Equals** on a number compares numerically. **Less than**, **At most**, **Greater than** and
  **At least** are ``<``, ``<=``, ``>`` and ``>=``. **Numeric range (inclusive)** takes a minimum, a
  maximum or both.
* Timestamp operators read the date and time in UTC, or in the local time zone when **Use local time** is
  on; the label above the fields says which. **Equals** and the inclusive bounds take in the whole
  millisecond entered. For **Between (inclusive)**, either end can be left empty.
* **Boolean** takes ``true`` or ``false``, typed as the value.
* On a custom series, the text operators also match a number or boolean result by the text its cell
  shows, such as ``18.0`` or ``true``.
* **Missing** lists the rows that do not have the value, and **JSON null** those where it is null.
  Neither takes a value.

A filter is checked when you add it: an invalid number, a minimum above the maximum, an invalid regular
expression or a start time after the end time is refused with a message in red.

Turning **Use local time** on or off converts the date and time being typed in a timestamp filter to the
new time zone. Filters already added keep the instant they were made with.

.. _pro_data_table_details:

Inspecting a Sample
===================

Click a row to select its sample.
The row is highlighted, the table stops following the newest sample, and the **Sample details** open below
the rows.
Drag the divider between the rows and the details to resize them.
The details need room: in a pane that is too short, only the rows are shown.

.. thumbnail:: /rst/figures/screenshots/data_table_details_pro.png
    :align: center

The details show:

* A summary: the topic, the domain (live), the timestamp and the number of partitions, then the writer,
  sequence numbers and times the sample has.
* The decoded sample as a tree. Expand structs and collections to see their members. In a live sample,
  an enumeration shows its ``name`` and ``value``, and a bitmask its ``value``, its ``binary`` bits and
  its ``active`` flags.

In the tree you can:

* Right-click a member to copy it with **Copy Property**, **Copy Value** or **Copy Row**. On a single
  value, **Plot on Time Series** and **Plot on Event Chart** open a new chart of that member; a Time
  Series plots numbers and booleans only.
* Drag a member onto a topic chart to plot it, or onto a Data Table to add it as a column.

The buttons of the details are:

* |copy| **Copy decoded JSON** copies the whole sample as JSON.
* |play| **Seek playback here** moves the playback of a recording to this sample (see
  :ref:`pro_data_table_offline`). Recordings only.
* |cross| **Close sample details** closes them.

If the selected sample leaves the table, because the history limits evicted it or a filter hides it, its
details stay open with the note *This sample is no longer in the table*, until you select another row or
close them.

With a cell selected, the *Up* and *Down* keys select the previous or next row, *Page Up* and *Page Down*
move a page, and *Ctrl+C* copies the cell. A struct or collection is copied as JSON.

.. _pro_data_table_csv:

Exporting to CSV
================

Click **Export to CSV** in the **ACTIONS** section of the Panel Configuration and choose a file.
The file holds:

* A header row with the titles of the shown columns. Hidden columns are left out.
* One line per listed row, after the search and filters, in the table's order.
* The values as the table shows them (timestamps in the table's time zone, enumerations by label),
  except structs and collections, which are written whole as JSON. Missing values are empty.

Values are separated by ``;``. A value containing ``;``, quotes or line breaks is written between double
quotes.
The export runs in the background. If it fails, a dialog gives the reason.

A live table exports the samples it holds, so set its history limits to keep what you want to export.
Export to CSV also works on a recording.

.. _pro_data_table_offline:

Recordings
==========

With a recording open (see :ref:`offline_mode`), a Data Table lists the samples of its topics in the range
loaded when the recording was opened.
Its topics are looked up in the recording by name.

* The table lists every sample of that range, whatever the playback position. It does not move with
  playback.
* Select a row and click |play| **Seek playback here** in the sample details to pause playback at that
  sample's time. The other panes then show the recording at that point.
* The rows can be sorted at any time, by clicking a column title.
* **Freeze**, **Follow newest**, **Clear history**, **Clear Table** and the history limits are not
  available: the table lists the recording as it is.
* In **ADD COLUMNS**, the topic list holds the recording's topics, without a **Monitor** choice. The
  ``domain`` system field is not offered.
* The ``timestamp`` and ``logTime`` columns show when each sample was recorded, and ``receptionTime`` shows
  ``-``. The ``writer`` column is filled for a SQLite recording only, ``channel`` for an MCAP one only,
  and ``partitions`` shows ``Unavailable``.

In a live session, **File → Start Recording...** and the recording configurations with **Record what is
visualized** record the samples of the topics shown in Data Table panes, among others (see
:ref:`pro_recording`).

.. _pro_data_table_config:

Panel Configuration
===================

Click |gear| **Panel Settings** in the title bar to open the :ref:`right_pane_config` sidebar for the
table.
Changes made here apply to the table at once.
The sidebar is headed **DATA TABLE**, with a |question| **Help** button, and has these sections:

.. figure:: /rst/figures/screenshots/data_table_config_pro.png
    :align: center

**TABLE NAME**
    The name shown in the title bar. The name applies when you press *Enter* or leave the field. An
    empty name restores **Data Table**.

**DISPLAY**
    * **Use local time**: show timestamps, and read timestamp filters, in the computer's time zone instead
      of UTC.
    * **Max samples** and **Max size (MB)**: the history limits of a live table (see
      :ref:`pro_data_table_live`). Press *Enter* or leave the field to apply them. Not shown for a
      recording.

**COLUMNS**
    The table's columns, in order, each with a drag handle, an |eye| visibility button and a |cross|
    remove button (see :ref:`pro_data_table_arranging`). **Add Columns** opens the **ADD COLUMNS** section
    and **Hide Add Columns** closes it.

**ADD COLUMNS**
    **Topic Columns**, **System Columns** and **Custom Series**, each with its **Add Column** button, and
    **Add Topic** (see :ref:`pro_data_table_columns`). The form stays as you left it when you go to
    another pane and come back.

**FILTERS**
    The column, operator and value of a new filter, **Add filter**, and the list of filters (see
    :ref:`pro_data_table_filters`).

**ACTIONS**
    * **Show All Columns** and **Hide All Columns**.
    * **Space Columns Evenly**.
    * **Clear Table**: the same as **Clear history** in the title bar. Live only.
    * **Export to CSV** (see :ref:`pro_data_table_csv`).

**PANEL ACTIONS**
    **Replace panel**, **Split right** and **Split down**, each listing the pane types.

.. _pro_data_table_workspace:

Saving in a Workspace
=====================

A :ref:`workspace <workspace>` saves each Data Table with:

* Its name, topics and columns: their order, widths and visibility.
* Its filters, each on or off.
* The search text and its **Aa** setting, and the sort column and direction.
* **Follow newest**, **Use local time** and the history limits.

The samples are not saved: a live table starts empty and fills as samples arrive, and a table opened with a
recording lists that recording's samples.
A table that is frozen is not frozen when the workspace is loaded again.

.. _pro_data_table_limits:

Limits
======

* A live table keeps at most 9999 samples and 128 MB of samples.
* A sample larger than 8 MB is not listed.
* A cell shows at most 1024 characters; *Ctrl+C*, **Copy decoded JSON** and the CSV export give the whole
  value.
* Long collections, such as image data, are summarized and cannot be listed element by element.
* A tab holds up to six panes (see :ref:`dockable_panes`).
