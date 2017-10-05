---
title: Usare i cmdlet PowerShell con Azure RemoteApp | Microsoft Docs
description: Informazioni su come usare i cmdlet Windows PowerShell in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="af1b0-103">Usare i cmdlet Windows PowerShell con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="af1b0-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="af1b0-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="af1b0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="af1b0-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="af1b0-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="af1b0-106">È possibile usare i cmdlet Azure RemoteApp PowerShell per amministrare e gestire le raccolte.</span><span class="sxs-lookup"><span data-stu-id="af1b0-106">You can use the Azure RemoteApp PowerShell cmdlets to administer and maintain your collections.</span></span> <span data-ttu-id="af1b0-107">Per iniziare, usare le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="af1b0-107">Use the following information to get started.</span></span>

## <a name="get-the-cmdlets"></a><span data-ttu-id="af1b0-108">Ottenere i cmdlet</span><span class="sxs-lookup"><span data-stu-id="af1b0-108">Get the cmdlets</span></span>
- - -
<span data-ttu-id="af1b0-109">Prima di tutto scaricare i cmdlet di Azure PowerShell [qui](http://go.microsoft.com/?linkid=9811175). I cmdlet di RemoteApp sono inclusi.</span><span class="sxs-lookup"><span data-stu-id="af1b0-109">First download the Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), the RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="af1b0-110">Vedere la [guida dei cmdlet di Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="af1b0-110">Check out the [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a><span data-ttu-id="af1b0-111">Configurare i cmdlet di Azure per usare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="af1b0-111">Configure Azure cmdlets to use your subscription</span></span>
- - -
<span data-ttu-id="af1b0-112">Seguire [questa guida](/powershell/azure/overview) per poter usare i cmdlet con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="af1b0-112">Follow [this guide](/powershell/azure/overview) so you can use the cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="af1b0-113">Per iniziare rapidamente è possibile eseguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="af1b0-113">You can use these steps to get started quickly:</span></span>

1. <span data-ttu-id="af1b0-114">Scaricare e installare i [cmdlet di Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="af1b0-114">Download and install the [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="af1b0-115">Avviare Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af1b0-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="af1b0-116">Eseguire **Add-AzureAccount** per l'autenticazione alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="af1b0-116">Run **Add-AzureAccount** to authenticate to your Azure subscription.</span></span> <span data-ttu-id="af1b0-117">Quando richiesto, immettere il nome utente e la password usati per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="af1b0-117">When prompted, enter the same user name and password that you use to sign in to Azure portal.</span></span>  
4. <span data-ttu-id="af1b0-118">Eseguire **Get-AzureSubscription** per elencare le sottoscrizioni associate all'account utente.</span><span class="sxs-lookup"><span data-stu-id="af1b0-118">Run **Get-AzureSubscription** to list the subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="af1b0-119">Eseguire **Select-AzureSubscription - SubscriptionName &lt;nome sottoscrizione&gt;**  o **Select-AzureSubscription - SubscriptionId &lt;ID sottoscrizione&gt;**  per specificare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="af1b0-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** to specify the subscription to use.</span></span>

<span data-ttu-id="af1b0-120">La console di Azure PowerShell è configurata e pronta per l'uso.</span><span class="sxs-lookup"><span data-stu-id="af1b0-120">Congratulations, your Azure PowerShell console is configured and ready to use.</span></span> <span data-ttu-id="af1b0-121">Tenere presente che sarà necessario ripetere i passaggi da 2 a 5 ogni volta che si avvia la console di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af1b0-121">Be aware that you'll need to repeate steps 2 through 5 each time you start the the Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="af1b0-122">Elencare tutte le raccolte</span><span class="sxs-lookup"><span data-stu-id="af1b0-122">List all collections</span></span>
- - -
     <span data-ttu-id="af1b0-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="af1b0-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="af1b0-124">Eliminare una raccolta</span><span class="sxs-lookup"><span data-stu-id="af1b0-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="af1b0-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="af1b0-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="af1b0-126">Esempio: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="af1b0-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="af1b0-127">Creare una raccolta nel cloud</span><span class="sxs-lookup"><span data-stu-id="af1b0-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="af1b0-128">È semplice, basta eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="af1b0-128">It's simple, run the following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="af1b0-129">Il comando precedente pubblica automaticamente le applicazioni di Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio e Word).</span><span class="sxs-lookup"><span data-stu-id="af1b0-129">The above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="af1b0-130">Per completare la creazione della raccolta possono essere necessari anche più di 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="af1b0-130">Collection creation can take 30 minutes or longer to complete.</span></span> <span data-ttu-id="af1b0-131">Questo comando restituisce quindi un ID di traccia che è possibile usare come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="af1b0-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="af1b0-132">Dopo aver completato la creazione della raccolta, è possibile aggiungervi utenti con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="af1b0-132">After the collection is done, you can add users to the collection with the following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="af1b0-133">L'operazione è così completata.</span><span class="sxs-lookup"><span data-stu-id="af1b0-133">And you're done!</span></span> <span data-ttu-id="af1b0-134">L'utente dovrebbe essere in grado di connettersi all'applicazione tramite il client Azure RemoteApp disponibile [qui](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="af1b0-134">That user should be able to connect to the application using the Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="af1b0-135">Cmdlet disponibili</span><span class="sxs-lookup"><span data-stu-id="af1b0-135">Available cmdlets</span></span>
<span data-ttu-id="af1b0-136">Sono disponibili molti altri comandi, la cui documentazione sarà disponibile a breve:</span><span class="sxs-lookup"><span data-stu-id="af1b0-136">There are lots of other commands that we have, the documentation for them will be coming shortly:</span></span>

<span data-ttu-id="af1b0-137">Cmdlet della raccolta RemoteApp di base:</span><span class="sxs-lookup"><span data-stu-id="af1b0-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="af1b0-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="af1b0-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="af1b0-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="af1b0-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="af1b0-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="af1b0-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="af1b0-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="af1b0-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="af1b0-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="af1b0-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="af1b0-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="af1b0-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="af1b0-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="af1b0-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="af1b0-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="af1b0-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="af1b0-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="af1b0-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="af1b0-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="af1b0-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="af1b0-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="af1b0-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="af1b0-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="af1b0-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="af1b0-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="af1b0-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="af1b0-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="af1b0-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="af1b0-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="af1b0-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="af1b0-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="af1b0-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="af1b0-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="af1b0-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="af1b0-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="af1b0-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="af1b0-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="af1b0-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="af1b0-157">Cmdlet della rete virtuale RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="af1b0-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="af1b0-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="af1b0-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="af1b0-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="af1b0-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="af1b0-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="af1b0-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="af1b0-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="af1b0-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="af1b0-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="af1b0-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="af1b0-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="af1b0-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="af1b0-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="af1b0-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="af1b0-165">Cmdlet dell'immagine modello RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="af1b0-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="af1b0-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="af1b0-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="af1b0-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="af1b0-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="af1b0-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="af1b0-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="af1b0-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="af1b0-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="af1b0-170">Altri cmdlet di RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="af1b0-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="af1b0-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="af1b0-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="af1b0-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="af1b0-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="af1b0-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="af1b0-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="af1b0-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="af1b0-174">Get-AzureRemoteAppOperationResult</span></span>

