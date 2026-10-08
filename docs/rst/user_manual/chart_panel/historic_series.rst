.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _historic_series:

#############
Historic Data
#############

.. _create_historic_series:

Create Historic Series Chartbox
===============================

To create a new static Chartbox in the central panel, use the :ref:`display_historic_data_button` button
in the :ref:`edit_menu` or in :ref:`shortcuts_bar_layout`. A static Chartbox can only contain series that refer to
the same *DataKind*.

Data Kind
---------
Select the *DataKind* to represent. See the common parameters explanation in :ref:`data_kind_parameter`.
Click `OK` to create a new Chartbox for the chosen *DataKind*, which will hold historic series.

.. _create_historic_series_dialog:

Create Historic Series Dialog
=============================
The :ref:`create_new_series_layout` creates a new data series in a Chartbox.
Its fields configure the data that will be displayed.
When all the data is set in the :ref:`create_historic_series_dialog`, press *Add* to create the series and
keep the same parameters to create another series.
Press *Add & Close* to create the series and close the dialog.
Press *Close* to close the window without creating any series.

Series label
------------
See the common parameters explanation in :ref:`series_label_parameter`.

Source Entity Id
----------------
See the common parameters explanation in :ref:`source_entity_id_parameter`.

Target Entity Id
----------------
See the common parameters explanation in :ref:`target_entity_id_parameter`.

.. _number_of_bins_parameter:

Number of bins
--------------
Number of *DataPoints* displayed for this *Chart Series*.
Each entity collects data as individual points, without a regular time interval or pattern.
To make the data easier to read, the time interval is split into fractions, and the points inside each
fraction are merged into a single point with the *cumulative function* (see  :ref:`statistics_kind_parameter`).
The *Number of bins* sets how many fractions the time interval is split into, and so how many points
the chart displays.
To see all the individual data points without accumulating them, set the *Number of bins* to 0.

.. note::

    When selecting *RAW DATA* as the *Statistic kind*, each bin will show the first data value received after
    the previous data point.

.. warning::

    Some of the queried data may not exist.
    In these cases the point is not plotted, and the number of points in the
    series does not match the number of bins.

.. _start_time_parameter:

Start time
----------
The lower time limit for the displayed data points.
Data that refers to a time before this value is not displayed.
*Default initial timestamp* is the time when the monitor was initialized.

.. _end_time_parameter:

End time
--------
The upper time limit for the displayed data points.
Data that refers to a time after this value is not displayed.
*Now* means the current time.
*Now* is not the maximum value you can set, but a time later than *Now* shows no data points
in the later time frames.

Statistic kind
---------------
See the common parameters explanation in :ref:`statistics_kind_parameter`.

Quick explanation of the data displayed
---------------------------------------
First, the application creates a complete list of data points by merging the data of all entities referred
to in this query
(see the example in :ref:`source_entity_id_parameter`).

The chart is made of a number of frames or bins, set by the :ref:`number_of_bins_parameter`
variable, from the :ref:`start_time_parameter` value to the :ref:`end_time_parameter` value.
Each frame can contain none, one or several data points.
If a frame has no data points, its value is ``0`` or it is not displayed in the chart.
If a frame has data points, the chart displays only one point for it.
This point is calculated by accumulating all the points inside the frame with the *cumulative function*
set in :ref:`statistics_kind_parameter`.

If the *Number of bins* is set to 0, there is no accumulation or time frame, so the chart displays
all the data points for this configuration, each at its own time value.

.. warning::

    Some of the queried data may not exist in the database for many reasons, e.g. the entity did not exist in
    the time range of the query, the entity does not report such data, or some data is reported
    with a lower frequency than the one requested.
    In these cases the line in the chart is not connected, and the points where no data is retrieved
    are not shown.
