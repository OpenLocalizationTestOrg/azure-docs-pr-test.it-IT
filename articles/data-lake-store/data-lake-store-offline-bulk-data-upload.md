---
title: aaaUpload elevati di dati in archivio Data Lake tramite metodi offline | Documenti Microsoft
description: TooData Lake archivio BLOB di hello utilizzare dati di toocopy AdlCopy dello strumento da archiviazione di Azure
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>Utilizzare il servizio di importazione/esportazione di Azure hello per copia offline di archivio data Lake di tooData
In questo articolo si apprenderà come set di dati di grandi dimensioni toocopy (> 200 GB) in un archivio Azure Data Lake utilizzando metodi di copia non in linea, ad esempio hello [servizio di importazione/esportazione di Azure](../storage/common/storage-import-export-service.md). In particolare, file hello utilizzato come un esempio in questo articolo è 339,420,860,416 byte, ovvero circa 319 GB su disco. Chiameremo questo file 319GB.tsv.

Hello servizio importazione/esportazione di Azure consente di tootransfer grandi quantità di dati in modo sicuro nell'archiviazione Blob da disco rigido shipping tooAzure unità tooan Data Center di Azure.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un account di archiviazione di Azure**.
* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>Preparazione dei dati hello
Prima di utilizzare il servizio di importazione/esportazione di hello, trasferiti interruzione hello dati file toobe **in copie di meno di 200 GB** dimensioni. lo strumento di importazione Hello non funziona con i file di dimensioni superiori a 200 GB. In questa esercitazione verranno suddivise file hello in blocchi di 100 GB. A tale scopo è possibile usare [Cygwin](https://cygwin.com/install.html). Cygwin supporta i comandi di Linux. In questo caso, utilizzare hello comando seguente:

    split -b 100m 319GB.tsv

operazione di divisione Hello crea file con i seguenti nomi hello.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>Preparare i dischi con i dati
Seguire le istruzioni hello [mediante il servizio di importazione/esportazione di Azure hello](../storage/common/storage-import-export-service.md) (in hello **preparare le unità** sezione) tooprepare le unità disco rigido. Ecco hello sequenza generale:

1. Ottenere un disco rigido che soddisfa hello requisito toobe utilizzato per il servizio di importazione/esportazione di Azure hello.
2. Identificare un account di archiviazione di Azure in cui verranno copiati i dati di hello dopo essere stato spedito toohello Data Center di Azure.
3. Hello utilizzare [strumento di importazione/esportazione di Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), un'utilità della riga di comando. Di seguito è riportato un frammento di esempio che illustra come toouse hello dello strumento.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    Vedere [mediante il servizio di importazione/esportazione di Azure hello](../storage/common/storage-import-export-service.md) per più frammenti di codice di esempio.
4. Hello comando precedente crea una registrazione di file hello percorso specificato. Utilizzare questo toocreate file journal un processo di importazione da hello [portale di Azure classico](https://manage.windowsazure.com).

## <a name="create-an-import-job"></a>Creare un processo di importazione
È ora possibile creare un processo di importazione utilizzando le istruzioni hello [mediante il servizio di importazione/esportazione di Azure hello](../storage/common/storage-import-export-service.md) (in hello **Crea processo di importazione hello** sezione). Per questo processo di importazione, con altri dettagli, fornire anche file journal hello creato durante la preparazione delle unità disco hello.

## <a name="physically-ship-hello-disks"></a>Fisicamente spedire i dischi di hello
È ora possibile fornire fisicamente hello dischi tooan Data Center di Azure. Dati hello non esiste, viene copiati sui blob di archiviazione di Azure toohello che immessa durante la creazione del processo di importazione hello. Inoltre, durante la creazione del processo di hello, se si è scelto di hello tooprovide in un secondo momento, le informazioni di rilevamento è ora possibile passare nuovamente tooyour importazione processo e aggiornamento hello numero di tracciabilità.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Copiare i dati dall'archivio Data Lake di archiviazione di Azure BLOB tooAzure
Dopo lo stato di hello di hello processo di importazione mostra che viene completato il processo, è possibile verificare se i dati di hello sono disponibili nei blob di archiviazione di Azure hello che è stato specificato. È quindi possibile utilizzare un'ampia gamma di metodi toomove che i dati da hello BLOB archivio tooAzure Data Lake. Per tutti hello opzioni disponibili per il caricamento dei dati, vedere [l'inserimento di dati in archivio Data Lake](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).

In questa sezione si forniscono le definizioni di hello JSON che è possibile utilizzare toocreate una pipeline di Data Factory di Azure per la copia dei dati. È possibile utilizzare queste definizioni JSON da hello [portale di Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).

### <a name="source-linked-service-azure-storage-blob"></a>Servizio collegato all'origine (BLOB di Archiviazione di Azure)
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a>Servizio collegato alla destinazione (Azure Data Lake Store)
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a>Set di dati di input
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a>Set di dati di output
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a>Pipeline (attività di copia)
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
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
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
Per ulteriori informazioni, vedere [spostare dati da archiviazione di Azure blob usando Azure Data Factory di archivio Data Lake tooAzure](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Ricostruire il file di dati hello in archivio Azure Data Lake
Siamo partiti da un file che era 319 GB e si è interrotta, verso il basso nei file di dimensioni minori in modo che possono essere trasferito tramite il servizio di importazione/esportazione di Azure hello. Dopo avere dati hello archivio Azure Data Lake, è possibile ricostruire dimensioni originali tooits di file hello. È possibile utilizzare hello seguente così toodo cmldts Azure PowerShell.

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a>Passaggi successivi
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
