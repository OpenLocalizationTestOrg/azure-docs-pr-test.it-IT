---
title: Introduzione ad Azure Data Lake Analytics con l'interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: 'Informazioni su come usare l''interfaccia della riga di comando di Azure 2.0 per creare un account Data Lake Analytics, definire un processo di Data Lake Analytics con U-SQL e inviare il processo. '
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
ms.openlocfilehash: fe2b84aac718ff5eddd4d73b5dc2120362952c1e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="22f04-103">Introduzione ad Azure Data Lake Analytics con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="22f04-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="22f04-104">In questa esercitazione verrà sviluppato un processo che legge un file con valori delimitati da tabulazioni (TSV) e lo converte in un file con valori delimitati da virgole (CSV).</span><span class="sxs-lookup"><span data-stu-id="22f04-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="22f04-105">Per eseguire la stessa esercitazione usando altri strumenti supportati, usare l'elenco a discesa disponibile nella parte superiore di questa sezione.</span><span class="sxs-lookup"><span data-stu-id="22f04-105">To go through the same tutorial using other supported tools, use the dropdown list on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22f04-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="22f04-106">Prerequisites</span></span>
<span data-ttu-id="22f04-107">Prima di iniziare questa esercitazione sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f04-107">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="22f04-108">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="22f04-108">**An Azure subscription**.</span></span> <span data-ttu-id="22f04-109">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22f04-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="22f04-110">**Interfaccia della riga di comando di Azure 2.0**.</span><span class="sxs-lookup"><span data-stu-id="22f04-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="22f04-111">Vedere [Installare e configurare l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="22f04-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="22f04-112">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="22f04-112">Log in to Azure</span></span>

<span data-ttu-id="22f04-113">Per accedere alla sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="22f04-113">To log in to your Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="22f04-114">Viene richiesto di passare a un URL e immettere un codice di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="22f04-114">You are requested to browse to a URL, and enter an authentication code.</span></span>  <span data-ttu-id="22f04-115">Seguire le istruzioni per immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="22f04-115">And then follow the instructions to enter your credentials.</span></span>

<span data-ttu-id="22f04-116">Dopo aver eseguito l'accesso, il comando di accesso elenca le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="22f04-116">Once you have logged in, the login command lists your subscriptions.</span></span>

<span data-ttu-id="22f04-117">Per usare una sottoscrizione specifica:</span><span class="sxs-lookup"><span data-stu-id="22f04-117">To use a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="22f04-118">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="22f04-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="22f04-119">Per poter eseguire un processo è necessario un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="22f04-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="22f04-120">Per creare un account Data Lake Analytics, specificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="22f04-120">To create a Data Lake Analytics account, you must specify the following items:</span></span>

* <span data-ttu-id="22f04-121">**Gruppo di risorse di Azure**.</span><span class="sxs-lookup"><span data-stu-id="22f04-121">**Azure Resource Group**.</span></span> <span data-ttu-id="22f04-122">L'account Data Lake Analytics deve essere creato all'interno di un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="22f04-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="22f04-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) consente di lavorare con le risorse dell'applicazione come gruppo.</span><span class="sxs-lookup"><span data-stu-id="22f04-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="22f04-124">È possibile distribuire, aggiornare o eliminare tutte le risorse per l'applicazione mediante un'unica operazione coordinata.</span><span class="sxs-lookup"><span data-stu-id="22f04-124">You can deploy, update, or delete all of the resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="22f04-125">Per elencare i gruppi di risorse esistenti nella sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="22f04-125">To list the existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="22f04-126">Per creare un nuovo gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="22f04-126">To create a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="22f04-127">**Nome dell'account Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="22f04-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="22f04-128">Ogni account Data Lake Analytics ha un nome.</span><span class="sxs-lookup"><span data-stu-id="22f04-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="22f04-129">**Località**.</span><span class="sxs-lookup"><span data-stu-id="22f04-129">**Location**.</span></span> <span data-ttu-id="22f04-130">Usare uno dei data center di Azure che supporta Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="22f04-130">Use one of the Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="22f04-131">**Account Data Lake Store predefinito**: ogni account Data Lake Analytics ha un account Data Lake Store predefinito.</span><span class="sxs-lookup"><span data-stu-id="22f04-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="22f04-132">Per elencare l'account Data Lake Store esistente:</span><span class="sxs-lookup"><span data-stu-id="22f04-132">To list the existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="22f04-133">Per creare un nuovo account Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="22f04-133">To create a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="22f04-134">Per creare un account Data Lake Analytics, usare la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="22f04-134">Use the following syntax to create a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="22f04-135">Dopo aver creato un account, è possibile usare i comandi seguenti per elencare gli account e visualizzarne i dettagli:</span><span class="sxs-lookup"><span data-stu-id="22f04-135">After creating an account, you can use the following commands to list the accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-to-data-lake-store"></a><span data-ttu-id="22f04-136">Caricare dati nell’Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="22f04-136">Upload data to Data Lake Store</span></span>
<span data-ttu-id="22f04-137">In questa esercitazione verrà eseguita l'elaborazione di alcuni log di ricerca.</span><span class="sxs-lookup"><span data-stu-id="22f04-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="22f04-138">Il log di ricerca può essere archiviato in Data Lake Store o in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="22f04-138">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="22f04-139">Il portale di Azure offre un’interfaccia utente per copiare alcuni file di dati di esempio nell'account Data Lake Store predefinito, tra cui anche un file di log di ricerca.</span><span class="sxs-lookup"><span data-stu-id="22f04-139">The Azure portal provides a user interface for copying some sample data files to the default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="22f04-140">Vedere [Preparare i dati di origine](data-lake-analytics-get-started-portal.md) per caricare i dati nell'account Archivio Data Lake predefinito.</span><span class="sxs-lookup"><span data-stu-id="22f04-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) to upload the data to the default Data Lake Store account.</span></span>

<span data-ttu-id="22f04-141">Per caricare i file usando l'interfaccia della riga di comando 2.0, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f04-141">To upload files using CLI 2.0, use the following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="22f04-142">Data Lake Analytics può inoltre accedere all'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="22f04-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="22f04-143">Per caricare i dati nell'archiviazione BLOB di Azure, vedere [Uso dell’interfaccia della riga di comando di Azure con Archiviazione di Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="22f04-143">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="22f04-144">Inviare processi di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="22f04-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="22f04-145">I processi di Data Lake Analtyics vengono scritti nel linguaggio U-SQL.</span><span class="sxs-lookup"><span data-stu-id="22f04-145">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="22f04-146">Per altre informazioni su U-SQL, vedere [Introduzione a U-SQL](data-lake-analytics-u-sql-get-started.md) e [U-SQL Language Reference](http://go.microsoft.com/fwlink/?LinkId=691348) (Informazioni di riferimento sul linguaggio U-SQL).</span><span class="sxs-lookup"><span data-stu-id="22f04-146">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="22f04-147">**Per creare uno script per il processo di Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="22f04-147">**To create a Data Lake Analytics job script**</span></span>

<span data-ttu-id="22f04-148">Creare un file di testo contenente il seguente script U-SQL e salvare il file di testo nella workstation in uso:</span><span class="sxs-lookup"><span data-stu-id="22f04-148">Create a text file with following U-SQL script, and save the text file to your workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="22f04-149">Questo script U-SQL legge il file di dati di origine con **Extractors.Tsv()** e quindi crea un file CSV con **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="22f04-149">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="22f04-150">Non modificare i due percorsi, a meno che il file di origine non sia stato copiato in una posizione diversa.</span><span class="sxs-lookup"><span data-stu-id="22f04-150">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="22f04-151">Data Lake Analytics creerà la cartella di output, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="22f04-151">Data Lake Analytics creates the output folder if it doesn't exist.</span></span>

<span data-ttu-id="22f04-152">Risulta più semplice usare i percorsi relativi dei file archiviati in account Data Lake Store predefiniti, ma</span><span class="sxs-lookup"><span data-stu-id="22f04-152">It is simpler to use relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="22f04-153">è possibile usare anche percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="22f04-153">You can also use absolute paths.</span></span>  <span data-ttu-id="22f04-154">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="22f04-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="22f04-155">È necessario usare percorsi assoluti per accedere ai file presenti negli account di archiviazione collegati.</span><span class="sxs-lookup"><span data-stu-id="22f04-155">You must use absolute paths to access files in linked Storage accounts.</span></span>  <span data-ttu-id="22f04-156">La sintassi dei file presenti in un account di Archiviazione di Azure collegato è:</span><span class="sxs-lookup"><span data-stu-id="22f04-156">The syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="22f04-157">Il contenitore BLOB di Azure con BLOB pubblici non è supportato.</span><span class="sxs-lookup"><span data-stu-id="22f04-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="22f04-158">Il contenitore BLOB di Azure con contenitori pubblici non è supportato.</span><span class="sxs-lookup"><span data-stu-id="22f04-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="22f04-159">**Per inviare processi**</span><span class="sxs-lookup"><span data-stu-id="22f04-159">**To submit jobs**</span></span>

<span data-ttu-id="22f04-160">Per inviare un processo, usare la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="22f04-160">Use the following syntax to submit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="22f04-161">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="22f04-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="22f04-162">**Per elencare i processi e visualizzarne i dettagli**</span><span class="sxs-lookup"><span data-stu-id="22f04-162">**To list jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="22f04-163">**Per annullare processi**</span><span class="sxs-lookup"><span data-stu-id="22f04-163">**To cancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="22f04-164">Recuperare i risultati di un processo</span><span class="sxs-lookup"><span data-stu-id="22f04-164">Retrieve job results</span></span>

<span data-ttu-id="22f04-165">Al termine di un processo, è possibile usare i comandi seguenti per elencare i file di output e scaricare i file:</span><span class="sxs-lookup"><span data-stu-id="22f04-165">After a job is completed, you can use the following commands to list the output files, and download the files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="22f04-166">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="22f04-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="22f04-167">Pipeline e ricorrenze</span><span class="sxs-lookup"><span data-stu-id="22f04-167">Pipelines and recurrences</span></span>

<span data-ttu-id="22f04-168">**Ottenere informazioni su pipeline e ricorrenze**</span><span class="sxs-lookup"><span data-stu-id="22f04-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="22f04-169">Usare i comandi `az dla job pipeline` per visualizzare le informazioni relative alle pipeline per i processi inviati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="22f04-169">Use the `az dla job pipeline` commands to see the pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="22f04-170">Usare i comandi `az dla job recurrence` per visualizzare le informazioni relative alle ricorrenze per i processi inviati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="22f04-170">Use the `az dla job recurrence` commands to see the recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="22f04-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22f04-171">Next steps</span></span>

* <span data-ttu-id="22f04-172">Per il documento di riferimento dell'interfaccia della riga di comando di Data Lake Analytics 2.0, vedere [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="22f04-172">To see the Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="22f04-173">Per il documento di riferimento dell'interfaccia della riga di comando di Data Lake Store 2.0, vedere [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="22f04-173">To see the Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="22f04-174">Per visualizzare una query più complessa, vedere [Analizzare i log del sito Web mediante Analisi Data Lake di Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="22f04-174">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
