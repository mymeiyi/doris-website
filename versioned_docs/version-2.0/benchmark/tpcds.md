---
{
    "title": "TPC-DS Benchmark",
    "language": "zh-CN"
}
---

<!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
-->

# TPC-DS Benchmark

TPC-DS (Transaction Processing Performance Council Decision Support Benchmark) is a benchmark test that focuses on decision support and aims to evaluate the performance of data warehousing and analytics systems. It was developed by the Transaction Processing Performance Council (TPC) organization to compare the capabilities of different systems in handling complex queries and large-scale data analysis.

The design goal of TPC-DS is to simulate complex decision support workloads in the real world. It tests the performance of systems through a series of complex queries and data operations, including joins, aggregations, sorting, filtering, subqueries, and more. These query patterns cover various scenarios ranging from simple to complex, such as report generation, data mining, and OLAP (Online Analytical Processing).

This document mainly introduces the performance of Doris on the TPC-DS 1000G test set.

On 99 queries on the TPC-DS standard test data set, we conducted a comparison test based on Apache Doris 2.1.1-rc03 and Apache Doris 2.0.6 versions.


![TPCDS_1000G](/images/tpcds_2.1.png)

## 1. Hardware Environment

| Hardware            | Configuration Instructions                |
|---------------------|-------------------------------------------|
| Number of mMachines | 4 Tencent Cloud Virtual Machine（1FE，3BEs） |
| CPU                 | AMD EPYC™ Milan(2.55GHz/3.5GHz)  48C      |
| Memory              | 192G                                      |
| Network             | 21Gbps                                    |
| Disk                | ESSD Cloud Hard Disk                      |

## 2. Software Environment

- Doris Deployed 3BEs and 1FE
- Kernel Version: Linux version 5.4.0-96-generic (buildd@lgw01-amd64-051)
- OS version: Ubuntu 20.04 LTS (Focal Fossa)
- Doris software version: Apache Doris 2.1.1-rc03, Apache Doris 2.0.6.
- JDK: openjdk version "1.8.0_131"

## 3. Test Data Volume

The TPC-DS 1000G data generated by the simulation of the entire test are respectively imported into Apache Doris 2.1.1-rc03 and Apache Doris 2.0.6 for testing. The following is the relevant description and data volume of the table.

| TPC-DS Table Name      | Rows          |
|------------------------|---------------|
| customer_demographics  | 1,920,800     |
| reason                 | 65            |
| warehouse              | 20            |
| date_dim               | 73,049        |
| catalog_sales          | 1,439,980,416 |
| call_center            | 42            |
| inventory              | 783,000,000   |
| catalog_returns        | 143,996,756   |
| household_demographics | 7,200         |
| customer_address       | 6,000,000     |
| income_band            | 20            |
| catalog_page           | 30,000        |
| item                   | 300,000       |
| web_returns            | 71,997,522    |
| web_site               | 54            |
| promotion              | 1,500         |
| web_sales              | 720,000,376   |
| store                  | 1,002         |
| web_page               | 3,000         |
| time_dim               | 86,400        |
| store_returns          | 287,999,764   |
| store_sales            | 2,879,987,999 |
| ship_mode              | 20            |
| customer               | 12,000,000    |

## 4. Test SQL

TPC-DS 99 test query statements : [TPC-DS-Query-SQL](https://github.com/apache/doris/tree/master/tools/tpcds-tools/queries/sf1000)

## 5. Test Results

Here we use Apache Doris 2.1.1-rc03 and Apache Doris 2.0.6 for comparative testing. In the test, we use Query Time(ms) as the main performance indicator. The test results are as follows:

| Query     | Apache Doris 2.1.1-rc03  (ms) | Apache Doris 2.0.6  (ms) |
|-----------|-------------------------------|--------------------------|
| query1    | 729                           | 914                      |
| query2    | 5120                          | 4669                     |
| query3    | 286                           | 285                      |
| query4    | 11633                         | 35148                    |
| query5    | 641                           | 22979                    |
| query6    | 267                           | 1351                     |
| query7    | 468                           | 517                      |
| query8    | 263                           | 591                      |
| query9    | 4444                          | 5430                     |
| query10   | 418                           | 3341                     |
| query11   | 7246                          | 23300                    |
| query12   | 115                           | 105                      |
| query13   | 661                           | 1719                     |
| query14   | 13955                         | 33254                    |
| query15   | 474                           | 1414                     |
| query16   | 366                           | 402                      |
| query17   | 1097                          | 2371                     |
| query18   | 581                           | 760                      |
| query19   | 283                           | 308                      |
| query20   | 137                           | 117                      |
| query21   | 110                           | 94                       |
| query22   | 1996                          | 2481                     |
| query23   | 44826                         | 77381                    |
| query24   | 9873                          | 23910                    |
| query25   | 666                           | 1021                     |
| query26   | 221                           | 213                      |
| query27   | 490                           | 544                      |
| query28   | 4089                          | 4593                     |
| query29   | 768                           | 1024                     |
| query30   | 313                           | 682                      |
| query31   | 1847                          | 2252                     |
| query32   | 71                            | 68                       |
| query33   | 460                           | 539                      |
| query34   | 629                           | 638                      |
| query35   | 1660                          | 10505                    |
| query36   | 412                           | 441                      |
| query37   | 94                            | 86                       |
| query38   | 8804                          | 8379                     |
| query39   | 606                           | 898                      |
| query40   | 164                           | 190                      |
| query41   | 55                            | 30                       |
| query42   | 115                           | 113                      |
| query43   | 804                           | 1332                     |
| query44   | 1509                          | 1520                     |
| query45   | 1678                          | 1306                     |
| query46   | 1196                          | 2167                     |
| query47   | 2812                          | 3859                     |
| query48   | 559                           | 1419                     |
| query49   | 646                           | 725                      |
| query50   | 757                           | 1299                     |
| query51   | 6380                          | 4954                     |
| query52   | 128                           | 123                      |
| query53   | 396                           | 391                      |
| query54   | 388                           | 8212                     |
| query55   | 124                           | 124                      |
| query56   | 360                           | 434                      |
| query57   | 1811                          | 2494                     |
| query58   | 304                           | 666                      |
| query59   | 5758                          | 7432                     |
| query60   | 474                           | 481                      |
| query61   | 486                           | 536                      |
| query62   | 647                           | 1082                     |
| query63   | 358                           | 303                      |
| query64   | 3250                          | 4968                     |
| query65   | 5410                          | 5971                     |
| query66   | 484                           | 603                      |
| query67   | 26347                         | 34052                    |
| query68   | 1422                          | 1428                     |
| query69   | 654                           | 808                      |
| query70   | 2285                          | 4462                     |
| query71   | 650                           | 1006                     |
| query72   | 4324                          | 4717                     |
| query73   | 500                           | 558                      |
| query74   | 6678                          | 14127                    |
| query75   | 3734                          | 6312                     |
| query76   | 1835                          | 1870                     |
| query77   | 382                           | 496                      |
| query78   | 19923                         | 23091                    |
| query79   | 3061                          | 4090                     |
| query80   | 851                           | 1559                     |
| query81   | 565                           | 960                      |
| query82   | 242                           | 221                      |
| query83   | 254                           | 415                      |
| query84   | 203                           | 131                      |
| query85   | 364                           | 444                      |
| query86   | 651                           | 931                      |
| query87   | 8972                          | 8554                     |
| query88   | 4095                          | 5202                     |
| query89   | 508                           | 480                      |
| query90   | 233                           | 322                      |
| query91   | 174                           | 159                      |
| query92   | 62                            | 59                       |
| query93   | 1601                          | 1618                     |
| query94   | 297                           | 297                      |
| query95   | 1240                          | 27354                    |
| query96   | 508                           | 847                      |
| query97   | 5449                          | 11528                    |
| query98   | 382                           | 287                      |
| query99   | 1410                          | 2147                     |
| **Total** | **264028**                    | **487990**               |

## 6. Environmental Preparation

Please refer to the [official document](../install/cluster-deployment/standard-deployment.md) to install and deploy Doris to obtain a normal running Doris cluster (at least 1 FE 1 BE, 1 FE 3 BE is recommended).

## 7. Data Preparation

### 7.1 Download and Install TPC-DS Data Generation Tool

Execute the following script to download and compile the [tpcds-tools](https://github.com/apache/doris/tree/master/tools/tpcds-tools) tool.

```shell
sh bin/build-tpcds-dbgen.sh
```

### 7.2 Generating the TPC-DS Test Set

Execute the following script to generate the TPC-H dataset:

```shell
sh bin/gen-tpcds-data.sh -s 1000
```

> Note 1: Check the script help via `sh gen-tpcds-data.sh -h`.
>
> Note 2: The data will be generated under the `tpcds-data/` directory with the suffix `.dat`. The total file size is about 1000GB and may need a few minutes to an hour to generate.
>
> Note 3: A standard test data set of 100G is generated by default.

### 7.3 Create Table

#### 7.3.1 Prepare the `doris-cluster.conf` File

Before import the script, you need to write the FE’s ip port and other information in the `doris-cluster.conf` file.

The file is located under `${DORIS_HOME}/tools/tpcds-tools/conf/` .

The content of the file includes FE's ip, HTTP port, user name, password and the DB name of the data to be imported:

```shell
# Any of FE host
export FE_HOST='127.0.0.1'
# http_port in fe.conf
export FE_HTTP_PORT=8030
# query_port in fe.conf
export FE_QUERY_PORT=9030
# Doris username
export USER='root'
# Doris password
export PASSWORD=''
# The database where TPC-H tables located
export DB='tpcds'
```

#### Execute the Following Script to Generate and Create TPC-H Table

```shell
sh bin/create-tpcds-tables.sh -s 1000
```
Or copy the table creation statement in [create-tpcds-tables.sql](https://github.com/apache/doris/blob/master/tools/tpcds-tools/ddl/create-tpcds-tables-sf1000.sql) and excute it in Doris.


### 7.4 Import Data

Please perform data import with the following command:

```shell
sh bin/load-tpcds-data.sh
```


### 7.5 Query Test

#### 7.5.1 Executing Query Scripts

Execute the above test SQL or execute the following command

```
sh bin/run-tpcds-queries.sh -s 1000
```

#### 7.5.2 Single SQL Execution

You can also retrieve the latest SQL from the code repository. The address for the latest test query statements of [TPC-DS](https://github.com/apache/doris/tree/master/tools/tpcds-tools/queries/sf1000).