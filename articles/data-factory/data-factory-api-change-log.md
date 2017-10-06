---
title: aaaData Factory - registro delle modifiche API .NET | Documenti Microsoft
description: "Vengono descritte le modifiche di rilievo, le aggiunte funzionalità, correzioni di bug e così via... in una versione specifica dell'API .NET per hello Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8208271b-7f4c-4214-b665-d2ff503c4470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: spelluru
ms.openlocfilehash: 1d44b45c3dc8f9d483d1f1cef7068edacc610932
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---net-api-change-log"></a>Azure Data Factory: log delle modifiche dell'API .NET
Questo articolo fornisce informazioni sulle modifiche tooAzure Data Factory SDK in una versione specifica. È possibile trovare il pacchetto NuGet più recente di hello Azure Data factory [qui](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>Versione 4.11.0
Aggiunte di funzionalità

* Hello seguenti tipi di servizio collegato sono state aggiunte:
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* è stati aggiunti i seguenti tipi di set di dati Hello:
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* esempio Hello copia origine sono stati aggiunti tipi:
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>Versione 4.10.0
* Hello le proprietà facoltative seguenti è state aggiunte tooTextFormat:
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* Hello seguenti tipi di servizio collegato sono state aggiunte:
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* è stati aggiunti i seguenti tipi di set di dati Hello:
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* esempio Hello copia origine sono stati aggiunti tipi:
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* Aggiungere [WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx) tooAzureMLBatchExecutionActivity proprietà
  * Abilitare il passaggio di più input di servizio web tooan esperimento di Azure Machine Learning

## <a name="version-491"></a>Versione 4.9.1
### <a name="bug-fix"></a>Correzione di bug
* Deprecazione dell'autenticazione basata su WebApi per [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx).

## <a name="version-490"></a>Versione 4.9.0
### <a name="feature-additions"></a>Aggiunte di funzionalità
* Aggiungere [EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx) e [StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) tooCopyActivity di proprietà. Vedere [staging copia](data-factory-copy-activity-performance.md#staged-copy) per informazioni dettagliate sulla funzionalità hello.

### <a name="bug-fix"></a>Correzione di bug
* Introduzione di un overload del metodo [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx) che usa un'istanza [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx).
* Contrassegno di [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) e [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx) come facoltativi in CopySink.

## <a name="version-480"></a>Versione 4.8.0
### <a name="feature-additions"></a>Aggiunte di funzionalità
* Hello le proprietà facoltative seguenti è stati aggiunti tooCopy attività digitare tooenable ottimizzazione delle prestazioni di copia:
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>Versione 4.7.0
### <a name="feature-additions"></a>Aggiunte di funzionalità
* Aggiungere nuovo tipo StorageFormat [OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx) digitare toocopy file in formato a colonne (ORC) con ottimizzazione per la riga.
* Aggiungere [AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx) e impostazioni PolyBaseSettings tooSqlDWSink di proprietà.
  * Consente l'utilizzo di hello dei dati toocopy PolyBase in SQL Data Warehouse.

## <a name="version-461"></a>Versione 4.6.1
### <a name="bug-fixes"></a>Correzioni di bug
* Corregge la richiesta HTTP relativa all'elenco delle finestre attività.
  * Rimuove il payload di richiesta di hello Nome gruppo di risorse hello e nome della data factory hello.

## <a name="version-460"></a>Versione 4.6.0
### <a name="feature-additions"></a>Aggiunte di funzionalità
* Hello seguenti sono state aggiunte proprietà troppo[PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx):
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [Set di dati](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* Hello seguenti sono state aggiunte proprietà troppo[PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx):
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* Aggiunte nuove [StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx) tipo [JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx) digitare toodefine set di dati i cui dati sono in formato JSON.

## <a name="version-450"></a>Versione 4.5.0
### <a name="feature-additions"></a>Aggiunte di funzionalità
* Aggiunta di [operazioni di tipo elenco per la finestra attività](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx).
  * Aggiunta di metodi tooretrieve attività di windows con i filtri in base ai tipi di entità hello (vale a dire data factory, i set di dati, pipeline e attività).
* Hello seguenti tipi di servizio collegato sono state aggiunte:
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx), [WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx)
* è stati aggiunti i seguenti tipi di set di dati Hello:
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx), [WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx)
* esempio Hello copia origine sono stati aggiunti tipi:     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>Versione 4.4.0
### <a name="feature-additions"></a>Aggiunte di funzionalità
* Hello seguente tipo di servizio collegato è stato aggiunto come origini dati e sink per le attività di copia:
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx). Per informazioni concettuali ed esempi, vedere [Servizio collegato di firma di accesso condiviso Archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) .

## <a name="version-430"></a>Versione 4.3.0
### <a name="feature-additions"></a>Aggiunte di funzionalità
* Hello seguenti utili di tipi di servizio collegato stati aggiunti come origini dati per le attività di copia:
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx). Per informazioni concettuali ed esempi, vedere [Spostare dati da HDFS con Data Factory](data-factory-hdfs-connector.md) .
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx). Per informazioni concettuali ed esempi, vedere [Spostare dati da archivi dati ODBC con Azure Data Factory](data-factory-odbc-connector.md) .

## <a name="version-420"></a>Versione 4.2.0
### <a name="feature-additions"></a>Aggiunte di funzionalità
* è stato aggiunto il nuovo tipo di attività seguente Hello: [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx). Per informazioni dettagliate sull'attività hello, vedere [utilizzando i modelli di aggiornamento di Azure ML hello attività della risorsa di aggiornamento](data-factory-azure-ml-batch-execution-activity.md).
* Una nuova proprietà facoltativa [updateresourceendpoint ' dal](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx) è stato aggiunto toohello [classe oggetto AzureMLLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx).
* [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx) e [LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx) proprietà sono state aggiunte toohello [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx) classe.
* Consentire la configurazione dei timeout hello per le chiamate di client toohello servizio Data Factory.

## <a name="version-410"></a>Versione 4.1.0
### <a name="feature-additions"></a>Aggiunte di funzionalità
* Hello seguenti tipi di servizio collegato sono state aggiunte:
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* è stati aggiunti i seguenti tipi di attività Hello:
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* è stati aggiunti i seguenti tipi di set di dati Hello:
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* Hello seguenti tipi di origine e sink per attività di copia sono state aggiunte:
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>Versione 4.0.1
### <a name="breaking-changes"></a>Modifiche di rilievo
è stata rinominata le seguenti classi Hello. nuovi nomi di Hello sono i nomi originali hello delle classi prima di rilasciare 4.0.0.

| Nome nella versione 4.0.0 | Nome nella versione 4.0.1 |
|:--- |:--- |
| AzureSqlDataWarehouseDataset |[AzureSqlDataWarehouseTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqldatawarehousetabledataset.aspx) |
| AzureSqlDataset |[AzureSqlTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqltabledataset.aspx) |
| AzureDataset |[AzureTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuretabledataset.aspx) |
| OracleDataset |[OracleTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.oracletabledataset.aspx) |
| RelationalDataset |[RelationalTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.relationaltabledataset.aspx) |
| SqlServerDataset |[SqlServerTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.sqlservertabledataset.aspx) |

## <a name="version-400"></a>Versione 4.0.0
### <a name="breaking-changes"></a>Modifiche di rilievo
* è stato rinominato Hello seguenti classi o interfacce.

| Nome precedente | Nuovo nome |
|:--- |:--- |
| ITableOperations |[IDatasetOperations](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.idatasetoperations.aspx) |
| Tabella |[Set di dati](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.dataset.aspx) |
| TableProperties |[DatasetProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetproperties.aspx) |
| TableTypeProprerties |[DatasetTypeProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasettypeproperties.aspx) |
| TableCreateOrUpdateParameters |[DatasetCreateOrUpdateParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateparameters.aspx) |
| TableCreateOrUpdateResponse |[DatasetCreateOrUpdateResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateresponse.aspx) |
| TableGetResponse |[DatasetGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetgetresponse.aspx) |
| TableListResponse |[DatasetListResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetlistresponse.aspx) |
| CreateOrUpdateWithRawJsonContentParameters |[DatasetCreateOrUpdateWithRawJsonContentParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdatewithrawjsoncontentparameters.aspx) |

* Hello **elenco** metodi restituiscono risultati di paging ora. Se la risposta hello contiene non vuoto **NextLink** proprietà, un'applicazione client hello deve pagina successiva hello recupero toocontinue fino a quando non vengono restituite tutte le pagine.  Di seguito è fornito un esempio:

    ```csharp
    PipelineListResponse response = client.Pipelines.List("ResourceGroupName", "DataFactoryName");
    var pipelines = new List<Pipeline>(response.Pipelines);

    string nextLink = response.NextLink;
    while (!string.IsNullOrEmpty(nextLink))
    {
        PipelineListResponse nextResponse = client.Pipelines.ListNext(nextLink);
        pipelines.AddRange(nextResponse.Pipelines);

        nextLink = nextResponse.NextLink;
    }
    ```
* **Elenco** pipeline API restituisce solo hello riepilogo di una pipeline anziché i dettagli completi. Ad esempio, le attività in un riepilogo delle pipeline può contenere solo il nome e il tipo.

### <a name="feature-additions"></a>Aggiunte di funzionalità
* Hello [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx) classe supporta due nuove proprietà, **SliceIdentifierColumnName** e **SqlWriterCleanupScript**, toosupport idempotente copia tooAzure dati SQL Warehouse. Vedere hello [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md) articolo per informazioni dettagliate su queste proprietà.
* È ora supportano l'esecuzione di stored procedure sul Database SQL di Azure e Azure SQL Data Warehouse origini come parte dell'attività di copia hello. Hello [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx) e [SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx) classi dispongono di hello seguenti proprietà: **SqlReaderStoredProcedureName** e **StoredProcedureParameters** . Vedere hello [Database SQL di Azure](data-factory-azure-sql-connector.md#sqlsource) e [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource) articoli su Azure.com per informazioni dettagliate su queste proprietà.  
