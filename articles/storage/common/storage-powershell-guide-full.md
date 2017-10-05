---
title: Uso di Azure PowerShell con Archiviazione di Azure | Microsoft Docs
description: Imparare a utilizzare i cmdlet PowerShell di Azure per l'archiviazione di Azure per creare e gestire gli account di archiviazione; lavorare con BLOB, tabelle, code e file. configurare analisi archiviazione di query e creare firme di accesso condiviso.
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 87a116111d085fe2913bf6f5f8751c3ff5f3c076
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="46b33-103">Uso di Azure PowerShell con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="46b33-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="46b33-104">Overview</span></span>
<span data-ttu-id="46b33-105">Azure PowerShell è un modulo che offre i cmdlet per gestire Azure tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46b33-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="46b33-106">Corrisponde a una shell della riga di comando basata su attività e un linguaggio di scripting progettato appositamente per l'amministrazione del sistema.</span><span class="sxs-lookup"><span data-stu-id="46b33-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="46b33-107">Con PowerShell è possibile controllare e automatizzare facilmente l'amministrazione dei servizi e delle applicazioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="46b33-108">È ad esempio possibile usare i cmdlet per eseguire le stesse attività eseguibili tramite il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="46b33-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="46b33-109">Questa guida illustra come usare i [cmdlet di Archiviazione di Azure](/powershell/module/azurerm.storage/#storage) per eseguire una serie di attività di sviluppo e di amministrazione con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="46b33-110">Nella guida si presuppone una certa esperienza nell'uso di [Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/) e [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="46b33-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="46b33-111">La guida fornisce diversi script che mostrano come usare PowerShell con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="46b33-112">Prima di eseguire gli script, è necessario aggiornarne le variabili in base alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="46b33-113">La prima sezione di questa guida fornisce una panoramica di Archiviazione di Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46b33-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="46b33-114">Per informazioni dettagliate e istruzioni, iniziare da [Prerequisiti per l'uso di Azure PowerShell con Archiviazione di Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="46b33-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="46b33-115">Introduzione ad Archiviazione di Azure e PowerShell in 5 minuti</span><span class="sxs-lookup"><span data-stu-id="46b33-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="46b33-116">Questa sezione descrive come accedere ad Archiviazione di Azure tramite PowerShell in 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="46b33-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="46b33-117">**Novità in Azure:** ottenere una sottoscrizione di Microsoft Azure e un account Microsoft associato alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="46b33-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="46b33-118">Per informazioni sulle opzioni di acquisto di Azure, vedere la [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/), le [opzioni di acquisto](https://azure.microsoft.com/pricing/purchase-options/) e le [offerte per i membri](https://azure.microsoft.com/pricing/member-offers/) (per i membri di MSDN, Microsoft Partner Network, BizSpark e altri programmi Microsoft).</span><span class="sxs-lookup"><span data-stu-id="46b33-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="46b33-119">Per altre informazioni sulle sottoscrizioni di Azure, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="46b33-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="46b33-120">**Dopo aver creato una sottoscrizione e un account di Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="46b33-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="46b33-121">Scaricare e installare la versione più recente di [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="46b33-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="46b33-122">Avviare Windows PowerShell Integrated Scripting Environment (ISE): Nel computer locale, passare al menù **Start** .</span><span class="sxs-lookup"><span data-stu-id="46b33-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="46b33-123">Digitare **Strumenti di amministrazione** e fare clic per eseguirli.</span><span class="sxs-lookup"><span data-stu-id="46b33-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="46b33-124">Nella finestra **Strumenti di amministrazione** fare clic con il pulsante destro del mouse su **Windows PowerShell ISE**, quindi scegliere **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="46b33-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="46b33-125">Nella finestra **Windows PowerShell ISE** fare clic su **File** > **Nuovo** per creare un nuovo file di script.</span><span class="sxs-lookup"><span data-stu-id="46b33-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="46b33-126">È disponibile a questo punto uno script semplice che mostra i comandi PowerShell di base per accedere ad Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="46b33-127">Lo script richiede innanzitutto le credenziali dell'account Azure per aggiungerlo all'ambiente PowerShell locale.</span><span class="sxs-lookup"><span data-stu-id="46b33-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="46b33-128">Lo script quindi imposta la sottoscrizione predefinita di Azure e crea un nuovo account di archiviazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="46b33-129">Lo script crea un nuovo contenitore in questo nuovo account di archiviazione e carica un file di immagine esistente (BLOB) in tale contenitore.</span><span class="sxs-lookup"><span data-stu-id="46b33-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="46b33-130">Dopo aver elencato tutti i BLOB nel contenitore, lo script crea una nuova directory di destinazione nel computer locale e scarica il file di immagine.</span><span class="sxs-lookup"><span data-stu-id="46b33-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="46b33-131">Nella sezione di codice riportata di seguito selezionare lo script tra **#begin** ed **#end**.</span><span class="sxs-lookup"><span data-stu-id="46b33-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="46b33-132">Premere CTRL+C per copiarlo negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="46b33-132">Press CTRL+C to copy it to the clipboard.</span></span>

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="46b33-133">In **Windows PowerShell ISE**, premere CTRL + V per copiare lo script.</span><span class="sxs-lookup"><span data-stu-id="46b33-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="46b33-134">Fare clic su **File** > **Salva**.</span><span class="sxs-lookup"><span data-stu-id="46b33-134">Click **File** > **Save**.</span></span> <span data-ttu-id="46b33-135">Nella finestra di dialogo **Salva con nome** digitare il nome del file di script, ad esempio "mystoragescript".</span><span class="sxs-lookup"><span data-stu-id="46b33-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="46b33-136">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="46b33-136">Click **Save**.</span></span>
7. <span data-ttu-id="46b33-137">A questo punto, è necessario aggiornare le variabili dello script in base alle impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="46b33-138">È necessario aggiornare la variabile **$SubscriptionName** con la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="46b33-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="46b33-139">È possibile mantenere le altre variabili come specificato nello script o aggiornarle secondo le proprie preferenze.</span><span class="sxs-lookup"><span data-stu-id="46b33-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="46b33-140">**$SubscriptionName:** è necessario aggiornare questa variabile con il proprio nome di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="46b33-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="46b33-141">Attenersi a uno dei tre modi seguenti per individuare il nome della sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="46b33-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="46b33-142">a.</span><span class="sxs-lookup"><span data-stu-id="46b33-142">a.</span></span> <span data-ttu-id="46b33-143">Nella finestra **Windows PowerShell ISE** fare clic su **File** > **Nuovo** per creare un nuovo file di script.</span><span class="sxs-lookup"><span data-stu-id="46b33-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="46b33-144">Copiare lo script seguente nel nuovo file di script e fare clic su **Debug** > **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="46b33-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="46b33-145">Lo script richiede innanzitutto le credenziali dell'account Azure per aggiungerlo all'ambiente PowerShell locale, quindi visualizza tutte le sottoscrizioni connesse alla sessione PowerShell locale.</span><span class="sxs-lookup"><span data-stu-id="46b33-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="46b33-146">Prendere nota del nome della sottoscrizione da usare durante questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="46b33-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="46b33-147">b.</span><span class="sxs-lookup"><span data-stu-id="46b33-147">b.</span></span> <span data-ttu-id="46b33-148">Per trovare e copiare il nome della sottoscrizione nel [portale di Azure](https://portal.azure.com), nel menu hub a sinistra fare clic su **Sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="46b33-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="46b33-149">Copiare il nome della sottoscrizione da usare durante l'esecuzione degli script specificati in questa guida.</span><span class="sxs-lookup"><span data-stu-id="46b33-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Portale di Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="46b33-151">c.</span><span class="sxs-lookup"><span data-stu-id="46b33-151">c.</span></span> <span data-ttu-id="46b33-152">Per individuare e copiare il nome della sottoscrizione nel [portale di Azure classico](https://manage.windowsazure.com/), scorrere verso il basso e fare clic su **Impostazioni** sul lato sinistro del portale.</span><span class="sxs-lookup"><span data-stu-id="46b33-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="46b33-153">Fare clic su **Sottoscrizioni** per visualizzare un elenco delle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="46b33-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="46b33-154">Copiare il nome della sottoscrizione da usare durante l'esecuzione degli script specificati in questa guida.</span><span class="sxs-lookup"><span data-stu-id="46b33-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![portale di Azure classico](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="46b33-156">**$StorageAccountName:** utilizzare il nome specificato nello script oppure immettere un nuovo nome per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="46b33-157">**Importante:** il nome dell'account di archiviazione deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="46b33-158">Utilizzare caratteri minuscoli.</span><span class="sxs-lookup"><span data-stu-id="46b33-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="46b33-159">**$Location:** utilizzare "West US" specificato nello script oppure scegliere altre posizioni di Azure, ad esempio Stati Uniti orientali, Europa settentrionale e così via.</span><span class="sxs-lookup"><span data-stu-id="46b33-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="46b33-160">**$ContainerName:** usare il nome specificato nello script oppure immettere un nuovo nome per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="46b33-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="46b33-161">**$ImageToUpload:** immettere il percorso di un'immagine nel computer locale, ad esempio "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="46b33-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="46b33-162">**$DestinationFolder:** immettere il percorso a una directory locale per archiviare i file scaricati da Archiviazione di Azure, ad esempio "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="46b33-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="46b33-163">Dopo aver aggiornato le variabili dello script nel file "mystoragescript.ps1", fare clic su **File** > **Salva**.</span><span class="sxs-lookup"><span data-stu-id="46b33-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="46b33-164">Fare clic su **Debug** > **Esegui** o premere **F5** per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="46b33-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="46b33-165">Dopo l'esecuzione dello script è necessario disporre di una cartella di destinazione locale che includa il file di immagine scaricato.</span><span class="sxs-lookup"><span data-stu-id="46b33-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="46b33-166">La schermata seguente mostra un output di esempio:</span><span class="sxs-lookup"><span data-stu-id="46b33-166">The following screenshot shows an example output:</span></span>

![Scaricare BLOB](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="46b33-168">La sezione "Introduzione ad Archiviazione di Azure e PowerShell in 5 minuti" fornisce un'introduzione rapida su come usare Azure PowerShell con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="46b33-169">Per informazioni dettagliate e istruzioni si consiglia di leggere le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="46b33-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="46b33-170">Prerequisiti per l'uso di Azure PowerShell con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="46b33-171">Sono necessari una sottoscrizione e un account di Azure per eseguire i cmdlet di PowerShell forniti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="46b33-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="46b33-172">Azure PowerShell è un modulo che offre i cmdlet per gestire Azure tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46b33-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="46b33-173">Per informazioni sull'installazione e sulla configurazione di Azure PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="46b33-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="46b33-174">Si consiglia di scaricare e installare oppure di aggiornare il modulo alla versione di Azure PowerShell più recente prima di usare questa guida.</span><span class="sxs-lookup"><span data-stu-id="46b33-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="46b33-175">È possibile eseguire i cmdlet nella console standard di Windows PowerShell o da Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="46b33-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="46b33-176">Per aprire **Windows PowerShell ISE**, nel menu Start digitare Strumenti di amministrazione e fare clic per eseguirli.</span><span class="sxs-lookup"><span data-stu-id="46b33-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="46b33-177">Nella finestra Strumenti di amministrazione fare clic con il pulsante destro del mouse su Windows PowerShell ISE, quindi scegliere Esegui come amministratore.</span><span class="sxs-lookup"><span data-stu-id="46b33-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="46b33-178">Come gestire gli account di archiviazione in Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="46b33-179">Di seguito è illustrata la gestione degli account di archiviazione in Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="46b33-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="46b33-180">Come impostare una sottoscrizione di Azure predefinita</span><span class="sxs-lookup"><span data-stu-id="46b33-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="46b33-181">Per gestire Archiviazione di Azure con Azure PowerShell è necessario eseguire l'autenticazione dell'ambiente client con Azure usando l'autenticazione di Azure Active Directory o l'autenticazione basata su certificato.</span><span class="sxs-lookup"><span data-stu-id="46b33-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="46b33-182">Per informazioni dettagliate, vedere il tutorial [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="46b33-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="46b33-183">In questa guida viene usata l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46b33-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="46b33-184">In Windows PowerShell ISE digitare il comando seguente per aggiungere l'account Azure all'ambiente PowerShell locale:</span><span class="sxs-lookup"><span data-stu-id="46b33-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="46b33-185">Nella finestra "Accesso a Microsoft Azure" digitare l'indirizzo di posta elettronica e la password associati all'account.</span><span class="sxs-lookup"><span data-stu-id="46b33-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="46b33-186">Le informazioni delle credenziali vengono autenticate e salvate in Azure, quindi la finestra viene chiusa.</span><span class="sxs-lookup"><span data-stu-id="46b33-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="46b33-187">Eseguire questo comando per visualizzare gli account Azure nell'ambiente PowerShell locale e verificare che l'account sia presente:</span><span class="sxs-lookup"><span data-stu-id="46b33-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="46b33-188">Quindi, eseguire il cmdlet seguente per visualizzare tutte le sottoscrizioni connesse alla sessione PowerShell locale e verificare che la sottoscrizione sia presente:</span><span class="sxs-lookup"><span data-stu-id="46b33-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="46b33-189">Per impostare la sottoscrizione di Azure predefinita, eseguire il cmdlet Select-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="46b33-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="46b33-190">Verificare il nome della sottoscrizione predefinita eseguendo il cmdlet Get-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="46b33-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="46b33-191">Per visualizzare tutti i cmdlet di PowerShell disponibili per Archiviazione di Azure, eseguire:</span><span class="sxs-lookup"><span data-stu-id="46b33-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="46b33-192">Come creare un nuovo account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="46b33-193">Per usare Archiviazione di Azure, è necessario un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="46b33-194">Dopo aver configurato il computer per connettersi alla sottoscrizione, è possibile creare un nuovo account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="46b33-195">Eseguire il cmdlet Get-AzureLocation per trovare tutte le posizioni dei data center disponibili:</span><span class="sxs-lookup"><span data-stu-id="46b33-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="46b33-196">Eseguire il cmdlet New-AzureStorageAccount per creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="46b33-197">Nell'esempio seguente viene creato un nuovo account di archiviazione nel data center "West US":</span><span class="sxs-lookup"><span data-stu-id="46b33-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="46b33-198">Il nome per l'account di archiviazione è univoco in Azure e deve essere in minuscolo.</span><span class="sxs-lookup"><span data-stu-id="46b33-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="46b33-199">Per le convenzioni di denominazione e le restrizioni, vedere [Informazioni sugli account di archiviazione di Azure](../storage-create-storage-account.md) e [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx) (Assegnazione di nome e riferimento a contenitori, BLOB e metadati).</span><span class="sxs-lookup"><span data-stu-id="46b33-199">For naming conventions and restrictions, see [About Azure Storage Accounts](../storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="46b33-200">Come impostare un account di archiviazione di Azure predefinito</span><span class="sxs-lookup"><span data-stu-id="46b33-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="46b33-201">È possibile avere più account di archiviazione nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="46b33-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="46b33-202">È possibile sceglierne uno e impostarlo come account di archiviazione predefinito per tutti i comandi di archiviazione nella stessa sessione PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46b33-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="46b33-203">Questo consente di eseguire i comandi di archiviazione di Azure PowerShell senza specificare in modo esplicito il contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="46b33-204">Per impostare un account di archiviazione predefinito per la sottoscrizione, è possibile eseguire il cmdlet Set-AzureSubscription.</span><span class="sxs-lookup"><span data-stu-id="46b33-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="46b33-205">Eseguire quindi il cmdlet Get-AzureSubscription per verificare che l'account di archiviazione sia associato all'account di sottoscrizione predefinito.</span><span class="sxs-lookup"><span data-stu-id="46b33-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="46b33-206">Questo comando restituisce le proprietà della sottoscrizione corrente, incluso l'account di archiviazione corrente.</span><span class="sxs-lookup"><span data-stu-id="46b33-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="46b33-207">Come elencare tutti gli account di archiviazione di Azure in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="46b33-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="46b33-208">Ogni sottoscrizione di Azure può avere fino a 100 account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="46b33-209">Per informazioni più aggiornate sui limiti, vedere [Sottoscrizione di Azure e limiti dei servizi, quote e vincoli](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="46b33-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="46b33-210">Eseguire il cmdlet seguente per trovare il nome e lo stato degli account di archiviazione nella sottoscrizione corrente:</span><span class="sxs-lookup"><span data-stu-id="46b33-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="46b33-211">Come creare un contesto di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-211">How to create an Azure storage context</span></span>
<span data-ttu-id="46b33-212">Il contesto di archiviazione di Azure è un oggetto in PowerShell che permette di incapsulare le credenziali di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="46b33-213">Usando il contesto di archiviazione durante l'esecuzione dei cmdlet successivi, è possibile autenticare la richiesta senza specificare in modo esplicito l'account di archiviazione e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="46b33-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="46b33-214">È possibile creare un contesto di archiviazione in molti modi, ad esempio usando la chiave di accesso e il nome dell'account di archiviazione, il token di firma di accesso condiviso, la stringa di connessione o il valore anonimo.</span><span class="sxs-lookup"><span data-stu-id="46b33-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="46b33-215">Per ulteriori informazioni, vedere [Nuovo AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="46b33-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="46b33-216">Usare uno dei seguenti tre metodi per creare un contesto di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="46b33-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="46b33-217">Eseguire il [Get AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet per individuare la chiave di accesso alle risorse di archiviazione primaria per l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-217">Run the [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="46b33-218">Chiamare quindi il cmdlet [New AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) per creare un contesto di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="46b33-218">Next, call the [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="46b33-219">Generare un token di firma di accesso condiviso per un contenitore di archiviazione di Azure e usarlo per creare un contesto di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="46b33-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="46b33-220">Per altre informazioni, vedere [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) e [Uso delle firme di accesso condiviso (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="46b33-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="46b33-221">In alcuni casi, è possibile specificare gli endpoint del servizio quando si crea un nuovo contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="46b33-222">Ciò potrebbe essere necessario quando un nome di dominio personalizzato per l'account di archiviazione viene registrato con il servizio BLOB oppure si vuole usare una firma di accesso condiviso per l'accesso alle risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="46b33-223">Impostare gli endpoint del servizio in una stringa di connessione e usarla per creare un nuovo contesto di archiviazione, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="46b33-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="46b33-224">Per altre informazioni su come configurare una stringa di connessione di archiviazione, vedere [Configurazione delle stringhe di connessione](../storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="46b33-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](../storage-configure-connection-string.md).</span></span>

<span data-ttu-id="46b33-225">Dopo aver configurato il computer e compreso come gestire le sottoscrizioni e gli account di archiviazione di Azure PowerShell, passare alla sezione successiva per informazioni su come gestire i BLOB e gli snapshot BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="46b33-226">Come recuperare e rigenerare le chiavi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="46b33-227">Un account di archiviazione di Azure viene fornito con due chiavi.</span><span class="sxs-lookup"><span data-stu-id="46b33-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="46b33-228">È possibile usare il cmdlet seguente per recuperare le chiavi.</span><span class="sxs-lookup"><span data-stu-id="46b33-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="46b33-229">Usare il cmdlet seguente per recuperare una chiave specifica.</span><span class="sxs-lookup"><span data-stu-id="46b33-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="46b33-230">I valori validi sono Primary e Secondary.</span><span class="sxs-lookup"><span data-stu-id="46b33-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="46b33-231">Per rigenerare le chiavi, usare il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="46b33-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="46b33-232">I valori validi per -KeyType sono "Primary" e "Secondary".</span><span class="sxs-lookup"><span data-stu-id="46b33-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="46b33-233">Come gestire i BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-233">How to manage Azure blobs</span></span>
<span data-ttu-id="46b33-234">Archivio BLOB di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binari, a cui è possibile accedere da qualsiasi parte del mondo tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="46b33-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="46b33-235">Questa sezione presuppone la conoscenza dei concetti relativi al servizio di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="46b33-236">Per informazioni dettagliate, vedere [Introduzione all'archivio BLOB di Azure con .NET](../blobs/storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx) (Concetti relativi al servizio BLOB).</span><span class="sxs-lookup"><span data-stu-id="46b33-236">For detailed information, see [Get started with Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="46b33-237">Come creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="46b33-237">How to create a container</span></span>
<span data-ttu-id="46b33-238">Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="46b33-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="46b33-239">È possibile creare un contenitore privato usando il cmdlet New-AzureStorageContainer:</span><span class="sxs-lookup"><span data-stu-id="46b33-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="46b33-240">Esistono tre livelli di accesso in lettura anonimo: **Off**, **BLOB** e **contenitore**.</span><span class="sxs-lookup"><span data-stu-id="46b33-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="46b33-241">Per impedire l'accesso anonimo ai BLOB, impostare il parametro di autorizzazione su **Disattivato**.</span><span class="sxs-lookup"><span data-stu-id="46b33-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="46b33-242">Per impostazione predefinita, il nuovo contenitore è privato ed è accessibile solo al proprietario dell'account.</span><span class="sxs-lookup"><span data-stu-id="46b33-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="46b33-243">Per consentire l'accesso in lettura pubblico anonimo alle risorse BLOB, ma non ai metadati del contenitore o all'elenco dei BLOB nel contenitore, impostare il parametro di autorizzazione su **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="46b33-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="46b33-244">Per consentire l'accesso in lettura pubblico completo alle risorse BLOB, ai metadati del contenitore e all'elenco dei BLOB nel contenitore, impostare il parametro di autorizzazione **su Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="46b33-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="46b33-245">Per altre informazioni, vedere [Gestire l'accesso in lettura anonimo a contenitori e BLOB](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="46b33-245">For more information, see [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="46b33-246">Come caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="46b33-246">How to upload a blob into a container</span></span>
<span data-ttu-id="46b33-247">In Archiviazione BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="46b33-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="46b33-248">Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="46b33-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="46b33-249">Per caricare i BLOB in un contenitore, è possibile usare il cmdlet [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) .</span><span class="sxs-lookup"><span data-stu-id="46b33-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="46b33-250">Per impostazione predefinita, questo comando carica i file locali in un BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="46b33-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="46b33-251">Per specificare il tipo per il BLOB, è possibile usare il parametro - BlobType.</span><span class="sxs-lookup"><span data-stu-id="46b33-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="46b33-252">Nell'esempio seguente viene eseguito il cmdlet [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) per ottenere tutti i file nella cartella specificata, e poi passarli al cmdlet successivo usando l'operatore pipeline.</span><span class="sxs-lookup"><span data-stu-id="46b33-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="46b33-253">Il cmdlet [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) consente di caricare i file locali nel contenitore:</span><span class="sxs-lookup"><span data-stu-id="46b33-253">The [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="46b33-254">Come scaricare i BLOB da un contenitore</span><span class="sxs-lookup"><span data-stu-id="46b33-254">How to download blobs from a container</span></span>
<span data-ttu-id="46b33-255">Nell'esempio seguente viene mostrato come scaricare i BLOB da un contenitore.</span><span class="sxs-lookup"><span data-stu-id="46b33-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="46b33-256">Innanzitutto viene stabilita una connessione ad Archiviazione di Azure usando il contesto dell'account di archiviazione che include il nome dell'account di archiviazione e la relativa chiave di accesso primaria.</span><span class="sxs-lookup"><span data-stu-id="46b33-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="46b33-257">Quindi, l'esempio recupera un riferimento BLOB usando il cmdlet [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) .</span><span class="sxs-lookup"><span data-stu-id="46b33-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="46b33-258">Nell'esempio viene usato il cmdlet [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) per scaricare i BLOB nella cartella di destinazione locale.</span><span class="sxs-lookup"><span data-stu-id="46b33-258">Next, the example uses the [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet to download blobs into the local destination folder.</span></span>

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="46b33-259">Come copiare i BLOB da un contenitore di archiviazione a un altro</span><span class="sxs-lookup"><span data-stu-id="46b33-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="46b33-260">È possibile copiare i BLOB tra aree e account di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="46b33-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="46b33-261">Nell'esempio seguente viene mostrato come copiare i BLOB da un contenitore di archiviazione a un altro in due diversi account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="46b33-262">L'esempio imposta prima le variabili per gli account di archiviazione di origine e di destinazione, quindi crea un contesto di archiviazione per ogni account.</span><span class="sxs-lookup"><span data-stu-id="46b33-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="46b33-263">Quindi, i BLOB vengono copiati dal contenitore di origine al contenitore di destinazione mediante il cmdlet [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) .</span><span class="sxs-lookup"><span data-stu-id="46b33-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="46b33-264">Nell'esempio si presuppone che i contenitori e gli account di archiviazione di origine e di destinazione esistano già.</span><span class="sxs-lookup"><span data-stu-id="46b33-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="46b33-265">In questo esempio viene eseguita una copia asincrona.</span><span class="sxs-lookup"><span data-stu-id="46b33-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="46b33-266">È possibile monitorare lo stato di ogni copia eseguendo il cmdlet [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) .</span><span class="sxs-lookup"><span data-stu-id="46b33-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="46b33-267">Come copiare i BLOB da una posizione secondaria</span><span class="sxs-lookup"><span data-stu-id="46b33-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="46b33-268">È possibile copiare i BLOB da una posizione secondaria di un account abilitato RA-GRS.</span><span class="sxs-lookup"><span data-stu-id="46b33-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="46b33-269">Come eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="46b33-269">How to delete a blob</span></span>
<span data-ttu-id="46b33-270">Per eliminare un BLOB, ottenere prima un riferimento al BLOB su cui chiamare il cmdlet Remove-AzureStorageBlob.</span><span class="sxs-lookup"><span data-stu-id="46b33-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="46b33-271">Nell'esempio seguente vengono eliminati tutti i BLOB in un contenitore specificato.</span><span class="sxs-lookup"><span data-stu-id="46b33-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="46b33-272">L'esempio imposta prima le variabili per un account di archiviazione, quindi crea un contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="46b33-273">Quindi, viene recuperato un riferimento BLOB usando il cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) e viene eseguito il cmdlet [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) per rimuovere i BLOB da un contenitore in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet to remove blobs from a container in Azure storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="46b33-274">Come gestire gli snapshot BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="46b33-275">Azure consente di creare uno snapshot di un BLOB.</span><span class="sxs-lookup"><span data-stu-id="46b33-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="46b33-276">Uno snapshot è una versione di sola lettura di un BLOB eseguito in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="46b33-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="46b33-277">Una volta creato uno snapshot, è possibile leggerlo, copiarlo o eliminarlo, ma non modificarlo.</span><span class="sxs-lookup"><span data-stu-id="46b33-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="46b33-278">Gli snapshot consentono di eseguire il backup di un BLOB così com'è in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="46b33-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="46b33-279">Per ulteriori informazioni, vedere [Creazione di uno Snapshot di un BLOB](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="46b33-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="46b33-280">Come creare uno snapshot BLOB</span><span class="sxs-lookup"><span data-stu-id="46b33-280">How to create a blob snapshot</span></span>
<span data-ttu-id="46b33-281">Per creare uno snapshot di un BLOB, ottenere prima un riferimento al BLOB su cui chiamare il `ICloudBlob.CreateSnapshot` metodo su di esso.</span><span class="sxs-lookup"><span data-stu-id="46b33-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="46b33-282">L'esempio seguente imposta prima le variabili per un account di archiviazione, quindi crea un contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="46b33-283">Quindi, viene recuperato un riferimento BLOB usando il cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) e viene eseguito il metodo [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) per creare uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="46b33-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="46b33-284">Come elencare gli snapshot di un BLOB</span><span class="sxs-lookup"><span data-stu-id="46b33-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="46b33-285">Non ci sono limiti agli snapshot creati per un BLOB.</span><span class="sxs-lookup"><span data-stu-id="46b33-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="46b33-286">È possibile elencare gli snapshot associati al BLOB per tenere traccia degli snapshot correnti.</span><span class="sxs-lookup"><span data-stu-id="46b33-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="46b33-287">Nell'esempio seguente viene usato un BLOB predefinito e chiamato il cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) per elencare gli snapshot del BLOB.</span><span class="sxs-lookup"><span data-stu-id="46b33-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="46b33-288">Come copiare uno snapshot di un BLOB</span><span class="sxs-lookup"><span data-stu-id="46b33-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="46b33-289">È possibile copiare uno snapshot di un BLOB per ripristinare lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="46b33-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="46b33-290">Per informazioni dettagliate e le restrizioni, vedere [Creazione di uno Snapshot di un BLOB](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="46b33-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="46b33-291">L'esempio seguente imposta prima le variabili per un account di archiviazione, quindi crea un contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="46b33-292">L'esempio definisce poi le variabili per il nome BLOB e il contenitore.</span><span class="sxs-lookup"><span data-stu-id="46b33-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="46b33-293">Nell'esempio viene recuperato un riferimento BLOB usando il cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) e viene eseguito il metodo [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) per creare uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="46b33-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="46b33-294">Poi viene eseguito il cmdlet [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) per copiare lo snapshot di un BLOB usando l'oggetto ICloudBlob per il BLOB di origine.</span><span class="sxs-lookup"><span data-stu-id="46b33-294">Then, the example runs the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="46b33-295">Assicurarsi di aggiornare le variabili in base alla configurazione prima di eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="46b33-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="46b33-296">Nell'esempio seguente si presuppone che i contenitori di origine e di destinazione e il BLOB di origine siano già presenti.</span><span class="sxs-lookup"><span data-stu-id="46b33-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="46b33-297">Dopo aver compreso come gestire i BLOB e gli snapshot BLOB di Azure, passare alla sezione successiva per informazioni su come gestire tabelle, code e file.</span><span class="sxs-lookup"><span data-stu-id="46b33-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="46b33-298">Come gestire le tabelle e le entità di tabella di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="46b33-299">Il servizio di archiviazione tabelle di Azure è un archivio dati NoSQL, che è possibile usare per archiviare ed eseguire query su grandi set di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="46b33-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="46b33-300">I componenti principali del servizio sono tabelle, entità e proprietà.</span><span class="sxs-lookup"><span data-stu-id="46b33-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="46b33-301">una tabella è una raccolta di entità.</span><span class="sxs-lookup"><span data-stu-id="46b33-301">A table is a collection of entities.</span></span> <span data-ttu-id="46b33-302">Un'entità è un set di proprietà.</span><span class="sxs-lookup"><span data-stu-id="46b33-302">An entity is a set of properties.</span></span> <span data-ttu-id="46b33-303">Ogni entità può avere fino a 252 proprietà, che corrispondono tutte a coppie nome-valore.</span><span class="sxs-lookup"><span data-stu-id="46b33-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="46b33-304">Questa sezione presuppone la conoscenza dei concetti relativi al servizio di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="46b33-305">Per informazioni dettagliate, vedere[Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) (Informazioni sul modello di dati del servizio tabelle) e [Introduzione all'archiviazione tabelle di Azure con .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="46b33-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="46b33-306">Le sottosezioni seguenti illustrano come gestire il servizio di archiviazione tabelle di Azure con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46b33-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="46b33-307">Gli scenari presentati includono **la creazione**, **l'eliminazione** e **il recupero** **delle tabelle**, oltre **all'aggiunta**, **all'esecuzione di query** e **all'eliminazione delle entità tabella**.</span><span class="sxs-lookup"><span data-stu-id="46b33-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="46b33-308">Come creare una tabella</span><span class="sxs-lookup"><span data-stu-id="46b33-308">How to create a table</span></span>
<span data-ttu-id="46b33-309">Ogni tabella deve risiedere in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="46b33-310">L'esempio seguente mostra come creare una tabella in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="46b33-311">Innanzitutto viene stabilita una connessione ad Archiviazione di Azure usando il contesto dell'account di archiviazione che include il nome dell'account di archiviazione e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="46b33-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="46b33-312">Viene quindi usato il cmdlet [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) per creare una tabella in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-312">Next, it uses the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="46b33-313">Come recuperare una tabella</span><span class="sxs-lookup"><span data-stu-id="46b33-313">How to retrieve a table</span></span>
<span data-ttu-id="46b33-314">È possibile eseguire query e recuperare una o tutte le tabelle di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="46b33-315">L'esempio seguente mostra come recuperare una determinata tabella usando il cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="46b33-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="46b33-316">Se si chiama il cmdlet Get-AzureStorageTable senza parametri, si ottengono tutte le tabelle di archiviazione per un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="46b33-317">Come eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="46b33-317">How to delete a table</span></span>
<span data-ttu-id="46b33-318">È possibile eliminare una tabella da un account di archiviazione usando il cmdlet [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="46b33-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="46b33-319">Come gestire le entità di tabella</span><span class="sxs-lookup"><span data-stu-id="46b33-319">How to manage table entities</span></span>
<span data-ttu-id="46b33-320">Attualmente, Azure PowerShell non fornisce i cmdlet per gestire direttamente le entità di tabella.</span><span class="sxs-lookup"><span data-stu-id="46b33-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="46b33-321">Per eseguire operazioni sulle entità di tabella, è possibile usare le classi fornite nella [libreria client di archiviazione di Azure per .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="46b33-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="46b33-322">Come aggiungere le entità di tabella</span><span class="sxs-lookup"><span data-stu-id="46b33-322">How to add table entities</span></span>
<span data-ttu-id="46b33-323">Per aggiungere un'entità a una tabella, creare prima un oggetto che definisca le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="46b33-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="46b33-324">Un'entità può contenere fino a 255 proprietà, incluse 3 proprietà di sistema: **PartitionKey**, **RowKey** e **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="46b33-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="46b33-325">L'utente è responsabile dell'inserimento e dell'aggiornamento dei valori di **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="46b33-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="46b33-326">Il server gestisce il valore **Timestamp**, che non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="46b33-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="46b33-327">Insieme **PartitionKey** e **RowKey** identificano in modo univoco tutte le entità di una tabella.</span><span class="sxs-lookup"><span data-stu-id="46b33-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="46b33-328">**PartitionKey**: determina la partizione in cui è archiviata l'entità.</span><span class="sxs-lookup"><span data-stu-id="46b33-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="46b33-329">**RowKey**: identifica in modo univoco l'entità all'interno della partizione.</span><span class="sxs-lookup"><span data-stu-id="46b33-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="46b33-330">È possibile definire fino a 252 proprietà personalizzate per un'entità.</span><span class="sxs-lookup"><span data-stu-id="46b33-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="46b33-331">Per altre informazioni, vedere [Informazioni sul modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="46b33-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="46b33-332">Nell'esempio seguente viene mostrato come aggiungere le entità a una tabella.</span><span class="sxs-lookup"><span data-stu-id="46b33-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="46b33-333">L'esempio mostra come recuperare la tabella employee e come aggiungere varie entità.</span><span class="sxs-lookup"><span data-stu-id="46b33-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="46b33-334">Innanzitutto viene stabilita una connessione ad Archiviazione di Azure usando il contesto dell'account di archiviazione che include il nome dell'account di archiviazione e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="46b33-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="46b33-335">Successivamente viene recuperata la tabella specificata usando il cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="46b33-335">Next, it retrieves the given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="46b33-336">Se la tabella non esiste, il cmdlet [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) viene usato per creare una tabella in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-336">If the table does not exist, the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="46b33-337">L'esempio definisce quindi una funzione personalizzata Add-Entity per aggiungere entità alla tabella specificando la partizione di ciascuna entità e la chiave di riga.</span><span class="sxs-lookup"><span data-stu-id="46b33-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="46b33-338">La funzione Add-Entity chiama il cmdlet [New-Object](http://technet.microsoft.com/library/hh849885.aspx) nella classe [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) per creare un oggetto entità.</span><span class="sxs-lookup"><span data-stu-id="46b33-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="46b33-339">Quindi, viene chiamato il metodo [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) nell'oggetto entità per aggiungerlo a una tabella.</span><span class="sxs-lookup"><span data-stu-id="46b33-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity to a table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="46b33-340">Come eseguire query sulle entità di tabella</span><span class="sxs-lookup"><span data-stu-id="46b33-340">How to query table entities</span></span>
<span data-ttu-id="46b33-341">Per eseguire query su una tabella, usare la classe [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx).</span><span class="sxs-lookup"><span data-stu-id="46b33-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="46b33-342">L'esempio seguente assume che lo script indicato nella sezione Come aggiungere le entità di questa guida sia stato già eseguito.</span><span class="sxs-lookup"><span data-stu-id="46b33-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="46b33-343">Innanzitutto viene stabilita una connessione ad Archiviazione di Azure usando il contesto di archiviazione che include il nome dell'account di archiviazione e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="46b33-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="46b33-344">Se tenta successivamente di recuperare la tabella "Employees" (Dipendenti) creata in precedenza usando il cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable).</span><span class="sxs-lookup"><span data-stu-id="46b33-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="46b33-345">La chiamata del cmdlet [New-Object](http://technet.microsoft.com/library/hh849885.aspx) nella classe Microsoft.WindowsAzure.Storage.Table.TableQuery crea un nuovo oggetto query.</span><span class="sxs-lookup"><span data-stu-id="46b33-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="46b33-346">Nell'esempio vengono cercate le entità con il valore 1 nella colonna 'ID', come specificato in un filtro di stringa.</span><span class="sxs-lookup"><span data-stu-id="46b33-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="46b33-347">Per informazioni dettagliate, vedere [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx) (Esecuzione di query su tabelle ed entità).</span><span class="sxs-lookup"><span data-stu-id="46b33-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="46b33-348">Quando si esegue questa query, vengono restituite tutte le entità che soddisfano i criteri di filtro.</span><span class="sxs-lookup"><span data-stu-id="46b33-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="46b33-349">Come eliminare le entità di tabella</span><span class="sxs-lookup"><span data-stu-id="46b33-349">How to delete table entities</span></span>
<span data-ttu-id="46b33-350">È possibile eliminare un'entità utilizzando le relative chiavi di riga e di partizione.</span><span class="sxs-lookup"><span data-stu-id="46b33-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="46b33-351">L'esempio seguente assume che lo script indicato nella sezione Come aggiungere le entità di questa guida sia stato già eseguito.</span><span class="sxs-lookup"><span data-stu-id="46b33-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="46b33-352">Innanzitutto viene stabilita una connessione ad Archiviazione di Azure usando il contesto di archiviazione che include il nome dell'account di archiviazione e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="46b33-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="46b33-353">Se tenta successivamente di recuperare la tabella "Employees" (Dipendenti) creata in precedenza usando il cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable).</span><span class="sxs-lookup"><span data-stu-id="46b33-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="46b33-354">Se la tabella esiste, viene chiamato il metodo [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) per recuperare un'entità in base ai relativi valori di chiave di riga e di partizione.</span><span class="sxs-lookup"><span data-stu-id="46b33-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="46b33-355">L'entità viene quindi passata al metodo [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) per l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="46b33-356">Come gestire le code e i messaggi della coda di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="46b33-357">Il servizio di archiviazione di accodamento di Azure consente di archiviare grandi quantità di messaggi ai quali è possibile accedere da qualsiasi parte del mondo mediante chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="46b33-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="46b33-358">Questa sezione presuppone la conoscenza dei concetti relativi al servizio di archiviazione di accodamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="46b33-359">Per informazioni dettagliate, vedere [Introduzione all'archivio code di Azure con .NET](../storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="46b33-359">For detailed information, see [Get started with Azure Queue storage using .NET](../storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="46b33-360">Questa sezione spiega come gestire il servizio di archiviazione di accodamento di Azure usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46b33-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="46b33-361">Gli scenari presentati includono **l'inserimento** e **l'eliminazione** dei messaggi in coda, oltre **alla creazione**, **all'eliminazione** e **al recupero di code**.</span><span class="sxs-lookup"><span data-stu-id="46b33-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="46b33-362">Come creare una coda</span><span class="sxs-lookup"><span data-stu-id="46b33-362">How to create a queue</span></span>
<span data-ttu-id="46b33-363">Innanzitutto viene stabilita una connessione ad Archiviazione di Azure usando il contesto dell'account di archiviazione che include il nome dell'account di archiviazione e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="46b33-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="46b33-364">Viene poi chiamato il cmdlet [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) per creare una coda denominata 'queuename'.</span><span class="sxs-lookup"><span data-stu-id="46b33-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="46b33-365">Per informazioni sulle convenzioni di denominazione per il servizio di accodamento di Azure, vedere [Denominazione di code e metadati](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="46b33-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="46b33-366">Come recuperare una coda</span><span class="sxs-lookup"><span data-stu-id="46b33-366">How to retrieve a queue</span></span>
<span data-ttu-id="46b33-367">È possibile eseguire query e recuperare una coda specifica o un elenco di tutte le code di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="46b33-368">L'esempio seguente mostra come recuperare una determinata coda usando il cmdlet [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) .</span><span class="sxs-lookup"><span data-stu-id="46b33-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="46b33-369">Se si chiama il cmdlet [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) senza parametri, si ottiene un elenco di tutte le code.</span><span class="sxs-lookup"><span data-stu-id="46b33-369">If you call the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="46b33-370">Come eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="46b33-370">How to delete a queue</span></span>
<span data-ttu-id="46b33-371">Per eliminare una coda e tutti i messaggi che contiene, chiamare il metodo Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="46b33-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="46b33-372">L'esempio seguente mostra come eliminare una determinata coda usando il cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="46b33-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="46b33-373">Come inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="46b33-373">How to insert a message into a queue</span></span>
<span data-ttu-id="46b33-374">Per inserire un messaggio in una coda esistente, creare innanzitutto una nuova istanza della classe [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) .</span><span class="sxs-lookup"><span data-stu-id="46b33-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="46b33-375">Quindi, chiamare il metodo [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) .</span><span class="sxs-lookup"><span data-stu-id="46b33-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="46b33-376">È possibile creare un oggetto CloudQueueMessage da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="46b33-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="46b33-377">Nell'esempio seguente viene mostrato come aggiungere un messaggio a una coda.</span><span class="sxs-lookup"><span data-stu-id="46b33-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="46b33-378">Innanzitutto viene stabilita una connessione ad Archiviazione di Azure usando il contesto dell'account di archiviazione che include il nome dell'account di archiviazione e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="46b33-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="46b33-379">Successivamente viene recuperata la coda specificata usando il cmdlet [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) .</span><span class="sxs-lookup"><span data-stu-id="46b33-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="46b33-380">Se la coda esiste, il cmdlet [New-Object](http://technet.microsoft.com/library/hh849885.aspx) viene usato per creare un'istanza della classe [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx).</span><span class="sxs-lookup"><span data-stu-id="46b33-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="46b33-381">Quindi, viene chiamato il metodo [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) nell'oggetto messaggio per aggiungerlo a una coda.</span><span class="sxs-lookup"><span data-stu-id="46b33-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="46b33-382">Di seguito è riportato il codice che consente di creare una coda e di inserire il messaggio 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="46b33-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="46b33-383">Come rimuovere il messaggio successivo dalla coda</span><span class="sxs-lookup"><span data-stu-id="46b33-383">How to de-queue at the next message</span></span>
<span data-ttu-id="46b33-384">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="46b33-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="46b33-385">Chiamando il metodo [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) , si ottiene il messaggio successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="46b33-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="46b33-386">Un messaggio restituito da **GetMessage** diventa invisibile a qualsiasi altro codice che legge i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="46b33-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="46b33-387">Per completare la rimozione del messaggio dalla coda, è necessario chiamare anche il metodo [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) .</span><span class="sxs-lookup"><span data-stu-id="46b33-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="46b33-388">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio non riesca a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="46b33-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="46b33-389">Il codice chiama **DeleteMessage** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="46b33-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="46b33-390">Come gestire condivisioni file e file di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="46b33-391">L'archiviazione file di Azure offre un'archiviazione condivisa per le applicazioni che usano il protocollo SMB standard.</span><span class="sxs-lookup"><span data-stu-id="46b33-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="46b33-392">Le macchine virtuali e i servizi cloud di Microsoft Azure possono condividere dati file tra componenti delle applicazioni tramite le condivisioni montate e le applicazioni locali possono accedere ai dati file in una condivisione tramite l'API dell'archiviazione file o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46b33-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="46b33-393">Per informazioni dettagliate su Archiviazione file di Azure, vedere [Introduzione ad Archiviazione file di Azure in Windows](../storage-dotnet-how-to-use-files.md) e [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx) (API REST del servizio file).</span><span class="sxs-lookup"><span data-stu-id="46b33-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="46b33-394">Come impostare ed eseguire query di Analisi archiviazione</span><span class="sxs-lookup"><span data-stu-id="46b33-394">How to set and query storage analytics</span></span>
<span data-ttu-id="46b33-395">È possibile utilizzare [Analisi archiviazione di Azure](../storage-analytics.md) per raccogliere le metriche per gli account di archiviazione di Azure e per registrare i dati sulle richieste inviate all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-395">You can use [Azure Storage Analytics](../storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="46b33-396">È possibile usare le metriche di archiviazione per monitorare l'integrità di un account di archiviazione e Registrazione archiviazione per diagnosticare e risolvere i problemi relativi al proprio account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="46b33-397">È possibile configurare il monitoraggio tramite il portale di Azure o Windows PowerShell oppure nel codice tramite la libreria del client di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="46b33-398">La Registrazione archiviazione viene eseguita sul lato server e consente all'utente di registrare i dettagli delle richieste, riuscite e non riuscite, nel proprio account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="46b33-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="46b33-399">Questi log consentono di visualizzare i dettagli delle operazioni di lettura, scrittura ed eliminazione a fronte delle proprie tabelle, code e BLOB, nonché i motivi per cui le richieste non sono riuscite.</span><span class="sxs-lookup"><span data-stu-id="46b33-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="46b33-400">Per informazioni su come abilitare e visualizzare i dati di Metriche di archiviazione con PowerShell, vedere [Come abilitare Metriche di archiviazione usando PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="46b33-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="46b33-401">Per informazioni su come abilitare e recuperare i dati di registrazione di archiviazione con PowerShell, vedere [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) (Come abilitare la registrazione di archiviazione con PowerShell) e [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata) (Trovare i dati del log di registrazione di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="46b33-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="46b33-402">Per informazioni dettagliate sull'uso di Metriche di archiviazione e Registrazione archiviazione per la risoluzione dei problemi di archiviazione, vedere [Monitoraggio, diagnosi e risoluzione dei problemi del servizio di archiviazione di Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="46b33-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="46b33-403">Come gestire la firma di accesso condiviso (SAS) e criteri di accesso archiviati</span><span class="sxs-lookup"><span data-stu-id="46b33-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="46b33-404">Le firme di accesso condiviso costituiscono una parte essenziale del modello di sicurezza di qualsiasi applicazione che usa il servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="46b33-405">Le firme di accesso condiviso sono utili per offrire autorizzazioni limitate all'account di archiviazione ai client ai quali non si desidera fornire la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="46b33-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="46b33-406">Per impostazione predefinita, solo il proprietario dell'account di archiviazione può accedere a BLOB, tabelle e code all'interno dell'account.</span><span class="sxs-lookup"><span data-stu-id="46b33-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="46b33-407">Se il servizio o l'applicazione deve rendere disponibili queste risorse ad altri client senza condividere la chiave di accesso, sono disponibili tre opzioni:</span><span class="sxs-lookup"><span data-stu-id="46b33-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="46b33-408">Impostare le autorizzazioni di un contenitore per consentire l'accesso in lettura anonimo al contenitore e ai relativi BLOB.</span><span class="sxs-lookup"><span data-stu-id="46b33-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="46b33-409">Questa operazione non è consentita per le tabelle o le code.</span><span class="sxs-lookup"><span data-stu-id="46b33-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="46b33-410">Usare una firma di accesso condiviso che concede diritti di accesso limitati a contenitori, BLOB, code e tabelle per un intervallo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="46b33-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="46b33-411">Usare criteri di accesso archiviati per ottenere un livello di controllo aggiuntivo sulle firme di accesso condiviso per un contenitore o i relativi BLOB, per una coda o per una tabella.</span><span class="sxs-lookup"><span data-stu-id="46b33-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="46b33-412">I criteri di accesso archiviati consentono di modificare l'ora di inizio, la scadenza o le autorizzazioni per una firma o di revocare la firma dopo che è stata emessa.</span><span class="sxs-lookup"><span data-stu-id="46b33-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="46b33-413">Una firma di accesso condiviso può assumere una delle due forme seguenti:</span><span class="sxs-lookup"><span data-stu-id="46b33-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="46b33-414">**SAS Ad hoc**quando si crea una firma di accesso condiviso ad hoc, l'ora di inizio, la scadenza e le autorizzazioni vengono tutte specificate nell'URI corrispondente.</span><span class="sxs-lookup"><span data-stu-id="46b33-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="46b33-415">Questo tipo di firma di accesso condiviso può essere creato per un contenitore, un BLOB, una tabella e una coda e non è revocabile.</span><span class="sxs-lookup"><span data-stu-id="46b33-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="46b33-416">**Firma di accesso condiviso con politica di accesso archiviazione**: i criteri di accesso archiviati vengono definiti per un contenitore di risorse, ovvero un contenitore BLOB, una tabella o una coda, e possono essere usati per gestire i vincoli per una o più firme di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="46b33-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="46b33-417">Quando si associa una firma di accesso condiviso a criteri di accesso archiviati, la firma eredita i vincoli, ovvero ora di inizio, scadenza e autorizzazioni, definiti per i criteri di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="46b33-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="46b33-418">Questo tipo di firma di accesso condiviso è revocabile.</span><span class="sxs-lookup"><span data-stu-id="46b33-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="46b33-419">Per altre informazioni, vedere [Uso delle firme di accesso condiviso (SAS)](../storage-dotnet-shared-access-signature-part-1.md) e [Gestire l'accesso in lettura anonimo a contenitori e BLOB](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="46b33-419">For more information, see [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="46b33-420">Nelle sezioni successive verrà illustrato come creare un token di firma di accesso condiviso e criteri di accesso archiviati per le tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="46b33-421">Azure PowerShell fornisce cmdlet simili per contenitori, BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="46b33-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="46b33-422">Per eseguire gli script in questa sezione, scaricare [Azure PowerShell versione 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="46b33-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="46b33-423">Come creare un token di firma di accesso condiviso basato su criteri</span><span class="sxs-lookup"><span data-stu-id="46b33-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="46b33-424">Usare il cmdlet New-AzureStorageTableStoredAccessPolicy per creare nuovi criteri di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="46b33-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="46b33-425">Chiamare quindi il nuovo cmdlet [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) per creare un nuovo token di firma di accesso condiviso basato sui criteri per una tabella di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="46b33-425">Then, call the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="46b33-426">Come creare un token di firma di accesso condiviso ad hoc (non revocabile)</span><span class="sxs-lookup"><span data-stu-id="46b33-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="46b33-427">Usare il cmdlet [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) per creare un nuovo token di firma di accesso condiviso ad hoc (non revocabile) per una tabella di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="46b33-427">Use the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="46b33-428">Come creare criteri di accesso archiviati</span><span class="sxs-lookup"><span data-stu-id="46b33-428">How to create a stored access policy</span></span>
<span data-ttu-id="46b33-429">Usare il cmdlet New-AzureStorageTableStoredAccessPolicy per creare nuovi criteri di accesso archiviati per una tabella di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="46b33-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="46b33-430">Come aggiornare criteri di accesso archiviati</span><span class="sxs-lookup"><span data-stu-id="46b33-430">How to update a stored access policy</span></span>
<span data-ttu-id="46b33-431">Usare il cmdlet Set-AzureStorageTableStoredAccessPolicy per aggiornare criteri di accesso archiviati esistenti per una tabella di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="46b33-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="46b33-432">Come eliminare criteri di accesso archiviati</span><span class="sxs-lookup"><span data-stu-id="46b33-432">How to delete a stored access policy</span></span>
<span data-ttu-id="46b33-433">Utilizzare il cmdlet Remove-AzureStorageTableStoredAccessPolicy per eliminare criteri di accesso archiviati in una tabella di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="46b33-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="46b33-434">Come usare Archiviazione di Azure per il governo degli Stati Uniti e Azure Cina</span><span class="sxs-lookup"><span data-stu-id="46b33-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="46b33-435">Un ambiente Azure è una distribuzione indipendente di Microsoft Azure, ad esempio [Azure Government per il governo degli Stati Uniti](https://azure.microsoft.com/features/gov/), [AzureCloud per Azure globale](https://portal.azure.com) e [AzureChinaCloud per Azure gestito da 21Vianet in Cina](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="46b33-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="46b33-436">È possibile distribuire nuovi ambienti Azure per il governo degli Stati Uniti e Azure Cina.</span><span class="sxs-lookup"><span data-stu-id="46b33-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="46b33-437">Per usare Archiviazione di Azure con AzureChinaCloud, è necessario creare un contesto di archiviazione associato ad AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="46b33-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="46b33-438">Seguire questi passaggi per iniziare:</span><span class="sxs-lookup"><span data-stu-id="46b33-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="46b33-439">Eseguire il cmdlet [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) per visualizzare gli ambienti Azure disponibili:</span><span class="sxs-lookup"><span data-stu-id="46b33-439">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="46b33-440">Aggiungere un account Azure Cina a Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="46b33-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="46b33-441">Creare un contesto di archiviazione per un account AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="46b33-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="46b33-442">Per utilizzare l'archiviazione di Azure con [il governo degli Stati Uniti](https://azure.microsoft.com/features/gov/), è necessario definire un nuovo ambiente e creare un nuovo contesto di archiviazione con questo ambiente:</span><span class="sxs-lookup"><span data-stu-id="46b33-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="46b33-443">Eseguire il cmdlet [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) per visualizzare gli ambienti Azure disponibili:</span><span class="sxs-lookup"><span data-stu-id="46b33-443">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="46b33-444">Aggiungere un account Azure per enti pubblici a Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="46b33-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="46b33-445">Creare un contesto di archiviazione per un account AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="46b33-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="46b33-446">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="46b33-446">For more information, see:</span></span>

* <span data-ttu-id="46b33-447">[Guida per gli sviluppatori di Microsoft Azure Government](../../azure-government/documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="46b33-447">[Microsoft Azure Government Developer Guide](../../azure-government/documentation-government-developer-guide.md).</span></span>
* [<span data-ttu-id="46b33-448">Panoramica delle differenze nella creazione di un'applicazione in China Service</span><span class="sxs-lookup"><span data-stu-id="46b33-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="46b33-449">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46b33-449">Next Steps</span></span>
<span data-ttu-id="46b33-450">In questa guida è stato appreso come gestire Archiviazione di Azure con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46b33-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="46b33-451">Per altre informazioni, vedere gli articoli e le risorse correlati seguenti:</span><span class="sxs-lookup"><span data-stu-id="46b33-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="46b33-452">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="46b33-453">Cmdlet di PowerShell per Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="46b33-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="46b33-454">Riferimenti Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="46b33-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
