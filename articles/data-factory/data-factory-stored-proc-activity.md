---
title: "aaaSQL attività Server Stored Procedure"
description: "Informazioni su come è possibile utilizzare l'attività di SQL Server Stored Procedure di hello tooinvoke una stored procedure in un Database SQL di Azure o Azure SQL Data Warehouse da una pipeline di Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>Attività di stored procedure di SQL Server
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Attività Hive](data-factory-hive-activity.md) 
> * [Attività di Pig](data-factory-pig-activity.md)
> * [Attività MapReduce](data-factory-map-reduce.md)
> * [Attività di Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
> * [Attività Spark](data-factory-spark.md)
> * [Attività di esecuzione batch di Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Attività della risorsa di aggiornamento di Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Attività stored procedure](data-factory-stored-proc-activity.md)
> * [Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md)
> * [Attività personalizzata di .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Panoramica
Utilizzare le attività di trasformazione di dati in una Data Factory [pipeline](data-factory-create-pipelines.md) tootransform ed elaborare i dati non elaborati in stime e approfondimenti. Hello attività Stored Procedure è una delle attività di trasformazione hello che supporta Data Factory. In questo articolo si basa su hello [le attività di trasformazione dati](data-factory-data-transformation-activities.md) articolo, che presenta una panoramica generale di trasformazione dei dati e le attività di trasformazione hello è supportato in Data Factory.

È possibile utilizzare una stored procedure in uno dei seguenti dati hello archivia nella propria azienda o in una macchina virtuale di Azure (VM) di hello attività Stored Procedure tooinvoke: 

- Database SQL di Azure
- Azure SQL Data Warehouse
- Database di SQL Server.  Se si utilizza SQL Server, installare il Gateway di gestione di dati in hello che stesso computer che ospita hello database o in un computer separato che dispone di database di access toohello. Gateway di gestione dati è un componente che connette in modo sicuro e gestito origini dati presenti in locale o in macchine virtuali di Azure ai servizi cloud. Per informazioni dettagliate, vedere [Data Management Gateway](data-factory-data-management-gateway.md) (Gateway di gestione dati).

> [!IMPORTANT]
> Quando si copiano dati in Database SQL di Azure o SQL Server, è possibile configurare hello **SqlSink** in attività di copia tooinvoke una stored procedure utilizzando hello **sqlWriterStoredProcedureName** proprietà. Per altre informazioni, vedere [Chiamare una stored procedure da un'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md). Per ulteriori informazioni sulla proprietà hello, vedere i seguenti articoli connettore: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). Non è possibile richiamare una stored procedure durante la copia dei dati in un Azure SQL Data Warehouse tramite un'attività di copia. Tuttavia, è possibile utilizzare hello stored procedure attività tooinvoke una stored procedure in un Data Warehouse di SQL. 
>  
> Quando si copiano dati da Database SQL di Azure o Azure SQL Data Warehouse e SQL Server, è possibile configurare **SqlSource** in tooinvoke attività copia dei dati di tooread una stored procedure dal database di origine hello utilizzando hello  **sqlReaderStoredProcedureName** proprietà. Per ulteriori informazioni, vedere i seguenti articoli connettore hello: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


seguendo questa procedura dettagliata Usa Hello hello attività Stored Procedure in un tooinvoke pipeline una stored procedure in un database SQL di Azure. 

## <a name="walkthrough"></a>Procedura dettagliata
### <a name="sample-table-and-stored-procedure"></a>Tabella di esempio e stored procedure
1. Creare i seguenti hello **tabella** nel Database di SQL Azure con SQL Server Management Studio o qualsiasi altro strumento si ha familiarità con. colonna datetimestamp Hello è hello data e l'ora in cui viene generato il corrispondente ID di hello.

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    ID è univoco hello identificato e hello datetimestamp hello data e l'ora in cui viene generato il corrispondente ID di hello.
    
    ![Dati di esempio](./media/data-factory-stored-proc-activity/sample-data.png)

    In questo esempio, hello archiviato consiste in un Database di SQL Azure. Se hello stored procedure si trova in un Database di SQL Server e in Azure SQL Data Warehouse, l'approccio di hello è simile. Per un database SQL Server, è necessario installare un [Gateway di gestione dati](data-factory-data-management-gateway.md).
2. Creare i seguenti hello **stored procedure di** che inserisce dati in toohello **tabella di esempio**.

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **Nome** e **maiuscole e minuscole** di hello parametro (DateTime in questo esempio) deve corrispondere a quello del parametro specificato nella pipeline/attività hello JSON. In hello definizione della stored procedure, assicurarsi che  **@**  viene utilizzato come prefisso per il parametro hello.

### <a name="create-a-data-factory"></a>Creare un'istanza di Data factory
1. Accedi troppo[portale di Azure](https://portal.azure.com/).
2. Fare clic su **NEW** scegliere dal menu a sinistra, hello **Intelligence + Analitica**, fare clic su **Data Factory**.

    ![Nuova data factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. In hello **nuova data factory** pannello immettere **SProcDF** per hello Name. I nomi di Data factory di Azure sono **univoci**. È necessario nome di hello tooprefix della hello data factory con il nome, la creazione corretta tooenable hello di factory di hello.

   ![Nuova data factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Selezionare la **sottoscrizione di Azure**.
5. Per **gruppo di risorse**, effettuare una delle hello alla procedura seguente:
   1. Fare clic su **Crea nuovo** e immettere un nome per il gruppo di risorse hello.
   2. Fare clic su **Usa esistente** e scegliere un gruppo di risorse esistente.  
6. Seleziona hello **percorso** per data factory di hello.
7. Selezionare **toodashboard Pin** in modo da poter visualizzare data factory di hello dashboard hello successivo tentativo di accesso.
8. Fare clic su **crea** su hello **nuova data factory** blade.
9. Vedrai data factory di hello viene creato nel hello **dashboard** di hello portale di Azure. Dopo aver hello data factory è stata creata correttamente, vedrai hello data factory pagina nella quale viene hello contenuto di data factory di hello.

   ![Home page di Data factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Creare un servizio collegato SQL di Azure
Dopo aver creato una data factory di hello, si crea un servizio collegato SQL Azure che si collega il database SQL di Azure, che contiene una tabella di tabella di esempio hello e sp_sample stored procedure, tooyour data factory di.

1. Fare clic su **autore e distribuire** su hello **Data Factory** pannello **SProcDF** toolaunch hello Editor delle Data Factory.
2. Fare clic su **nuovo archivio dati** hello barra dei comandi e scegliere **Database SQL di Azure**. Dovrebbe essere hello script JSON per la creazione di un SQL di Azure il servizio nell'editor di hello collegato.

   ![Nuovo archivio dati](media/data-factory-stored-proc-activity/new-data-store.png)
3. In hello script JSON, apportare hello seguenti modifiche:

   1. Sostituire `<servername>` con nome hello del server di Database SQL di Azure.
   2. Sostituire `<databasename>` con database hello in cui viene creato nella tabella hello e hello stored procedure.
   3. Sostituire `<username@servername>` con account utente di hello con database di access toohello.
   4. Sostituire `<password>` con password hello per account utente di hello.

      ![Nuovo archivio dati](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy hello servizio collegato, fare clic su **Distribuisci** hello barra dei comandi. Assicurarsi di visualizzare hello AzureSqlLinkedService nella struttura ad albero hello visualizzare a sinistra di hello.

    ![Visualizzazione albero con servizio collegato](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>Creare un set di dati di output
È necessario specificare che un set di dati di output per un'attività di stored procedure anche se hello stored procedure non produce i dati. Ciò avviene perché l'output di hello set di dati che l'unità di pianificazione di hello dell'attività hello (frequenza hello attività viene eseguita - oraria, giornaliera e così via). Hello set di dati di output deve utilizzare un **servizio collegato** che fa riferimento tooan Database SQL di Azure o di un Data Warehouse di SQL Azure o di un Database di SQL Server in cui si desidera hello toorun stored procedure. Hello set di dati di output può essere utilizzato come un risultato hello toopass modo procedure hello archiviato per l'elaborazione successiva da un'altra attività ([concatenamento di attività](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) nella pipeline hello. Tuttavia, Data Factory non scrive automaticamente output di hello di un set di dati toothis stored procedure. È hello stored procedure di scritture tooa SQL tabella punti di set di dati di output di hello. In alcuni casi, il set di dati di hello output può essere un **set di dati fittizio** (un set di dati che fa riferimento a tabella tooa che non contiene effettivamente l'output di hello stored procedure). Questo set di dati fittizio viene utilizzato solo pianificazione hello toospecify per l'esecuzione di hello attività stored procedure. 

1. Fare clic su **... Ulteriori** sulla barra degli strumenti hello, fare clic su **nuovo set di dati**, fare clic su **SQL Azure**. **Nuovo set di dati** sul comando hello barra e selezionare **SQL Azure**.

    ![Visualizzazione albero con servizio collegato](media/data-factory-stored-proc-activity/new-dataset.png)
2. Copiare e incollare lo script JSON nell'editor di JSON toohello seguente hello.

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy hello set di dati, fare clic su **Distribuisci** hello barra dei comandi. Confermare la visualizzazione dei set di dati di hello in visualizzazione struttura ad albero di hello.

    ![Visualizzazione albero con servizi collegati](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>Creare una pipeline con l'attività SqlServerStoredProcedure
Si crea ora una pipeline con un'attività stored procedure. 

Si noti hello le proprietà seguenti: 

- Hello **tipo** impostata troppo**SqlServerStoredProcedure**. 
- Hello **storedProcedureName** nel tipo di proprietà è impostata troppo**sp_sample** (nome di hello stored procedure).
- Hello **storedProcedureParameters** sezione contiene un parametro denominato **DataTime**. Nome e le maiuscole e minuscole del parametro hello in JSON devono corrispondere nome hello e maiuscole e minuscole del parametro hello nella definizione di hello stored procedure. Se è necessario passare null per un parametro, utilizzare la sintassi di hello: `"param1": null` (tutti in lettere minuscole).
 
1. Fare clic su **... Ulteriori** hello barra dei comandi e fare clic su **nuova pipeline**.
2. Copiare e incollare hello frammento di codice JSON seguente:   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. pipeline di hello toodeploy, fare clic su **Distribuisci** sulla barra degli strumenti hello.  

### <a name="monitor-hello-pipeline"></a>Pipeline hello monitoraggio
1. Fare clic su **X** tooclose Editor delle Data Factory pannelli e toonavigate il pannello Data Factory toohello e fare clic su **diagramma**.

    ![Riquadro Diagramma](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. In hello **vista diagramma**, si visualizza una panoramica delle pipeline hello e set di dati utilizzati in questa esercitazione.

    ![Riquadro Diagramma](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. In vista diagramma hello, fare doppio clic sul set di dati hello `sprocsampleout`. Vedrai sezioni hello in stato pronto. Non vi saranno cinque sezioni perché viene prodotta una sezione per ogni ora tra l'ora di inizio hello e l'ora di fine da hello JSON.

    ![Riquadro Diagramma](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. Quando una sezione è in **pronto** stato, eseguire una `select * from sampletable` query hello Azure SQL database tooverify che hello dati è stato inserito nella tabella toohello dalla procedura archiviata hello.

   ![Dati di output](./media/data-factory-stored-proc-activity/output.png)

   Vedere [pipeline hello monitoraggio](data-factory-monitor-manage-pipelines.md) per informazioni dettagliate sul monitoraggio delle pipeline di Data Factory di Azure.  


## <a name="specify-an-input-dataset"></a>Specificare un set di dati di input
In questa procedura dettagliata hello, attività stored procedure non dispone di qualsiasi set di dati di input. Se si specifica un set di dati di input, hello attività stored procedure non viene eseguito fino a quando non è disponibile la porzione di hello del set di dati input (nello stato Ready). set di dati Hello può essere un set di dati esterno (che non sia stato generato da un'altra attività hello stessa pipeline) o un set di dati interno è prodotto da un'attività padre (attività hello che viene eseguito prima di questa attività). È possibile specificare più set di dati di input per l'attività di hello stored procedure. Se in tal caso, hello attività stored procedure viene eseguita solo quando sono disponibili tutte le sezioni di set di dati input hello (nello stato Ready). set di dati Hello input non può essere utilizzato nella procedura hello archiviato come parametro. È solo toocheck utilizzati hello dipendenza prima hello Inizia attività stored procedure.

## <a name="chaining-with-other-activities"></a>Concatenamento con altre attività
Se si desidera toochain un'attività upstream con questa attività, specificare l'output di hello di attività upstream hello come input di questa attività. Quando si esegue questa operazione, hello attività stored procedure non viene eseguito fino al completamento dell'attività upstream hello e set di dati di attività upstream hello output di hello è disponibile (in stato pronto). È possibile specificare i set di dati di output di più attività upstream come set di dati di input dell'attività di hello stored procedure. Quando esegue questa operazione, hello attività stored procedure viene eseguita solo quando sono disponibili tutte le sezioni di set di dati input hello.  

In hello l'esempio seguente, l'output di hello di attività di copia hello è: OutputDataset, che è un input di hello attività stored procedure. Pertanto, hello attività stored procedure non viene eseguito fino al completamento dell'attività di copia hello e sezione OutputDataset hello è disponibile (nello stato Ready). Se si specificano più set di dati di input, hello attività stored procedure non viene eseguito fino a quando non sono disponibili tutte le sezioni di set di dati input hello (nello stato Ready). set di dati di input Hello non può essere utilizzato direttamente come attività di parametri toohello stored procedure. 

Per altre informazioni sul concatenamento di attività, vedere [attività multiple in una pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

Analogamente, toolink store procedure attività hello con **attività downstream** (attività hello che eseguire dopo il completamento hello attività stored procedure), specificare set di dati di attività di hello stored procedure come output di hello un input dell'attività a valle hello nella pipeline hello.

> [!IMPORTANT]
> Quando si copiano dati in Database SQL di Azure o SQL Server, è possibile configurare hello **SqlSink** in attività di copia tooinvoke una stored procedure utilizzando hello **sqlWriterStoredProcedureName** proprietà. Per altre informazioni, vedere [Chiamare una stored procedure da un'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md). Per ulteriori informazioni sulla proprietà hello, vedere i seguenti articoli connettore hello: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).
>  
> Quando si copiano dati da Database SQL di Azure o Azure SQL Data Warehouse e SQL Server, è possibile configurare **SqlSource** in tooinvoke attività copia dei dati di tooread una stored procedure dal database di origine hello utilizzando hello  **sqlReaderStoredProcedureName** proprietà. Per ulteriori informazioni, vedere i seguenti articoli connettore hello: [Database SQL di Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>Formato JSON
Di seguito è riportato il formato JSON hello per la definizione di un'attività di Stored Procedure:

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

Hello nella tabella seguente vengono descritte queste proprietà JSON:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| name | Nome dell'attività hello |Sì |
| description |Testo che descrive le attività di hello viene utilizzato per |No |
| type | Deve essere impostato su: **SqlServerStoredProcedure** | Sì |
| inputs | Facoltativo. Se si specifica un set di dati di input, deve essere disponibile (in stato "Pronto") per hello stored procedure toorun di attività. set di dati Hello input non può essere utilizzato nella procedura hello archiviato come parametro. È solo toocheck utilizzati hello dipendenza prima hello Inizia attività stored procedure. |No |
| outputs | È necessario specificare un set di dati di output per un'attività della stored procedure. Set di dati di output specifica hello **pianificazione** per hello attività stored procedure (ogni ora, settimanale, mensile, ecc.). <br/><br/>Hello set di dati di output deve utilizzare un **servizio collegato** che fa riferimento tooan Database SQL di Azure o di un Data Warehouse di SQL Azure o di un Database di SQL Server in cui si desidera hello toorun stored procedure. <br/><br/>Hello set di dati di output può essere utilizzato come un risultato hello toopass modo procedure hello archiviato per l'elaborazione successiva da un'altra attività ([concatenamento di attività](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) nella pipeline hello. Tuttavia, Data Factory non scrive automaticamente output di hello di un set di dati toothis stored procedure. È hello stored procedure di scritture tooa SQL tabella punti di set di dati di output di hello. <br/><br/>In alcuni casi, il set di dati di hello output può essere un **set di dati fittizio**, che viene utilizzato solo pianificazione hello toospecify per l'esecuzione di hello attività stored procedure. |Sì |
| storedProcedureName |Specificare il nome di hello di hello stored procedure in database SQL di Azure hello o un database Azure SQL Data Warehouse o SQL Server che è rappresentato dal servizio hello collegato che Usa tabella di output di hello. |Sì |
| storedProcedureParameters |Specificare i valori dei parametri della stored procedure. Se è necessario toopass null per un parametro, utilizzare la sintassi di hello: "param1": null (lettere minuscole). Vedere hello seguente toolearn esempio sull'utilizzo di questa proprietà. |No |

## <a name="passing-a-static-value"></a>Passaggio di un valore statico
A questo punto, si prendano in considerazione l'aggiunta di un'altra colonna denominata 'Scenario' nella tabella hello contenente un valore statico denominato 'Documento di esempio'.

![Dati di esempio 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**Tabella:**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**Stored procedure:**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

A questo punto, passare hello **Scenario** valore di parametro e hello da hello attività stored procedure. Hello **typeProperties** sezione nel precedente esempio aspetto hello seguente frammento di codice hello:

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Set di dati di Data factory:**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pipeline di Data factory**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```