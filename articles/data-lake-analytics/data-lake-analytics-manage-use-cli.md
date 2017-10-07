---
title: aaaManage Azure Data Lake Analitica utilizzando l'interfaccia della riga di comando di Azure | Documenti Microsoft
description: Informazioni su come account Data Lake Analitica toomanage, origini dati, processi e utenti tramite l'interfaccia CLI di Azure
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Gestire Azure Data Lake Analytics mediante l’interfaccia della riga di comando (CLI) di Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Informazioni su come account di Azure Data Lake Analitica toomanage, origini dati, gli utenti e i processi tramite hello CLI di Azure. argomenti relativi alla gestione toosee con altri strumenti, scegliere hello scheda precedente.


**Prerequisiti**

Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Interfaccia della riga di comando di Azure**. Vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).
  * Scaricare e installare hello **definitive** [strumenti di Azure CLI](https://github.com/MicrosoftBigData/AzureDataLake/releases) in ordine toocomplete questa demo.
* **Autenticazione**tramite hello il seguente comando:
  
        azure login
    Per ulteriori informazioni sull'autenticazione con un account aziendale o dell'istituto di istruzione, vedere [connettersi tooan sottoscrizione di Azure da hello Azure CLI](../xplat-cli-connect.md).
* **Cambia modalità di gestione risorse di Azure toohello**tramite hello il seguente comando:
  
        azure config mode arm

**comandi di archivio Data Lake e Data Lake Analitica di hello toolist:**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>Gestisci account
Prima di eseguire qualsiasi processo di Analisi Data Lake, è necessario disporre di un account di Analisi Data Lake. A differenza di Azure HDInsight, un account di Analisi non è soggetto ad alcun pagamento fino a quando il processo non è in esecuzione.  Si paga solo per il tempo di hello quando è in esecuzione un processo.  Per altre informazioni, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Creare account
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>Aggiornare account
il comando seguente Hello Aggiorna hello le proprietà di un Account esistente di Data Lake Analitica

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>Elencare gli account
Elencare gli account di Data Lake Analytics 

    azure datalake analytics account list

Elencare gli account di Data Lake Analytics all'interno di un gruppo di risorse specifico

    azure datalake analytics account list -g "<Azure Resource Group Name>"

Ottenere i dettagli di un account specifico di Data Lake Analytics

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>Eliminare gli account di Data Lake Analytics
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>Gestire le origini dati degli account
Data Lake Analitica supporta attualmente hello seguenti origini dati:

* [Archivio Data Lake di Azure](../data-lake-store/data-lake-store-overview.md)
* [Archiviazione di Azure](../storage/common/storage-introduction.md)

Quando si crea un account Analitica, è necessario specificare un account di archiviazione Azure Data Lake Storage account toobe hello predefinito. Hello ADL storage account predefinito viene utilizzato toostore metadati del processo e processo di log di controllo. Dopo aver creato un account di Analytics, è possibile aggiungere altri account di archiviazione di Data Lake e/o account di archiviazione di Azure. 

### <a name="find-hello-default-adl-storage-account"></a>Trovare l'account di archiviazione ADL hello predefinito
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

il valore di Hello è elencato nella proprietà: datalakeStoreAccount:name.

### <a name="add-additional-azure-blob-storage-accounts"></a>Aggiungere altri account di archiviazione BLOB di Azure
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> Sono supportati solo nomi brevi di archiviazione BLOB.  Non utilizzare FQDN, ad esempio "myblob.blob.core.windows.net".
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>Aggiungere altri account di Data Lake Store
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-d] è tooindicate un parametro facoltativo se hello Data Lake da aggiungere è l'account Data Lake hello predefinito. 

### <a name="update-existing-data-source"></a>Aggiornare l'origine dati esistente
tooset un valore predefinito hello toobe account archivio Data Lake esistente:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

tooupdate una chiave di account di archiviazione Blob esistente:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>Elencare le origini dati:
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Origine dati dell'elenco Data Lake Analytics](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Eliminare origini dati:
toodelete un account archivio Data Lake:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete un account di archiviazione Blob:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>Gestire i processi
È necessario disporre di un account di Data Lake Analytics prima di poter creare un processo.  Per altre informazioni, vedere [Gestire gli account di Analisi Data Lake](#manage-accounts).

### <a name="list-jobs"></a>Elencare i processi
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Origine dati dell'elenco Data Lake Analytics](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>Ottenere i dettagli dei processi
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>Inviare i processi
> [!NOTE]
> priorità predefinita Hello di un processo è 1000 e hello predefinito grado di parallelismo per un processo è 1.
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>Annullare i processi
Id di processo hello hello elenco comando toofind utilizzare e quindi annullare un processo toocancel hello.

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>Gestire il catalogo
catalogo Hello U-SQL è usato toostructure dati e il codice affinché possano essere condivisi da script U-SQL. catalogo Hello consente prestazioni più elevate hello possibile i dati in Azure Data Lake. Per altre informazioni, vedere la pagina di [Usare il catalogo di U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-catalog-items"></a>Elencare gli elementi del catalogo
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

tipi di Hello includono database, schema, assembly, origine dati esterna, tabella, la funzione con valori di tabella o le statistiche della tabella.

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>Utilizzare i gruppi ARM
Le applicazioni sono in genere costituite da molti componenti, ad esempio app Web, database, server di database, risorsa di archiviazione e servizi di terze parti. Azure Resource Manager (ARM) consente toowork con risorse hello dell'applicazione come un tooas gruppo, a cui viene fatto riferimento, un gruppo di risorse di Azure. È possibile distribuire, aggiornare, monitorare o eliminare tutte le risorse di hello per l'applicazione in un'operazione singola, coordinata. È possibile descrivere le risorse del gruppo in un modello JSON per la distribuzione e quindi usare tale modello per ambienti diversi, ad esempio di testing, staging  e produzione. Si può aiutare a chiarire la fatturazione per l'organizzazione visualizzando i costi di roll-up hello per l'intero gruppo hello. Per altre informazioni, vedere [Panoramica di Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md). 

Un servizio di Data Lake Analitica può includere hello seguenti componenti:

* Account di Azure Data Lake Analytics
* Account di archiviazione predefinito obbligatorio di Azure Data Lake
* Account di archiviazione aggiuntivi di Azure Data Lake
* Account di archiviazione aggiuntivi di Azure

È possibile creare tutti questi componenti in uno ARM gruppo toomake li toomanage più semplice.

![Account e archiviazione di Azure Data Lake Analytics](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Un account Data Lake Analitica e gli account di archiviazione dipendenti hello devono essere inseriti in hello stesso data center di Azure.
gruppo ARM Hello tuttavia può trovarsi in un data center diverso.  

## <a name="see-also"></a>Vedere anche
* [Panoramica di Analisi Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Introduzione a Analisi Data Lake tramite il portale di Azure](data-lake-analytics-get-started-portal.md)
* [Gestire Analisi Data Lake di Azure tramite il portale di Azure](data-lake-analytics-manage-use-portal.md)
* [Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

