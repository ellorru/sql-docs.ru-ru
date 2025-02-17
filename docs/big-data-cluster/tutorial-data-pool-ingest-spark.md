---
title: Прием данных с помощью заданий Spark
titleSuffix: SQL Server big data clusters
description: В этом руководстве показано, как принимать данные в пул данных [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] с помощью заданий Spark в Azure Data Studio.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6ebcc95d48f894ff8cef9771946130fc67216a45
ms.sourcegitcommit: c8b8101c62a6af3e4a7244683e3f34f7189c150f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2019
ms.locfileid: "73182633"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>Учебник. прием данных в пул данных SQL Server с помощью заданий Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

В этом руководстве показано, как использовать задания Spark для загрузки данных в [пул данных](concept-data-pool.md) [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. 

В этом руководстве описано следующее.

> [!div class="checklist"]
> * Создание внешней таблицы в пуле данных.
> * Создание задания Spark для загрузки данных из HDFS.
> * Запрос результатов во внешней таблице.

> [!TIP]
> При необходимости вы можете скачать и выполнить скрипт, содержащий команды из этого руководства. См. инструкции в разделе [Примеры пулов данных](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) на сайте GitHub.

## <a id="prereqs"></a> предварительные требования

- [Средства работы с большими данными](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Расширение SQL Server 2019**
- [Загрузка примера данных в кластер больших данных](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Создание внешней таблицы в пуле данных

Выполните следующие действия, чтобы создать внешнюю таблицу с именем **web_clickstreams_spark_results** в пуле данных. В дальнейшем эта таблица может использоваться для приема данных в кластер больших данных.

1. В Azure Data Studio установите подключение к главному экземпляру SQL Server в кластере больших данных. Дополнительные сведения см. в разделе [Подключение к главному экземпляру SQL Server](connect-to-big-data-cluster.md#master).

1. Дважды щелкните подключение в окне **Серверы**, чтобы открыть панель мониторинга сервера для главного экземпляра SQL Server. Выберите **Создать запрос**.

   ![Запрос главного экземпляра SQL Server](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. Создайте внешний источник данных для пула данных, если это не было сделано ранее.

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. Создайте внешнюю таблицу с именем **web_clickstreams_spark_results** в пуле данных.

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstreams_spark_results')
      CREATE EXTERNAL TABLE [web_clickstreams_spark_results]
      ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. В CTP 3.1 создание пула данных выполняется асинхронно, однако на данный момент не реализованы способы определить момент завершения этого процесса. Прежде чем продолжать, подождите примерно две минуты, чтобы удостовериться в создании пула данных.

## <a name="start-a-spark-streaming-job"></a>Запуск задания потоковой передачи Spark

Следующим шагом является создание задания потоковой передачи Spark, которое загружает сведения о посещениях из пула носителей (HDFS) во внешнюю таблицу, созданную в пуле данных. Эти данные были добавлены в/clickstream_data в процессе [загрузки демонстрационных данных в кластер больших данных](tutorial-load-sample-data.md).

1. В Azure Data Studio установите подключение к главному экземпляру в кластере больших данных. Дополнительные сведения см. в разделе [Подключение к кластеру больших данных](connect-to-big-data-cluster.md).

2. Создание новой записной книжки и выбор Spark | Scala в качестве ядра.

3. Запуск задания приема Spark
   1. Настройка параметров соединителя Spark-SQL
      ```
      import org.apache.spark.sql.types._
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}

      // Change per your installation
      val user= "username"
      val password= "****"
      val database =  "MyTestDatabase"
      val sourceDir = "/clickstream_data"
      val datapool_table = "web_clickstreams_spark_results"
      val datasource_name = "SqlDataPool"
      val schema = StructType(Seq(
      StructField("wcs_click_date_sk",IntegerType,true), StructField("wcs_click_time_sk",IntegerType,true), StructField("wcs_sales_sk",IntegerType,true), StructField("wcs_item_sk",IntegerType,true), 
      StructField("wcs_web_page_sk",IntegerType,true), StructField("wcs_user_sk",IntegerType,true)
      ))

      val hostname = "master-0.master-svc"
      val port = 1433
      val url = s"jdbc:sqlserver://${hostname}:${port};database=${database};user=${user};password=${password};"
      ```
   2. Определение и запуск задания Spark
      * Каждое задание состоит из двух частей: Реадстреам и Вритестреам. Ниже мы создадим кадр данных, используя определенную выше схему, а затем выполним запись во внешнюю таблицу в пуле данных.
      ```
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}
      
      val df = spark.readStream.format("csv").schema(schema).option("header", true).load(sourceDir)
      val query = df.writeStream.outputMode("append").foreachBatch{ (batchDF: DataFrame, batchId: Long) => 
                batchDF.write
                 .format("com.microsoft.sqlserver.jdbc.spark")
                 .mode("append")
                  .option("url", url)
                  .option("dbtable", datapool_table)
                  .option("user", user)
                  .option("password", password)
                  .option("dataPoolDataSource",datasource_name).save()
               }.start()

      query.processAllAvailable()
      query.awaitTermination(40000)
      ```
## <a name="query-the-data"></a>Запрос данных

Следующие шаги показывают, что задание потоковой передачи Spark загрузило данные из HDFS в пул данных.

1. Перед запросом полученных данных просмотрите состояние выполнения Spark, включая идентификатор приложения Yarn, Пользовательский интерфейс Spark и журналы драйверов.

   ![Сведения о выполнении Spark](./media/tutorial-data-pool-ingest-spark/Spark-Joblog-sparkui-yarn.png)

1. Вернитесь в окно запроса главного экземпляра SQL Server, которое было открыто в начале работы с этим руководством.

1. Выполните приведенный ниже запрос, чтобы изучить принятые данные.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```
1. Данные также можно запрашивать в Spark. Например, приведенный ниже код выводит число записей в таблице.
   ```
   def df_read(dbtable: String,
                url: String,
                dataPoolDataSource: String=""): DataFrame = {
        spark.read
             .format("com.microsoft.sqlserver.jdbc.spark")
             .option("url", url)
             .option("dbtable", dbtable)
             .option("user", user)
             .option("password", password)
             .option("dataPoolDataSource", dataPoolDataSource)
             .load()
             }

   val new_df = df_read(datapool_table, url, dataPoolDataSource=datasource_name)
   println("Number of rows is " +  new_df.count)
   ```
## <a name="clean-up"></a>Очистка

Выполните следующую команду, чтобы удалить объекты базы данных, созданные в рамках этого руководства.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>Следующие шаги

См. сведения о запуске примера записной книжки в Azure Data Studio:
> [!div class="nextstepaction"]
> [Запуск примера записной книжки](tutorial-notebook-spark.md).
