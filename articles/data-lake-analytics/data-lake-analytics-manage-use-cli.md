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
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="8c391-103">Gestire Azure Data Lake Analytics mediante l’interfaccia della riga di comando (CLI) di Azure</span><span class="sxs-lookup"><span data-stu-id="8c391-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="8c391-104">Informazioni su come account di Azure Data Lake Analitica toomanage, origini dati, gli utenti e i processi tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c391-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="8c391-105">argomenti relativi alla gestione toosee con altri strumenti, scegliere hello scheda precedente.</span><span class="sxs-lookup"><span data-stu-id="8c391-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="8c391-106">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="8c391-106">**Prerequisites**</span></span>

<span data-ttu-id="8c391-107">Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="8c391-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="8c391-108">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8c391-108">**An Azure subscription**.</span></span> <span data-ttu-id="8c391-109">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c391-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8c391-110">**Interfaccia della riga di comando di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8c391-110">**Azure CLI**.</span></span> <span data-ttu-id="8c391-111">Vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8c391-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="8c391-112">Scaricare e installare hello **definitive** [strumenti di Azure CLI](https://github.com/MicrosoftBigData/AzureDataLake/releases) in ordine toocomplete questa demo.</span><span class="sxs-lookup"><span data-stu-id="8c391-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="8c391-113">**Autenticazione**tramite hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="8c391-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="8c391-114">Per ulteriori informazioni sull'autenticazione con un account aziendale o dell'istituto di istruzione, vedere [connettersi tooan sottoscrizione di Azure da hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8c391-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="8c391-115">**Cambia modalità di gestione risorse di Azure toohello**tramite hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="8c391-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="8c391-116">**comandi di archivio Data Lake e Data Lake Analitica di hello toolist:**</span><span class="sxs-lookup"><span data-stu-id="8c391-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="8c391-117">Gestisci account</span><span class="sxs-lookup"><span data-stu-id="8c391-117">Manage accounts</span></span>
<span data-ttu-id="8c391-118">Prima di eseguire qualsiasi processo di Analisi Data Lake, è necessario disporre di un account di Analisi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8c391-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="8c391-119">A differenza di Azure HDInsight, un account di Analisi non è soggetto ad alcun pagamento fino a quando il processo non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8c391-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="8c391-120">Si paga solo per il tempo di hello quando è in esecuzione un processo.</span><span class="sxs-lookup"><span data-stu-id="8c391-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="8c391-121">Per altre informazioni, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8c391-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="8c391-122">Creare account</span><span class="sxs-lookup"><span data-stu-id="8c391-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="8c391-123">Aggiornare account</span><span class="sxs-lookup"><span data-stu-id="8c391-123">Update accounts</span></span>
<span data-ttu-id="8c391-124">il comando seguente Hello Aggiorna hello le proprietà di un Account esistente di Data Lake Analitica</span><span class="sxs-lookup"><span data-stu-id="8c391-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="8c391-125">Elencare gli account</span><span class="sxs-lookup"><span data-stu-id="8c391-125">List accounts</span></span>
<span data-ttu-id="8c391-126">Elencare gli account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8c391-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="8c391-127">Elencare gli account di Data Lake Analytics all'interno di un gruppo di risorse specifico</span><span class="sxs-lookup"><span data-stu-id="8c391-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="8c391-128">Ottenere i dettagli di un account specifico di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8c391-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="8c391-129">Eliminare gli account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8c391-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="8c391-130">Gestire le origini dati degli account</span><span class="sxs-lookup"><span data-stu-id="8c391-130">Manage account data sources</span></span>
<span data-ttu-id="8c391-131">Data Lake Analitica supporta attualmente hello seguenti origini dati:</span><span class="sxs-lookup"><span data-stu-id="8c391-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="8c391-132">Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="8c391-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="8c391-133">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8c391-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="8c391-134">Quando si crea un account Analitica, è necessario specificare un account di archiviazione Azure Data Lake Storage account toobe hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="8c391-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="8c391-135">Hello ADL storage account predefinito viene utilizzato toostore metadati del processo e processo di log di controllo.</span><span class="sxs-lookup"><span data-stu-id="8c391-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="8c391-136">Dopo aver creato un account di Analytics, è possibile aggiungere altri account di archiviazione di Data Lake e/o account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c391-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="8c391-137">Trovare l'account di archiviazione ADL hello predefinito</span><span class="sxs-lookup"><span data-stu-id="8c391-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="8c391-138">il valore di Hello è elencato nella proprietà: datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="8c391-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="8c391-139">Aggiungere altri account di archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="8c391-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="8c391-140">Sono supportati solo nomi brevi di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="8c391-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="8c391-141">Non utilizzare FQDN, ad esempio "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="8c391-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="8c391-142">Aggiungere altri account di Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8c391-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="8c391-143">[-d] è tooindicate un parametro facoltativo se hello Data Lake da aggiungere è l'account Data Lake hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="8c391-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="8c391-144">Aggiornare l'origine dati esistente</span><span class="sxs-lookup"><span data-stu-id="8c391-144">Update existing data source</span></span>
<span data-ttu-id="8c391-145">tooset un valore predefinito hello toobe account archivio Data Lake esistente:</span><span class="sxs-lookup"><span data-stu-id="8c391-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="8c391-146">tooupdate una chiave di account di archiviazione Blob esistente:</span><span class="sxs-lookup"><span data-stu-id="8c391-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="8c391-147">Elencare le origini dati:</span><span class="sxs-lookup"><span data-stu-id="8c391-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Origine dati dell'elenco Data Lake Analytics](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="8c391-149">Eliminare origini dati:</span><span class="sxs-lookup"><span data-stu-id="8c391-149">Delete data sources:</span></span>
<span data-ttu-id="8c391-150">toodelete un account archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="8c391-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="8c391-151">toodelete un account di archiviazione Blob:</span><span class="sxs-lookup"><span data-stu-id="8c391-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="8c391-152">Gestire i processi</span><span class="sxs-lookup"><span data-stu-id="8c391-152">Manage jobs</span></span>
<span data-ttu-id="8c391-153">È necessario disporre di un account di Data Lake Analytics prima di poter creare un processo.</span><span class="sxs-lookup"><span data-stu-id="8c391-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="8c391-154">Per altre informazioni, vedere [Gestire gli account di Analisi Data Lake](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="8c391-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="8c391-155">Elencare i processi</span><span class="sxs-lookup"><span data-stu-id="8c391-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Origine dati dell'elenco Data Lake Analytics](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="8c391-157">Ottenere i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="8c391-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="8c391-158">Inviare i processi</span><span class="sxs-lookup"><span data-stu-id="8c391-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="8c391-159">priorità predefinita Hello di un processo è 1000 e hello predefinito grado di parallelismo per un processo è 1.</span><span class="sxs-lookup"><span data-stu-id="8c391-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="8c391-160">Annullare i processi</span><span class="sxs-lookup"><span data-stu-id="8c391-160">Cancel jobs</span></span>
<span data-ttu-id="8c391-161">Id di processo hello hello elenco comando toofind utilizzare e quindi annullare un processo toocancel hello.</span><span class="sxs-lookup"><span data-stu-id="8c391-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="8c391-162">Gestire il catalogo</span><span class="sxs-lookup"><span data-stu-id="8c391-162">Manage catalog</span></span>
<span data-ttu-id="8c391-163">catalogo Hello U-SQL è usato toostructure dati e il codice affinché possano essere condivisi da script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="8c391-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="8c391-164">catalogo Hello consente prestazioni più elevate hello possibile i dati in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8c391-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="8c391-165">Per altre informazioni, vedere la pagina di [Usare il catalogo di U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="8c391-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="8c391-166">Elencare gli elementi del catalogo</span><span class="sxs-lookup"><span data-stu-id="8c391-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="8c391-167">tipi di Hello includono database, schema, assembly, origine dati esterna, tabella, la funzione con valori di tabella o le statistiche della tabella.</span><span class="sxs-lookup"><span data-stu-id="8c391-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="8c391-168">Utilizzare i gruppi ARM</span><span class="sxs-lookup"><span data-stu-id="8c391-168">Use ARM groups</span></span>
<span data-ttu-id="8c391-169">Le applicazioni sono in genere costituite da molti componenti, ad esempio app Web, database, server di database, risorsa di archiviazione e servizi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="8c391-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="8c391-170">Azure Resource Manager (ARM) consente toowork con risorse hello dell'applicazione come un tooas gruppo, a cui viene fatto riferimento, un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c391-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="8c391-171">È possibile distribuire, aggiornare, monitorare o eliminare tutte le risorse di hello per l'applicazione in un'operazione singola, coordinata.</span><span class="sxs-lookup"><span data-stu-id="8c391-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="8c391-172">È possibile descrivere le risorse del gruppo in un modello JSON per la distribuzione e quindi usare tale modello per ambienti diversi, ad esempio di testing, staging  e produzione.</span><span class="sxs-lookup"><span data-stu-id="8c391-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="8c391-173">Si può aiutare a chiarire la fatturazione per l'organizzazione visualizzando i costi di roll-up hello per l'intero gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="8c391-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="8c391-174">Per altre informazioni, vedere [Panoramica di Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8c391-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="8c391-175">Un servizio di Data Lake Analitica può includere hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="8c391-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="8c391-176">Account di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8c391-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="8c391-177">Account di archiviazione predefinito obbligatorio di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8c391-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="8c391-178">Account di archiviazione aggiuntivi di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8c391-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="8c391-179">Account di archiviazione aggiuntivi di Azure</span><span class="sxs-lookup"><span data-stu-id="8c391-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="8c391-180">È possibile creare tutti questi componenti in uno ARM gruppo toomake li toomanage più semplice.</span><span class="sxs-lookup"><span data-stu-id="8c391-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Account e archiviazione di Azure Data Lake Analytics](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="8c391-182">Un account Data Lake Analitica e gli account di archiviazione dipendenti hello devono essere inseriti in hello stesso data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c391-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="8c391-183">gruppo ARM Hello tuttavia può trovarsi in un data center diverso.</span><span class="sxs-lookup"><span data-stu-id="8c391-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="8c391-184">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8c391-184">See also</span></span>
* [<span data-ttu-id="8c391-185">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8c391-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="8c391-186">Introduzione a Analisi Data Lake tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8c391-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="8c391-187">Gestire Analisi Data Lake di Azure tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8c391-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="8c391-188">Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8c391-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

