---
title: 'Creare e modificare un circuito ExpressRoute: PowerShell: Azure classico| Microsoft Docs'
description: In questo articolo vengono illustrati i passaggi hello per la creazione e il provisioning di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornare, o eliminare, quindi eseguire il deprovisioning del circuito.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="7732e-104">Creare e modificare un circuito ExpressRoute mediante PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="7732e-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7732e-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7732e-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="7732e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7732e-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="7732e-107">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7732e-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="7732e-108">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7732e-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="7732e-109">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="7732e-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="7732e-110">In questo articolo illustra hello passaggi toocreate un circuito ExpressRoute di Azure con modello di distribuzione classica hello e di cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7732e-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="7732e-111">Mostra anche come stato hello toocheck, aggiornare, o eliminare e il deprovisioning di un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7732e-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="7732e-112">**Informazioni sui modelli di distribuzione di Azure**</span><span class="sxs-lookup"><span data-stu-id="7732e-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="7732e-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7732e-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="7732e-114">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="7732e-114">Step 1.</span></span> <span data-ttu-id="7732e-115">Rivedere i prerequisiti di hello e gli articoli del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="7732e-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="7732e-116">Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="7732e-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="7732e-117">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="7732e-117">Step 2.</span></span> <span data-ttu-id="7732e-118">Installare le versioni più recenti di hello dei moduli di PowerShell di gestione del servizio di Azure (SM) hello</span><span class="sxs-lookup"><span data-stu-id="7732e-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="7732e-119">Seguire le istruzioni hello [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/overview) per istruzioni dettagliate su come tooconfigure i moduli di Azure PowerShell hello toouse computer.</span><span class="sxs-lookup"><span data-stu-id="7732e-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="7732e-120">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="7732e-120">Step 3.</span></span> <span data-ttu-id="7732e-121">Accedi tooyour account Azure e selezionare una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="7732e-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="7732e-122">Aprire la console di PowerShell con diritti elevati e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="7732e-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="7732e-123">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="7732e-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="7732e-124">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="7732e-125">Se si dispone di più di una sottoscrizione, selezionare una sottoscrizione di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="7732e-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="7732e-126">Successivamente, utilizzare hello seguente cmdlet tooadd tooPowerShell la sottoscrizione di Azure per il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="7732e-127">Creare un circuito ExpressRoute ed eseguirne il provisioning</span><span class="sxs-lookup"><span data-stu-id="7732e-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="7732e-128">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="7732e-128">Step 1.</span></span> <span data-ttu-id="7732e-129">Importare i moduli di PowerShell hello per ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7732e-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="7732e-130">Se non è già stato fatto, è necessario importare i moduli di Azure ed ExpressRoute hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="7732e-131">Importare i moduli di hello da hello percorso in cui erano installati tooon nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="7732e-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="7732e-132">In base al metodo hello è utilizzato moduli hello tooinstall, percorso hello potrebbe essere diverso da hello esempio illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7732e-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="7732e-133">Se necessario, modificare l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="7732e-134">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="7732e-134">Step 2.</span></span> <span data-ttu-id="7732e-135">Ottenere l'elenco di hello di provider supportati, posizioni e delle larghezze di banda</span><span class="sxs-lookup"><span data-stu-id="7732e-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="7732e-136">Prima di creare un circuito ExpressRoute, è necessario l'elenco di hello del provider di connettività supportate, località e le opzioni di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="7732e-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="7732e-137">cmdlet di PowerShell Hello `Get-AzureDedicatedCircuitServiceProvider` restituisce queste informazioni, che verranno usati nei passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="7732e-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="7732e-138">Controllare toosee se viene elencato il provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="7732e-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="7732e-139">Prendere nota di hello perché sarà necessaria successivamente quando si crea un circuito le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="7732e-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="7732e-140">Nome</span><span class="sxs-lookup"><span data-stu-id="7732e-140">Name</span></span>
* <span data-ttu-id="7732e-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="7732e-141">PeeringLocations</span></span>
* <span data-ttu-id="7732e-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="7732e-142">BandwidthsOffered</span></span>

<span data-ttu-id="7732e-143">Si è ora pronto toocreate un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7732e-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="7732e-144">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="7732e-144">Step 3.</span></span> <span data-ttu-id="7732e-145">Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7732e-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="7732e-146">Hello di esempio seguente viene illustrato come un ExpressRoute a 200 Mbps toocreate circuit tramite Equinix Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="7732e-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="7732e-147">Se si usa un altro provider e impostazioni diverse, sostituire tali informazioni al momento della richiesta.</span><span class="sxs-lookup"><span data-stu-id="7732e-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7732e-148">Dal momento hello che viene eseguita una chiave del servizio verrà addebitato il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7732e-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="7732e-149">Assicurarsi di eseguire questa operazione quando il provider di connettività hello è circuito hello tooprovision pronto.</span><span class="sxs-lookup"><span data-stu-id="7732e-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="7732e-150">di seguito Hello è un esempio di richiesta per una nuova chiave di servizio:</span><span class="sxs-lookup"><span data-stu-id="7732e-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="7732e-151">In alternativa, se si desidera toocreate un circuito ExpressRoute con il componente aggiuntivo premium hello, hello di utilizzare l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="7732e-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="7732e-152">Fare riferimento toohello [domande frequenti su ExpressRoute](expressroute-faqs.md) per ulteriori informazioni sul componente aggiuntivo di hello premium.</span><span class="sxs-lookup"><span data-stu-id="7732e-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="7732e-153">risposta Hello conterrà la chiave di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-153">hello response will contain hello service key.</span></span> <span data-ttu-id="7732e-154">È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="7732e-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="7732e-155">Passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="7732e-155">Step 4.</span></span> <span data-ttu-id="7732e-156">Elenco di tutti i circuiti ExpressRoute hello</span><span class="sxs-lookup"><span data-stu-id="7732e-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="7732e-157">È possibile eseguire hello `Get-AzureDedicatedCircuit` comando hello di tooget un elenco di tutti i circuiti ExpressRoute creato:</span><span class="sxs-lookup"><span data-stu-id="7732e-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="7732e-158">risposta di Hello sarà simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="7732e-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7732e-159">È possibile recuperare queste informazioni in qualsiasi momento utilizzando hello `Get-AzureDedicatedCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7732e-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="7732e-160">Effettuare hello chiamata senza parametri, vengono elencati tutti i circuiti hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="7732e-161">La chiave del servizio sarà elencata nel hello *ServiceKey* campo.</span><span class="sxs-lookup"><span data-stu-id="7732e-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7732e-162">È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="7732e-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="7732e-163">Passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="7732e-163">Step 5.</span></span> <span data-ttu-id="7732e-164">Inviare i provider di connettività di hello servizio tooyour chiave per il provisioning</span><span class="sxs-lookup"><span data-stu-id="7732e-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="7732e-165">*ServiceProviderProvisioningState* fornisce informazioni sullo stato corrente di hello di provisioning sul lato di provider di servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="7732e-166">*Stato* fornisce lo stato di hello in hello lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7732e-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="7732e-167">Per ulteriori informazioni sul provisioning stati circuito, vedere hello [flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states) articolo.</span><span class="sxs-lookup"><span data-stu-id="7732e-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="7732e-168">Quando si crea un nuovo circuito ExpressRoute, circuito hello sarà nel seguente stato hello:</span><span class="sxs-lookup"><span data-stu-id="7732e-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="7732e-169">circuito Hello andrà toohello seguente lo stato quando il provider di connettività hello è in corso di hello di abilitarlo per l'utente:</span><span class="sxs-lookup"><span data-stu-id="7732e-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="7732e-170">Un circuito ExpressRoute deve essere nel seguente stato si toobe in grado di toouse hello è:</span><span class="sxs-lookup"><span data-stu-id="7732e-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="7732e-171">Passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="7732e-171">Step 6.</span></span> <span data-ttu-id="7732e-172">Controllare periodicamente hello stato della chiave circuito hello e hello</span><span class="sxs-lookup"><span data-stu-id="7732e-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="7732e-173">In questo modo è possibile sapere quando il provider ha abilitato il circuito.</span><span class="sxs-lookup"><span data-stu-id="7732e-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="7732e-174">Dopo aver configurato il circuito hello, *ServiceProviderProvisioningState* verrà visualizzato come *provisioning eseguito* come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7732e-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="7732e-175">Passaggio 7.</span><span class="sxs-lookup"><span data-stu-id="7732e-175">Step 7.</span></span> <span data-ttu-id="7732e-176">Creare la configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="7732e-176">Create your routing configuration</span></span>
<span data-ttu-id="7732e-177">Fare riferimento toohello [configurazione del routing circuito ExpressRoute (creare e modificare il circuito peering)](expressroute-howto-routing-classic.md) per istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="7732e-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7732e-178">Queste istruzioni si applicano solo toocircuits creati con i provider di servizi che offrono servizi di livello 2 di connettività.</span><span class="sxs-lookup"><span data-stu-id="7732e-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="7732e-179">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IP VPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7732e-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="7732e-180">Passaggio 8.</span><span class="sxs-lookup"><span data-stu-id="7732e-180">Step 8.</span></span> <span data-ttu-id="7732e-181">Collegare un circuito ExpressRoute di tooan rete virtuale</span><span class="sxs-lookup"><span data-stu-id="7732e-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="7732e-182">Successivamente, collegare un circuito ExpressRoute di tooyour rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="7732e-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="7732e-183">Fare riferimento troppo[toovirtual reti i circuiti ExpressRoute collegamento](expressroute-howto-linkvnet-classic.md) per istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="7732e-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="7732e-184">Se è necessario toocreate una rete virtuale usando il modello di distribuzione classica hello per ExpressRoute, vedere [creare una rete virtuale per ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="7732e-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="7732e-185">Ottenere lo stato di hello di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7732e-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="7732e-186">È possibile recuperare queste informazioni in qualsiasi momento utilizzando hello `Get-AzureCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7732e-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="7732e-187">Effettuare hello chiamata senza parametri, vengono elencati tutti i circuiti hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-187">Making hello call without any parameters lists all hello circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7732e-188">È possibile ottenere informazioni su un circuito ExpressRoute specifico passando la chiave di servizio hello come una chiamata di toohello parametro.</span><span class="sxs-lookup"><span data-stu-id="7732e-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="7732e-189">È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="7732e-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="7732e-190">Modifica di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7732e-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="7732e-191">È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.</span><span class="sxs-lookup"><span data-stu-id="7732e-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="7732e-192">È possibile eseguire hello seguenti senza tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="7732e-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="7732e-193">Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7732e-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="7732e-194">Aumento della larghezza di banda hello del circuito ExpressRoute fornito è la capacità disponibile sulla porta hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="7732e-195">Si noti che il downgrade della larghezza di banda hello di un circuito non è supportato.</span><span class="sxs-lookup"><span data-stu-id="7732e-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="7732e-196">Modificare hello piano dati a consumo tooUnlimited dati di controllo.</span><span class="sxs-lookup"><span data-stu-id="7732e-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="7732e-197">Si noti tale piano del controllo modifica hello da dati senza limiti tooMetered che dati non è supportata.</span><span class="sxs-lookup"><span data-stu-id="7732e-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="7732e-198">È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).</span><span class="sxs-lookup"><span data-stu-id="7732e-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="7732e-199">Fare riferimento toohello [domande frequenti su ExpressRoute](expressroute-faqs.md) per ulteriori informazioni su limiti e limitazioni.</span><span class="sxs-lookup"><span data-stu-id="7732e-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="7732e-200">componente aggiuntivo di tooenable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="7732e-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="7732e-201">È possibile abilitare il componente aggiuntivo di hello ExpressRoute premium per il circuito esistente utilizzando hello seguente cmdlet di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7732e-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="7732e-202">Il circuito avranno ora le funzionalità dei componenti aggiuntivi di hello ExpressRoute premium abilitata.</span><span class="sxs-lookup"><span data-stu-id="7732e-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="7732e-203">Si noti che si inizierà fatturazione è per la funzionalità di componente aggiuntivo di hello premium come comando hello è stata eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="7732e-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="7732e-204">componente aggiuntivo di toodisable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="7732e-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7732e-205">Questa operazione può non riuscire se si utilizza le risorse che sono maggiori di ciò che è consentito per il circuito standard hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="7732e-206">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="7732e-206">Considerations</span></span>

* <span data-ttu-id="7732e-207">È necessario assicurarsi che il numero di hello del circuito toohello collegato reti virtuali è inferiore a 10 prima effettuare il downgrade da premium toostandard.</span><span class="sxs-lookup"><span data-stu-id="7732e-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="7732e-208">Se non si esegue questa operazione, la richiesta di aggiornamento avrà esito negativo e sarà tariffe fatturati hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="7732e-209">È necessario scollegare tutte le reti virtuali in altre aree geopolitiche.</span><span class="sxs-lookup"><span data-stu-id="7732e-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="7732e-210">Se non si esegue questa operazione, la richiesta di aggiornamento avrà esito negativo e sarà tariffe fatturati hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="7732e-211">La tabella di route deve includere meno di 4.000 route per il peering privato.</span><span class="sxs-lookup"><span data-stu-id="7732e-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="7732e-212">Se le dimensioni di tabella di route sono maggiore di 4.000 route, sessione BGP hello verrà eliminato e non verrà riabilitata fino a quando il numero di hello di prefissi annunciati scende sotto 4.000.</span><span class="sxs-lookup"><span data-stu-id="7732e-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="7732e-213">Disabilitare il componente aggiuntivo di hello premium</span><span class="sxs-lookup"><span data-stu-id="7732e-213">Disable hello premium add-on</span></span>
<span data-ttu-id="7732e-214">È possibile disabilitare il componente aggiuntivo di hello ExpressRoute premium per il circuito esistente utilizzando hello cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="7732e-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="7732e-215">larghezza di banda circuito ExpressRoute hello tooupdate</span><span class="sxs-lookup"><span data-stu-id="7732e-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="7732e-216">Controllare hello [domande frequenti su ExpressRoute](expressroute-faqs.md) per le opzioni della larghezza di banda per il provider è supportato.</span><span class="sxs-lookup"><span data-stu-id="7732e-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="7732e-217">È possibile scegliere qualsiasi dimensione è maggiore della dimensione hello del circuito esistente, purché (in cui viene creato il circuito) la porta fisica hello consente.</span><span class="sxs-lookup"><span data-stu-id="7732e-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7732e-218">Potrebbe essere circuito ExpressRoute di hello toorecreate se ha capacità insufficiente sulla porta esistente hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="7732e-219">Se non è presente capacità aggiuntive disponibili in tale posizione non è possibile aggiornare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="7732e-220">È possibile ridurre la larghezza di banda hello di un circuito ExpressRoute senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="7732e-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="7732e-221">Il downgrade della larghezza di banda è necessario il circuito ExpressRoute toodeprovision hello e quindi ripetere il provisioning di un nuovo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7732e-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="7732e-222">Ridimensionare un circuito</span><span class="sxs-lookup"><span data-stu-id="7732e-222">Resize a circuit</span></span>

<span data-ttu-id="7732e-223">Dopo aver stabilito quali dimensioni, è necessario, è possibile utilizzare il circuito hello tooresize di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7732e-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7732e-224">Il circuito verrà sono stato ridimensionato sul lato Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="7732e-225">È necessario contattare le configurazioni di tooupdate provider di connettività nella loro toomatch lato questa modifica.</span><span class="sxs-lookup"><span data-stu-id="7732e-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="7732e-226">Si noti che si inizierà di fatturazione per hello aggiornato opzione larghezza di banda da questo punto.</span><span class="sxs-lookup"><span data-stu-id="7732e-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="7732e-227">Se viene visualizzato il seguente errore durante l'aumento della larghezza di banda circuito hello hello, significa non esiste alcuna larghezza di banda sufficiente a sinistra sulla porta di hello fisico in cui è stato creato il circuito esistente.</span><span class="sxs-lookup"><span data-stu-id="7732e-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="7732e-228">Si crea un nuovo circuito delle dimensioni di hello che è necessario includere toodelete questo circuito.</span><span class="sxs-lookup"><span data-stu-id="7732e-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="7732e-229">Deprovisioning ed eliminazione di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7732e-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="7732e-230">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="7732e-230">Considerations</span></span>

* <span data-ttu-id="7732e-231">È necessario scollegare tutte le reti virtuali da hello circuito ExpressRoute per toosucceed questa operazione.</span><span class="sxs-lookup"><span data-stu-id="7732e-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="7732e-232">Controllare toosee se si dispone di alcuna rete virtuale che sono collegati circuito toohello se questa operazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="7732e-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="7732e-233">Se il provider del servizio di circuito ExpressRoute di hello lo stato di provisioning **Provisioning** o **provisioning eseguito** è necessario collaborare con il circuito di hello toodeprovision provider del servizio sul relativo lato.</span><span class="sxs-lookup"><span data-stu-id="7732e-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="7732e-234">Si continuerà tooreserve risorse e a pagamento fino a quando il provider di servizi di hello completa deprovisioning circuito hello e invia una notifica di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7732e-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="7732e-235">Se il provider di servizi di hello è deprovisioning circuito hello (provider di servizi di hello lo stato di provisioning è stato impostato troppo**non è stato eseguito il provisioning**) è possibile eliminare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="7732e-236">Questa operazione arresterà la fatturazione per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="7732e-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="7732e-237">Eliminare un circuito</span><span class="sxs-lookup"><span data-stu-id="7732e-237">Delete a circuit</span></span>

<span data-ttu-id="7732e-238">È possibile eliminare il circuito ExpressRoute eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7732e-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="7732e-239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7732e-239">Next steps</span></span>
<span data-ttu-id="7732e-240">Dopo aver creato il circuito, verificare che hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7732e-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="7732e-241">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7732e-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="7732e-242">Collegamento del circuito ExpressRoute di tooyour di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="7732e-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

