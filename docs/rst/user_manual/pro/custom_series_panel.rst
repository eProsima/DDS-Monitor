.. include:: ../../exports/pro_alias.include
.. include:: ../../exports/roles.include

.. _custom_series_panel:

#########################
Custom Series Panel |Pro|
#########################

A *Custom Series* is a user-defined data series computed from a JavaScript formula.
You bind one or more topic fields (and optional constants) to variables and write a short function
that returns the value to plot.
The result behaves like any other topic-chart series: it can be dragged onto a :ref:`Topic Chart
<topic_charts>`, colored, hidden, and exported.

.. thumbnail:: /rst/figures/screenshots/custom_series_chart_pro.png
    :align: center

You manage custom series from the *Custom Series* panel in the left sidebar and edit them in a
central-tab editor.
Open the panel by clicking the **Custom Series** icon in the vertical icon bar on the far left of the
window (hover any icon to see its tooltip).

The panel header reads *CUSTOM SERIES* and has, from left to right:

* |file_up| **Export Custom Series** - saves all defined series to a ``.json`` file.
* |file_down| **Import Custom Series** - loads series definitions from a ``.json`` file.
* |question| - opens a contextual help panel with usage tips and a link to this documentation page.
* |plus| - creates a new custom series and opens the editor.

When no series are defined yet, the panel shows *No custom series defined* and a **New custom series**
button.

Each defined series appears as a row showing its name. Hovering a row reveals a |gear| **Edit** button,
a |copy| **Duplicate** button, and a red |cross| **Delete** button. Right-clicking a row opens a context
menu with:

* **Change alias** - rename the series.
* **Plot on Time Series** - open a new :ref:`Time Series Chart <time_series>` with the series. Disabled
  while the series has only returned text, which only an Event Chart can show.
* **Plot on Event Chart** - open a new :ref:`Event Chart <event_charts>` with the series.
* **Edit** - open the formula editor.
* **Duplicate** - create a copy named ``<name>_copy`` (``<name>_copy_2`` and so on if that name is
  taken) with the same data sources, global variables, and formula.
* **Delete** - remove the series (asks for confirmation; this cannot be undone).

You can also plot a series by dragging its row onto a Topic Chart pane, or onto a
:ref:`Data Table <pro_data_table>` to add it as a column. A series that has an error
cannot be created until the error is fixed.

.. _custom_series_editor:

The Formula Editor
==================

Creating or editing a series opens a central-tab editor with these sections:

* **SERIES NAME** - the series name. It must be non-empty and unique across all custom
  series.

* **DATA SOURCES** - each *data source* binds a field of a DDS topic to a variable name that
  the formula can read. Select a **Monitor** and a **Topic**, pick a **Field** from the field tree
  (the *Filter fields...* field narrows the list; each field shows its kind: ``number``, ``string``, or
  ``boolean``), enter a variable name in **As var** (a valid
  JavaScript identifier: start with a letter, ``_`` or ``$``; no spaces or special characters), and
  click **Add Binding**. Added bindings are listed as ``varName = topic.fieldPath`` and can be
  removed individually. At least one data source binding is required before a series can be saved.

* **GLOBAL VARIABLES** - optional named constants available to the formula. Enter a **name** and a
  **value** and click **Add Global Variable**. The value must be a JavaScript literal of one of the
  following types: number, string, boolean, or null.

* **JAVASCRIPT FUNCTION BODY** - the formula itself. The editor shows an auto-generated signature line
  that updates as you add data sources, ``function(time, <your variables>) { ... }``, where ``time``
  is the sample timestamp and each bound variable and global variable is in scope. Return the
  value to plot (a number, a text, or a boolean), or return ``undefined`` (or
  nothing) to skip a point without producing an error.

* **Save**, **Save & Exit**, **Cancel** - *Save* validates and saves while keeping the editor open.
  *Save & Exit* also closes the editor, but first waits briefly for a runtime error and stays open if
  the formula throws on its first evaluation. *Cancel* discards changes.

.. thumbnail:: /rst/figures/screenshots/custom_series_editor_pro.png
    :align: center

.. _custom_series_formula:

Each data source variable holds the latest value of its field, with its own type: a number, a string,
or a boolean. An enum field is listed as two fields: ``<field>.name``, its name as a string, and
``<field>.value``, its number.

The formula returns the value of the series:

* A **number** is plotted on every kind of topic chart.
* A **text** (string) is shown by Event Charts as a state. Time Series and XY Charts plot nothing for it,
  and the legend entry of the series says so.
* A **boolean** is shown by Event Charts as ``true`` or ``false``, and plotted as 1 or 0 by Time Series
  and XY Charts.

For example, with ``state`` bound to ``RobotStatus.state.name`` and ``battery`` to
``RobotStatus.battery_level``, this formula gives a text status to follow on an Event Chart:

.. code-block:: javascript

    if (state === "FAULT") return "FAULT";
    return battery < 70 ? "LOW BATTERY" : "OK";

The series fails, and stops computing new values until you save a fix, when its formula throws an
exception, takes more than 100 ms in one call, or returns another kind of value (an object or an array).

Formulas run in *Qt*'s built-in JavaScript engine (``QJSEngine``) and support standard ECMAScript. All
standard built-ins are available, including ``Math``, ``JSON``, ``Number``, ``String``, ``Array``,
``Object``, ``Date``, ``RegExp``, ``parseInt``, ``parseFloat``, ``isNaN``, and ``isFinite``.

For safety, the following identifiers are **not** available inside a formula:
``console``, ``window``, ``document``, ``XMLHttpRequest``, ``fetch``, ``setTimeout``,
``clearTimeout``, ``setInterval``, ``clearInterval``, and ``qt``.

.. _custom_series_saving:

A successful save shows *Series saved successfully.* If validation fails, the editor reports a
specific message, for example when the series name is empty or already exists, when no
data source binding has been added, when a variable name is not a valid identifier, or when the
function body is empty.

If you changed the formula, the bindings, or the global variables of a series that a chart or a table
shows, the **Custom Series In Use** dialog lists where it is shown. **Save** recalculates it everywhere
with the new formula (live charts showing it start again from now), **Save as Copy** keeps the series
as it was and saves your changes as a new series, which the editor then edits, and **Cancel** returns
to the editor.

.. _custom_series_import_export:

Importing and Exporting
=======================

You can save custom series definitions to disk and share them between sessions or machines:

* **Export Custom Series** (panel button, or **File → Export Custom Series...**) writes every defined
  series to a ``.json`` file.
* **Import Custom Series** (panel button, or **File → Import Custom Series...**) loads series
  definitions from a ``.json`` file.

See :ref:`pro_application_menu` for the corresponding menu entries.
