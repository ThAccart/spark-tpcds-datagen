[![Build Status](https://travis-ci.org/maropu/spark-tpcds-datagen.svg?branch=master)](https://travis-ci.org/maropu/spark-tpcds-datagen)

This is the TPCDS data generator for Apache Spark, which is split off from [spark-sql-perf](https://github.com/databricks/spark-sql-perf)
and includes pre-built [tpcds-kit](https://github.com/davies/tpcds-kit) for x86_64 on Mac/Linux platforms.
To check performance regression, TPCDS benchmark results for Spark master are daily stored
in [reports](https://github.com/maropu/spark-tpcds-datagen/blob/master/reports/tpcds-avg-results.csv) and
[charts](https://docs.google.com/spreadsheets/d/1V8xoKR9ElU-rOXMH84gb5BbLEw0XAPTJY8c8aZeIqus/edit#gid=2074944948) in Google Spreadsheet
are generated per the update.

## How to generate TPCDS data

First of all, you need to set up Spark:

    $ git clone https://github.com/apache/spark.git

    $ cd spark && ./build/mvn clean package -DskipTests

    $ export SPARK_HOME=`pwd`

Then, you can generate TPCDS test data in `/tmp`:

    $ ./bin/dsdgen /tmp

## How to run TPC-DS queries in Spark

You can run TPC-DS quries by using test data in `/tmp`:

    $ ./bin/spark-submit --class org.apache.spark.sql.execution.benchmark.TPCDSQueryBenchmark sql/core/target/spark-sql_<scala.version>-<spark.version>-tests.jar /tmp

## Options for the generator

    $ ./bin/dsdgen --help

    Usage: ./bin/dsdgen [options] [output dir]
    ...
    dsdgen options:
      --conf spark.sql.dsdgen.scaleFactor=NUM                    Scale factor (Default: 1).
      --conf spark.sql.dsdgen.format=STR                         Output format (Default: parquet).
      --conf spark.sql.dsdgen.overwrite=BOOL                     Wheter it overwrites existing data (Default: false).
      --conf spark.sql.dsdgen.partitionTables=BOOL               Wheter it partitions output data (Default: false).
      --conf spark.sql.dsdgen.useDoubleForDecimal=BOOL           Wheter it prefers double types (Default: false).
      --conf spark.sql.dsdgen.clusterByPartitionColumns=BOOL     Wheter it cluster output data by partition columns (Default: false).
      --conf spark.sql.dsdgen.filterOutNullPartitionValues=BOOL  Wheter it filters out NULL partitions (Default: false).
      --conf spark.sql.dsdgen.tableFilter=STR                    Filters a specific table.
      --conf spark.sql.dsdgen.numPartitions=NUM                  # of partitions (Default: 100).

## Bug reports

If you hit some bugs and requests, please leave some comments on [Issues](https://github.com/maropu/spark-sql-server/issues)
or Twitter([@maropu](http://twitter.com/#!/maropu)).

