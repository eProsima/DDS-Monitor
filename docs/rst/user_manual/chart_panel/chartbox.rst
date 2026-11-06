.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _chartbox:

########
Chartbox
########

A :ref:`chartbox_layout` is a window in the :ref:`main_panel_layout` that displays entity data with different
configurations.

To start a new Chartbox, press :ref:`display_historic_data_button` or :ref:`display_dynamic_data_button`
in :ref:`edit_menu` or in :ref:`shortcuts_bar`.
Each Chartbox appears in the central panel with the title of the *DataKind* it refers to,
and displays the data series that the user creates.
To create a new series, see :ref:`create_historic_series` or :ref:`create_dynamic_series`.

.. _chartbox_chart_menu:

Chart Menu
----------
The top bar of each Chartbox has a *Chart* menu tab with the following buttons.

.. _chartbox_chart_menu_reset_zoom:

Reset zoom
^^^^^^^^^^
Reset the zoom of the Chartbox to the standard one, which fits all the data currently displayed.
You can also click the |resize| button in the same chart box.

.. _chartbox_chart_menu_set_axes:

Set axes
^^^^^^^^
Opens a dialog to set the axes of the chart.
Changing the X-axis (time axis) is disabled by default, so the chart keeps the time values it currently displays.
This lets dynamic charts keep updating the X-axis while the Y-axis stays fixed.
You can also open this dialog with the |editaxis| button in the same chart box.

.. figure:: /rst/figures/screenshots/set_axes.png
    :align: center

To return to the original time axis and let the Y-axis update dynamically again, click the
:ref:`chartbox_chart_menu_reset_zoom` button to the right of the chart.

Clear chart
^^^^^^^^^^^
Remove every data configuration displayed in the Chartbox.

Rename chart box
^^^^^^^^^^^^^^^^
Change the name of the chart box.

Close chart box
^^^^^^^^^^^^^^^
Remove the Chartbox and every configuration in it.
You can also press the ``x`` button at the top of the chart.

Export to CSV
^^^^^^^^^^^^^
Export the data of all series in the chart box to a CSV file.
See :ref:`export_data` for the format of the generated CSV file.

Chart Controls
^^^^^^^^^^^^^^
Opens the *Chart Interactive Controls* dialog, which lists the available mouse and keyboard interactions
(see :ref:`chartbox_chart_interaction`). Its *Extra Help...* button opens this documentation.
You can also open this dialog with the |help| button in the chart header.


.. figure:: /rst/figures/screenshots/Chartbox_info.png
    :align: center


Series Menu
-----------
The top bar of each Chartbox has a *Series* menu tab with these buttons.

Add series
^^^^^^^^^^
Add a new series to this Chartbox.
This opens a new :ref:`create_historic_series` or :ref:`create_dynamic_series`.

Hide all series
^^^^^^^^^^^^^^^
Hide all series in this Chartbox.

Display all series
^^^^^^^^^^^^^^^^^^
Show all series in this Chartbox.

.. _chartbox_chart_interaction:

Chart Interaction
-----------------
You can resize and move the view of the Chartbox and the data in it.

Point description
^^^^^^^^^^^^^^^^^
Click any point of a displayed series to open an info box with the ``x`` and ``y``
label values of the data point.

Moving the view
^^^^^^^^^^^^^^^
Press and hold the ``Ctrl`` key and left click on a point of the Chartbox.
Move the mouse to scroll over the data.

Zoom in/out
^^^^^^^^^^^
Press and hold the ``Ctrl`` key and scroll up to zoom in to the center of the Chartbox.
Press and hold the ``Ctrl`` key and scroll down to zoom out from the center of the Chartbox.

Zoom in over an area
^^^^^^^^^^^^^^^^^^^^
Press and hold the ``Shift`` key, then left click and drag to select an area of the Chartbox to zoom in on.

.. note::

    In dynamic Chartboxes, these interactions are only available while the real-time update is paused.

.. _chartbox_series_configuration:

Series Configuration
--------------------
Right click the name of a series in the *Legend* to open a dialog with the available configurations for
that series.

Remove series
^^^^^^^^^^^^^
Remove this series.

Rename series
^^^^^^^^^^^^^
Change the name of this series.

Change color
^^^^^^^^^^^^
Opens a dialog to choose a new color for the series and its points.
You can also left click the color of the series in the *Legend*.

Hide/Show series
^^^^^^^^^^^^^^^^
Hide the series if it is displayed, or show it if it is hidden.
You can also left click the name of the series in the *Legend*.

Export to CSV
^^^^^^^^^^^^^
Export the series data to a CSV file.
See :ref:`export_data` for the format of the generated CSV file.

Set max data points
^^^^^^^^^^^^^^^^^^^
Set a limit on the number of data points displayed for this data series.

Dynamic Chartbox
----------------
A Chartbox that holds dynamic series has some extra functionality.
You can stop it at any time, or play it again if it is stopped.
Stopping it stops the axis from updating, so you can zoom and move along the chart.
The data in the Chartbox keeps updating at the same time interval whether it is playing or stopped.

To pause the real-time update of the time axis, click the Real Time menu or the |play|/|pause| button on
the right side of the chart, or set the axes to a specific value with the :ref:`chartbox_chart_menu_set_axes` button.
