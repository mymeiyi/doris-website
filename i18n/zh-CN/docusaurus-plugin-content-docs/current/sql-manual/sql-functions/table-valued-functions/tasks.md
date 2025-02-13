---
{
    "title": "TASKS",
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

## `tasks`

### Name

tasks

## 描述

表函数，生成 tasks 临时表，可以查看当前 doris 集群中的 job 产生的 tasks 信息。

该函数用于 from 子句中。

该函数自 2.1.0 版本支持。

## 语法

`tasks("type"="insert");`
**参数说明**

| 参数名  | 说明     | 类型     | 是否必填 |
|:-----|:-------|:-------|:-----|
| type | 作业类型   | string | 是    |

type 支持的类型：

- insert：insert into 类型的任务。
- mv: mv 类型的任务

##### Insert tasks
`tasks("type"="insert");`表结构：
```
mysql> desc  function tasks("type"="insert");;
+---------------+------+------+-------+---------+-------+
| Field         | Type | Null | Key   | Default | Extra |
+---------------+------+------+-------+---------+-------+
| TaskId        | TEXT | No   | false | NULL    | NONE  |
| JobId         | TEXT | No   | false | NULL    | NONE  |
| JobName       | TEXT | No   | false | NULL    | NONE  |
| Label         | TEXT | No   | false | NULL    | NONE  |
| Status        | TEXT | No   | false | NULL    | NONE  |
| ErrorMsg      | TEXT | No   | false | NULL    | NONE  |
| CreateTime    | TEXT | No   | false | NULL    | NONE  |
| FinishTime    | TEXT | No   | false | NULL    | NONE  |
| TrackingUrl   | TEXT | No   | false | NULL    | NONE  |
| LoadStatistic | TEXT | No   | false | NULL    | NONE  |
| User          | TEXT | No   | false | NULL    | NONE  |
+---------------+------+------+-------+---------+-------+
11 row in set (0.01 sec)
```
- TaskId：task id
- JobId：job id
- JobName：job 名称
- Label：label
- Status：task 状态
- ErrorMsg：task 失败信息
- CreateTime：task 创建时间
- FinishTime：task 结束时间
- TrackingUrl：task tracking url
- LoadStatistic：task 统计信息
- User：执行用户
##### MV tasks
```sql
mysql> desc function tasks("type"="mv");
+-----------------------+------+------+-------+---------+-------+
| Field                 | Type | Null | Key   | Default | Extra |
+-----------------------+------+------+-------+---------+-------+
| TaskId                | TEXT | No   | false | NULL    | NONE  |
| JobId                 | TEXT | No   | false | NULL    | NONE  |
| JobName               | TEXT | No   | false | NULL    | NONE  |
| MvId                  | TEXT | No   | false | NULL    | NONE  |
| MvName                | TEXT | No   | false | NULL    | NONE  |
| MvDatabaseId          | TEXT | No   | false | NULL    | NONE  |
| MvDatabaseName        | TEXT | No   | false | NULL    | NONE  |
| Status                | TEXT | No   | false | NULL    | NONE  |
| ErrorMsg              | TEXT | No   | false | NULL    | NONE  |
| CreateTime            | TEXT | No   | false | NULL    | NONE  |
| StartTime             | TEXT | No   | false | NULL    | NONE  |
| FinishTime            | TEXT | No   | false | NULL    | NONE  |
| DurationMs            | TEXT | No   | false | NULL    | NONE  |
| TaskContext           | TEXT | No   | false | NULL    | NONE  |
| RefreshMode           | TEXT | No   | false | NULL    | NONE  |
| NeedRefreshPartitions | TEXT | No   | false | NULL    | NONE  |
| CompletedPartitions   | TEXT | No   | false | NULL    | NONE  |
| Progress              | TEXT | No   | false | NULL    | NONE  |
+-----------------------+------+------+-------+---------+-------+
18 rows in set (0.00 sec)
```
* TaskId：task id
* JobId：job id
* JobName：job 名称
* MvId：物化视图 id
* MvName：物化视图名称
* MvDatabaseId：物化视图所属 db id
* MvDatabaseName：物化视图所属 db 名称
* Status：task 状态
* ErrorMsg：task 失败信息
* CreateTime：task 创建时间
* StartTime：task 开始运行时间
* FinishTime：task 结束运行时间
* DurationMs：task 运行时间
* TaskContext：task 运行参数
* RefreshMode：刷新模式
* NeedRefreshPartitions：本次 task 需要刷新的分区信息
* CompletedPartitions：本次 task 刷新完成的分区信息
* Progress：task 运行进度

## 举例
#### Insert Tasks
```
mysql>  select * from tasks("type"="insert") limit 1 \G
*************************** 1. row ***************************
       TaskId: 667704038678903
        JobId: 10069
        Label: 10069_667704038678903
       Status: FINISHED
      EtlInfo: \N
     TaskInfo: cluster:N/A; timeout(s):14400; max_filter_ratio:0.0; priority:NORMAL
     ErrorMsg: \N
 CreateTimeMs: 2023-12-08 16:46:57
 FinishTimeMs: 2023-12-08 16:46:57
  TrackingUrl: 
LoadStatistic: {"Unfinished backends":{},"ScannedRows":0,"TaskNumber":0,"LoadBytes":0,"All backends":{},"FileNumber":0,"FileSize":0}
         User: root
1 row in set (0.05 sec)

```
#### MV Tasks
1. 查看所有物化视图的 task

```sql
mysql> select * from tasks("type"="mv");
```

2. 查看 jobName 为`inner_mtmv_75043`的所有 task

```sql
mysql> select * from tasks("type"="mv") where JobName="inner_mtmv_75043";
```

### keywords

     tasks, job, insert, mv, materilized view
