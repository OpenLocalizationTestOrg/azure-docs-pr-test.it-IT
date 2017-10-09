---
title: aaaUse PowerShell tooget avviato con l'archivio Azure Data Lake | Documenti Microsoft
description: Usare Azure PowerShell toocreate un account archivio Data Lake ed eseguire operazioni di base
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
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="b253f-103">Introduzione all'archivio Azure Data Lake mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b253f-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b253f-104">Portale</span><span class="sxs-lookup"><span data-stu-id="b253f-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="b253f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b253f-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="b253f-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="b253f-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="b253f-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="b253f-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="b253f-108">API REST</span><span class="sxs-lookup"><span data-stu-id="b253f-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="b253f-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b253f-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="b253f-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="b253f-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="b253f-111">Python</span><span class="sxs-lookup"><span data-stu-id="b253f-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="b253f-112">Informazioni sulla modalità di memorizzazione una Data Lake di Azure di toouse Azure PowerShell toocreate account e di eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare file di dati, eliminare l'account, e così via. Per altre informazioni su Data Lake Store, vedere [Panoramica di Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b253f-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b253f-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b253f-113">Prerequisites</span></span>
<span data-ttu-id="b253f-114">Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="b253f-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="b253f-115">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="b253f-115">**An Azure subscription**.</span></span> <span data-ttu-id="b253f-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b253f-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b253f-117">**Azure PowerShell 1.0 o versioni successive**.</span><span class="sxs-lookup"><span data-stu-id="b253f-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="b253f-118">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b253f-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="b253f-119">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="b253f-119">Authentication</span></span>
<span data-ttu-id="b253f-120">In questo articolo utilizza un approccio più semplice di autenticazione con archivio Data Lake in cui ti trovi tooenter richieste le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="b253f-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="b253f-121">Hello accesso livello tooData Lake archivio account file system e quindi è disciplinato dal livello di accesso hello di hello utente connesso.</span><span class="sxs-lookup"><span data-stu-id="b253f-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="b253f-122">Tuttavia, esistono altri approcci come ben tooauthenticate con archivio Data Lake, che sono **autenticazione dell'utente finale** o **authentication service to service**.</span><span class="sxs-lookup"><span data-stu-id="b253f-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="b253f-123">Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b253f-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="b253f-124">Creare un account di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b253f-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="b253f-125">Dal desktop, aprire una nuova finestra di Windows PowerShell e immettere hello seguente frammento di codice toolog in tooyour account Azure, impostare la sottoscrizione hello e registrare il provider di archivio Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="b253f-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="b253f-126">Quando richiesto toolog, assicurarsi che si accede con uno dei hello admininistrators/proprietario della sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="b253f-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="b253f-127">Un account di Archivio Azure Data Lake è associato a un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b253f-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="b253f-128">Per iniziare, creare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b253f-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="b253f-129">![Creare un gruppo di risorse di Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span><span class="sxs-lookup"><span data-stu-id="b253f-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="b253f-130">Creare un account Archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b253f-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="b253f-131">specificare nome Hello deve contenere solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="b253f-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="b253f-132">![Creare un account di Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span><span class="sxs-lookup"><span data-stu-id="b253f-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="b253f-133">Verificare che account hello è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b253f-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="b253f-134">deve trattarsi di output di Hello **True**.</span><span class="sxs-lookup"><span data-stu-id="b253f-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="b253f-135">Creare strutture di directory in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b253f-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="b253f-136">È possibile creare le directory sotto la toomanage account archivio Azure Data Lake e archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="b253f-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="b253f-137">Specificare una directory radice.</span><span class="sxs-lookup"><span data-stu-id="b253f-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="b253f-138">Creare una nuova directory denominata **mynewdirectory** sotto la radice specificata hello.</span><span class="sxs-lookup"><span data-stu-id="b253f-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="b253f-139">Verificare che la nuova directory hello viene creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="b253f-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="b253f-140">Dovrebbe visualizzare un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b253f-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="b253f-141">![Verificare la directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span><span class="sxs-lookup"><span data-stu-id="b253f-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="b253f-142">Caricare l'archivio dati tooyour Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b253f-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="b253f-143">È possibile caricare l'archivio data Lake di tooData direttamente in hello livello o tooa directory radice che è stato creato all'interno di account hello.</span><span class="sxs-lookup"><span data-stu-id="b253f-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="b253f-144">Hello i frammenti di codice riportato di seguito viene illustrato come tooupload alcune directory toohello dati di esempio (**mynewdirectory**) creata nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b253f-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="b253f-145">Se si sta cercando alcuni tooupload di dati di esempio, è possibile ottenere hello **dati ambulanza** cartella hello [Git Repository di Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="b253f-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="b253f-146">Scaricare il file hello e archiviarlo in una directory locale nel computer in uso, ad esempio C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="b253f-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="b253f-147">Rinominare, scaricare ed eliminare i dati da Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b253f-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="b253f-148">toorename un file, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b253f-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="b253f-149">toodownload un file, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b253f-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="b253f-150">toodelete un file, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b253f-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="b253f-151">Quando richiesto, immettere **Y** elemento hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="b253f-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="b253f-152">Se si dispone di più di un file toodelete, è possibile fornire tutti i percorsi di hello separati da virgola.</span><span class="sxs-lookup"><span data-stu-id="b253f-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="b253f-153">Eliminare l'account di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b253f-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="b253f-154">Utilizzare hello comando che segue toodelete account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b253f-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="b253f-155">Quando richiesto, immettere **Y** account hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="b253f-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="b253f-156">Linee guida sulle prestazioni durante l'uso di PowerShell</span><span class="sxs-lookup"><span data-stu-id="b253f-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="b253f-157">Di seguito è hello impostazioni più importanti che possono essere ottimizzate tooget hello ottenere prestazioni ottimali durante l'utilizzo di PowerShell toowork con archivio Data Lake:</span><span class="sxs-lookup"><span data-stu-id="b253f-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="b253f-158">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b253f-158">Property</span></span>            | <span data-ttu-id="b253f-159">Default</span><span class="sxs-lookup"><span data-stu-id="b253f-159">Default</span></span> | <span data-ttu-id="b253f-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b253f-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="b253f-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="b253f-161">PerFileThreadCount</span></span>  | <span data-ttu-id="b253f-162">10</span><span class="sxs-lookup"><span data-stu-id="b253f-162">10</span></span>      | <span data-ttu-id="b253f-163">Questo parametro consente di numero di hello toochoose di thread paralleli per caricare o scaricare ciascun file.</span><span class="sxs-lookup"><span data-stu-id="b253f-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="b253f-164">Questo numero rappresenta i thread max hello che possono essere allocati per ogni file, ma è possibile ottenere meno thread a seconda dello scenario (ad esempio, se si sta caricando un file di 1 KB, si otterrà un thread anche se richiede di 20 thread).</span><span class="sxs-lookup"><span data-stu-id="b253f-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="b253f-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="b253f-165">ConcurrentFileCount</span></span> | <span data-ttu-id="b253f-166">10</span><span class="sxs-lookup"><span data-stu-id="b253f-166">10</span></span>      | <span data-ttu-id="b253f-167">Questo parametro viene usato specificamente per il caricamento e il download delle cartelle.</span><span class="sxs-lookup"><span data-stu-id="b253f-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="b253f-168">Questo parametro determina il numero di hello di file simultanei che possono essere caricate o scaricate.</span><span class="sxs-lookup"><span data-stu-id="b253f-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="b253f-169">Questo numero rappresenta hello il numero massimo di file simultanei che possono essere caricati o scaricati in una sola volta, ma è possibile ottenere inferiore di concorrenza a seconda dello scenario (ad esempio, se si siano caricando due file, si otterranno due caricamenti di file simultanee, anche se si richiede 15).</span><span class="sxs-lookup"><span data-stu-id="b253f-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="b253f-170">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="b253f-170">**Example**</span></span>

<span data-ttu-id="b253f-171">Questo comando Scarica i file da un'unità locale di archivio Azure Data Lake toohello utente tramite 20 thread per file e di 100 file simultanei.</span><span class="sxs-lookup"><span data-stu-id="b253f-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="b253f-172">Come è possibile determinare hello valore tooset per questi parametri?</span><span class="sxs-lookup"><span data-stu-id="b253f-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="b253f-173">Ecco alcune linee guida che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="b253f-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="b253f-174">**Passaggio 1: Determinare il numero totale di thread di hello** -è consigliabile iniziare il calcolo toouse numero totale di thread di hello.</span><span class="sxs-lookup"><span data-stu-id="b253f-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="b253f-175">Come regola generale, è consigliabile usare 6 thread per ogni core fisico.</span><span class="sxs-lookup"><span data-stu-id="b253f-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="b253f-176">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="b253f-176">**Example**</span></span>

    <span data-ttu-id="b253f-177">Presupponendo che si esegue PowerShell hello comandi da una macchina virtuale D14 con 16 core</span><span class="sxs-lookup"><span data-stu-id="b253f-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="b253f-178">**Passaggio 2: Calcolare PerFileThreadCount** -si calcola il nostro PerFileThreadCount in base alle dimensioni di hello dei file hello.</span><span class="sxs-lookup"><span data-stu-id="b253f-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="b253f-179">Per i file di dimensioni inferiori a 2,5 GB, sono non infatti toochange è necessario questo parametro hello valore predefinito di 10 è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="b253f-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="b253f-180">Per i file più grandi di 2,5 GB, è consigliabile utilizzare 10 thread come base hello per hello prima 2,5 GB e aggiungere 1 thread per ogni incremento di 256 MB aggiuntivi nelle dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="b253f-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="b253f-181">Se si copia una cartella con un'ampia gamma di dimensioni dei file, è consigliabile raggrupparle in file di dimensioni simili.</span><span class="sxs-lookup"><span data-stu-id="b253f-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="b253f-182">Il raggruppamento in file di dimensioni diverse può comportare prestazioni non ottimali.</span><span class="sxs-lookup"><span data-stu-id="b253f-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="b253f-183">Se non è possibile toogroup dimensioni del file simile, è necessario impostare PerFileThreadCount in base alle dimensioni del file hello più grande.</span><span class="sxs-lookup"><span data-stu-id="b253f-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="b253f-184">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="b253f-184">**Example**</span></span>

    <span data-ttu-id="b253f-185">Se che si dispone di 100 file compreso tra 1GB too10GB, utilizziamo hello dimensioni per l'equazione, leggerà hello seguente del file di 10GB come hello più grande.</span><span class="sxs-lookup"><span data-stu-id="b253f-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="b253f-186">**Passaggio 3: Calcolare ConcurrentFilecount** -utilizza il numero totale di thread di hello e PerFileThreadCount toocalculate ConcurrentFileCount basati su hello seguente equazione.</span><span class="sxs-lookup"><span data-stu-id="b253f-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="b253f-187">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="b253f-187">**Example**</span></span>

    <span data-ttu-id="b253f-188">In base ai valori di esempio hello che utilizziamo</span><span class="sxs-lookup"><span data-stu-id="b253f-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="b253f-189">In tal caso, **ConcurrentFileCount** è **2.4**, che è possibile arrotondare troppo**2**.</span><span class="sxs-lookup"><span data-stu-id="b253f-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="b253f-190">Ottimizzazione ulteriore</span><span class="sxs-lookup"><span data-stu-id="b253f-190">Further tuning</span></span>

<span data-ttu-id="b253f-191">È possibile richiedere un'ulteriore ottimizzazione perché è un intervallo di toowork le dimensioni dei file con.</span><span class="sxs-lookup"><span data-stu-id="b253f-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="b253f-192">Hello sopra calcolo funziona anche se tutte o la maggior parte dei file hello sono più grandi e più simili toohello intervallo di 10GB.</span><span class="sxs-lookup"><span data-stu-id="b253f-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="b253f-193">Se invece sono presenti diverse dimensioni di file con molti file più piccoli, è possibile ridurre PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="b253f-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="b253f-194">Grazie alla riduzione hello PerFileThreadCount, migliorare ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="b253f-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="b253f-195">In tal caso, se si suppone che la maggior parte di questo file sono più piccolo nell'intervallo di 5GB hello, è possibile eseguire nuovamente il calcolo:</span><span class="sxs-lookup"><span data-stu-id="b253f-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="b253f-196">In tal caso, **ConcurrentFileCount** verrà ora 96/20, vale a dire 4.8, arrotondata troppo**4**.</span><span class="sxs-lookup"><span data-stu-id="b253f-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="b253f-197">È possibile continuare tootune queste impostazioni modificando hello **PerFileThreadCount** verticale a seconda distribuzione hello delle dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="b253f-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="b253f-198">Limitazione</span><span class="sxs-lookup"><span data-stu-id="b253f-198">Limitation</span></span>

* <span data-ttu-id="b253f-199">**Numero di file è minore di ConcurrentFileCount**: se il numero di hello dei file che si sta caricando è minore di hello **ConcurrentFileCount** che è stato calcolato, quindi è necessario ridurre  **ConcurrentFileCount** toobe toohello uguale numero di file.</span><span class="sxs-lookup"><span data-stu-id="b253f-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="b253f-200">È possibile utilizzare qualsiasi esempio di thread rimanenti tooincrease **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="b253f-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="b253f-201">**Troppi thread**: se si aumenta thread conteggio troppa senza aumentare la dimensione del cluster, si corre il rischio di hello di riduzione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b253f-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="b253f-202">Possono esistere problemi di contesa durante il cambio di contesto su hello della CPU.</span><span class="sxs-lookup"><span data-stu-id="b253f-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="b253f-203">**Concorrenza insufficiente**: se la concorrenza hello non è sufficiente, quindi il cluster potrebbe essere troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="b253f-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="b253f-204">È possibile aumentare il numero di hello dei nodi del cluster in modo da maggiore concorrenza.</span><span class="sxs-lookup"><span data-stu-id="b253f-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="b253f-205">**Errori di limitazione**: se la concorrenza è troppo elevata, è possibile che vengano visualizzati errori di limitazione.</span><span class="sxs-lookup"><span data-stu-id="b253f-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="b253f-206">Se vengono visualizzati errori di limitazione, si deve ridurre concorrenza hello o contattare Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b253f-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b253f-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b253f-207">Next steps</span></span>
* [<span data-ttu-id="b253f-208">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b253f-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="b253f-209">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b253f-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="b253f-210">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b253f-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

