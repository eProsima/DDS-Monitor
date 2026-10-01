.. include:: ../../exports/alias.include
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
* |help| - opens a contextual help panel with usage tips and a link to this documentation page.
* |plus| - creates a new custom series and opens the editor.

When no series are defined yet, the panel shows *No custom series defined. Click + to create one.*

Each defined series appears as a row showing its name. Hovering a row reveals a |gear| **Edit** button
and a red |cross| **Delete** button. Right-clicking a row opens a context menu with:

* **Change alias** - rename the series.
* **Plot on chart** - add the series to the active :ref:`Topic Chart <topic_charts>` (disabled when
  the series has an error).
* **Edit** - open the formula editor.
* **Delete** - remove the series (asks for confirmation; this cannot be undone).

You can also plot a series by dragging its row onto a Topic Chart pane. A series that has an error
cannot be created until the error is fixed.

.. _custom_series_editor:

The Formula Editor
==================

Creating or editing a series opens a central-tab editor with these sections:

* **Series Name** - the series name. It must be non-empty and unique across all custom
  series.

* **Data Sources** - each *data source* binds a numeric field of a DDS topic to a variable name that
  the formula can read. Select a **Domain** and a **Topic**, pick a **Field** from the field tree
  (the *Filter fields...* field narrows the list), enter a variable name in **As var** (a valid
  JavaScript identifier: start with a letter, ``_`` or ``$``; no spaces or special characters), and
  click **Add Binding**. Added bindings are listed as ``varName = topic.fieldPath`` and can be
  removed individually. At least one data source binding is required before a series can be saved.

* **Global Variables** - optional named constants available to the formula. Enter a **name** and a
  **value** and click **Add Global Variable**. The value must be a JavaScript literal of one of the
  following types: number, string, boolean, or null.

* **JavaScript Function Body** - the formula itself. The editor shows an auto-generated signature line
  that updates as you add data sources, ``function(time, <your variables>) { ... }``, where ``time``
  is the sample timestamp and each bound variable and global variable is in scope. Return the
  value to plot (the returned number becomes the series data point), or return ``undefined`` (or
  nothing) to skip a point without producing an error.

* **Save**, **Save & Exit**, **Cancel** - *Save* validates and saves while keeping the editor open.
  *Save & Exit* also closes the editor, but first waits briefly for a runtime error and stays open if
  the formula throws on its first evaluation. *Cancel* discards changes.

.. thumbnail:: /rst/figures/screenshots/custom_series_editor_pro.png
    :align: center

.. _custom_series_formula:

Formulas run in *Qt*'s built-in JavaScript engine (``QJSEngine``) and support standard ECMAScript. All
standard built-ins are available, including ``Math``, ``JSON``, ``Number``, ``String``, ``Array``,
``Object``, ``Date``, ``RegExp``, ``parseInt``, ``parseFloat``, ``isNaN``, and ``isFinite``.

For safety, the following identifiers are **not** available inside a formula and are rejected during
validation: ``console``, ``window``, ``document``, ``XMLHttpRequest``, ``fetch``, ``setTimeout``,
``clearTimeout``, ``setInterval``, ``clearInterval``, and ``qt``.

.. _custom_series_saving:

A successful save shows *Series saved successfully.* If validation fails, the editor reports a
specific message, for example when the series name is empty or already exists, when no
data source binding has been added, when a variable name is not a valid identifier, or when the
function body is empty.

.. _custom_series_import_export:

Importing and Exporting
=======================

You can save custom series definitions to disk and share them between sessions or machines:

* **Export Custom Series** (panel button, or **File → Export Custom Series...**) writes every defined
  series to a ``.json`` file.
* **Import Custom Series** (panel button, or **File → Import Custom Series...**) loads series
  definitions from a ``.json`` file.

See :ref:`pro_application_menu` for the corresponding menu entries.
