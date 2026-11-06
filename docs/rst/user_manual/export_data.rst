.. include:: ../exports/alias.include
.. include:: ../exports/roles.include

.. _export_data:

###########
Export data
###########

*DDS Monitor* can export the data generated in each monitoring session.

Export charts in a CSV file
===========================

The monitor can export to a CSV file all the data that has been or is being shown in
each *Chartbox*, for both historical and real-time charts.

There are three options:

* Export the data of a single series.
  Use the series menu, as explained in section :ref:`chartbox_series_configuration`.
* Export the data of all the series belonging to a *Chartbox*.
  Use the *Chart* menu of the *Chartbox*, explained in section
  :ref:`chartbox_chart_menu`.
* Export all the data of all the series of all the *Chartboxes*.
  Use the application *File* menu, as explained in section :ref:`application_menu_file`.

Format of the CSV file
----------------------

The CSV file with the exported data has this format:

.. list-table::
    :header-rows: 4

    *   -
        - <DataKind>
    *   -
        - <Chart box name>
    *   - ms
        - <DataKind units>
    *   - UnixTime
        - <Series name>
    *   - <unix_time>
        - <data_value>

Export database in a JSON file
==============================

The monitor can dump the data from the database to a JSON file, with two options:

* Dump.
  Explained in section :ref:`dump_button`.
* Dump and clear.
  Explained in section :ref:`dump_clear_button`.

Format of the JSON file
-----------------------

The JSON file with the exported data has this format:

.. code-block:: json

    {
        "datareaders":{},
        "datawriters":{},
        "domains": {
            "0": {
                "alias":"0",
                "alive":true,
                "discovery_source": "discovery",
                "domain_id":0,
                "metatraffic":false,
                "name":"0",
                "participants":[],
                "status":0,
                "topics":[]
            }
        },
        "hosts":{},
        "locators":{},
        "participants":{},
        "processes":{},
        "topics":{},
        "users":{},
        "version":"0.0"
    }
