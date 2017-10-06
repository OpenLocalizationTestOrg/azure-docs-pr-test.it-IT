---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: dati aaaLoad con Data Factory di Azure | Documenti Microsoft
description: Informazioni su dati tooload con Data Factory di Azure
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a>Caricare i dati con Azure Data Factory
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)  
> 
> 

In questa esercitazione illustra come toocreate una pipeline di dati di Azure Data Factory toomove da tooAzure Blob di archiviazione di Azure SQL Data Warehouse. Con hello viene visualizzata la procedura seguente:

* Configurare dati di esempio in un BLOB del servizio di archiviazione di Azure.
* Connettere le risorse tooAzure Data Factory.
* Creare una pipeline di dati toomove da tooSQL BLOB di archiviazione del Data Warehouse.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>Prima di iniziare
toofamiliarize familiarità con Azure Data Factory, vedere [tooAzure introduzione Data Factory][Introduction tooAzure Data Factory].

### <a name="create-or-identify-resources"></a>Creare o identificare le risorse
Prima di iniziare questa esercitazione, è necessario hello toohave seguenti risorse:

* **Blob di archiviazione Azure**: questa esercitazione viene utilizzato il Blob di archiviazione di Azure come origine dati hello per la pipeline di Data Factory di Azure hello e pertanto è necessario toohave un toostore disponibili hello campione di dati. Se non hai uno già, informazioni su come troppo[creare un account di archiviazione][Create a storage account].
* **SQL Data Warehouse**: questa esercitazione Sposta i dati di hello dal Blob di archiviazione di Azure troppo SQL Data Warehouse e pertanto necessario toohave un data warehouse online che viene caricato con i dati di esempio AdventureWorksDW hello. Se si dispone già di un data warehouse, informazioni su come troppo[eseguire il provisioning di uno][Create a SQL Data Warehouse]. Se si dispone di un data warehouse, ma non effettuare il provisioning con i dati di esempio hello, è possibile [caricarla manualmente][Load sample data into SQL Data Warehouse].
* **Azure Data Factory**: Data Factory di Azure completa carico effettivo hello e pertanto è necessario toohave uno che è possibile utilizzare pipeline lo spostamento dei dati di toobuild hello. Se non hai uno già, informazioni su come toocreate uno nel passaggio 1 di [Introduzione a Data Factory di Azure (Editor delle Data Factory)][Get started with Azure Data Factory (Data Factory Editor)].
* **AZCopy**: È necessario dati di esempio hello toocopy AZCopy del Blob di archiviazione di Azure di tooyour client locale. Per le istruzioni di installazione, vedere hello [AZCopy documentazione][AZCopy documentation].

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>Passaggio 1: Copiare dati di esempio tooAzure Blob di archiviazione
Dopo aver creato tutti i componenti di hello pronti, si è pronti toocopy esempio dati tooyour Blob di archiviazione di Azure.

1. [Scaricare i dati di esempio][Download sample data]. Questi dati aggiunge un altro tre anni di dati di vendita tooyour dati di esempio AdventureWorksDW.
2. Utilizzare questo comando di AZCopy toocopy hello tre anni di dati tooyour Blob di archiviazione di Azure.
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a>Passaggio 2: Connettere le risorse tooAzure Data Factory
Ora che i dati di hello sono sul posto è possibile creare hello Azure Data Factory pipeline toomove hello dati dall'archiviazione blob di Azure in SQL Data Warehouse.

tooget avviato, aprire hello [portale di Azure] [ Azure portal] e selezionare la data factory dal menu a sinistra di hello.

### <a name="step-21-create-linked-service"></a>Passaggio 2.1: Creare servizi collegati
Collegare l'account di archiviazione di Azure e SQL Data Warehouse tooyour data factory.  

1. Innanzitutto, avviare il processo di registrazione di hello facendo clic nella sezione 'Servizi collegati' hello della data factory e quindi fare clic su 'Nuovo archivio dati.' Scegliere un nome tooregister l'archiviazione di azure in archiviazione di Azure selezionare il tipo e quindi immettere il nome dell'Account e la chiave dell'Account.
2. SQL Data Warehouse tooregister passare toohello 'Autore e Distribuisci' sezione, selezionare 'Nuovo archivio dati' e 'Azure SQL Data Warehouse'. Copiare e incollare in questo modello e quindi immettere le informazioni specifiche.
   
    ```JSON
    {
        "name": "<Linked Service Name>",
        "properties": {
            "description": "",
            "type": "AzureSqlDW",
            "typeProperties": {
                 "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
             }
        }
    }
    ```

### <a name="step-22-define-hello-dataset"></a>Passaggio 2.2: Definire set di dati hello
Dopo la creazione di hello servizi collegati, abbiamo toodefine hello set di dati.  In questo caso, ciò significa definizione della struttura di dati viene spostati dal data warehouse tooyour archiviazione hello hello.  Altre informazioni sulla creazione

1. Avviare questo processo, passando toohello ' autore Distribuisci ' sezione e la data factory.
2. Fare clic su "Nuovo set di dati" e quindi toolink 'Archiviazione Blob di Azure' la data factory tooyour di archiviazione.  È possibile utilizzare i dati hello sotto toodefine script nell'archiviazione Blob di Azure:
   
    ```JSON
    {
        "name": "<Dataset Name>",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "<linked storage name>",
            "typeProperties": {
                "folderPath": "<containter name>",
                "fileName": "FactInternetSales.csv",
                "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }
    ```
3. Verrà ora definito il set di dati per SQL Data Warehouse. Si inizierà in hello allo stesso modo, facendo clic su "Nuovo set di dati" e quindi 'Azure SQL Data Warehouse'.
   
    ```JSON
    {
        "name": "DWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": "AzureSqlDWLinkedService",
            "typeProperties": {
                "tableName": "FactInternetSales"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

## <a name="step-3-create-and-run-your-pipeline"></a>Passaggio 3: Creare ed eseguire la pipeline
Infine, è impostato ed eseguire pipeline hello in Azure Data Factory.  Si tratta di operazione hello che viene completato lo spostamento dei dati effettivi hello.  È possibile trovare una visualizzazione completa di operazioni di hello che è possibile completare con SQL Data Warehouse e Data Factory di Azure [qui][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].

Nella sezione 'Autore e Distribuisci' hello, fare clic su 'Più comandi' e quindi 'Nuova Pipeline'.  Dopo aver creato la pipeline hello, è possibile utilizzare hello seguito codice tootransfer hello dati tooyour del data warehouse:

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
              }
            ],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
toolearn, iniziare la visualizzazione:

* [Percorso di apprendimento per Azure Data Factory][Azure Data Factory learning path].
* [Connettore Azure SQL Data Warehouse][Azure SQL Data Warehouse Connector]. Questo è l'argomento di riferimento hello core per l'utilizzo di Data Factory di Azure con Azure SQL Data Warehouse.

Questi argomenti forniscono informazioni dettagliate su Azure Data Factory. Vengono illustrate HDInsight o Database SQL di Azure, ma hello informazioni si applicano anche tooAzure SQL Data Warehouse.

* [Esercitazione: Introduzione a Data Factory di Azure] [ Tutorial: Get started with Azure Data Factory] si tratta di hello esercitazione di base per l'elaborazione dei dati con Data Factory di Azure. In questa esercitazione verrà compilare le pipeline prima che utilizza tootransform HDInsight e analizzare i log web su base mensile. Si noti che questa esercitazione non prevede attività di copia.
* [Esercitazione: Copiare i dati da tooAzure Blob di archiviazione di Azure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]. In questa esercitazione è creare una pipeline di dati di Azure Data Factory toocopy da tooAzure Blob di archiviazione di Azure SQL Database.

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
