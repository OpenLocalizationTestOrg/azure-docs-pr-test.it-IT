---
title: 'Creare e modificare un circuito ExpressRoute: PowerShell: Azure classico| Microsoft Docs'
description: Questo articolo illustra i passaggi per la creazione e il provisioning di un circuito ExpressRoute. Questo articolo descrive anche come controllare lo stato, eseguire l'aggiornamento o effettuare l'eliminazione e il deprovisioning di un circuito.
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
ms.openlocfilehash: 3b12bbb21ebf6a0160227c4a281c420cf192d6f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="a0f66-104">Creare e modificare un circuito ExpressRoute mediante PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="a0f66-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0f66-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a0f66-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="a0f66-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0f66-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="a0f66-107">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a0f66-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="a0f66-108">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a0f66-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="a0f66-109">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="a0f66-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="a0f66-110">Questo articolo illustra i passaggi per creare un circuito di Azure ExpressRoute tramite i cmdlet di PowerShell e il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="a0f66-110">This article walks you through the steps to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the classic deployment model.</span></span> <span data-ttu-id="a0f66-111">L'articolo illustra anche le procedure di controllo di stato, aggiornamento, eliminazione e deprovisioning di un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0f66-111">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="a0f66-112">**Informazioni sui modelli di distribuzione di AzureAbout Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="a0f66-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="a0f66-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a0f66-113">Before you begin</span></span>
### <a name="step-1-review-the-prerequisites-and-workflow-articles"></a><span data-ttu-id="a0f66-114">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="a0f66-114">Step 1.</span></span> <span data-ttu-id="a0f66-115">Consultare gli articoli sui prerequisiti e sul flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="a0f66-115">Review the prerequisites and workflow articles</span></span>
<span data-ttu-id="a0f66-116">Prima di procedere con la configurazione, assicurarsi di avere verificato i [prerequisiti](expressroute-prerequisites.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="a0f66-116">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-the-latest-versions-of-the-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="a0f66-117">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="a0f66-117">Step 2.</span></span> <span data-ttu-id="a0f66-118">Installare le versioni più recenti dei moduli di PowerShell per Gestione dei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0f66-118">Install the latest versions of the Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="a0f66-119">Per istruzioni dettagliate sulla configurazione del computer per l'uso con i moduli di Azure PowerShell, vedere [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) (Introduzione ai cmdlet di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a0f66-119">Follow the instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="a0f66-120">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="a0f66-120">Step 3.</span></span> <span data-ttu-id="a0f66-121">Accedere all'account Azure e selezionare una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="a0f66-121">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="a0f66-122">Aprire la console di PowerShell con diritti elevati e connettersi all'account.</span><span class="sxs-lookup"><span data-stu-id="a0f66-122">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="a0f66-123">Per eseguire la connessione, usare gli esempi che seguono:</span><span class="sxs-lookup"><span data-stu-id="a0f66-123">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="a0f66-124">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="a0f66-124">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="a0f66-125">Se sono disponibili più sottoscrizioni, selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="a0f66-125">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="a0f66-126">Successivamente, utilizzare il cmdlet seguente per aggiungere la sottoscrizione di Azure a PowerShell per il modello di distribuzione classico.</span><span class="sxs-lookup"><span data-stu-id="a0f66-126">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="a0f66-127">Creare un circuito ExpressRoute ed eseguirne il provisioning</span><span class="sxs-lookup"><span data-stu-id="a0f66-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-the-powershell-modules-for-expressroute"></a><span data-ttu-id="a0f66-128">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="a0f66-128">Step 1.</span></span> <span data-ttu-id="a0f66-129">Importare i moduli di PowerShell per ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-129">Import the PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="a0f66-130">Se ancora non è stato fatto, per iniziare a usare i cmdlet per ExpressRoute, è necessario importare i moduli di Azure ed ExpressRoute nella sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0f66-130">If you have not already done so, you must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="a0f66-131">Importare i moduli dal percorso in cui sono stati installati sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="a0f66-131">You import the modules from the location that they were installed to on your local computer.</span></span> <span data-ttu-id="a0f66-132">A seconda del metodo usato per installare i moduli, il percorso potrebbe essere diverso da quello illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="a0f66-132">Depending on the method you used to install the modules, the location may be different than the following example shows.</span></span> <span data-ttu-id="a0f66-133">Se necessario, modificare l'esempio.</span><span class="sxs-lookup"><span data-stu-id="a0f66-133">Modify the example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="a0f66-134">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="a0f66-134">Step 2.</span></span> <span data-ttu-id="a0f66-135">Ottenere l'elenco dei provider, delle località e delle larghezze di banda supportate</span><span class="sxs-lookup"><span data-stu-id="a0f66-135">Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="a0f66-136">Prima di creare un circuito ExpressRoute, è necessario avere l'elenco delle località, delle opzioni di larghezza di banda e dei provider di connettività supportati.</span><span class="sxs-lookup"><span data-stu-id="a0f66-136">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="a0f66-137">Il cmdlet `Get-AzureDedicatedCircuitServiceProvider` di PowerShell restituisce queste informazioni, che verranno usate nei passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="a0f66-137">The PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="a0f66-138">Verificare se sia presente anche il proprio provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="a0f66-138">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="a0f66-139">Prendere nota delle informazioni seguenti, perché saranno necessarie al momento della creazione di un circuito:</span><span class="sxs-lookup"><span data-stu-id="a0f66-139">Make a note of the following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="a0f66-140">Nome</span><span class="sxs-lookup"><span data-stu-id="a0f66-140">Name</span></span>
* <span data-ttu-id="a0f66-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="a0f66-141">PeeringLocations</span></span>
* <span data-ttu-id="a0f66-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="a0f66-142">BandwidthsOffered</span></span>

<span data-ttu-id="a0f66-143">È ora possibile creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0f66-143">You're now ready to create an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="a0f66-144">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="a0f66-144">Step 3.</span></span> <span data-ttu-id="a0f66-145">Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="a0f66-146">L'esempio seguente illustra come creare un circuito ExpressRoute a 200 Mbps tramite Equinix nella Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="a0f66-146">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="a0f66-147">Se si usa un altro provider e impostazioni diverse, sostituire tali informazioni al momento della richiesta.</span><span class="sxs-lookup"><span data-stu-id="a0f66-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0f66-148">Il circuito ExpressRoute viene addebitato dal momento in cui emessa una chiave di servizio.</span><span class="sxs-lookup"><span data-stu-id="a0f66-148">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="a0f66-149">Verificare che l'operazione venga eseguita quando il provider di connettività è pronto a effettuare il provisioning del circuito.</span><span class="sxs-lookup"><span data-stu-id="a0f66-149">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="a0f66-150">Di seguito è riportato un esempio di richiesta di una nuova chiave di servizio:</span><span class="sxs-lookup"><span data-stu-id="a0f66-150">The following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="a0f66-151">Se invece si vuole creare un circuito ExpressRoute con il componente aggiuntivo Premium, usare l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="a0f66-151">Or, if you want to create an ExpressRoute circuit with the premium add-on, use the following example.</span></span> <span data-ttu-id="a0f66-152">Per altri dettagli sul componente aggiuntivo Premium, vedere [Domande frequenti su ExpressRoute](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="a0f66-152">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more details about the premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="a0f66-153">La risposta conterrà la chiave di servizio.</span><span class="sxs-lookup"><span data-stu-id="a0f66-153">The response will contain the service key.</span></span> <span data-ttu-id="a0f66-154">È possibile ottenere descrizioni dettagliate di tutti i parametri eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="a0f66-154">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-the-expressroute-circuits"></a><span data-ttu-id="a0f66-155">Passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="a0f66-155">Step 4.</span></span> <span data-ttu-id="a0f66-156">Elencare tutti i circuiti ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-156">List all the ExpressRoute circuits</span></span>
<span data-ttu-id="a0f66-157">Per ottenere un elenco di tutti i circuiti ExpressRoute creati, eseguire il comando `Get-AzureDedicatedCircuit`:</span><span class="sxs-lookup"><span data-stu-id="a0f66-157">You can run the `Get-AzureDedicatedCircuit` command to get a list of all the ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="a0f66-158">La risposta sarà simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a0f66-158">The response will be something similar to the following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="a0f66-159">È possibile recuperare queste informazioni in qualsiasi momento usando il cmdlet `Get-AzureDedicatedCircuit` .</span><span class="sxs-lookup"><span data-stu-id="a0f66-159">You can retrieve this information at any time by using the `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="a0f66-160">Se si effettua la chiamata senza parametri, verranno elencati tutti i circuiti.</span><span class="sxs-lookup"><span data-stu-id="a0f66-160">Making the call without any parameters lists all the circuits.</span></span> <span data-ttu-id="a0f66-161">La chiave di servizio verrà elencata nel campo *ServiceKey* .</span><span class="sxs-lookup"><span data-stu-id="a0f66-161">Your service key will be listed in the *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="a0f66-162">È possibile ottenere descrizioni dettagliate di tutti i parametri eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="a0f66-162">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="a0f66-163">Passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="a0f66-163">Step 5.</span></span> <span data-ttu-id="a0f66-164">Inviare la chiave di servizio al provider di connettività per il provisioning</span><span class="sxs-lookup"><span data-stu-id="a0f66-164">Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="a0f66-165">*ServiceProviderProvisioningState* offre informazioni sullo stato di provisioning corrente sul lato provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="a0f66-165">*ServiceProviderProvisioningState* provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="a0f66-166">*Status* indica lo stato sul lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a0f66-166">*Status* provides the state on the Microsoft side.</span></span> <span data-ttu-id="a0f66-167">Per altre informazioni sullo stato di provisioning dei circuiti, vedere l'articolo relativo ai [flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="a0f66-167">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="a0f66-168">Quando si crea un nuovo circuito ExpressRoute, il circuito ha lo stato seguente:</span><span class="sxs-lookup"><span data-stu-id="a0f66-168">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="a0f66-169">Il circuito passa allo stato seguente quando è in corso l'abilitazione da parte del provider di connettività:</span><span class="sxs-lookup"><span data-stu-id="a0f66-169">The circuit will go to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="a0f66-170">Un circuito ExpressRoute può essere usato solo se è impostato sullo stato seguente:</span><span class="sxs-lookup"><span data-stu-id="a0f66-170">An ExpressRoute circuit must be in the following state for you to be able to use it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="a0f66-171">Passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="a0f66-171">Step 6.</span></span> <span data-ttu-id="a0f66-172">Controllare periodicamente lo stato e la condizione della chiave del circuito</span><span class="sxs-lookup"><span data-stu-id="a0f66-172">Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="a0f66-173">In questo modo è possibile sapere quando il provider ha abilitato il circuito.</span><span class="sxs-lookup"><span data-stu-id="a0f66-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="a0f66-174">Dopo la configurazione del circuito, *ServiceProviderProvisioningState* verrà visualizzato come *Provisioning eseguito*, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a0f66-174">After the circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in the following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="a0f66-175">Passaggio 7.</span><span class="sxs-lookup"><span data-stu-id="a0f66-175">Step 7.</span></span> <span data-ttu-id="a0f66-176">Creare la configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="a0f66-176">Create your routing configuration</span></span>
<span data-ttu-id="a0f66-177">Per istruzioni dettagliate, vedere l'articolo relativo alla [configurazione del routing per un circuito ExpressRoute (creazione e modifica del peering del circuito)](expressroute-howto-routing-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="a0f66-177">Refer to the [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0f66-178">Queste istruzioni si applicano solo ai circuiti creati con provider di servizi che offrono servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="a0f66-178">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="a0f66-179">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IP VPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a0f66-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="a0f66-180">Passaggio 8.</span><span class="sxs-lookup"><span data-stu-id="a0f66-180">Step 8.</span></span> <span data-ttu-id="a0f66-181">Collegare una rete virtuale a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-181">Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="a0f66-182">Collegare quindi una rete virtuale al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0f66-182">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="a0f66-183">Per istruzioni dettagliate, vedere [Collegare una rete virtuale a un circuito ExpressRoute](expressroute-howto-linkvnet-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="a0f66-183">Refer to [Linking ExpressRoute circuits to virtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="a0f66-184">Se è necessario creare una rete virtuale usando il modello di distribuzione classica per ExpressRoute, vedere l'articolo relativo alla [Creazione di una rete virtuale per ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="a0f66-184">If you need to create a virtual network using the classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="a0f66-185">Ottenere lo stato di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-185">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="a0f66-186">È possibile recuperare queste informazioni in qualsiasi momento usando il cmdlet `Get-AzureCircuit` .</span><span class="sxs-lookup"><span data-stu-id="a0f66-186">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="a0f66-187">Se si effettua la chiamata senza parametri, verranno elencati tutti i circuiti.</span><span class="sxs-lookup"><span data-stu-id="a0f66-187">Making the call without any parameters lists all the circuits.</span></span>

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

<span data-ttu-id="a0f66-188">È possibile ottenere informazioni su un circuito ExpressRoute specifico passando la chiave di servizio come parametro alla chiamata.</span><span class="sxs-lookup"><span data-stu-id="a0f66-188">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="a0f66-189">È possibile ottenere descrizioni dettagliate di tutti i parametri eseguendo, ad esempio, questo comando:</span><span class="sxs-lookup"><span data-stu-id="a0f66-189">You can get detailed descriptions of all the parameters by running the following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="a0f66-190">Modifica di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="a0f66-191">È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.</span><span class="sxs-lookup"><span data-stu-id="a0f66-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="a0f66-192">È possibile eseguire le operazioni seguenti senza tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="a0f66-192">You can do the following with no downtime:</span></span>

* <span data-ttu-id="a0f66-193">Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0f66-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="a0f66-194">Aumentare la larghezza di banda del circuito ExpressRoute, a condizione che sulla porta sia disponibile capacità.</span><span class="sxs-lookup"><span data-stu-id="a0f66-194">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="a0f66-195">Si noti che il downgrade della larghezza di banda di un circuito non è supportato.</span><span class="sxs-lookup"><span data-stu-id="a0f66-195">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="a0f66-196">Modificare il piano di misurazione da Dati a consumo a Dati senza limiti.</span><span class="sxs-lookup"><span data-stu-id="a0f66-196">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="a0f66-197">Si noti che la modifica del piano di misurazione da Dati senza limiti a Dati a consumo non è supportata.</span><span class="sxs-lookup"><span data-stu-id="a0f66-197">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="a0f66-198">È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).</span><span class="sxs-lookup"><span data-stu-id="a0f66-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="a0f66-199">Per altre informazioni su limiti e limitazioni, vedere [Domande frequenti su ExpressRoute](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="a0f66-199">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="a0f66-200">Per abilitare il componente aggiuntivo ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="a0f66-200">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="a0f66-201">È possibile abilitare il componente aggiuntivo ExpressRoute Premium per il circuito esistente usando il cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="a0f66-201">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="a0f66-202">Il circuito avrà le funzionalità del componente aggiuntivo ExpressRoute Premium abilitate.</span><span class="sxs-lookup"><span data-stu-id="a0f66-202">Your circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="a0f66-203">La fatturazione della funzionalità del componente aggiuntivo Premium inizierà non appena il comando verrà eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="a0f66-203">Note that we will start billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="a0f66-204">Per disabilitare il componente aggiuntivo ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="a0f66-204">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a0f66-205">Questa operazione può avere esito negativo se si usano più risorse di quelle consentite per il circuito standard.</span><span class="sxs-lookup"><span data-stu-id="a0f66-205">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="a0f66-206">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="a0f66-206">Considerations</span></span>

* <span data-ttu-id="a0f66-207">È necessario assicurarsi che il numero di reti virtuali collegate al circuito sia minore di 10 prima di eseguire il downgrade da premium a standard.</span><span class="sxs-lookup"><span data-stu-id="a0f66-207">You must ensure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span></span> <span data-ttu-id="a0f66-208">In caso contrario, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="a0f66-208">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="a0f66-209">È necessario scollegare tutte le reti virtuali in altre aree geopolitiche.</span><span class="sxs-lookup"><span data-stu-id="a0f66-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="a0f66-210">In caso contrario, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="a0f66-210">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="a0f66-211">La tabella di route deve includere meno di 4.000 route per il peering privato.</span><span class="sxs-lookup"><span data-stu-id="a0f66-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="a0f66-212">Se la tabella di route include più di 4000 route, la sessione BGP verrà eliminata e non sarà riabilitata finché il numero di prefissi pubblicati non scenderà al di sotto di 4000.</span><span class="sxs-lookup"><span data-stu-id="a0f66-212">If your route table size is greater than 4,000 routes, the BGP session will drop and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-the-premium-add-on"></a><span data-ttu-id="a0f66-213">Disabilitare il componente aggiuntivo Premium</span><span class="sxs-lookup"><span data-stu-id="a0f66-213">Disable the premium add-on</span></span>
<span data-ttu-id="a0f66-214">È possibile disabilitare il componente aggiuntivo ExpressRoute Premium per il circuito esistente usando il cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="a0f66-214">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="a0f66-215">Per aggiornare la larghezza di banda del circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-215">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="a0f66-216">Per le opzioni relative alla larghezza di banda supportate per il provider, vedere [Domande frequenti su ExpressRoute](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="a0f66-216">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="a0f66-217">È possibile scegliere qualsiasi dimensione maggiore della dimensione del circuito esistente, a condizione che sia consentita dalla porta fisica in cui viene creato il circuito.</span><span class="sxs-lookup"><span data-stu-id="a0f66-217">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0f66-218">Se la capacità sulla porta esistente non è sufficiente, potrebbe essere necessario ricreare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0f66-218">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="a0f66-219">Il circuito non può essere aggiornato se in tale posizione non è disponibile capacità aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="a0f66-219">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="a0f66-220">Non è possibile ridurre la larghezza di banda di un circuito ExpressRoute senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="a0f66-220">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="a0f66-221">Il downgrade della larghezza di banda richiede il deprovisioning del circuito ExpressRoute e quindi il provisioning di un nuovo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0f66-221">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="a0f66-222">Ridimensionare un circuito</span><span class="sxs-lookup"><span data-stu-id="a0f66-222">Resize a circuit</span></span>

<span data-ttu-id="a0f66-223">Dopo aver stabilito le dimensioni necessarie, usare il comando seguente per ridimensionare il circuito:</span><span class="sxs-lookup"><span data-stu-id="a0f66-223">After you decide what size you need, you can use the following command to resize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="a0f66-224">Il circuito verrà ridimensionato sul lato di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a0f66-224">Your circuit will have been sized up on the Microsoft side.</span></span> <span data-ttu-id="a0f66-225">È necessario contattare il provider di connettività per aggiornare le configurazioni corrispondenti in base a questa modifica.</span><span class="sxs-lookup"><span data-stu-id="a0f66-225">You must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="a0f66-226">Si noti che inizierà la fatturazione per la larghezza di banda aggiornata da questo punto in poi.</span><span class="sxs-lookup"><span data-stu-id="a0f66-226">Note that we will start billing you for the updated bandwidth option from this point on.</span></span>

<span data-ttu-id="a0f66-227">Se quando si aumenta la larghezza di banda del circuito viene visualizzato l'errore seguente, significa che la larghezza di banda rimasta nella porta fisica in cui è stato creato il circuito esistente non è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="a0f66-227">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span></span> <span data-ttu-id="a0f66-228">È necessario eliminare questo circuito e crearne uno nuovo delle dimensioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="a0f66-228">You have to delete this circuit and create a new circuit of the size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="a0f66-229">Deprovisioning ed eliminazione di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="a0f66-230">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="a0f66-230">Considerations</span></span>

* <span data-ttu-id="a0f66-231">Affinché l'operazione abbia esito positivo, è necessario scollegare tutte le reti virtuali dal circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0f66-231">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span></span> <span data-ttu-id="a0f66-232">Se l'operazione ha esito negativo, controllare se sono presenti reti virtuali collegate al circuito.</span><span class="sxs-lookup"><span data-stu-id="a0f66-232">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span></span>
* <span data-ttu-id="a0f66-233">Se lo stato di provisioning del provider del servizio del circuito ExpressRoute è **Provisioning in corso** o **Provisioning eseguito**, è necessario collaborare con il provider di servizi per eseguire il deprovisioning del circuito sul lato del provider.</span><span class="sxs-lookup"><span data-stu-id="a0f66-233">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="a0f66-234">Le risorse continueranno a essere riservate e la fatturazione continuerà a essere applicata finché il provider di servizi non avrà completato il deprovisioning del circuito e inviato una notifica a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a0f66-234">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="a0f66-235">Se il provider di servizi ha eseguito il deprovisioning del circuito, ovvero lo stato di provisioning del provider di servizi è impostato su **Senza provisioning**, è possibile eliminare il circuito.</span><span class="sxs-lookup"><span data-stu-id="a0f66-235">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="a0f66-236">Non verrà più applicata la fatturazione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a0f66-236">This will stop billing for the circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="a0f66-237">Eliminare un circuito</span><span class="sxs-lookup"><span data-stu-id="a0f66-237">Delete a circuit</span></span>

<span data-ttu-id="a0f66-238">È possibile eliminare un circuito ExpressRoute eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="a0f66-238">You can delete your ExpressRoute circuit by running the following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="a0f66-239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a0f66-239">Next steps</span></span>
<span data-ttu-id="a0f66-240">Dopo aver creato il circuito, verificare di eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0f66-240">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="a0f66-241">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="a0f66-242">Collegare la rete virtuale al circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a0f66-242">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

