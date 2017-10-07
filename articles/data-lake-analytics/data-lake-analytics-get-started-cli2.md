---
title: aaaGet avviato con Azure Data Lake Analitica mediante Azure CLI 2.0 | Documenti Microsoft
description: 'Informazioni su come creare un processo di Data Lake Analitica con U-SQL, toouse hello interfaccia della riga di comando di Azure 2.0 toocreate un account Data Lake Analitica e inviare il processo di hello. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Introduzione ad Azure Data Lake Analytics con l'interfaccia della riga di comando di Azure 2.0
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

In questa esercitazione verrà sviluppato un processo che legge un file con valori delimitati da tabulazioni (TSV) e lo converte in un file con valori delimitati da virgole (CSV). toogo tramite hello supportato stesso esercitazione usare altri strumenti, elenco a discesa hello in primo piano hello in questa sezione.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Interfaccia della riga di comando di Azure 2.0**. Vedere [Installare e configurare l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-tooazure"></a>Accedi tooAzure

toolog in tooyour sottoscrizione di Azure:

```
azurecli
az login
```

Si sono toobrowse richiesto tooa URL e immettere un codice di autenticazione.  E quindi seguire hello istruzioni tooenter le credenziali.

Dopo aver eseguito l'accesso, il comando di accesso hello Elenca le sottoscrizioni.

toouse una sottoscrizione specifica:

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>Creare un account di Analisi Data Lake
Per poter eseguire un processo è necessario un account Data Lake Analytics. toocreate un account Data Lake Analitica, è necessario specificare hello seguenti elementi:

* **Gruppo di risorse di Azure**. L'account Data Lake Analytics deve essere creato all'interno di un gruppo di risorse di Azure. [Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) consente toowork con risorse hello dell'applicazione come un gruppo. È possibile distribuire, aggiornare o eliminare tutte le risorse di hello per l'applicazione in un'operazione singola, coordinata.  

toolist hello gruppi di risorse esistenti nella sottoscrizione:

```
az group list
```

toocreate un nuovo gruppo di risorse:

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Nome dell'account Data Lake Analytics**. Ogni account Data Lake Analytics ha un nome.
* **Località**. Utilizzare uno dei hello data center di Azure che supporta Data Lake Analitica.
* **Account Data Lake Store predefinito**: ogni account Data Lake Analytics ha un account Data Lake Store predefinito.

account toolist hello esistente archivio Data Lake:

```
az dls account list
```

toocreate un nuovo account archivio Data Lake:

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

Utilizzare hello segue sintassi toocreate un account Data Lake Analitica:

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

Dopo aver creato un account, è possibile utilizzare hello seguendo gli account di comandi toolist hello e visualizzare i dettagli dell'account:

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>Carica archivio data Lake di tooData
In questa esercitazione verrà eseguita l'elaborazione di alcuni log di ricerca.  Hello ricerca log può essere archiviato nell'archivio Data Lake o archiviazione Blob di Azure.

Hello portale di Azure fornisce un'interfaccia utente per la copia di un esempio dati file toohello archivio Data Lake account predefinito, che includono un file di log di ricerca. Vedere [preparare i dati di origine](data-lake-analytics-get-started-portal.md) account archivio Data Lake di tooupload hello dati toohello predefinito.

file tooupload utilizzando 2.0 CLI, utilizzare hello seguenti comandi:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

Data Lake Analytics può inoltre accedere all'archivio BLOB di Azure.  Per il caricamento di archiviazione Blob di dati tooAzure, vedere [Using hello CLI di Azure con l'archiviazione di Azure](../storage/common/storage-azure-cli.md).

## <a name="submit-data-lake-analytics-jobs"></a>Inviare processi di Data Lake Analytics
i processi di Data Lake Analitica Hello vengono scritti in hello linguaggio U-SQL. toolearn ulteriori informazioni su U-SQL, vedere [introduzione U-SQL language](data-lake-analytics-u-sql-get-started.md) e [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).

**script per un processo Data Lake Analitica toocreate**

Creare un file di testo con script U-SQL seguente e salvare workstation di tooyour file testo hello:

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

Questo script U-SQL legge hello origine dati file utilizzando **Extractors.Tsv()**e quindi crea un file csv utilizzando **Outputters.Csv()**.

Non modificare due percorsi hello, a meno che non si copia il file di origine hello in un percorso diverso.  Data Lake Analitica Crea cartella di output di hello se non esiste.

È più semplice toouse i percorsi relativi per i file archiviati in account archivio Data Lake predefiniti. è possibile usare anche percorsi assoluti.  ad esempio:

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

È necessario utilizzare i file di percorsi assoluti tooaccess negli account di archiviazione collegato.  sintassi di Hello per i file archiviati in account di archiviazione di Azure collegato è:

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> Il contenitore BLOB di Azure con BLOB pubblici non è supportato.      
> Il contenitore BLOB di Azure con contenitori pubblici non è supportato.      
>

**processi toosubmit**

Utilizzare hello segue sintassi toosubmit un processo.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

ad esempio:

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**i processi toolist e Mostra i dettagli dei processi**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**processi toocancel**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>Recuperare i risultati di un processo

Al termine di un processo, è possibile utilizzare i seguenti file di output di comandi toolist hello hello e scaricare file hello:

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

ad esempio:

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>Pipeline e ricorrenze

**Ottenere informazioni su pipeline e ricorrenze**

Hello utilizzare `az dla job pipeline` comandi informazioni sulle pipeline di hello toosee i processi inviati in precedenza.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Hello utilizzare `az dla job recurrence` comandi toosee le informazioni sull'occorrenza hello per i processi inviati in precedenza.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>Passaggi successivi

* hello toosee documento di riferimento Data Lake Analitica CLI 2.0, vedere [Data Lake Analitica](https://docs.microsoft.com/cli/azure/dla).
* hello toosee documento di riferimento Data Lake archivio CLI 2.0, vedere [archivio Data Lake](https://docs.microsoft.com/cli/azure/dls).
* toosee una query più complessa, vedere [sito Web di analizzare i log di Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).
