---
title: "Gestire Azure Data Lake Analytics mediante l’interfaccia della riga di comando (CLI) di Azure | Documentazione Microsoft"
description: "Informazioni su come gestire gli account, le origini dati, i processi e gli utenti di Data Lake Analytics tramite l’interfaccia della riga di comando di Azure"
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
ms.openlocfilehash: f90bada3572c0ed40b07d76ec02c1b499bbd1428
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="cab86-103">Gestire Azure Data Lake Analytics mediante l’interfaccia della riga di comando (CLI) di Azure</span><span class="sxs-lookup"><span data-stu-id="cab86-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="cab86-104">Informazioni su come gestire gli account, le origini dati, gli utenti e i processi di Azure Data Lake Analytics usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="cab86-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span></span> <span data-ttu-id="cab86-105">Per visualizzare gli argomenti relativi alla gestione tramite altri strumenti, fare clic sul selettore di scheda riportato sopra.</span><span class="sxs-lookup"><span data-stu-id="cab86-105">To see management topics using other tools, click the tab select above.</span></span>


<span data-ttu-id="cab86-106">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="cab86-106">**Prerequisites**</span></span>

<span data-ttu-id="cab86-107">Prima di iniziare questa esercitazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="cab86-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="cab86-108">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="cab86-108">**An Azure subscription**.</span></span> <span data-ttu-id="cab86-109">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cab86-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cab86-110">**Interfaccia della riga di comando di Azure**.</span><span class="sxs-lookup"><span data-stu-id="cab86-110">**Azure CLI**.</span></span> <span data-ttu-id="cab86-111">Vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cab86-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="cab86-112">Scaricare e installare gli **Strumenti di Azure CLI** [pre-release](https://github.com/MicrosoftBigData/AzureDataLake/releases) per completare questa demo.</span><span class="sxs-lookup"><span data-stu-id="cab86-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="cab86-113">**Autenticazione**, utilizzando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cab86-113">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="cab86-114">Per altre informazioni sull'autenticazione con un account aziendale o dell'istituto di istruzione, vedere [Connettersi a una sottoscrizione Azure dall'interfaccia della riga di comando di Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="cab86-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="cab86-115">**Passare alla modalità Gestione risorse di Azure**, usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cab86-115">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="cab86-116">**Per elencare i comandi Data Lake Store e Data Lake Analytics :**</span><span class="sxs-lookup"><span data-stu-id="cab86-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="cab86-117">Gestire account</span><span class="sxs-lookup"><span data-stu-id="cab86-117">Manage accounts</span></span>
<span data-ttu-id="cab86-118">Prima di eseguire qualsiasi processo di Analisi Data Lake, è necessario disporre di un account di Analisi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="cab86-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="cab86-119">A differenza di Azure HDInsight, un account di Analisi non è soggetto ad alcun pagamento fino a quando il processo non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cab86-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="cab86-120">Il pagamento, infatti, viene richiesto solo per la durata di esecuzione di un processo.</span><span class="sxs-lookup"><span data-stu-id="cab86-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="cab86-121">Per altre informazioni, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cab86-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="cab86-122">Creare account</span><span class="sxs-lookup"><span data-stu-id="cab86-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="cab86-123">Aggiornare account</span><span class="sxs-lookup"><span data-stu-id="cab86-123">Update accounts</span></span>
<span data-ttu-id="cab86-124">Il seguente comando aggiorna le proprietà di un account Data Lake Analytics esistente</span><span class="sxs-lookup"><span data-stu-id="cab86-124">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="cab86-125">Elencare gli account</span><span class="sxs-lookup"><span data-stu-id="cab86-125">List accounts</span></span>
<span data-ttu-id="cab86-126">Elencare gli account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cab86-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="cab86-127">Elencare gli account di Data Lake Analytics all'interno di un gruppo di risorse specifico</span><span class="sxs-lookup"><span data-stu-id="cab86-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="cab86-128">Ottenere i dettagli di un account specifico di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cab86-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="cab86-129">Eliminare gli account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cab86-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="cab86-130">Gestire le origini dati degli account</span><span class="sxs-lookup"><span data-stu-id="cab86-130">Manage account data sources</span></span>
<span data-ttu-id="cab86-131">Analisi Data Lake supporta attualmente le seguenti origini dati:</span><span class="sxs-lookup"><span data-stu-id="cab86-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="cab86-132">Archivio Data Lake di Azure</span><span class="sxs-lookup"><span data-stu-id="cab86-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="cab86-133">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cab86-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="cab86-134">Quando si crea un account di Analytics, è necessario impostare un account di archiviazione di Azure Data Lake come account di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="cab86-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="cab86-135">L'account di archiviazione ADL predefinito viene usato per archiviare i metadati dei processi e i log di controllo dei processi.</span><span class="sxs-lookup"><span data-stu-id="cab86-135">The default ADL storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="cab86-136">Dopo aver creato un account di Analytics, è possibile aggiungere altri account di archiviazione di Data Lake e/o account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cab86-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-adl-storage-account"></a><span data-ttu-id="cab86-137">Cercare l'account di archiviazione ADL predefinito</span><span class="sxs-lookup"><span data-stu-id="cab86-137">Find the default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="cab86-138">Il valore è elencato in properties:datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="cab86-138">The value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="cab86-139">Aggiungere altri account di archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="cab86-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="cab86-140">Sono supportati solo nomi brevi di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="cab86-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="cab86-141">Non utilizzare FQDN, ad esempio "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="cab86-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="cab86-142">Aggiungere altri account di Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cab86-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="cab86-143">[-d] è un parametro facoltativo per indicare se il Data Lake da aggiungere è l'account Data Lake predefinito.</span><span class="sxs-lookup"><span data-stu-id="cab86-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="cab86-144">Aggiornare l'origine dati esistente</span><span class="sxs-lookup"><span data-stu-id="cab86-144">Update existing data source</span></span>
<span data-ttu-id="cab86-145">Per impostare un account Archivio Data Lake esistente come impostazione predefinita:</span><span class="sxs-lookup"><span data-stu-id="cab86-145">To set an existing Data Lake Store account to be the default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="cab86-146">Per aggiornare una chiave di account di archiviazione BLOB esistente:</span><span class="sxs-lookup"><span data-stu-id="cab86-146">To update an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="cab86-147">Elencare le origini dati:</span><span class="sxs-lookup"><span data-stu-id="cab86-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Origine dati dell'elenco Data Lake Analytics](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="cab86-149">Eliminare origini dati:</span><span class="sxs-lookup"><span data-stu-id="cab86-149">Delete data sources:</span></span>
<span data-ttu-id="cab86-150">Per eliminare un account Archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="cab86-150">To delete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="cab86-151">Per eliminare un account di archiviazione BLOB:</span><span class="sxs-lookup"><span data-stu-id="cab86-151">To delete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="cab86-152">Gestire i processi</span><span class="sxs-lookup"><span data-stu-id="cab86-152">Manage jobs</span></span>
<span data-ttu-id="cab86-153">È necessario disporre di un account di Data Lake Analytics prima di poter creare un processo.</span><span class="sxs-lookup"><span data-stu-id="cab86-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="cab86-154">Per altre informazioni, vedere [Gestire gli account di Analisi Data Lake](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="cab86-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="cab86-155">Elencare i processi</span><span class="sxs-lookup"><span data-stu-id="cab86-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Origine dati dell'elenco Data Lake Analytics](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="cab86-157">Ottenere i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="cab86-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="cab86-158">Inviare i processi</span><span class="sxs-lookup"><span data-stu-id="cab86-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="cab86-159">La priorità predefinita di un processo è 1000 e il livello predefinito di parallelismo per un processo è 1.</span><span class="sxs-lookup"><span data-stu-id="cab86-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="cab86-160">Annullare i processi</span><span class="sxs-lookup"><span data-stu-id="cab86-160">Cancel jobs</span></span>
<span data-ttu-id="cab86-161">Utilizzare il comando list per cercare l'id del processo e quindi utilizzare cancel per annullare il processo.</span><span class="sxs-lookup"><span data-stu-id="cab86-161">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="cab86-162">Gestire il catalogo</span><span class="sxs-lookup"><span data-stu-id="cab86-162">Manage catalog</span></span>
<span data-ttu-id="cab86-163">Il catalogo di U-SQL viene usato per definire la struttura dei dati e del codice in modo da poterli condividere mediante U-SQL.</span><span class="sxs-lookup"><span data-stu-id="cab86-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="cab86-164">Il catalogo consente di ottenere le migliori prestazioni possibili con i dati in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="cab86-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="cab86-165">Per altre informazioni, vedere la pagina di [Usare il catalogo di U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="cab86-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="cab86-166">Elencare gli elementi del catalogo</span><span class="sxs-lookup"><span data-stu-id="cab86-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="cab86-167">I tipi includono database, schema, assembly, origine dati esterna, tabella, funzione con valori di tabella o statistiche tabelle.</span><span class="sxs-lookup"><span data-stu-id="cab86-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="cab86-168">Utilizzare i gruppi ARM</span><span class="sxs-lookup"><span data-stu-id="cab86-168">Use ARM groups</span></span>
<span data-ttu-id="cab86-169">Le applicazioni sono in genere costituite da molti componenti, ad esempio app Web, database, server di database, risorsa di archiviazione e servizi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="cab86-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="cab86-170">Gestione risorse di Azure (ARM) consente di usare le risorse dell'applicazione come gruppo, detto Gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="cab86-170">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="cab86-171">È quindi possibile distribuire, aggiornare, monitorare o eliminare tutte le risorse per l'applicazione con una singola operazione coordinata.</span><span class="sxs-lookup"><span data-stu-id="cab86-171">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="cab86-172">È possibile descrivere le risorse del gruppo in un modello JSON per la distribuzione e quindi usare tale modello per ambienti diversi, ad esempio di testing, staging  e produzione.</span><span class="sxs-lookup"><span data-stu-id="cab86-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="cab86-173">È possibile chiarire la fatturazione per l'organizzazione visualizzando i costi per l'intero gruppo.</span><span class="sxs-lookup"><span data-stu-id="cab86-173">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="cab86-174">Per altre informazioni, vedere [Panoramica di Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cab86-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="cab86-175">Un servizio di Analisi Data Lake può includere i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cab86-175">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="cab86-176">Account di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cab86-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="cab86-177">Account di archiviazione predefinito obbligatorio di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="cab86-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="cab86-178">Account di archiviazione aggiuntivi di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="cab86-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="cab86-179">Account di archiviazione aggiuntivi di Azure</span><span class="sxs-lookup"><span data-stu-id="cab86-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="cab86-180">È possibile creare tutti questi componenti in un unico gruppo ARM per semplificarne la gestione.</span><span class="sxs-lookup"><span data-stu-id="cab86-180">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Account e archiviazione di Azure Data Lake Analytics](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="cab86-182">Un account di Analisi Data Lake e gli account di archiviazione dipendenti devono trovarsi nello stesso data center di Azure,</span><span class="sxs-lookup"><span data-stu-id="cab86-182">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="cab86-183">mentre il gruppo ARM può trovarsi anche in un data center diverso.</span><span class="sxs-lookup"><span data-stu-id="cab86-183">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="cab86-184">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cab86-184">See also</span></span>
* [<span data-ttu-id="cab86-185">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="cab86-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="cab86-186">Introduzione a Analisi Data Lake tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cab86-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="cab86-187">Gestire Analisi Data Lake di Azure tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cab86-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="cab86-188">Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cab86-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

