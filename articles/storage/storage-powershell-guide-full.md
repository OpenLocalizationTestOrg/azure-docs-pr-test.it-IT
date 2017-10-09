---
title: aaaUsing Azure PowerShell con l'archiviazione di Azure | Documenti Microsoft
description: Informazioni su come toouse hello cmdlet PowerShell di Azure per toocreate di archiviazione di Azure e gestire gli account di archiviazione; utilizzo di BLOB, tabelle, code e i file; configurare e analitica di archiviazione di query e creare firme di accesso condiviso.
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
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="83b40-103">Uso di Azure PowerShell con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="83b40-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="83b40-104">Overview</span></span>
<span data-ttu-id="83b40-105">Azure PowerShell è un modulo che fornisce i cmdlet toomanage Azure tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83b40-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="83b40-106">Corrisponde a una shell della riga di comando basata su attività e un linguaggio di scripting progettato appositamente per l'amministrazione del sistema.</span><span class="sxs-lookup"><span data-stu-id="83b40-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="83b40-107">Con PowerShell, è possibile controllare facilmente e automatizzare l'amministrazione di hello di applicazioni e i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="83b40-108">Ad esempio, è possibile utilizzare hello tooperform di cmdlet hello stessa attività che è possibile eseguire tramite hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83b40-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="83b40-109">In questa Guida, si esamineranno come hello toouse [cmdlet di archiviazione di Azure](/powershell/module/azurerm.storage/#storage) tooperform un'ampia gamma di attività di sviluppo e amministrazione con l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="83b40-110">Nella guida si presuppone una certa esperienza nell'uso di [Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/) e [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="83b40-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="83b40-111">Guida di Hello fornisce un numero di script utilizzo hello toodemonstrate di PowerShell con l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="83b40-112">È necessario aggiornare le variabili dello script hello in base alla configurazione prima di eseguire ogni script.</span><span class="sxs-lookup"><span data-stu-id="83b40-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="83b40-113">Hello prima sezione in questa guida fornisce una panoramica di archiviazione di Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83b40-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="83b40-114">Per informazioni dettagliate e istruzioni, avviare da hello [prerequisiti per l'utilizzo di Azure PowerShell con l'archiviazione di Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="83b40-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="83b40-115">Introduzione ad Archiviazione di Azure e PowerShell in 5 minuti</span><span class="sxs-lookup"><span data-stu-id="83b40-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="83b40-116">In questa sezione illustra come tooaccess di archiviazione di Azure tramite PowerShell in 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="83b40-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="83b40-117">**Nuovo tooAzure:** ottenere una sottoscrizione di Microsoft Azure e un account Microsoft associato a tale sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="83b40-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="83b40-118">Per informazioni sulle opzioni di acquisto di Azure, vedere la [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/), le [opzioni di acquisto](https://azure.microsoft.com/pricing/purchase-options/) e le [offerte per i membri](https://azure.microsoft.com/pricing/member-offers/) (per i membri di MSDN, Microsoft Partner Network, BizSpark e altri programmi Microsoft).</span><span class="sxs-lookup"><span data-stu-id="83b40-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="83b40-119">Per altre informazioni sulle sottoscrizioni di Azure, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="83b40-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="83b40-120">**Dopo aver creato una sottoscrizione e un account di Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="83b40-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="83b40-121">Scaricare e installare più recente hello [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="83b40-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="83b40-122">Avviare Windows PowerShell Integrated Scripting Environment (ISE): Nel computer locale, passare toohello **avviare** menu.</span><span class="sxs-lookup"><span data-stu-id="83b40-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="83b40-123">Tipo **strumenti di amministrazione** e fare clic su toorun è.</span><span class="sxs-lookup"><span data-stu-id="83b40-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="83b40-124">In hello **strumenti di amministrazione** finestra, fare doppio clic su **Windows PowerShell ISE**, fare clic su **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="83b40-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="83b40-125">In **Windows PowerShell ISE**, fare clic su **File** > **New** toocreate un nuovo file script.</span><span class="sxs-lookup"><span data-stu-id="83b40-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="83b40-126">A questo punto, verrà fornita è un semplice script che mostra base tooaccess di comandi di PowerShell di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="83b40-127">script Hello chiederà innanzitutto il tooadd le credenziali di account Azure account Azure toohello PowerShell ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="83b40-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="83b40-128">Quindi, hello script impostare il valore predefinito di hello sottoscrizione di Azure e creare un nuovo account di archiviazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="83b40-129">Successivamente, hello script creare un nuovo contenitore in questo nuovo account di archiviazione e caricare un contenitore toothat (blob) di file di immagine esistente.</span><span class="sxs-lookup"><span data-stu-id="83b40-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="83b40-130">Dopo aver hello script permette di elencare tutti i BLOB nel contenitore, verrà creare una nuova directory di destinazione nel computer locale e scaricare i file di immagine hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="83b40-131">In hello seguente sezione di codice, selezionare script hello tra la sezione Osservazioni hello **#begin** e **#end**.</span><span class="sxs-lookup"><span data-stu-id="83b40-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="83b40-132">Premere CTRL + C toocopy è toohello Appunti.</span><span class="sxs-lookup"><span data-stu-id="83b40-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
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
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="83b40-133">In **Windows PowerShell ISE**, premere script hello toocopy CTRL + V.</span><span class="sxs-lookup"><span data-stu-id="83b40-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="83b40-134">Fare clic su **File** > **Salva**.</span><span class="sxs-lookup"><span data-stu-id="83b40-134">Click **File** > **Save**.</span></span> <span data-ttu-id="83b40-135">In hello **Salva con nome** finestra di dialogo, il nome del tipo hello del file di script hello, ad esempio "mystoragescript".</span><span class="sxs-lookup"><span data-stu-id="83b40-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="83b40-136">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="83b40-136">Click **Save**.</span></span>
7. <span data-ttu-id="83b40-137">A questo punto, è necessario tooupdate hello scripting di variabili in base alle impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="83b40-138">È necessario aggiornare hello **$SubscriptionName** variabile con la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="83b40-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="83b40-139">È possibile mantenere hello altre variabili come specificato nello script hello o aggiornarle nel modo desiderato.</span><span class="sxs-lookup"><span data-stu-id="83b40-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="83b40-140">**$SubscriptionName:** è necessario aggiornare questa variabile con il proprio nome di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="83b40-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="83b40-141">Effettuare una delle hello dopo tre modi toolocate hello nome della sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="83b40-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="83b40-142">a.</span><span class="sxs-lookup"><span data-stu-id="83b40-142">a.</span></span> <span data-ttu-id="83b40-143">In **Windows PowerShell ISE**, fare clic su **File** > **New** toocreate un nuovo file script.</span><span class="sxs-lookup"><span data-stu-id="83b40-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="83b40-144">Esempio hello copia script toohello nuovo file di script e fare clic su **Debug** > **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="83b40-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="83b40-145">Hello lo script seguente verrà prima chiedere il tooadd le credenziali di account di Azure dell'ambiente di PowerShell locale toohello account Azure e di visualizzare tutte le sottoscrizioni di hello che sono connessi toohello sessione di PowerShell locale.</span><span class="sxs-lookup"><span data-stu-id="83b40-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="83b40-146">Prendere nota del nome hello della sottoscrizione hello che si desidera toouse durante questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="83b40-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="83b40-147">b.</span><span class="sxs-lookup"><span data-stu-id="83b40-147">b.</span></span> <span data-ttu-id="83b40-148">toolocate e copiare la sottoscrizione nome nel hello [portale di Azure](https://portal.azure.com)in hello menu Hub hello a sinistra, fare clic su **sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="83b40-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="83b40-149">Copia nome hello di sottoscrizione che si desidera toouse durante l'esecuzione di script hello in questa Guida.</span><span class="sxs-lookup"><span data-stu-id="83b40-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Portale di Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="83b40-151">c.</span><span class="sxs-lookup"><span data-stu-id="83b40-151">c.</span></span> <span data-ttu-id="83b40-152">toolocate e copiare la sottoscrizione nome nel hello [portale di Azure classico](https://manage.windowsazure.com/), scorrere verso il basso e fare clic su **impostazioni** sul lato sinistro di portale hello hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="83b40-153">Fare clic su **sottoscrizioni** toosee un elenco delle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="83b40-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="83b40-154">Copia nome hello di sottoscrizione che si desidera toouse durante l'esecuzione di script hello specificato in questa Guida.</span><span class="sxs-lookup"><span data-stu-id="83b40-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![portale di Azure classico](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="83b40-156">**$StorageAccountName:** utilizzare hello dato nome nello script hello o immettere un nuovo nome per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="83b40-157">**Importante:** nome hello hello dell'account di archiviazione deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="83b40-158">Utilizzare caratteri minuscoli.</span><span class="sxs-lookup"><span data-stu-id="83b40-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="83b40-159">**$Location:** utilizzare hello "Stati Uniti occidentali" specificato nello script hello o scegliere altre posizioni di Azure, ad esempio Stati Uniti orientali, Europa settentrionale e così via.</span><span class="sxs-lookup"><span data-stu-id="83b40-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="83b40-160">**$ContainerName:** utilizzare hello dato nome nello script hello o immettere un nuovo nome per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="83b40-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="83b40-161">**$ImageToUpload:** immettere un'immagine di tooa percorso sul computer locale, ad esempio: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="83b40-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="83b40-162">**$DestinationFolder:** immettere un percorso tooa directory locale toostore scaricare i file dall'archiviazione di Azure, ad esempio: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="83b40-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="83b40-163">Dopo aver aggiornato le variabili dello script hello nel file "mystoragescript.ps1" hello, fare clic su **File** > **salvare**.</span><span class="sxs-lookup"><span data-stu-id="83b40-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="83b40-164">Quindi, fare clic su **Debug** > **eseguire** o premere **F5** script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="83b40-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="83b40-165">Dopo l'esecuzione di script hello è una cartella di destinazione locale che include i file di immagine scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="83b40-166">Hello seguente schermata mostra un esempio dell'output:</span><span class="sxs-lookup"><span data-stu-id="83b40-166">hello following screenshot shows an example output:</span></span>

![Scaricare BLOB](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="83b40-168">Hello "Introduzione a PowerShell e di archiviazione di Azure in 5 minuti" sezione fornita una rapida introduzione su come toouse Azure PowerShell con l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="83b40-169">Per informazioni dettagliate e istruzioni, si consiglia di hello tooread le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="83b40-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="83b40-170">Prerequisiti per l'uso di Azure PowerShell con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="83b40-171">È necessario un account e sottoscrizione toorun hello cmdlet di Azure PowerShell fornito in questa Guida, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="83b40-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="83b40-172">Azure PowerShell è un modulo che fornisce i cmdlet toomanage Azure tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83b40-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="83b40-173">Per informazioni sull'installazione e configurazione di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="83b40-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="83b40-174">È consigliabile scaricare e installare o aggiornare il modulo PowerShell di Azure più recente di toohello prima di utilizzare questa Guida.</span><span class="sxs-lookup"><span data-stu-id="83b40-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="83b40-175">È possibile eseguire i cmdlet di hello nella console di Windows PowerShell standard hello o hello Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="83b40-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="83b40-176">Ad esempio, tooopen **Windows PowerShell ISE**passare dal menu Start toohello, digitare strumenti di amministrazione e fare clic su toorun è.</span><span class="sxs-lookup"><span data-stu-id="83b40-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="83b40-177">Nella finestra Strumenti di amministrazione di hello, fare doppio clic su Windows PowerShell ISE, fare clic su Esegui come amministratore.</span><span class="sxs-lookup"><span data-stu-id="83b40-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="83b40-178">Come account di archiviazione toomanage in Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="83b40-179">Di seguito è illustrata la gestione degli account di archiviazione in Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="83b40-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="83b40-180">Come tooset predefinito sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="83b40-181">toomanage archiviazione di Azure con Azure PowerShell, è necessario tooauthenticate ambiente client con Azure tramite l'autenticazione di Azure Active Directory o l'autenticazione basata su certificato.</span><span class="sxs-lookup"><span data-stu-id="83b40-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="83b40-182">Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="83b40-183">Questa guida utilizza l'autenticazione di Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="83b40-184">In Windows PowerShell ISE, digitare hello successivo comando tooadd account Azure toohello PowerShell ambiente locale:</span><span class="sxs-lookup"><span data-stu-id="83b40-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="83b40-185">Nella finestra "Accedi tooMicrosoft Azure" hello, indirizzo di posta elettronica di tipo hello e la password associata al proprio account.</span><span class="sxs-lookup"><span data-stu-id="83b40-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="83b40-186">Azure autentica e Salva le informazioni sulle credenziali hello e chiude la finestra hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="83b40-187">Quindi, eseguire hello comando tooview hello Azure gli account nell'ambiente di PowerShell locale e verificare che l'account sia elencato di seguito:</span><span class="sxs-lookup"><span data-stu-id="83b40-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="83b40-188">Quindi, eseguire hello seguente cmdlet tooview tutte le sottoscrizioni di hello che sono connessi toohello sessione di PowerShell locale e verificare che la sottoscrizione sia elencata:</span><span class="sxs-lookup"><span data-stu-id="83b40-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="83b40-189">tooset predefinito sottoscrizione di Azure, eseguire il cmdlet Select-AzureSubscription hello:</span><span class="sxs-lookup"><span data-stu-id="83b40-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="83b40-190">Verificare nome hello della sottoscrizione predefinita hello esegue il cmdlet Get-AzureSubscription hello:</span><span class="sxs-lookup"><span data-stu-id="83b40-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="83b40-191">toosee tutti hello cmdlet di PowerShell disponibili per l'archiviazione di Azure, eseguire:</span><span class="sxs-lookup"><span data-stu-id="83b40-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="83b40-192">Come toocreate un nuovo account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="83b40-193">toouse archiviazione di Azure, è necessario un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="83b40-194">Dopo aver configurato la sottoscrizione di tooyour tooconnect computer, è possibile creare un nuovo account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="83b40-195">Eseguire toofind di cmdlet Get-AzureLocation hello tutte le posizioni dei Data Center disponibili hello:</span><span class="sxs-lookup"><span data-stu-id="83b40-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="83b40-196">Successivamente, eseguire toocreate di cmdlet New-AzureStorageAccount hello un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="83b40-197">Hello seguente viene creato un nuovo account di archiviazione nel Data Center di hello "Stati Uniti occidentali".</span><span class="sxs-lookup"><span data-stu-id="83b40-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="83b40-198">nome di Hello dell'account di archiviazione deve essere univoco all'interno di Azure e deve essere minuscole.</span><span class="sxs-lookup"><span data-stu-id="83b40-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="83b40-199">Per le convenzioni di denominazione e le restrizioni, vedere [Informazioni sugli account di archiviazione di Azure](storage-create-storage-account.md) e [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx) (Assegnazione di nome e riferimento a contenitori, BLOB e metadati).</span><span class="sxs-lookup"><span data-stu-id="83b40-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="83b40-200">Come tooset un account di archiviazione di Azure predefinito</span><span class="sxs-lookup"><span data-stu-id="83b40-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="83b40-201">È possibile avere più account di archiviazione nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="83b40-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="83b40-202">È possibile scegliere uno di essi e impostarlo come account di archiviazione di hello predefinito per tutti hello archiviazione comandi in hello stessa sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83b40-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="83b40-203">Ciò consente di comandi di archiviazione di Azure PowerShell hello toorun senza specificare in modo esplicito il contesto di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="83b40-204">tooset un account di archiviazione predefinito per la sottoscrizione, è possibile eseguire i cmdlet Set-AzureSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="83b40-205">Successivamente, eseguire Get-AzureSubscription hello cmdlet tooverify che l'account di archiviazione hello è associata con l'account della sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="83b40-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="83b40-206">Questo comando restituisce le proprietà di sottoscrizione hello nella sottoscrizione corrente di hello incluso il relativo account di archiviazione corrente.</span><span class="sxs-lookup"><span data-stu-id="83b40-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="83b40-207">Come toolist account di archiviazione di Azure tutte in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="83b40-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="83b40-208">Ogni sottoscrizione di Azure può essere composto too100 gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="83b40-209">Per informazioni più aggiornate di hello sui limiti, vedere [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="83b40-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="83b40-210">Eseguire hello toofind cmdlet out hello nome e lo stato hello di account di archiviazione nella sottoscrizione corrente hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="83b40-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="83b40-211">Come toocreate un contesto di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="83b40-212">Contesto di archiviazione di Azure è un oggetto in credenziali di archiviazione hello tooencapsulate di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83b40-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="83b40-213">Utilizzando un contesto di archiviazione durante l'esecuzione di qualsiasi cmdlet successivi consente si tooauthenticate la richiesta senza specificare in modo esplicito l'account di archiviazione hello e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="83b40-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="83b40-214">È possibile creare un contesto di archiviazione in molti modi, ad esempio usando la chiave di accesso e il nome dell'account di archiviazione, il token di firma di accesso condiviso, la stringa di connessione o il valore anonimo.</span><span class="sxs-lookup"><span data-stu-id="83b40-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="83b40-215">Per ulteriori informazioni, vedere [Nuovo AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="83b40-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="83b40-216">Utilizzare uno dei seguenti tre modi toocreate hello un contesto di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="83b40-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="83b40-217">Eseguire hello [Get AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind cmdlet out chiave di accesso hello archiviazione primaria per l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="83b40-218">Successivamente, chiamare hello [New AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) toocreate cmdlet un contesto di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="83b40-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="83b40-219">Generare un token di firma di accesso condiviso per un contenitore di archiviazione di Azure e usarlo toocreate un contesto di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="83b40-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="83b40-220">Per altre informazioni, vedere [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) e [Uso delle firme di accesso condiviso (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="83b40-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="83b40-221">In alcuni casi, è consigliabile gli endpoint del servizio hello toospecify quando si crea un nuovo contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="83b40-222">Potrebbe essere necessario quando è stato registrato un nome di dominio personalizzato per l'account di archiviazione con il servizio di Blob hello o si desidera toouse una firma di accesso condiviso per accedere alle risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="83b40-223">Impostare gli endpoint del servizio hello in una stringa di connessione e utilizzare toocreate un nuovo contesto di archiviazione come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="83b40-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="83b40-224">Per ulteriori informazioni su come tooconfigure una stringa di connessione di archiviazione, vedere [la configurazione delle stringhe di connessione](storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="83b40-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="83b40-225">Configurare il computer e appreso come toomanage sottoscrizioni e account di archiviazione tramite Azure PowerShell, passare toohello successiva sezione toolearn come BLOB di Azure toomanage e gli snapshot del blob.</span><span class="sxs-lookup"><span data-stu-id="83b40-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="83b40-226">Come tooretrieve e rigenerare le chiavi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="83b40-227">Un account di archiviazione di Azure viene fornito con due chiavi.</span><span class="sxs-lookup"><span data-stu-id="83b40-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="83b40-228">Utilizzare le chiavi di hello tooretrieve cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="83b40-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="83b40-229">Utilizzare hello seguente cmdlet tooretrieve una chiave specifica.</span><span class="sxs-lookup"><span data-stu-id="83b40-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="83b40-230">I valori validi sono Primary e Secondary.</span><span class="sxs-lookup"><span data-stu-id="83b40-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="83b40-231">Se si desidera tooregenerate le chiavi, utilizzare hello cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="83b40-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="83b40-232">I valori validi per -KeyType sono "Primary" e "Secondary".</span><span class="sxs-lookup"><span data-stu-id="83b40-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="83b40-233">Come BLOB di Azure toomanage</span><span class="sxs-lookup"><span data-stu-id="83b40-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="83b40-234">Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="83b40-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="83b40-235">In questa sezione si presuppone che si conoscono già i concetti di hello Azure Blob Storage Service.</span><span class="sxs-lookup"><span data-stu-id="83b40-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="83b40-236">Per informazioni dettagliate, vedere [Introduzione all'archivio BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx) (Concetti relativi al servizio BLOB).</span><span class="sxs-lookup"><span data-stu-id="83b40-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="83b40-237">Come un contenitore toocreate</span><span class="sxs-lookup"><span data-stu-id="83b40-237">How toocreate a container</span></span>
<span data-ttu-id="83b40-238">Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="83b40-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="83b40-239">È possibile creare un contenitore privato utilizzando il cmdlet New-AzureStorageContainer hello:</span><span class="sxs-lookup"><span data-stu-id="83b40-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="83b40-240">Esistono tre livelli di accesso in lettura anonimo: **Off**, **BLOB** e **contenitore**.</span><span class="sxs-lookup"><span data-stu-id="83b40-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="83b40-241">tooprevent anonimo accesso troppo accedere tooblobs, il parametro di autorizzazione del set di hello**Off**.</span><span class="sxs-lookup"><span data-stu-id="83b40-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="83b40-242">Per impostazione predefinita, hello nuovo contenitore è privato e accessibile solo dal proprietario dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="83b40-243">in lettura pubblico anonimo tooallow tooblob di accedere alle risorse, ma non toocontainer metadati o toohello elenco di BLOB nel contenitore di hello, impostare il parametro di autorizzazione hello troppo**Blob**.</span><span class="sxs-lookup"><span data-stu-id="83b40-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="83b40-244">in lettura pubblico completo tooallow tooblob di accedere alle risorse e i metadati del contenitore elenco hello di BLOB nel contenitore di hello, impostare il parametro di autorizzazione hello troppo**contenitore**.</span><span class="sxs-lookup"><span data-stu-id="83b40-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="83b40-245">Per ulteriori informazioni, vedere [gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="83b40-245">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="83b40-246">Come tooupload un blob in un contenitore</span><span class="sxs-lookup"><span data-stu-id="83b40-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="83b40-247">In Archiviazione BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="83b40-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="83b40-248">Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="83b40-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="83b40-249">i BLOB nel contenitore tooa tooupload, è possibile utilizzare hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="83b40-250">Per impostazione predefinita, questo comando Carica blob in blocchi tooa hello file locali.</span><span class="sxs-lookup"><span data-stu-id="83b40-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="83b40-251">tipo di hello toospecify per blob hello, è possibile utilizzare il parametro - BlobType hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="83b40-252">esempio Hello esegue hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget cmdlet hello tutti i file nella cartella specificata hello e quindi li passa cmdlet successivo toohello utilizzando l'operatore pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="83b40-253">Hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet carica contenitore tooyour di hello file locali:</span><span class="sxs-lookup"><span data-stu-id="83b40-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="83b40-254">Come toodownload BLOB da un contenitore</span><span class="sxs-lookup"><span data-stu-id="83b40-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="83b40-255">Hello di esempio seguente viene illustrato come toodownload BLOB da un contenitore.</span><span class="sxs-lookup"><span data-stu-id="83b40-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="83b40-256">esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso primaria.</span><span class="sxs-lookup"><span data-stu-id="83b40-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="83b40-257">Quindi, hello esempio recupera un riferimento di blob utilizzando hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="83b40-258">Successivamente, esempio hello utilizza hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) BLOB toodownload cmdlet nella cartella di destinazione locale hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="83b40-259">Come toocopy BLOB da un tooanother di contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="83b40-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="83b40-260">È possibile copiare i BLOB tra aree e account di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="83b40-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="83b40-261">Hello esempio seguente viene illustrato come toocopy BLOB da archiviazione di un contenitore tooanother in due diversi account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="83b40-262">esempio Hello prima imposta le variabili per gli account di archiviazione di origine e di destinazione e quindi crea un contesto per ogni account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="83b40-263">Successivamente, esempio hello copia BLOB dal contenitore destinazione hello origine contenitore toohello utilizzando hello [inizio AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="83b40-264">Hello si presuppone che i contenitori e account di archiviazione di origine e destinazione hello esistano già.</span><span class="sxs-lookup"><span data-stu-id="83b40-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="83b40-265">In questo esempio viene eseguita una copia asincrona.</span><span class="sxs-lookup"><span data-stu-id="83b40-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="83b40-266">È possibile monitorare lo stato di hello di ogni copia eseguendo hello [Get AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="83b40-267">Come toocopy BLOB da una posizione secondaria</span><span class="sxs-lookup"><span data-stu-id="83b40-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="83b40-268">È possibile copiare BLOB dal percorso secondario di hello di un account RA-GRS abilitato.</span><span class="sxs-lookup"><span data-stu-id="83b40-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="83b40-269">Come toodelete un blob</span><span class="sxs-lookup"><span data-stu-id="83b40-269">How toodelete a blob</span></span>
<span data-ttu-id="83b40-270">un blob, toodelete innanzitutto ottenere un riferimento di blob, quindi chiamare cmdlet Remove-AzureStorageBlob hello su di esso.</span><span class="sxs-lookup"><span data-stu-id="83b40-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="83b40-271">Hello di esempio seguente elimina tutti i BLOB hello in un contenitore specificato.</span><span class="sxs-lookup"><span data-stu-id="83b40-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="83b40-272">esempio Hello prima imposta le variabili per un account di archiviazione e quindi crea un contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="83b40-273">Successivamente, hello esempio recupera un riferimento di blob utilizzando hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello cmdlet e viene eseguito [Remove AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove BLOB da un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="83b40-274">Come toomanage Azure blob snapshot</span><span class="sxs-lookup"><span data-stu-id="83b40-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="83b40-275">Azure consente di creare uno snapshot di un BLOB.</span><span class="sxs-lookup"><span data-stu-id="83b40-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="83b40-276">Uno snapshot è una versione di sola lettura di un BLOB eseguito in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="83b40-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="83b40-277">Una volta creato uno snapshot, è possibile leggerlo, copiarlo o eliminarlo, ma non modificarlo.</span><span class="sxs-lookup"><span data-stu-id="83b40-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="83b40-278">Gli snapshot forniscono un modo tooback backup di un blob così come viene visualizzato in un momento.</span><span class="sxs-lookup"><span data-stu-id="83b40-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="83b40-279">Per ulteriori informazioni, vedere [Creazione di uno Snapshot di un BLOB](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="83b40-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="83b40-280">Come toocreate uno snapshot di blob</span><span class="sxs-lookup"><span data-stu-id="83b40-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="83b40-281">toocreate dello stile di vita di un blob, innanzitutto ottenere un riferimento di blob e quindi chiamare hello `ICloudBlob.CreateSnapshot` metodo su di esso.</span><span class="sxs-lookup"><span data-stu-id="83b40-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="83b40-282">Hello esempio seguente imposta prima di tutto le variabili per un account di archiviazione e quindi crea un contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="83b40-283">Successivamente, hello esempio recupera un riferimento di blob utilizzando hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello cmdlet e viene eseguito [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate metodo uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="83b40-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="83b40-284">La modalità snapshot di toolist un blob</span><span class="sxs-lookup"><span data-stu-id="83b40-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="83b40-285">Non ci sono limiti agli snapshot creati per un BLOB.</span><span class="sxs-lookup"><span data-stu-id="83b40-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="83b40-286">È possibile elencare gli snapshot di hello associati tootrack i blob degli snapshot correnti.</span><span class="sxs-lookup"><span data-stu-id="83b40-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="83b40-287">esempio Hello utilizza un hello predefinito di blob e chiama [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) snapshot hello toolist di cmdlet del blob.</span><span class="sxs-lookup"><span data-stu-id="83b40-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="83b40-288">Come toocopy uno snapshot di un blob</span><span class="sxs-lookup"><span data-stu-id="83b40-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="83b40-289">È possibile copiare uno snapshot di uno snapshot di blob toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="83b40-290">Per informazioni dettagliate e le restrizioni, vedere [Creazione di uno Snapshot di un BLOB](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="83b40-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="83b40-291">Hello esempio seguente imposta prima di tutto le variabili per un account di archiviazione e quindi crea un contesto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="83b40-292">Successivamente, esempio hello definisce le variabili di nome contenitore e del blob hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="83b40-293">esempio Hello recupera un riferimento di blob utilizzando hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello cmdlet e viene eseguito [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate metodo uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="83b40-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="83b40-294">Esempio hello esegue quindi hello [inizio AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) snapshot hello toocopy di cmdlet di un blob utilizzando l'oggetto ICloudBlob hello per blob di origine hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="83b40-295">Essere assicurarsi che le variabili di hello tooupdate in base alla configurazione prima di esempio hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="83b40-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="83b40-296">Si noti che hello di esempio seguente si presuppone che hello contenitori di origine e di destinazione e il blob di origine hello esiste già.</span><span class="sxs-lookup"><span data-stu-id="83b40-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="83b40-297">Ora che si è appreso come BLOB di Azure toomanage e relativi snapshot con Azure PowerShell, passare toohello successiva sezione toolearn come toomanage tabelle, code e i file.</span><span class="sxs-lookup"><span data-stu-id="83b40-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="83b40-298">Come Azure toomanage tabelle e le entità di tabella</span><span class="sxs-lookup"><span data-stu-id="83b40-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="83b40-299">Servizio di archiviazione tabelle di Azure è un archivio dati NoSQL, che è possibile utilizzare set di grandi dimensioni toostore e query di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="83b40-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="83b40-300">componenti principali di Hello del servizio hello sono tabelle, entità e proprietà.</span><span class="sxs-lookup"><span data-stu-id="83b40-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="83b40-301">una tabella è una raccolta di entità.</span><span class="sxs-lookup"><span data-stu-id="83b40-301">A table is a collection of entities.</span></span> <span data-ttu-id="83b40-302">Un'entità è un set di proprietà.</span><span class="sxs-lookup"><span data-stu-id="83b40-302">An entity is a set of properties.</span></span> <span data-ttu-id="83b40-303">Ogni entità può avere proprietà too252, che sono tutte le coppie nome-valore.</span><span class="sxs-lookup"><span data-stu-id="83b40-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="83b40-304">In questa sezione si presuppone che si ha già familiarità con concetti del servizio di archiviazione tabelle Azure hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="83b40-305">Per informazioni dettagliate, vedere [hello comprensione modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx) e [Introduzione all'archiviazione tabelle di Azure usando .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="83b40-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="83b40-306">In hello seguenti sottosezioni, si apprenderà come toomanage archiviazione tabelle di Azure del servizio con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83b40-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="83b40-307">Hello scenari trattati includono **creazione**, **eliminazione**, e **recupero** **tabelle**, così come **aggiunta**, **l'esecuzione di query**, e **l'eliminazione di entità di tabella**.</span><span class="sxs-lookup"><span data-stu-id="83b40-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="83b40-308">Come toocreate una tabella</span><span class="sxs-lookup"><span data-stu-id="83b40-308">How toocreate a table</span></span>
<span data-ttu-id="83b40-309">Ogni tabella deve risiedere in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="83b40-310">Hello esempio seguente viene illustrato come toocreate una tabella in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="83b40-311">esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="83b40-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="83b40-312">Viene quindi utilizzato hello [New AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) toocreate cmdlet una tabella in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="83b40-313">Come tooretrieve una tabella</span><span class="sxs-lookup"><span data-stu-id="83b40-313">How tooretrieve a table</span></span>
<span data-ttu-id="83b40-314">È possibile eseguire query e recuperare una o tutte le tabelle di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="83b40-315">Hello esempio seguente viene illustrato come tooretrieve una determinata tabella utilizzando hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="83b40-316">Se si chiama il cmdlet Get-AzureStorageTable hello senza parametri, ottiene tutte le tabelle di archiviazione per un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="83b40-317">Come toodelete una tabella</span><span class="sxs-lookup"><span data-stu-id="83b40-317">How toodelete a table</span></span>
<span data-ttu-id="83b40-318">È possibile eliminare una tabella da un account di archiviazione tramite hello [Remove AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="83b40-319">Come toomanage tabella entità</span><span class="sxs-lookup"><span data-stu-id="83b40-319">How toomanage table entities</span></span>
<span data-ttu-id="83b40-320">Attualmente, Azure PowerShell non fornisce direttamente i cmdlet toomanage entità della tabella.</span><span class="sxs-lookup"><span data-stu-id="83b40-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="83b40-321">tooperform operazioni su entità tabella, è possibile utilizzare le classi di hello all'hello [Azure Storage Client Library per .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="83b40-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="83b40-322">Come tooadd tabella entità</span><span class="sxs-lookup"><span data-stu-id="83b40-322">How tooadd table entities</span></span>
<span data-ttu-id="83b40-323">tooadd tabella tooa un'entità, creare innanzitutto un oggetto che definisce le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="83b40-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="83b40-324">Un'entità può contenere proprietà too255, incluse 3 proprietà di sistema: **PartitionKey**, **RowKey**, e **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="83b40-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="83b40-325">L'utente è responsabile per l'inserimento e aggiornamento dei valori hello di **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="83b40-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="83b40-326">server Hello gestisce il valore di hello di **Timestamp**, che non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="83b40-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="83b40-327">Hello insieme **PartitionKey** e **RowKey** identificare in modo univoco ogni entità in una tabella.</span><span class="sxs-lookup"><span data-stu-id="83b40-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="83b40-328">**PartitionKey**: determina partizione hello archiviati in entità hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="83b40-329">**RowKey**: identifica in modo univoco l'entità hello all'interno della partizione hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="83b40-330">È possibile definire le proprietà personalizzate di too252 per un'entità.</span><span class="sxs-lookup"><span data-stu-id="83b40-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="83b40-331">Per ulteriori informazioni, vedere [hello comprensione modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="83b40-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="83b40-332">Hello esempio seguente viene illustrato come tabella di tooa tooadd entità.</span><span class="sxs-lookup"><span data-stu-id="83b40-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="83b40-333">Hello riportato di seguito viene illustrato tooretrieve hello tabella employee e come aggiungere alcune entità al suo interno.</span><span class="sxs-lookup"><span data-stu-id="83b40-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="83b40-334">Prima di tutto, stabilisce un tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="83b40-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="83b40-335">Successivamente, viene recuperata hello data tabella utilizzando hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="83b40-336">Se non esiste nella tabella hello, hello [New AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet è toocreate utilizzata una tabella in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="83b40-337">Successivamente, hello esempio definisce una funzione personalizzata nella tabella toohello entità tooadd Aggiungi entità specificando ogni di partizione e chiave di riga.</span><span class="sxs-lookup"><span data-stu-id="83b40-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="83b40-338">hello chiamate di funzione Hello Aggiungi entità [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate classe un oggetto entità.</span><span class="sxs-lookup"><span data-stu-id="83b40-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="83b40-339">In un secondo momento, esempio hello chiama hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) metodo su questo tooadd oggetto entità tooa tabella.</span><span class="sxs-lookup"><span data-stu-id="83b40-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
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

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="83b40-340">Come tooquery tabella entità</span><span class="sxs-lookup"><span data-stu-id="83b40-340">How tooquery table entities</span></span>
<span data-ttu-id="83b40-341">tooquery una tabella, utilizzare hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="83b40-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="83b40-342">Hello seguente si presuppone di aver già eseguire script hello all'hello come sezione entità tooadd di questa Guida.</span><span class="sxs-lookup"><span data-stu-id="83b40-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="83b40-343">esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto archiviazione hello, che include nome account di archiviazione hello e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="83b40-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="83b40-344">Successivamente, si tenta di tabella di dipendenti"hello creato in precedenza" tooretrieve utilizzando hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="83b40-345">Chiamare il metodo hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello Microsoft.WindowsAzure.Storage.Table.TableQuery classe crea un nuovo oggetto di query.</span><span class="sxs-lookup"><span data-stu-id="83b40-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="83b40-346">esempio Hello ricerca entità hello che dispongono di una colonna di 'ID' il cui valore è 1, come specificato in un filtro di stringa.</span><span class="sxs-lookup"><span data-stu-id="83b40-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="83b40-347">Per informazioni dettagliate, vedere [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx) (Esecuzione di query su tabelle ed entità).</span><span class="sxs-lookup"><span data-stu-id="83b40-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="83b40-348">Quando si esegue questa query, restituisce tutte le entità che soddisfano i criteri di filtro hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="83b40-349">Come toodelete tabella entità</span><span class="sxs-lookup"><span data-stu-id="83b40-349">How toodelete table entities</span></span>
<span data-ttu-id="83b40-350">È possibile eliminare un'entità utilizzando le relative chiavi di riga e di partizione.</span><span class="sxs-lookup"><span data-stu-id="83b40-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="83b40-351">Hello seguente si presuppone di aver già eseguire script hello all'hello come sezione entità tooadd di questa Guida.</span><span class="sxs-lookup"><span data-stu-id="83b40-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="83b40-352">esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto archiviazione hello, che include nome account di archiviazione hello e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="83b40-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="83b40-353">Successivamente, si tenta di tabella di dipendenti"hello creato in precedenza" tooretrieve utilizzando hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="83b40-354">Se hello tabella esiste, l'esempio hello chiama hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve metodo un'entità in base ai relativi valori chiavi di riga e di partizione.</span><span class="sxs-lookup"><span data-stu-id="83b40-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="83b40-355">Passare quindi hello entità toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete metodo.</span><span class="sxs-lookup"><span data-stu-id="83b40-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="83b40-356">Come mettere in coda e coda di messaggi toomanage Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="83b40-357">Archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="83b40-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="83b40-358">In questa sezione si presuppone che si conoscono già i concetti di hello servizio di archiviazione di Accodamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="83b40-359">Per informazioni dettagliate, vedere [Introduzione all'archivio code di Azure con .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="83b40-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="83b40-360">Questa sezione verranno illustrate le modalità di servizio con Azure PowerShell toomanage l'archiviazione delle code di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="83b40-361">Hello scenari trattati includono **inserimento** e **eliminazione** coda di messaggi, nonché **creazione**, **eliminazione**, e**il recupero delle code**.</span><span class="sxs-lookup"><span data-stu-id="83b40-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="83b40-362">Come toocreate una coda</span><span class="sxs-lookup"><span data-stu-id="83b40-362">How toocreate a queue</span></span>
<span data-ttu-id="83b40-363">Hello esempio stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="83b40-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="83b40-364">Successivamente, chiama [New AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) toocreate cmdlet una coda denominata 'queuename'.</span><span class="sxs-lookup"><span data-stu-id="83b40-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="83b40-365">Per informazioni sulle convenzioni di denominazione per il servizio di accodamento di Azure, vedere [Denominazione di code e metadati](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="83b40-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="83b40-366">Come tooretrieve una coda</span><span class="sxs-lookup"><span data-stu-id="83b40-366">How tooretrieve a queue</span></span>
<span data-ttu-id="83b40-367">È possibile eseguire una query e recuperare un elenco di tutte le code di hello in un account di archiviazione o di una coda specifica.</span><span class="sxs-lookup"><span data-stu-id="83b40-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="83b40-368">Hello esempio seguente viene illustrato come una coda specificata tramite tooretrieve hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="83b40-369">Se si chiama hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet senza parametri, ottiene un elenco di tutte le code di hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="83b40-370">Come toodelete una coda</span><span class="sxs-lookup"><span data-stu-id="83b40-370">How toodelete a queue</span></span>
<span data-ttu-id="83b40-371">toodelete una coda e tutti i messaggi hello in esso contenuti, cmdlet Remove-AzureStorageQueue hello chiamata.</span><span class="sxs-lookup"><span data-stu-id="83b40-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="83b40-372">Hello di esempio seguente viene illustrato come una coda specificata tramite toodelete hello cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="83b40-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="83b40-373">Come tooinsert un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="83b40-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="83b40-374">tooinsert un messaggio in una coda esistente, creare innanzitutto una nuova istanza di hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="83b40-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="83b40-375">Successivamente, chiamare hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metodo.</span><span class="sxs-lookup"><span data-stu-id="83b40-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="83b40-376">È possibile creare un oggetto CloudQueueMessage da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="83b40-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="83b40-377">Hello di esempio seguente viene illustrato come tooadd tooa coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="83b40-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="83b40-378">esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="83b40-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="83b40-379">Successivamente, viene recuperato utilizzando hello la coda specificata hello [Get AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83b40-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="83b40-380">Se la coda hello, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet viene utilizzato toocreate un'istanza di hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="83b40-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="83b40-381">In un secondo momento, esempio hello chiama hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metodo su questo tooadd di oggetto del messaggio è tooa coda.</span><span class="sxs-lookup"><span data-stu-id="83b40-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="83b40-382">Ecco il codice che consente di recuperare una coda e inserisce il messaggio hello 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="83b40-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="83b40-383">Il messaggio successivo toode-coda hello</span><span class="sxs-lookup"><span data-stu-id="83b40-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="83b40-384">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="83b40-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="83b40-385">Quando si chiama hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) metodo, di ottenere il messaggio hello successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="83b40-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="83b40-386">Un messaggio restituito da **GetMessage** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda.</span><span class="sxs-lookup"><span data-stu-id="83b40-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="83b40-387">toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) metodo.</span><span class="sxs-lookup"><span data-stu-id="83b40-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="83b40-388">Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare.</span><span class="sxs-lookup"><span data-stu-id="83b40-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="83b40-389">Il codice chiama **DeleteMessage** subito dopo il messaggio hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="83b40-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="83b40-390">Come file di Azure toomanage condivide e i file</span><span class="sxs-lookup"><span data-stu-id="83b40-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="83b40-391">Archiviazione di File di Azure offre archiviazione condivisa per applicazioni che utilizzano il protocollo SMB standard di hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="83b40-392">Macchine virtuali di Microsoft Azure e servizi cloud possono condividere i dati di file nei componenti delle applicazioni tramite condivisioni montate e applicazioni locali possono accedere ai dati dei file in una condivisione tramite API di archiviazione di File hello o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83b40-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="83b40-393">Per informazioni dettagliate su Archiviazione file di Azure, vedere [Introduzione ad Archiviazione file di Azure in Windows](storage-dotnet-how-to-use-files.md) e [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx) (API REST del servizio file).</span><span class="sxs-lookup"><span data-stu-id="83b40-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="83b40-394">La modalità query e tooset analitica di archiviazione</span><span class="sxs-lookup"><span data-stu-id="83b40-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="83b40-395">È possibile utilizzare [Analitica di archiviazione di Azure](storage-analytics.md) toocollect metriche per l'account di archiviazione di Azure e sulle richieste di dati del log inviati tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-395">You can use [Azure Storage Analytics](storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="83b40-396">È possibile utilizzare stato toomonitor hello metriche di archiviazione di un account di archiviazione e l'archiviazione registrazione toodiagnose e risolvere i problemi con l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="83b40-397">È possibile configurare il monitoraggio tramite hello portale di Azure o Windows PowerShell o a livello di programmazione tramite libreria client di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="83b40-398">Registrazione di archiviazione si verifica sul lato server e consente toorecord dettagli per le richieste con esito positivo e non riuscite nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="83b40-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="83b40-399">Questi log consentono di dettagli toosee di lettura, scrittura e le operazioni di eliminazione contro le tabelle, code e BLOB, nonché motivi hello per le richieste non riuscite.</span><span class="sxs-lookup"><span data-stu-id="83b40-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="83b40-400">toolearn tooenable e visualizzare i dati di metrica di archiviazione usando PowerShell, vedere [come tooenable metriche di archiviazione con PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="83b40-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="83b40-401">toolearn tooenable e recuperare dati di registrazione archiviazione usando PowerShell, vedere [come tooenable archiviazione registrazione tramite PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) e [ricerca dei dati di log di registrazione archiviazione](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="83b40-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="83b40-402">Per informazioni dettagliate sull'uso di metriche di archiviazione e i problemi di archiviazione tootroubleshoot alla registrazione di archiviazione, vedere [monitoraggio, diagnostica e risoluzione dei problemi di archiviazione di Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="83b40-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="83b40-403">Come toomanage condiviso (SAS) di firma di accesso e criteri di accesso archiviati</span><span class="sxs-lookup"><span data-stu-id="83b40-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="83b40-404">Firme di accesso condiviso sono una parte importante del modello di sicurezza hello per le applicazioni che utilizzano l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="83b40-405">Sono utili per fornire autorizzazioni limitate tooyour storage account tooclients che non dovrebbero essere chiave dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="83b40-406">Per impostazione predefinita, solo il hello proprietario dell'account di archiviazione hello può accedere BLOB, tabelle e code all'interno di tale account.</span><span class="sxs-lookup"><span data-stu-id="83b40-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="83b40-407">Se il servizio o l'applicazione deve toomake questi client tooother disponibili risorse senza condividere la chiave di accesso, sono disponibili tre opzioni:</span><span class="sxs-lookup"><span data-stu-id="83b40-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="83b40-408">Impostare autorizzazioni toopermit accesso in lettura anonimo toohello contenitore di un contenitore e i relativi BLOB.</span><span class="sxs-lookup"><span data-stu-id="83b40-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="83b40-409">Questa operazione non è consentita per le tabelle o le code.</span><span class="sxs-lookup"><span data-stu-id="83b40-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="83b40-410">Utilizzare una firma di accesso condiviso che concede toocontainers diritti di accesso limitato, BLOB, code e tabelle per un intervallo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="83b40-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="83b40-411">Utilizzare un tooobtain di criteri di accesso archiviati un ulteriore livello di controllo sulle firme di accesso condiviso per un contenitore o i relativi BLOB, per una coda o per una tabella.</span><span class="sxs-lookup"><span data-stu-id="83b40-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="83b40-412">Hello criteri di accesso archiviati consentono ora di inizio hello toochange, ora di scadenza o le autorizzazioni per una firma, o toorevoke dopo è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="83b40-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="83b40-413">Una firma di accesso condiviso può assumere una delle due forme seguenti:</span><span class="sxs-lookup"><span data-stu-id="83b40-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="83b40-414">**Firma di accesso condiviso ad hoc**: quando si crea una firma di accesso condiviso ad hoc, l'ora di inizio hello, ora di scadenza e le autorizzazioni per hello SAS vengono specificate in hello URI SAS.</span><span class="sxs-lookup"><span data-stu-id="83b40-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="83b40-415">Questo tipo di firma di accesso condiviso può essere creato per un contenitore, un BLOB, una tabella e una coda e non è revocabile.</span><span class="sxs-lookup"><span data-stu-id="83b40-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="83b40-416">**Firma di accesso condiviso con criteri di accesso archiviati**: è definito un criterio di accesso archiviati in un contenitore di risorse un contenitore blob, tabella o coda - ed è possibile utilizzarlo toomanage vincoli per uno o più firme di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="83b40-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="83b40-417">Quando si associa una firma di accesso condiviso con criteri di accesso archiviati, hello SAS eredita i vincoli di hello: hello ora di inizio, ora di scadenza e le autorizzazioni - definite per i criteri di accesso archiviato hello.</span><span class="sxs-lookup"><span data-stu-id="83b40-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="83b40-418">Questo tipo di firma di accesso condiviso è revocabile.</span><span class="sxs-lookup"><span data-stu-id="83b40-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="83b40-419">Per ulteriori informazioni, vedere [tramite firme di accesso condiviso (SAS)](storage-dotnet-shared-access-signature-part-1.md) e [gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="83b40-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="83b40-420">Nelle sezioni successive di hello, si apprenderà come toocreate un criterio di accesso stored e token di firma di accesso condiviso per le tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="83b40-421">Azure PowerShell fornisce cmdlet simili per contenitori, BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="83b40-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="83b40-422">script di hello toorun in questa sezione, scaricare hello [Azure PowerShell versione 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="83b40-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="83b40-423">Il token di firma di accesso condiviso toocreate basata su criteri</span><span class="sxs-lookup"><span data-stu-id="83b40-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="83b40-424">Utilizzare toocreate di cmdlet New-AzureStorageTableStoredAccessPolicy hello un nuovo criterio di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="83b40-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="83b40-425">Chiamare quindi hello [New AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate cmdlet un nuovo token di firma basata su criteri di accesso condiviso per una tabella di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83b40-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="83b40-426">Come toocreate un token di firma di accesso condiviso ad hoc (non revocabile)</span><span class="sxs-lookup"><span data-stu-id="83b40-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="83b40-427">Hello utilizzare [New AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate cmdlet un token di firma di accesso condiviso (non revocabile) a ad hoc nuovo per una tabella di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="83b40-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="83b40-428">Come criteri di accesso archiviati toocreate</span><span class="sxs-lookup"><span data-stu-id="83b40-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="83b40-429">Utilizzare toocreate cmdlet New-AzureStorageTableStoredAccessPolicy hello un nuovo criterio di accesso archiviati per una tabella di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="83b40-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="83b40-430">Come criteri di accesso archiviati tooupdate</span><span class="sxs-lookup"><span data-stu-id="83b40-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="83b40-431">Utilizzare tooupdate di cmdlet Set-AzureStorageTableStoredAccessPolicy hello un criterio di accesso archiviati per una tabella di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="83b40-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="83b40-432">Come criteri di accesso archiviati toodelete</span><span class="sxs-lookup"><span data-stu-id="83b40-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="83b40-433">Utilizzare toodelete cmdlet Remove-AzureStorageTableStoredAccessPolicy hello criteri di accesso archiviati in una tabella di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="83b40-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="83b40-434">Come toouse di archiviazione di Azure per governo degli Stati Uniti e Cina di Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="83b40-435">Un ambiente Azure è una distribuzione indipendente di Microsoft Azure, ad esempio [Azure Government per il governo degli Stati Uniti](https://azure.microsoft.com/features/gov/), [AzureCloud per Azure globale](https://portal.azure.com) e [AzureChinaCloud per Azure gestito da 21Vianet in Cina](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="83b40-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="83b40-436">È possibile distribuire nuovi ambienti Azure per il governo degli Stati Uniti e Azure Cina.</span><span class="sxs-lookup"><span data-stu-id="83b40-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="83b40-437">Archiviazione di Azure con AzureChinaCloud toouse, è necessario un contesto di archiviazione associato AzureChinaCloud toocreate.</span><span class="sxs-lookup"><span data-stu-id="83b40-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="83b40-438">Seguire tooget questi passaggi per iniziare:</span><span class="sxs-lookup"><span data-stu-id="83b40-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="83b40-439">Eseguire hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet hello ambienti Azure disponibili:</span><span class="sxs-lookup"><span data-stu-id="83b40-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="83b40-440">Aggiungere un tooWindows account Cina di Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="83b40-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="83b40-441">Creare un contesto di archiviazione per un account AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="83b40-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="83b40-442">Archiviazione di Azure toouse con [Stati Uniti degli Stati Uniti](https://azure.microsoft.com/features/gov/), è necessario definire un nuovo ambiente e creare un nuovo contesto di archiviazione con questo ambiente:</span><span class="sxs-lookup"><span data-stu-id="83b40-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="83b40-443">Eseguire hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet hello ambienti Azure disponibili:</span><span class="sxs-lookup"><span data-stu-id="83b40-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="83b40-444">Aggiungere un tooWindows di account di Azure del governo PowerShell:</span><span class="sxs-lookup"><span data-stu-id="83b40-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="83b40-445">Creare un contesto di archiviazione per un account AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="83b40-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="83b40-446">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="83b40-446">For more information, see:</span></span>

* <span data-ttu-id="83b40-447">[Guida per gli sviluppatori di Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="83b40-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="83b40-448">Panoramica delle differenze nella creazione di un'applicazione in China Service</span><span class="sxs-lookup"><span data-stu-id="83b40-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="83b40-449">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83b40-449">Next Steps</span></span>
<span data-ttu-id="83b40-450">In questa Guida, si è appreso come toomanage archiviazione di Azure con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83b40-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="83b40-451">Per altre informazioni, vedere gli articoli e le risorse correlati seguenti:</span><span class="sxs-lookup"><span data-stu-id="83b40-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="83b40-452">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="83b40-453">Cmdlet di PowerShell per Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="83b40-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="83b40-454">Riferimenti Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="83b40-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
