.. include:: ../../exports/alias.include
.. include:: ../../exports/roles.include

.. _dynamic_series:

##############
Real-Time Data
##############

A **Dynamic** or **Real-Time** series displays the data the monitor is receiving at the current moment.
It is a pseudo-real-time display of a running DDS network:
instead of showing the network activity at the exact moment it happens, it shows a periodic update of the
last seconds of the network.

All displayed data is delayed by 5 seconds so that it accurately represents all the data reported by the network.
Fast DDS does not report data instantly, so without this delay the data used to update the
chart might be incomplete.

.. _create_dynamic_series:

Create Dynamic Series Chartbox
==============================
To create a new dynamic Chartbox in the central panel, use the :ref:`display_dynamic_data_button` button in
the :ref:`edit_menu` or in :ref:`shortcuts_bar_layout`. A dynamic Chartbox can only contain series that refer to the
same *DataKind*. A dialog opens to set some parameters that all the
series created in this new Chartbox share.

Data Kind
---------
See the common parameters explanation in :ref:`data_kind_parameter`.

.. _time_window_parameter:

Time window
-----------
The default size and value of the X axis.
When the chart starts, the rightmost point of the X axis is the current moment by default,
and the leftmost point is the current time minus the `Time window`.

.. _update_period_parameter:

Update period
-------------
The time between two updates of the Chartbox series.
Every `Update period` seconds, each series in the Chartbox is updated with the new data collected.

.. _chart_panel_maximum_data_points:

Advanced: Maximum data points
-----------------------------
The default maximum number of data points for all series in this Chartbox.
See the :ref:`series_maximum_data_points` section for more information.

Click `OK` to create a new Chartbox for the chosen *DataKind*, which will hold the dynamic series.

Create Dynamic Series Dialog
============================
The :ref:`create_new_series_layout` creates a new data series in a Chartbox.
Its fields configure the data that will be displayed.
When all the data is set in the :ref:`create_dynamic_series`, press *Add* to create the series and keep
the same parameters to create another series.
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

Statistic kind
---------------
This parameter works as explained in :ref:`statistics_kind_parameter`, except for the *RAW DATA* kind.
With *RAW DATA*, the chart displays all the data available in the time interval given by
:ref:`update_period_parameter`, with no accumulation.

.. note::

    Data is never displayed at the moment it arrives.
    It always appears after each :ref:`update_period_parameter`.

.. _series_maximum_data_points:

Advanced: Maximum data points
-----------------------------
Sets a limit on the number of data points displayed for a specific data series.
Data points are added to the series continuously, which can exhaust memory and cause efficiency problems.
To prevent this, the parameter limits the number of data points by removing older data as new points are
added. Use value ``0`` for unlimited series.

You can change this value per series at any time in the series menu.


Advanced: Cumulative data
-------------------------

Sets the time interval over which the statistic selected in "Statistic kind" is
calculated.
If you set a time interval for accumulated statistics, the statistic is applied
to all the data the monitor collected in that time interval.
This makes the update interval of the chart independent of the time interval used to calculate the statistic.

As an example, consider monitoring the latency of a publisher and a subscriber in the Shapes Demo
application launched with statistics enabled (this `video tutorial <https://www.youtube.com/watch?v=6ZEb0a7Ei4Y>`_
shows a detailed example of DDS Monitor monitoring a Shapes Demo application).
First, create a chart to monitor the application latency with a time window of 5 minutes and an update period of
5 seconds.
Then open the dialog for creating series in the chart.
Select your host as source and target entities, and the monitor automatically detects the DataWriters and
DataReaders running on your machine.
Select the mean as the statistic to apply.
Finally, create three series with three different types of accumulation:

- **No accumulation**.
  The average latency between publisher and subscriber is calculated over the last update period (5 seconds in
  this case).
- **With accumulation from the first available data point**.
  The average latency between publisher and subscriber is calculated from the time the monitor has the first
  available data until the current time.
  The current time moves forward every update period, adding new points to the calculated statistic.
- **With accumulation by setting a time interval**.
  The average latency between publisher and subscriber is calculated from the current time minus the cumulative time
  interval set until the current time.

The image below shows the three series. The series with a longer accumulation period tends
to have a steady latency value and is less affected by strong but brief latency variations.
The series that uses only the data of the last 5 seconds varies much more, because it has
fewer data points to calculate the statistic.

.. thumbnail:: /rst/figures/screenshots/Cumulative_chart.png
    :align: center

Quick explanation of the data displayed
---------------------------------------
First, the application creates an empty chart where the X axis covers the time from the current moment
minus the :ref:`time_window_parameter` size up to the current moment.
This window moves continuously to always show the current time.
You can pause this X axis movement at any moment to move and resize the chart,
and new data will still appear.

Every :ref:`update_period_parameter`, new data appears on the right side of the chart.
This new data is the cumulative value of the data stored during that period.

.. warning::

    Some of the queried data may not exist in the database for many reasons, e.g. the entity did not report anything
    in the time range of the query.
    In these cases, no point appears for that :ref:`update_period_parameter`, and the line in the chart
    connects to the next interval with data.
