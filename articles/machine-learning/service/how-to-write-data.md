---
title: 使用 Azure 机器学习数据准备 SDK 写入数据 - Python
description: 了解如何使用 Azure 机器学习数据准备 SDK 写入数据。 可在数据流中的任何位置写出数据，也可以将数据写入我们支持的任何位置（本地文件系统、Azure Blob 存储和 Azure Data Lake Storage）的文件中。
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.author: cforbe
author: cforbe
manager: cgronlun
ms.reviewer: jmartens
ms.date: 09/24/2018
ms.openlocfilehash: 81344d388fbba0db034b8adb06adab6797ec2ce1
ms.sourcegitcommit: 51a1476c85ca518a6d8b4cc35aed7a76b33e130f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2018
ms.locfileid: "47166735"
---
# <a name="write-data-using-the-azure-machine-learning-data-prep-sdk"></a>使用 Azure 机器学习数据准备 SDK 写入数据
可在数据流中的任何位置写出数据。 系统将这些写入操作视为步骤添加到生成的数据流中，并在数据流每次运行时运行它们。 数据写入多个分区文件以实现并行写入。

由于对管道中有多少写步骤没有限制，因此你可以轻松添加更多写步骤来获取中间结果以用于故障排除或用于其他管道。 

每次运行写步骤时，都会完全拉取数据流中的数据。 例如，具有三个写步骤的数据流将读取并处理数据集中的每个记录三次。

## <a name="supported-data-types-and-location"></a>支持的数据类型和位置

支持以下文件格式
-   带分隔符的文件（CSV、TSV 等）
-   Parquet 文件

使用 [Azure 机器学习数据准备 python SDK](https://aka.ms/data-prep-sdk)，可以将数据写入到：
+ 本地文件系统
+ Azure Blob 存储
+ Azure Data Lake 存储

## <a name="spark-considerations"></a>Spark 注意事项
在 Spark 中运行数据流时，必须写入空文件夹。 尝试运行向现有文件夹进行写入的操作将会失败。 确保目标文件夹为空，或为每次运行使用不同的目标位置，否则写入将失败。

## <a name="monitoring-write-operations"></a>监视写入操作
为方便你进行监视，在写入完成后，会生成一个名为 SUCCESS 的哨兵文件。 该文件可帮助你确定中间写入的完成时间，而无需等待整个管道的完成。

## <a name="example-write-code"></a>示例写入代码

对于此示例，首先将数据加载到数据流中。 我们将通过不同格式重复使用此数据。

```python
import azureml.dataprep as dprep
t = dprep.smart_read_file('./data/fixed_width_file.txt')
t = t.to_number('Column3')
t.head(10)
```   

示例输出：
|   |  Column1 |    Column2 | Column3 | Column4  |Column5   | Column6 | Column7 | Column8 | Column9 |
| -------- |  -------- | -------- | -------- |  -------- |  -------- |  -------- |  -------- |  -------- |  -------- |
| 0 |   10000.0 |   99999.0 |   None|       NO|     NO  |   ENRS    |NaN    |   NaN |   NaN|    
|   1|      10003.0 |   99999.0 |   None|       NO|     NO  |   ENSO|       NaN|        NaN |NaN|   
|   2|  10010.0|    99999.0|    None|   NO| JN| ENJA|   70933.0|    -8667.0 |90.0|
|3| 10013.0|    99999.0|    None|   NO| NO| |   NaN|    NaN|    NaN|
|4| 10014.0|    99999.0|    None|   NO| NO| ENSO|   59783.0|    5350.0| 500.0|
|5| 10015.0|    99999.0|    None|   NO| NO| ENBL|   61383.0|    5867.0| 3270.0|
|6| 10016.0 |99999.0|   None|   NO| NO|     |64850.0|   11233.0|    140.0|
|7| 10017.0|    99999.0|    None|   NO| NO| ENFR|   59933.0|    2417.0| 480.0|
|8| 10020.0|    99999.0|    None|   NO| SV|     |80050.0|   16250.0|    80.0|
|9| 10030.0|    99999.0|    None|   NO| SV|     |77000.0|   15500.0|    120.0|

### <a name="delimited-file-example"></a>带分隔符的文件示例

在本部分中，你可以看到使用 `write_to_csv` 函数通过带分隔符的文件进行写入的示例。

```python
# Create a new data flow using `write_to_csv` 
write_t = t.write_to_csv(directory_path=dprep.LocalFileOutput('./test_out/'))

# Run the data flow to begin the write operation.
write_t.run_local()

written_files = dprep.read_csv('./test_out/part-*')
written_files.head(10)
```

示例输出：
|   |  Column1 |    Column2 | Column3 | Column4  |Column5   | Column6 | Column7 | Column8 | Column9 |
| -------- |  -------- | -------- | -------- |  -------- |  -------- |  -------- |  -------- |  -------- |  -------- |
| 0 |   10000.0 |   99999.0 |   ERROR |       NO|     NO  |   ENRS    |ERROR    |   ERROR |   ERROR|    
|   1|      10003.0 |   99999.0 |   ERROR |       NO|     NO  |   ENSO|       ERROR|        ERROR |ERROR|   
|   2|  10010.0|    99999.0|    ERROR |   NO| JN| ENJA|   70933.0|    -8667.0 |90.0|
|3| 10013.0|    99999.0|    ERROR |   NO| NO| |   ERROR|    ERROR|    ERROR|
|4| 10014.0|    99999.0|    ERROR |   NO| NO| ENSO|   59783.0|    5350.0| 500.0|
|5| 10015.0|    99999.0|    ERROR |   NO| NO| ENBL|   61383.0|    5867.0| 3270.0|
|6| 10016.0 |99999.0|   ERROR |   NO| NO|     |64850.0|   11233.0|    140.0|
|7| 10017.0|    99999.0|    ERROR |   NO| NO| ENFR|   59933.0|    2417.0| 480.0|
|8| 10020.0|    99999.0|    ERROR |   NO| SV|     |80050.0|   16250.0|    80.0|
|9| 10030.0|    99999.0|    ERROR |   NO| SV|     |77000.0|   15500.0|    120.0|

在前面的输出中，你可以看到，由于未正确分析数字，数值列中出现了多个错误。 默认情况下，写入 CSV 时，这些 NULL 值将替换为字符串“ERROR”。 

可在 write 调用中添加参数，并指定一个字符串用于表示 NULL 值。 例如：

```python
write_t = t.write_to_csv(directory_path=dprep.LocalFileOutput('./test_out/'), 
                         error='BadData',
                         na='NA')
write_t.run_local()
written_files = dprep.read_csv('./test_out/part-*')
written_files.head(10)
```

前面的代码生成了以下输出：
|   |  Column1 |    Column2 | Column3 | Column4  |Column5   | Column6 | Column7 | Column8 | Column9 |
| -------- |  -------- | -------- | -------- |  -------- |  -------- |  -------- |  -------- |  -------- |  -------- |
| 0 |   10000.0 |   99999.0 |   BadData |       NO|     NO  |   ENRS    |BadData    |   BadData |   BadData|    
|   1|      10003.0 |   99999.0 |   BadData |       NO|     NO  |   ENSO|       BadData|        BadData |BadData|   
|   2|  10010.0|    99999.0|    BadData |   NO| JN| ENJA|   70933.0|    -8667.0 |90.0|
|3| 10013.0|    99999.0|    BadData |   NO| NO| |   BadData|    BadData|    BadData|
|4| 10014.0|    99999.0|    BadData |   NO| NO| ENSO|   59783.0|    5350.0| 500.0|
|5| 10015.0|    99999.0|    BadData |   NO| NO| ENBL|   61383.0|    5867.0| 3270.0|
|6| 10016.0 |99999.0|   BadData |   NO| NO|     |64850.0|   11233.0|    140.0|
|7| 10017.0|    99999.0|    BadData |   NO| NO| ENFR|   59933.0|    2417.0| 480.0|
|8| 10020.0|    99999.0|    BadData |   NO| SV|     |80050.0|   16250.0|    80.0|
|9| 10030.0|    99999.0|    BadData |   NO| SV|     |77000.0|   15500.0|    120.0|


### <a name="parquet-file-example"></a>Parquet 文件示例

与 `write_to_csv` 类似，`write_to_parquet` 函数将返回一个带有 Parquet 写入步骤的新数据流，该步骤在数据流运行时执行。

```python
write_parquet_t = t.write_to_parquet(directory_path=dprep.LocalFileOutput('./test_parquet_out/'),
error='MiscreantData')
```

接下来，你可以运行数据流来启动写入操作。

```
write_parquet_t.run_local()

written_parquet_files = dprep.read_parquet_file('./test_parquet_out/part-*')
written_parquet_files.head(10)
```

前面的代码生成了以下输出：
|   |  Column1 |    Column2 | Column3 | Column4  |Column5   | Column6 | Column7 | Column8 | Column9 |
| -------- |  -------- | -------- | -------- |  -------- |  -------- |  -------- |  -------- |  -------- |  -------- |
| 0 |   10000.0 |   99999.0 |   MiscreantData |       NO|     NO  |   ENRS    |MiscreantData    |   MiscreantData |   MiscreantData|    
|   1|      10003.0 |   99999.0 |   MiscreantData |       NO|     NO  |   ENSO|       MiscreantData|        MiscreantData |MiscreantData|   
|   2|  10010.0|    99999.0|    MiscreantData |   NO| JN| ENJA|   70933.0|    -8667.0 |90.0|
|3| 10013.0|    99999.0|    MiscreantData |   NO| NO| |   MiscreantData|    MiscreantData|    MiscreantData|
|4| 10014.0|    99999.0|    MiscreantData |   NO| NO| ENSO|   59783.0|    5350.0| 500.0|
|5| 10015.0|    99999.0|    MiscreantData |   NO| NO| ENBL|   61383.0|    5867.0| 3270.0|
|6| 10016.0 |99999.0|   MiscreantData |   NO| NO|     |64850.0|   11233.0|    140.0|
|7| 10017.0|    99999.0|    MiscreantData |   NO| NO| ENFR|   59933.0|    2417.0| 480.0|
|8| 10020.0|    99999.0|    MiscreantData |   NO| SV|     |80050.0|   16250.0|    80.0|
|9| 10030.0|    99999.0|    MiscreantData |   NO| SV|     |77000.0|   15500.0|    120.0|
