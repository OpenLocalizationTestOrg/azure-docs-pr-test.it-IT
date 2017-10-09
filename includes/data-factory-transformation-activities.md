Data Factory di Azure supporta hello seguente attività di trasformazione che può essere aggiunto toopipelines singolarmente o concatenati con un'altra attività.

| Attività di trasformazione dei dati | Ambiente di calcolo |
|:--- |:--- |
| [Hive](../articles/data-factory/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop Streaming](../articles/data-factory/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/data-factory-spark.md) | HDInsight [Hadoop] |
| [Attività di Machine Learning: esecuzione batch e aggiornamento risorse](../articles/data-factory/data-factory-azure-ml-batch-execution-activity.md) |Macchina virtuale di Azure |
| [Stored procedure](../articles/data-factory/data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL Data Warehouse o SQL Server |
| [Attività U-SQL di Data Lake Analytics](../articles/data-factory/data-factory-usql-activity.md) |Azure Data Lake Analytics. |
| [DotNet](../articles/data-factory/data-factory-use-custom-activities.md) |HDInsight [Hadoop] o Batch di Azure |

> [!NOTE]
> È possibile utilizzare i programmi MapReduce attività toorun Spark il cluster HDInsight Spark. Per i dettagli, vedere [Chiamare i programmi Spark da Azure Data Factory](../articles/data-factory/data-factory-spark.md) .
> È possibile creare gli script R toorun un'attività personalizzata nel cluster di HDInsight con R installato. Vedere [RunRScriptUsingADFSample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)(Esempio relativo all'esecuzione di script R con Azure Data Factory).
> 
> 

