====================
Apache Parquet Tool
====================

Build
------
Build the Apache Parquet Tool using Visual Studio 2022.

1. Open **BruceProject.sln** in VS 2022
2. Set build options to x64 and Release
3. Build the **ParquetToolStatic** project

Debug Log
----------------
Debug log is written to **logs\ParquetTool_<number>.log** in the current directory.
The log file is created when the program starts and closed when the program ends.   


Helper Command
--------------

Show help message
^^^^^^^^^^^^^^^^^^
Show help message for ParquetToolStatic.exe.

**Command line**
::
    ParquetToolStatic.exe --help

**Console output**
::
    [20:34:21] [info] Log Start
    [20:34:21] [info] Generic options:
    --read                read parquet
    --write               write parquet
    --schema              print schema
    --csv                 write to csv
    --parquet             write to parquet
    --input arg           pathname for input
    --output arg          pathname for output
    --name arg            element name
    --index arg           element index
    --help                print usage message

Read Command
--------------

Read Parquet file
^^^^^^^^^^^^^^^^^^
Read a Parquet file and print the schema and data to the console.

**Command line**
::
    ParquetToolStatic.exe --read --input <input_file>

    Parameters:
        - input: <input_file> Full Pathname for input file. The file must be a Parquet file.

**Console output**
::
    .\ParquetToolStatic.exe --read --input "C:\BruceData\Project\Data\Parquet\CSVToParquet.parquet"

    [20:37:08] [info] Log Start
    [20:37:08] [info] Read parquet file
    [20:37:08] [info] Open File: C:\BruceData\Project\Data\Parquet\CSVToParquet.parquet
    [20:37:08] [info]
      id: int64
      name: string
      age: int64
      email: string
    ----
      id:
        [
          [
            1,
            2,
            3
          ]
        ]
      name:
        [
          [
            "Alice",
            "Bob",
            "Charlie"
          ]
        ]
      age:
        [
          [
            30,
            25,
            35
          ]
        ]
      email:
        [
          [
            "alice@example.com",
            "bob@example.com",
            "charlie@example.com"
          ]
        ]

Read Parquet schema
^^^^^^^^^^^^^^^^^^^^
Read a Parquet file and print the schema to the console.

**Command line**
::
    ParquetToolStatic.exe --read --schema --input <input_file>

    Parameters:
        - input: <input_file> Full Pathname for input file. The file must be a Parquet file.

**Console output**
::
    .\ParquetToolStatic.exe --read --input "C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.parquet" --schema

    [21:02:08] [info] Log Start
    [21:02:08] [info] Read parquet file schema
    [21:02:08] [info] Open File: C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.parquet
    [21:02:08] [info]
      VendorID: int32
      tpep_pickup_datetime: timestamp[us]
      tpep_dropoff_datetime: timestamp[us]
      passenger_count: int64
      trip_distance: double
      RatecodeID: int64
      store_and_fwd_flag: large_string
      PULocationID: int32
      DOLocationID: int32
      payment_type: int64
      fare_amount: double
      extra: double
      mta_tax: double
      tip_amount: double
      tolls_amount: double
      improvement_surcharge: double
      total_amount: double
      congestion_surcharge: double
      Airport_fee: double
      cbd_congestion_fee: double

Read Parquet file by column index
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Read a Parquet file and print the schema and data to the console by column index.

**Command line**
::
    ParquetToolStatic.exe --read --input <input_file> --index <column_index>

    Parameters:
        - input: <input_file> Full Pathname for input file. The file must be a Parquet file.
        - index: <column_index> Column index. The index starts from 0.

**Console output**
::
    .\ParquetToolStatic.exe --read --input "C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.parquet" --index 0

    [21:04:16] [info] Log Start
    [21:04:16] [info] Read parquet file with column name
    [21:04:16] [info] Open File: C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.parquet , Column Index: 0
    [21:04:16] [info]
      VendorID: int32
    ----
      VendorID:
        [
          [
            1,
            1,
            1,
            2,
            2,
            2,
            1,
            1,
            1,
            2,
            ...
            2,
            2,
            2,
            2,
            2,
            2,
            2,
            2,
            2,
            2
          ]
        ]

Read Parquet file by column name
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Read a Parquet file and print the schema and data to the console by column name.

**Command line**
::
    ParquetToolStatic.exe --read --input <input_file> --name <column_name>

    Parameters:
        - input: <input_file> Full Pathname for input file. The file must be a Parquet file.
        - name: <column_name> Column name. The name is case sensitive.

**Console output**
::
    .\ParquetToolStatic.exe --read --input "C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.parquet" --name "VendorID"

    [21:06:22] [info] Log Start
    [21:06:22] [info] Read parquet file with column name
    [21:06:22] [info] Open File: C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.parquet , Column Name: VendorID
    [21:06:22] [info]
      VendorID: int32
    ----
      VendorID:
        [
          [
            1,
            1,
            1,
            2,
            2,
            2,
            1,
            1,
            1,
            2,
            ...
            2,
            2,
            2,
            2,
            2,
            2,
            2,
            2,
            2,
            2
          ]
        ]

Convert Command
--------------

Convert CSV to Parquet
^^^^^^^^^^^^^^^^^^
Convert a CSV file to a Parquet file.

**Command line**
::
    .\ParquetToolStatic.exe --convert --toparquet --input <csv_file> --output <parquet_file>

    Parameters:
        - input: <csv_file> Full Pathname for input file. The file must be a CSV file.
        - output: <parquet_file> Full Pathname for output file. The file must be a Parquet file.

**Console output**
::
    .\ParquetToolStatic.exe --convert --toparquet --input "C:\BruceData\Project\Data\Parquet\userinfo.csv" --output "C:\BruceData\Project\Data\Parquet\userinfoParquet.parquet"

    [21:20:09] [info] Log Start
    [21:20:09] [info] Convert CSV to Parquet
    [21:20:09] [info] CSV File: C:\BruceData\Project\Data\Parquet\userinfo.csv , Ouptut Parquet: C:\BruceData\Project\Data\Parquet\userinfoParquet.parquet
    [21:20:09] [info] CSV successfully converted to Parquet.

Convert Parquet to CSV
^^^^^^^^^^^^^^^^^^
Convert a Parquet file to a CSV file.

**Command line**
::
    .\ParquetToolStatic.exe --convert --tocsv --input <csv_file> --output <parquet_file>

    Parameters:
        - input: <csv_file> Full Pathname for input file. The file must be a CSV file.
        - output: <parquet_file> Full Pathname for output file. The file must be a Parquet file.

**Console output**
::
    .\ParquetToolStatic.exe --convert --tocsv --input "C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.parquet" --output "C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.csv"
    
    [21:32:11] [info] Log Start
    [21:32:11] [info] Convert Parquet to CSV
    [21:32:11] [info] Input Parquet: C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.parquet , Ouptut CSV: C:\BruceData\Project\Data\Parquet\yellow_tripdata_2025-01.csv
    [21:32:16] [info] Parquet successfully converted to CSV.