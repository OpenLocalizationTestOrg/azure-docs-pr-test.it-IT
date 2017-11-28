---
title: i cmdlet di PowerShell con Azure RemoteApp aaaUse | Documenti Microsoft
description: Informazioni su come toouse cmdlet di Windows PowerShell in Azure RemoteApp.
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
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="635e1-103">Usare i cmdlet Windows PowerShell con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="635e1-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="635e1-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="635e1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="635e1-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="635e1-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="635e1-106">È possibile utilizzare tooadminister i cmdlet di PowerShell di Azure RemoteApp hello e mantenere le raccolte.</span><span class="sxs-lookup"><span data-stu-id="635e1-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="635e1-107">Utilizzare hello seguente tooget informazioni avviato.</span><span class="sxs-lookup"><span data-stu-id="635e1-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="635e1-108">Ottenere i cmdlet di hello</span><span class="sxs-lookup"><span data-stu-id="635e1-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="635e1-109">Prima di scaricare i cmdlet di Azure Powershell hello [qui](http://go.microsoft.com/?linkid=9811175), sono inclusi i cmdlet di RemoteApp hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="635e1-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="635e1-110">Estrarre hello [Guida sui cmdlet di Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="635e1-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="635e1-111">Configura la sottoscrizione di toouse i cmdlet di Azure</span><span class="sxs-lookup"><span data-stu-id="635e1-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="635e1-112">Seguire [questa Guida](/powershell/azure/overview) in modo è possibile utilizzare i cmdlet di hello rispetto alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="635e1-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="635e1-113">È possibile utilizzare tooget questi passaggi in tempi brevi:</span><span class="sxs-lookup"><span data-stu-id="635e1-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="635e1-114">Scaricare e installare hello [cmdlet di Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="635e1-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="635e1-115">Avviare Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="635e1-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="635e1-116">Eseguire **Add-AzureAccount** tooauthenticate tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="635e1-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="635e1-117">Quando richiesto, immettere hello stesso nome utente e password che si usa toosign nel portale di tooAzure.</span><span class="sxs-lookup"><span data-stu-id="635e1-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="635e1-118">Eseguire **Get-AzureSubscription** sottoscrizioni hello toolist associate all'account utente.</span><span class="sxs-lookup"><span data-stu-id="635e1-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="635e1-119">Eseguire **Select-AzureSubscription - SubscriptionName &lt;nome sottoscrizione&gt;**  o **Select-AzureSubscription - SubscriptionId &lt;ID sottoscrizione&gt;**  toospecify hello sottoscrizione toouse.</span><span class="sxs-lookup"><span data-stu-id="635e1-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="635e1-120">Complimenti, la console di PowerShell di Azure è configurato e pronto toouse.</span><span class="sxs-lookup"><span data-stu-id="635e1-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="635e1-121">Tenere presente che è necessario toorepeate i passaggi da 2 a 5 ogni volta che si avvia console di Azure PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="635e1-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="635e1-122">Elencare tutte le raccolte</span><span class="sxs-lookup"><span data-stu-id="635e1-122">List all collections</span></span>
- - -
     <span data-ttu-id="635e1-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="635e1-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="635e1-124">Eliminare una raccolta</span><span class="sxs-lookup"><span data-stu-id="635e1-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="635e1-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="635e1-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="635e1-126">Esempio: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="635e1-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="635e1-127">Creare una raccolta nel cloud</span><span class="sxs-lookup"><span data-stu-id="635e1-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="635e1-128">È semplice, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="635e1-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="635e1-129">Hello sopra comando Pubblica automaticamente le applicazioni di Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio e Word).</span><span class="sxs-lookup"><span data-stu-id="635e1-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="635e1-130">Creazione della raccolta può richiedere 30 minuti o più toocomplete.</span><span class="sxs-lookup"><span data-stu-id="635e1-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="635e1-131">Questo comando restituisce quindi un ID di traccia che è possibile usare come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="635e1-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="635e1-132">Al termine dell'insieme di hello, è possibile aggiungere una raccolta degli utenti toohello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="635e1-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="635e1-133">L'operazione è così completata.</span><span class="sxs-lookup"><span data-stu-id="635e1-133">And you're done!</span></span> <span data-ttu-id="635e1-134">Tale utente deve essere in grado di tooconnect toohello applicazione utilizzando il client di Azure RemoteApp hello trovato [qui](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="635e1-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="635e1-135">Cmdlet disponibili</span><span class="sxs-lookup"><span data-stu-id="635e1-135">Available cmdlets</span></span>
<span data-ttu-id="635e1-136">Esistono molti altri comandi che è disponibile, a breve sarà presto documentazione hello:</span><span class="sxs-lookup"><span data-stu-id="635e1-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="635e1-137">Cmdlet della raccolta RemoteApp di base:</span><span class="sxs-lookup"><span data-stu-id="635e1-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="635e1-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="635e1-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="635e1-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="635e1-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="635e1-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="635e1-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="635e1-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="635e1-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="635e1-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="635e1-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="635e1-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="635e1-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="635e1-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="635e1-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="635e1-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="635e1-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="635e1-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="635e1-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="635e1-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="635e1-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="635e1-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="635e1-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="635e1-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="635e1-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="635e1-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="635e1-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="635e1-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="635e1-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="635e1-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="635e1-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="635e1-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="635e1-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="635e1-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="635e1-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="635e1-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="635e1-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="635e1-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="635e1-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="635e1-157">Cmdlet della rete virtuale RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="635e1-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="635e1-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="635e1-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="635e1-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="635e1-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="635e1-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="635e1-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="635e1-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="635e1-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="635e1-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="635e1-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="635e1-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="635e1-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="635e1-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="635e1-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="635e1-165">Cmdlet dell'immagine modello RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="635e1-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="635e1-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="635e1-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="635e1-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="635e1-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="635e1-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="635e1-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="635e1-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="635e1-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="635e1-170">Altri cmdlet di RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="635e1-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="635e1-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="635e1-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="635e1-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="635e1-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="635e1-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="635e1-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="635e1-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="635e1-174">Get-AzureRemoteAppOperationResult</span></span>

