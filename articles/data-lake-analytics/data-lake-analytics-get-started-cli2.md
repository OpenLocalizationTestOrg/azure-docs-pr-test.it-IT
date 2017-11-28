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
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="368da-103">Introduzione ad Azure Data Lake Analytics con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="368da-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="368da-104">In questa esercitazione verrà sviluppato un processo che legge un file con valori delimitati da tabulazioni (TSV) e lo converte in un file con valori delimitati da virgole (CSV).</span><span class="sxs-lookup"><span data-stu-id="368da-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="368da-105">toogo tramite hello supportato stesso esercitazione usare altri strumenti, elenco a discesa hello in primo piano hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="368da-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="368da-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="368da-106">Prerequisites</span></span>
<span data-ttu-id="368da-107">Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="368da-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="368da-108">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="368da-108">**An Azure subscription**.</span></span> <span data-ttu-id="368da-109">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="368da-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="368da-110">**Interfaccia della riga di comando di Azure 2.0**.</span><span class="sxs-lookup"><span data-stu-id="368da-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="368da-111">Vedere [Installare e configurare l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="368da-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="368da-112">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="368da-112">Log in tooAzure</span></span>

<span data-ttu-id="368da-113">toolog in tooyour sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="368da-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="368da-114">Si sono toobrowse richiesto tooa URL e immettere un codice di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="368da-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="368da-115">E quindi seguire hello istruzioni tooenter le credenziali.</span><span class="sxs-lookup"><span data-stu-id="368da-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="368da-116">Dopo aver eseguito l'accesso, il comando di accesso hello Elenca le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="368da-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="368da-117">toouse una sottoscrizione specifica:</span><span class="sxs-lookup"><span data-stu-id="368da-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="368da-118">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="368da-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="368da-119">Per poter eseguire un processo è necessario un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="368da-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="368da-120">toocreate un account Data Lake Analitica, è necessario specificare hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="368da-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="368da-121">**Gruppo di risorse di Azure**.</span><span class="sxs-lookup"><span data-stu-id="368da-121">**Azure Resource Group**.</span></span> <span data-ttu-id="368da-122">L'account Data Lake Analytics deve essere creato all'interno di un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="368da-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="368da-123">[Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md) consente toowork con risorse hello dell'applicazione come un gruppo.</span><span class="sxs-lookup"><span data-stu-id="368da-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="368da-124">È possibile distribuire, aggiornare o eliminare tutte le risorse di hello per l'applicazione in un'operazione singola, coordinata.</span><span class="sxs-lookup"><span data-stu-id="368da-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="368da-125">toolist hello gruppi di risorse esistenti nella sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="368da-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="368da-126">toocreate un nuovo gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="368da-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="368da-127">**Nome dell'account Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="368da-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="368da-128">Ogni account Data Lake Analytics ha un nome.</span><span class="sxs-lookup"><span data-stu-id="368da-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="368da-129">**Località**.</span><span class="sxs-lookup"><span data-stu-id="368da-129">**Location**.</span></span> <span data-ttu-id="368da-130">Utilizzare uno dei hello data center di Azure che supporta Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="368da-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="368da-131">**Account Data Lake Store predefinito**: ogni account Data Lake Analytics ha un account Data Lake Store predefinito.</span><span class="sxs-lookup"><span data-stu-id="368da-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="368da-132">account toolist hello esistente archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="368da-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="368da-133">toocreate un nuovo account archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="368da-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="368da-134">Utilizzare hello segue sintassi toocreate un account Data Lake Analitica:</span><span class="sxs-lookup"><span data-stu-id="368da-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="368da-135">Dopo aver creato un account, è possibile utilizzare hello seguendo gli account di comandi toolist hello e visualizzare i dettagli dell'account:</span><span class="sxs-lookup"><span data-stu-id="368da-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="368da-136">Carica archivio data Lake di tooData</span><span class="sxs-lookup"><span data-stu-id="368da-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="368da-137">In questa esercitazione verrà eseguita l'elaborazione di alcuni log di ricerca.</span><span class="sxs-lookup"><span data-stu-id="368da-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="368da-138">Hello ricerca log può essere archiviato nell'archivio Data Lake o archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="368da-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="368da-139">Hello portale di Azure fornisce un'interfaccia utente per la copia di un esempio dati file toohello archivio Data Lake account predefinito, che includono un file di log di ricerca.</span><span class="sxs-lookup"><span data-stu-id="368da-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="368da-140">Vedere [preparare i dati di origine](data-lake-analytics-get-started-portal.md) account archivio Data Lake di tooupload hello dati toohello predefinito.</span><span class="sxs-lookup"><span data-stu-id="368da-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="368da-141">file tooupload utilizzando 2.0 CLI, utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="368da-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="368da-142">Data Lake Analytics può inoltre accedere all'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="368da-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="368da-143">Per il caricamento di archiviazione Blob di dati tooAzure, vedere [Using hello CLI di Azure con l'archiviazione di Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="368da-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="368da-144">Inviare processi di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="368da-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="368da-145">i processi di Data Lake Analitica Hello vengono scritti in hello linguaggio U-SQL.</span><span class="sxs-lookup"><span data-stu-id="368da-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="368da-146">toolearn ulteriori informazioni su U-SQL, vedere [introduzione U-SQL language](data-lake-analytics-u-sql-get-started.md) e [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="368da-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="368da-147">**script per un processo Data Lake Analitica toocreate**</span><span class="sxs-lookup"><span data-stu-id="368da-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="368da-148">Creare un file di testo con script U-SQL seguente e salvare workstation di tooyour file testo hello:</span><span class="sxs-lookup"><span data-stu-id="368da-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

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

<span data-ttu-id="368da-149">Questo script U-SQL legge hello origine dati file utilizzando **Extractors.Tsv()**e quindi crea un file csv utilizzando **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="368da-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="368da-150">Non modificare due percorsi hello, a meno che non si copia il file di origine hello in un percorso diverso.</span><span class="sxs-lookup"><span data-stu-id="368da-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="368da-151">Data Lake Analitica Crea cartella di output di hello se non esiste.</span><span class="sxs-lookup"><span data-stu-id="368da-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="368da-152">È più semplice toouse i percorsi relativi per i file archiviati in account archivio Data Lake predefiniti.</span><span class="sxs-lookup"><span data-stu-id="368da-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="368da-153">è possibile usare anche percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="368da-153">You can also use absolute paths.</span></span>  <span data-ttu-id="368da-154">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="368da-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="368da-155">È necessario utilizzare i file di percorsi assoluti tooaccess negli account di archiviazione collegato.</span><span class="sxs-lookup"><span data-stu-id="368da-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="368da-156">sintassi di Hello per i file archiviati in account di archiviazione di Azure collegato è:</span><span class="sxs-lookup"><span data-stu-id="368da-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="368da-157">Il contenitore BLOB di Azure con BLOB pubblici non è supportato.</span><span class="sxs-lookup"><span data-stu-id="368da-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="368da-158">Il contenitore BLOB di Azure con contenitori pubblici non è supportato.</span><span class="sxs-lookup"><span data-stu-id="368da-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="368da-159">**processi toosubmit**</span><span class="sxs-lookup"><span data-stu-id="368da-159">**toosubmit jobs**</span></span>

<span data-ttu-id="368da-160">Utilizzare hello segue sintassi toosubmit un processo.</span><span class="sxs-lookup"><span data-stu-id="368da-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="368da-161">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="368da-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="368da-162">**i processi toolist e Mostra i dettagli dei processi**</span><span class="sxs-lookup"><span data-stu-id="368da-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="368da-163">**processi toocancel**</span><span class="sxs-lookup"><span data-stu-id="368da-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="368da-164">Recuperare i risultati di un processo</span><span class="sxs-lookup"><span data-stu-id="368da-164">Retrieve job results</span></span>

<span data-ttu-id="368da-165">Al termine di un processo, è possibile utilizzare i seguenti file di output di comandi toolist hello hello e scaricare file hello:</span><span class="sxs-lookup"><span data-stu-id="368da-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="368da-166">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="368da-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="368da-167">Pipeline e ricorrenze</span><span class="sxs-lookup"><span data-stu-id="368da-167">Pipelines and recurrences</span></span>

<span data-ttu-id="368da-168">**Ottenere informazioni su pipeline e ricorrenze**</span><span class="sxs-lookup"><span data-stu-id="368da-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="368da-169">Hello utilizzare `az dla job pipeline` comandi informazioni sulle pipeline di hello toosee i processi inviati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="368da-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="368da-170">Hello utilizzare `az dla job recurrence` comandi toosee le informazioni sull'occorrenza hello per i processi inviati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="368da-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="368da-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="368da-171">Next steps</span></span>

* <span data-ttu-id="368da-172">hello toosee documento di riferimento Data Lake Analitica CLI 2.0, vedere [Data Lake Analitica](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="368da-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="368da-173">hello toosee documento di riferimento Data Lake archivio CLI 2.0, vedere [archivio Data Lake](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="368da-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="368da-174">toosee una query più complessa, vedere [sito Web di analizzare i log di Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="368da-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
