---
title: Usare PowerShell per iniziare a usare Azure Data Lake Store | Documentazione Microsoft
description: Usare Azure PowerShell per creare un account di Data Lake Store ed eseguire operazioni di base
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 23c9aaa089251bff5132652475f4daadc2c128fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="f90a7-103">Introduzione all'archivio Azure Data Lake mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f90a7-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f90a7-104">Portale</span><span class="sxs-lookup"><span data-stu-id="f90a7-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="f90a7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f90a7-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="f90a7-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="f90a7-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="f90a7-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="f90a7-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="f90a7-108">API REST</span><span class="sxs-lookup"><span data-stu-id="f90a7-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="f90a7-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f90a7-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="f90a7-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="f90a7-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="f90a7-111">Python</span><span class="sxs-lookup"><span data-stu-id="f90a7-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="f90a7-112">Informazioni su come usare Azure PowerShell per creare un account di Azure Data Lake Store ed eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare i file di dati, eliminare l'account e così via. Per altre informazioni su Data Lake Store, vedere [Panoramica di Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f90a7-112">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f90a7-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f90a7-113">Prerequisites</span></span>
<span data-ttu-id="f90a7-114">Prima di iniziare questa esercitazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f90a7-114">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="f90a7-115">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f90a7-115">**An Azure subscription**.</span></span> <span data-ttu-id="f90a7-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f90a7-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f90a7-117">**Azure PowerShell 1.0 o versioni successive**.</span><span class="sxs-lookup"><span data-stu-id="f90a7-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="f90a7-118">Vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f90a7-118">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="f90a7-119">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="f90a7-119">Authentication</span></span>
<span data-ttu-id="f90a7-120">Questo articolo usa un approccio di autenticazione più semplice con Data Lake Store con cui viene richiesto di immettere le credenziali del proprio account di Azure.</span><span class="sxs-lookup"><span data-stu-id="f90a7-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="f90a7-121">Il livello di accesso al file system e all'account Data Lake Store viene quindi regolato dal livello di accesso dell'utente connesso.</span><span class="sxs-lookup"><span data-stu-id="f90a7-121">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="f90a7-122">Esistono tuttavia altri approcci oltre all'autenticazione con Data Lake Store, ad esempio l'**autenticazione dell'utente finale** o l'**autenticazione da servizio a servizio**.</span><span class="sxs-lookup"><span data-stu-id="f90a7-122">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="f90a7-123">Per altre informazioni e istruzioni su come eseguire l'autenticazione, vedere [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticazione da servizio a servizio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="f90a7-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="f90a7-124">Creare un account di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f90a7-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="f90a7-125">Dal desktop aprire una nuova finestra di Windows PowerShell e immettere il seguente frammento per accedere al proprio account di Azure, impostare la sottoscrizione e registrare il provider di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f90a7-125">From your desktop, open a new Windows PowerShell window, and enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span></span> <span data-ttu-id="f90a7-126">Quando viene richiesto di effettuare l'accesso, assicurarsi di accedere come amministratore/proprietario della sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="f90a7-126">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="f90a7-127">Un account di Archivio Azure Data Lake è associato a un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f90a7-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="f90a7-128">Per iniziare, creare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f90a7-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="f90a7-129">![Creare un gruppo di risorse di Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span><span class="sxs-lookup"><span data-stu-id="f90a7-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="f90a7-130">Creare un account di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f90a7-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="f90a7-131">Il nome specificato deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="f90a7-131">The name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="f90a7-132">![Creare un account di Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span><span class="sxs-lookup"><span data-stu-id="f90a7-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="f90a7-133">Verificare che l'account sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="f90a7-133">Verify that the account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="f90a7-134">L'output di questa operazione deve essere **True**.</span><span class="sxs-lookup"><span data-stu-id="f90a7-134">The output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="f90a7-135">Creare strutture di directory in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f90a7-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="f90a7-136">È possibile creare una directory con il proprio account di Azure Data Lake Store per gestire e archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="f90a7-136">You can create directories under your Azure Data Lake Store account to manage and store data.</span></span>

1. <span data-ttu-id="f90a7-137">Specificare una directory radice.</span><span class="sxs-lookup"><span data-stu-id="f90a7-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="f90a7-138">Creare una nuova directory denominata **mynewdirectory** sotto la radice specificata.</span><span class="sxs-lookup"><span data-stu-id="f90a7-138">Create a new directory called **mynewdirectory** under the specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="f90a7-139">Verificare che la nuova directory sia stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="f90a7-139">Verify that the new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="f90a7-140">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f90a7-140">It should show an output like the following:</span></span>

    <span data-ttu-id="f90a7-141">![Verificare la directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span><span class="sxs-lookup"><span data-stu-id="f90a7-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-to-your-azure-data-lake-store"></a><span data-ttu-id="f90a7-142">Caricare dati in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f90a7-142">Upload data to your Azure Data Lake Store</span></span>
<span data-ttu-id="f90a7-143">È possibile caricare i dati in Data Lake Store direttamente a livello di radice o in una directory creata all'interno dell'account.</span><span class="sxs-lookup"><span data-stu-id="f90a7-143">You can upload your data to Data Lake Store directly at the root level or to a directory that you created within the account.</span></span> <span data-ttu-id="f90a7-144">I frammenti di codice riportati di seguito illustrano come caricare alcuni dati di esempio nella directory (**mynewdirectory**) creata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="f90a7-144">The snippets below demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span></span>

<span data-ttu-id="f90a7-145">Se si stanno cercando dati di esempio da caricare, è possibile ottenere la cartella **Ambulance Data** dal [Repository GitHub per Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="f90a7-145">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="f90a7-146">Scaricare il file e archiviarlo in una directory locale nel computer, ad esempio C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="f90a7-146">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="f90a7-147">Rinominare, scaricare ed eliminare i dati da Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f90a7-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="f90a7-148">Per rinominare un file, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90a7-148">To rename a file, use the following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="f90a7-149">Per scaricare un file, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90a7-149">To download a file, use the following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="f90a7-150">Per eliminare un file, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f90a7-150">To delete a file, use the following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="f90a7-151">Quando viene richiesto, immettere **Y** per eliminare l'elemento.</span><span class="sxs-lookup"><span data-stu-id="f90a7-151">When prompted, enter **Y** to delete the item.</span></span> <span data-ttu-id="f90a7-152">Se sono presenti più file da eliminare, è possibile fornire tutti i percorsi separati da una virgola.</span><span class="sxs-lookup"><span data-stu-id="f90a7-152">If you have more than one file to delete, you can provide all the paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="f90a7-153">Eliminare l'account di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f90a7-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="f90a7-154">Usare il comando seguente per eliminare l'account di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f90a7-154">Use the following command to delete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="f90a7-155">Quando viene richiesto, immettere **Y** per eliminare l'account.</span><span class="sxs-lookup"><span data-stu-id="f90a7-155">When prompted, enter **Y** to delete the account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="f90a7-156">Linee guida sulle prestazioni durante l'uso di PowerShell</span><span class="sxs-lookup"><span data-stu-id="f90a7-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="f90a7-157">Di seguito sono indicate le impostazioni più importanti che possono essere ottimizzate per ottenere le migliori prestazioni durante l'uso di PowerShell con Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="f90a7-157">Below are the most important settings that can be tuned to get the best performance while using PowerShell to work with Data Lake Store:</span></span>

| <span data-ttu-id="f90a7-158">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f90a7-158">Property</span></span>            | <span data-ttu-id="f90a7-159">Default</span><span class="sxs-lookup"><span data-stu-id="f90a7-159">Default</span></span> | <span data-ttu-id="f90a7-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f90a7-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="f90a7-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="f90a7-161">PerFileThreadCount</span></span>  | <span data-ttu-id="f90a7-162">10</span><span class="sxs-lookup"><span data-stu-id="f90a7-162">10</span></span>      | <span data-ttu-id="f90a7-163">Questo parametro consente di scegliere il numero di thread paralleli per il caricamento o il download di ogni file.</span><span class="sxs-lookup"><span data-stu-id="f90a7-163">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="f90a7-164">Questo valore rappresenta il numero massimo di thread che può essere allocato per ogni file, ma è possibile ottenere meno thread a seconda dello scenario (ad esempio, se si sta caricando un file da 1 KB, si otterrà un thread anche se si chiedono 20 thread).</span><span class="sxs-lookup"><span data-stu-id="f90a7-164">This number represents the max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="f90a7-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="f90a7-165">ConcurrentFileCount</span></span> | <span data-ttu-id="f90a7-166">10</span><span class="sxs-lookup"><span data-stu-id="f90a7-166">10</span></span>      | <span data-ttu-id="f90a7-167">Questo parametro viene usato specificamente per il caricamento e il download delle cartelle.</span><span class="sxs-lookup"><span data-stu-id="f90a7-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="f90a7-168">Questo parametro determina il numero di file che possono essere caricati o scaricati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="f90a7-168">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="f90a7-169">Questo valore rappresenta il numero massimo di file che possono essere caricati o scaricati contemporaneamente in una sola volta, ma è possibile ottenere un valore inferiore di concorrenza a seconda dello scenario (ad esempio, se si caricano due file, si otterrà il caricamento di due file contemporaneamente anche se ne vengono richiesti 15).</span><span class="sxs-lookup"><span data-stu-id="f90a7-169">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="f90a7-170">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="f90a7-170">**Example**</span></span>

<span data-ttu-id="f90a7-171">Questo comando scarica i file da Azure Data Lake Store al disco locale dell'utente usando 20 thread per file e 100 file contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="f90a7-171">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-the-value-to-set-for-these-parameters"></a><span data-ttu-id="f90a7-172">Come è possibile determinare il valore da impostare per questi parametri?</span><span class="sxs-lookup"><span data-stu-id="f90a7-172">How do I determine the value to set for these parameters?</span></span>

<span data-ttu-id="f90a7-173">Ecco alcune linee guida che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="f90a7-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="f90a7-174">**Passaggio 1: Determinare il numero totale di thread** - È consigliabile iniziare calcolando il numero totale di thread da usare.</span><span class="sxs-lookup"><span data-stu-id="f90a7-174">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span></span> <span data-ttu-id="f90a7-175">Come regola generale, è consigliabile usare 6 thread per ogni core fisico.</span><span class="sxs-lookup"><span data-stu-id="f90a7-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="f90a7-176">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="f90a7-176">**Example**</span></span>

    <span data-ttu-id="f90a7-177">Supponendo che si eseguano i comandi PowerShell da una macchina virtuale D14 con 16 core</span><span class="sxs-lookup"><span data-stu-id="f90a7-177">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="f90a7-178">**Passaggio 2: Calcolare PerFileThreadCount** - Viene calcolato il parametro PerFileThreadCount in base alla dimensione dei file.</span><span class="sxs-lookup"><span data-stu-id="f90a7-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span></span> <span data-ttu-id="f90a7-179">Per i file di dimensioni inferiori a 2,5 GB, non è necessario modificare questo parametro, perché il valore predefinito di 10 è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="f90a7-179">For files smaller than 2.5GB, there is no need to change this parameter because the default of 10 is sufficient.</span></span> <span data-ttu-id="f90a7-180">Per i file di dimensioni superiori a 2,5 GB, è necessario usare 10 thread come base per i primi 2,5 GB e aggiungere 1 thread per ogni incremento aggiuntivo di 256 MB alle dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="f90a7-180">For files larger than 2.5GB, you should use 10 threads as the base for the first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="f90a7-181">Se si copia una cartella con un'ampia gamma di dimensioni dei file, è consigliabile raggrupparle in file di dimensioni simili.</span><span class="sxs-lookup"><span data-stu-id="f90a7-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="f90a7-182">Il raggruppamento in file di dimensioni diverse può comportare prestazioni non ottimali.</span><span class="sxs-lookup"><span data-stu-id="f90a7-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="f90a7-183">Se non è possibile raggruppare file di dimensioni simili, è necessario impostare PerFileThreadCount in base alle dimensioni del file più grande.</span><span class="sxs-lookup"><span data-stu-id="f90a7-183">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span></span>

        PerFileThreadCount = 10 threads for the first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="f90a7-184">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="f90a7-184">**Example**</span></span>

    <span data-ttu-id="f90a7-185">Se si dispone di 100 file da 1 GB a 10 GB, viene usata la dimensione di 10 GB come riferimento per l'equazione, interpretata come segue.</span><span class="sxs-lookup"><span data-stu-id="f90a7-185">Assuming you have 100 files ranging from 1GB to 10GB, we use the 10GB as the largest file size for equation, which would read like the following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="f90a7-186">**Passaggio 3: Calcolare ConcurrentFilecount** - Usare il numero totale di thread e PerFileThreadCount per calcolare ConcurrentFileCount in base all'equazione seguente.</span><span class="sxs-lookup"><span data-stu-id="f90a7-186">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="f90a7-187">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="f90a7-187">**Example**</span></span>

    <span data-ttu-id="f90a7-188">In base ai valori di esempio usati</span><span class="sxs-lookup"><span data-stu-id="f90a7-188">Based on the example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="f90a7-189">Pertanto, **ConcurrentFileCount** è **2.4**, che è possibile arrotondare a **2**.</span><span class="sxs-lookup"><span data-stu-id="f90a7-189">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="f90a7-190">Ottimizzazione ulteriore</span><span class="sxs-lookup"><span data-stu-id="f90a7-190">Further tuning</span></span>

<span data-ttu-id="f90a7-191">È possibile richiedere un'ulteriore ottimizzazione perché è presente un intervallo di dimensioni di file da usare.</span><span class="sxs-lookup"><span data-stu-id="f90a7-191">You might require further tuning because there is a range of file sizes to work with.</span></span> <span data-ttu-id="f90a7-192">Il calcolo precedente funziona bene se tutti o la maggior parte dei file è più grande e più vicina all'intervallo di 10 GB.</span><span class="sxs-lookup"><span data-stu-id="f90a7-192">The above calculation works well if all or most of the files are larger and closer to the 10GB range.</span></span> <span data-ttu-id="f90a7-193">Se invece sono presenti diverse dimensioni di file con molti file più piccoli, è possibile ridurre PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="f90a7-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="f90a7-194">Riducendo PerFileThreadCount, è possibile aumentare il valore di ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="f90a7-194">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="f90a7-195">Pertanto, se si presume che la maggior parte dei file è minore dell'intervallo di 5 GB, è possibile eseguire nuovamente il calcolo:</span><span class="sxs-lookup"><span data-stu-id="f90a7-195">So, if we assume that most of our files are smaller in the 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="f90a7-196">Pertanto, **ConcurrentFileCount** avrà un valore di 96/20, ovvero 4,8, arrotondato a **4**.</span><span class="sxs-lookup"><span data-stu-id="f90a7-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off to **4**.</span></span>

<span data-ttu-id="f90a7-197">È possibile continuare a ottimizzare le impostazioni modificando il valore di **PerFileThreadCount** in base alla distribuzione delle dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="f90a7-197">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="f90a7-198">Limitazione</span><span class="sxs-lookup"><span data-stu-id="f90a7-198">Limitation</span></span>

* <span data-ttu-id="f90a7-199">**Numero di file minore di ConcurrentFileCount**: se il numero di file che si sta caricando è minore del valore di **ConcurrentFileCount** calcolato, è necessario ridurre **ConcurrentFileCount** in modo che risulti uguale al numero di file.</span><span class="sxs-lookup"><span data-stu-id="f90a7-199">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span></span> <span data-ttu-id="f90a7-200">È possibile usare i thread rimanenti per aumentare **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="f90a7-200">You can use any remaining threads to increase **PerFileThreadCount**.</span></span>

* <span data-ttu-id="f90a7-201">**Troppi thread**: se si aumenta il numero dei thread in maniera eccessiva senza aumentare le dimensioni del cluster, si corre il rischio di ridurre le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="f90a7-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span></span> <span data-ttu-id="f90a7-202">È possibile che si verifichino problemi di conflitto dovuti al cambio di contesto nella CPU.</span><span class="sxs-lookup"><span data-stu-id="f90a7-202">There can be contention issues when context-switching on the CPU.</span></span>

* <span data-ttu-id="f90a7-203">**Concorrenza insufficiente**: se la concorrenza non è sufficiente, è possibile che il cluster sia troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="f90a7-203">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="f90a7-204">È possibile aumentare il numero di nodi del cluster in modo da avere maggiore concorrenza.</span><span class="sxs-lookup"><span data-stu-id="f90a7-204">You can increase the number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="f90a7-205">**Errori di limitazione**: se la concorrenza è troppo elevata, è possibile che vengano visualizzati errori di limitazione.</span><span class="sxs-lookup"><span data-stu-id="f90a7-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="f90a7-206">Se si riscontrano errori di limitazione, è necessario ridurre la concorrenza o contattare Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f90a7-206">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f90a7-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f90a7-207">Next steps</span></span>
* [<span data-ttu-id="f90a7-208">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f90a7-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="f90a7-209">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f90a7-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="f90a7-210">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f90a7-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

