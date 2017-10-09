---
title: un gateway applicazione utilizzando l'URL di routing regole aaaCreate | Documenti Microsoft
description: Questa pagina fornisce istruzioni toocreate, configurare un gateway applicazione Azure utilizzando le regole di routing di URL
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="2aa8b-103">Creare un gateway applicazione con il routing basato sul percorso</span><span class="sxs-lookup"><span data-stu-id="2aa8b-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2aa8b-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2aa8b-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="2aa8b-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2aa8b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="2aa8b-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="2aa8b-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="2aa8b-107">Il routing basato sul percorso URL consente di tooassociate route in base al percorso URL hello di una richiesta Http.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="2aa8b-108">Verifica la presenza di un pool di back-end tooa route configurati per l'URL di hello presentati in hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway.</span></span> <span data-ttu-id="2aa8b-109">Invia quindi toohello il traffico di rete hello è definito il pool back-end.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-109">It then sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="2aa8b-110">Un utilizzo comune per il routing basato su URL è tooload bilanciamento delle richieste per i pool di server back-end toodifferent diversi tipi di contenuto.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-110">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="2aa8b-111">Routing basato su URL introduce un nuovo gateway tooapplication tipo di regola.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-111">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="2aa8b-112">Per il gateway applicazione sono disponibili due tipi di regole: basic e PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="2aa8b-113">Tipo di regola di base fornisce servizio round robin per hello back-end pool inoltre PathBasedRouting durante la distribuzione round robin tooround, accetta inoltre il modello del percorso dell'URL di richiesta hello in considerazione durante la scelta di pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-113">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="2aa8b-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="2aa8b-114">Scenario</span></span>

<span data-ttu-id="2aa8b-115">Nell'esempio seguente di hello, Gateway applicazione gestisce il traffico per contoso.com con due pool di server back-end: pool di server video e immagine pool dei server.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-115">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="2aa8b-116">Le richieste di http://contoso.com/image * vengono indirizzati vengono indirizzati i pool di server tooimage (pool1) e http://contoso.com/video * toovideo pool di server (pool2).</span><span class="sxs-lookup"><span data-stu-id="2aa8b-116">Requests for http://contoso.com/image* are routed tooimage server pool (pool1), and http://contoso.com/video* are routed toovideo server pool (pool2).</span></span> <span data-ttu-id="2aa8b-117">Se nessuno dei modelli di percorso hello corrisponde, viene selezionato un pool di server predefinito (pool1).</span><span class="sxs-lookup"><span data-stu-id="2aa8b-117">if none of hello path patterns match, a default server pool (pool1) is selected.</span></span>

![route dell'URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="2aa8b-119">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2aa8b-119">Before you begin</span></span>

1. <span data-ttu-id="2aa8b-120">Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="2aa8b-121">È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2aa8b-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="2aa8b-122">Creare una rete virtuale e una subnet per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="2aa8b-123">Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-123">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="2aa8b-124">gateway applicazione Hello deve essere da solo in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-124">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="2aa8b-125">server Hello aggiunto deve essere presente il gateway applicazione hello di toohello pool back-end toouse o i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-125">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="2aa8b-126">Che cos'è toocreate necessario un gateway applicazione?</span><span class="sxs-lookup"><span data-stu-id="2aa8b-126">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="2aa8b-127">**Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="2aa8b-128">gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="2aa8b-129">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="2aa8b-130">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="2aa8b-131">**Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="2aa8b-132">Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="2aa8b-133">**Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="2aa8b-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="2aa8b-134">**Regola:** regola hello associa listener hello, pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-134">**Rule:** hello rule binds hello listener, hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="2aa8b-135">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="2aa8b-135">Create an application gateway</span></span>

<span data-ttu-id="2aa8b-136">differenza Hello tra l'utilizzo di Azure classico e Gestione risorse di Azure è ordine hello in cui è stato creato il gateway di applicazione hello e gli elementi hello necessario toobe configurato.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-136">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="2aa8b-137">Gestione risorse di tutti gli elementi che costituiscono un gateway applicazione vengono configurati singolarmente e riunire risorsa per il gateway applicazione toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-137">With Resource Manager, all items that make an application gateway are configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="2aa8b-138">Ecco i passaggi hello toocreate necessario un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="2aa8b-138">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="2aa8b-139">Creare un gruppo di risorse per Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="2aa8b-140">Creare una rete virtuale, subnet e l'indirizzo IP pubblico per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-140">Create a virtual network, subnet, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="2aa8b-141">Creare un oggetto di configurazione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="2aa8b-142">Creare una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="2aa8b-143">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="2aa8b-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="2aa8b-144">Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-144">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="2aa8b-145">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2aa8b-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="2aa8b-146">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="2aa8b-146">Step 1</span></span>

<span data-ttu-id="2aa8b-147">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="2aa8b-147">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="2aa8b-148">Si è tooauthenticate richiesta con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-148">You are prompted tooauthenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="2aa8b-149">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="2aa8b-149">Step 2</span></span>

<span data-ttu-id="2aa8b-150">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-150">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="2aa8b-151">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="2aa8b-151">Step 3</span></span>

<span data-ttu-id="2aa8b-152">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-152">Choose which of your Azure subscriptions toouse.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="2aa8b-153">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="2aa8b-153">Step 4</span></span>

<span data-ttu-id="2aa8b-154">Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="2aa8b-155">In alternativa, è anche possibile creare tag del gruppo di risorse per il gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="2aa8b-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="2aa8b-156">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="2aa8b-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="2aa8b-157">Questo gruppo di risorse viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-157">This resource group is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="2aa8b-158">Assicurarsi che tutti i comandi toocreate un hello di uso di gateway applicazione stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-158">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="2aa8b-159">Nell'esempio hello sopra, viene creato un gruppo di risorse denominato "appgw-RG" e il percorso "Stati Uniti occidentali".</span><span class="sxs-lookup"><span data-stu-id="2aa8b-159">In hello example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="2aa8b-160">Se è necessario tooconfigure un probe personalizzato per il gateway applicazione, vedere [creare un gateway applicazione con probe personalizzati usando PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2aa8b-160">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="2aa8b-161">Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="2aa8b-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="2aa8b-162">Creare una rete virtuale e una subnet per il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="2aa8b-162">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="2aa8b-163">Hello seguente esempio viene illustrato come toocreate una rete virtuale usando Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-163">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="2aa8b-164">Questo esempio viene creata una rete virtuale per hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-164">This example creates a VNET for hello Application Gateway.</span></span> <span data-ttu-id="2aa8b-165">Gateway applicazione richiede il proprio subnet, per questo motivo subnet hello creata per il Gateway applicazione hello è minore di hello spazio degli indirizzi di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-165">Application Gateway requires its own subnet, for this reason hello subnet created for hello Application Gateway is smaller than hello VNET address space.</span></span> <span data-ttu-id="2aa8b-166">Altre risorse, incluse in questo modo, ma non limitata tooweb server toobe configurati in hello stesso rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-166">This allows for other resources, including but not limited tooweb servers toobe configured in hello same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="2aa8b-167">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="2aa8b-167">Step 1</span></span>

<span data-ttu-id="2aa8b-168">Assegnare hello indirizzo intervallo 10.0.0.0/24 toohello subnet toobe variabile utilizzata toocreate una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-168">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toocreate a virtual network.</span></span>  <span data-ttu-id="2aa8b-169">Questo crea l'oggetto di configurazione di subnet di hello per Gateway di applicazione, che viene utilizzato nell'esempio riportato di seguito hello hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-169">This creates hello subnet configuration object for hello Application Gateway, which is used in hello next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="2aa8b-170">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="2aa8b-170">Step 2</span></span>

<span data-ttu-id="2aa8b-171">Creare una rete virtuale denominata **appgwvnet** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello con hello prefisso 10.0.0.0/16 10.0.0.0/24 subnet.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="2aa8b-172">Configurazione di hello di hello rete virtuale con una singola subnet per tooreside di Gateway applicazione hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-172">This completes hello configuration of hello VNET with a single subnet for hello Application Gateway tooreside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="2aa8b-173">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="2aa8b-173">Step 3</span></span>

<span data-ttu-id="2aa8b-174">Assegnare variabile subnet hello per hello passaggi successivi, viene passato toohello `New-AzureRMApplicationGateway` cmdlet in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-174">Assign hello subnet variable for hello next steps, this is passed toohello `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="2aa8b-175">Creare un indirizzo IP pubblico per la configurazione front-end hello</span><span class="sxs-lookup"><span data-stu-id="2aa8b-175">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="2aa8b-176">Creare una risorsa IP pubblica **publicIP01** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="2aa8b-177">Gateway applicazione può utilizzare un indirizzo IP pubblico, l'indirizzo IP interno o entrambe le richieste tooreceive per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-177">Application Gateway can use a public IP address, internal IP address or both tooreceive requests for load balancing.</span></span>  <span data-ttu-id="2aa8b-178">Per questo esempio è stato usato solo un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-178">This example only uses a public IP address.</span></span> <span data-ttu-id="2aa8b-179">Nell'esempio seguente di hello, nessun nome DNS è configurato per la creazione di indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-179">In hello following example, no DNS name is configured for creating hello Public IP address.</span></span>  <span data-ttu-id="2aa8b-180">Il gateway applicazione non supporta i nomi DNS personalizzati negli indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="2aa8b-181">Se un nome personalizzato è necessario per l'endpoint pubblico hello, un record CNAME deve essere creato nome DNS del toopoint toohello generato automaticamente per l'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-181">If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="2aa8b-182">Viene assegnato a un indirizzo IP gateway applicazione toohello all'avvio del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-182">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="2aa8b-183">Creare la configurazione del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="2aa8b-183">Create application gateway configuration</span></span>

<span data-ttu-id="2aa8b-184">Tutti gli elementi di configurazione necessario impostare prima di creare i gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-184">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="2aa8b-185">Hello seguenti passaggi necessari per creare hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-185">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="2aa8b-186">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="2aa8b-186">Step 1</span></span>

<span data-ttu-id="2aa8b-187">Creare una configurazione IP del gateway applicazione denominata **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="2aa8b-188">Avvio di Gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-188">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="2aa8b-189">Tenere presente che ogni istanza ha un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="2aa8b-190">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="2aa8b-190">Step 2</span></span>

<span data-ttu-id="2aa8b-191">Configurare hello pool di indirizzi IP back-end denominato **pool01** e **pool2** con indirizzi IP per **pool1** e **pool2**.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-191">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="2aa8b-192">Questi indirizzi IP sono gli indirizzi IP hello delle risorse di hello che ospitano toobe di applicazione web hello protetti da gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-192">These IP addresses are hello IP addresses of hello resources that are hosting hello web application toobe protected by hello application gateway.</span></span> <span data-ttu-id="2aa8b-193">Questi membri di pool back-end sono tutti toobe convalidato integro tramite probe base probe o probe personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-193">These backend pool members are all validated toobe healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="2aa8b-194">Il traffico viene indirizzato toothem quando le richieste provengano in gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-194">Traffic is then routed toothem when requests come into hello application gateway.</span></span> <span data-ttu-id="2aa8b-195">Pool back-end può essere utilizzato da più regole all'interno di gateway applicazione hello, ovvero un pool back-end possono essere utilizzate per più applicazioni web che si trovano su hello stesso host.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-195">Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="2aa8b-196">In questo esempio, sono disponibili due pool back-end tooroute il traffico di rete in base al percorso URL hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-196">In this example, there are two back-end pools tooroute network traffic based on hello URL path.</span></span> <span data-ttu-id="2aa8b-197">Un pool riceve il traffico dal percorso dell'URL "/video" e l'altro riceve il traffico dal percorso "/image".</span><span class="sxs-lookup"><span data-stu-id="2aa8b-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="2aa8b-198">Sostituire hello precedente tooadd gli indirizzi IP endpoint dell'indirizzo IP la propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-198">Replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="2aa8b-199">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="2aa8b-199">Step 3</span></span>

<span data-ttu-id="2aa8b-200">Configurare impostazioni del gateway applicazione **poolsetting01** e **poolsetting02** hello con bilanciamento del carico del traffico di rete nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="2aa8b-201">In questo esempio, configurare le impostazioni del pool back-end diverso per il pool di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-201">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="2aa8b-202">Ogni pool back-end può avere un'impostazione del pool back-end dedicata.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="2aa8b-203">Le impostazioni HTTP back-end vengono utilizzate per i membri del pool back-end corretto toohello traffico tooroute regole.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-203">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="2aa8b-204">Questo parametro determina il protocollo di hello e la porta utilizzata durante l'invio di traffico toohello i membri del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-204">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="2aa8b-205">Sessioni basate su cookie sono determinate anche dalle impostazioni HTTP back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-205">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="2aa8b-206">Se abilitata, l'affinità di sessione basato su cookie invia traffico toohello stesso back-end come richieste precedenti per ogni pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-206">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="2aa8b-207">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="2aa8b-207">Step 4</span></span>

<span data-ttu-id="2aa8b-208">Configurazione IP front-end hello con endpoint IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-208">Configure hello front-end IP with public IP endpoint.</span></span> <span data-ttu-id="2aa8b-209">oggetto di configurazione IP front-end Hello viene utilizzato un hello toorelate listener rivolti verso l'indirizzo IP con listener hello verso l'esterno.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-209">hello front-end IP configuration object is used by a listener toorelate hello outward facing IP address with hello listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="2aa8b-210">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="2aa8b-210">Step 5</span></span>

<span data-ttu-id="2aa8b-211">Configurare hello porta front-end per un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-211">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="2aa8b-212">oggetto di configurazione di Hello porta front-end viene utilizzato un toodefine listener cosa porta hello Gateway applicazione è in attesa del traffico listener hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-212">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="2aa8b-213">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="2aa8b-213">Step 6</span></span>

<span data-ttu-id="2aa8b-214">Configurare il listener di hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-214">Configure hello listener.</span></span> <span data-ttu-id="2aa8b-215">Questo passaggio consente di configurare il listener hello per l'indirizzo IP pubblico hello e la porta utilizzata tooreceive il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-215">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="2aa8b-216">Hello di esempio seguente accetta la configurazione IP front-end hello configurato in precedenza, la configurazione della porta front-end e un protocollo (http o https) e configura il listener hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-216">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="2aa8b-217">In questo esempio, il listener hello è in attesa di traffico tooHTTP sulla porta 80 all'indirizzo IP pubblico hello è stato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-217">In this example, hello listener listens tooHTTP traffic on port 80 on hello public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="2aa8b-218">Passaggio 7</span><span class="sxs-lookup"><span data-stu-id="2aa8b-218">Step 7</span></span>

<span data-ttu-id="2aa8b-219">Configurare i percorsi di regola di URL per il pool di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-219">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="2aa8b-220">Questo passaggio consente di configurare un percorso di hello usato dal gateway di applicazione e definisce il mapping di hello tra il percorso di URL hello e un pool back-end hello viene assegnato il traffico in ingresso di toohandle hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-220">This step configures hello relative path used by application gateway and defines hello mapping between hello URL path and hello back-end pool that is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2aa8b-221">Ogni percorso deve iniziare con / e hello solo un "\*" è consentita, al fine di hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-221">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="2aa8b-222">Alcuni esempi validi sono /xyz, /xyz* o /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="2aa8b-223">Hello stringa inserito toohello matcher di percorso non include alcun testo dopo hello innanzitutto "?" o "#" e tali caratteri non consentiti.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-223">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="2aa8b-224">esempio Hello crea due regole: uno per il percorso "immagine /" routing del traffico "pool1" tooback-end e un'altra per "video /" percorso di routing del traffico tooback-end "pool2".</span><span class="sxs-lookup"><span data-stu-id="2aa8b-224">hello following example creates two rules: one for "/image/" path routing traffic tooback-end "pool1" and another one for "/video/" path routing traffic tooback-end "pool2."</span></span> <span data-ttu-id="2aa8b-225">Queste regole assicurano che il traffico per ogni set di URL di back-end toohello indirizzato.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-225">These rules ensure that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="2aa8b-226">Ad esempio, http://contoso.com/image/figure1.jpg passa toopool1 e http://contoso.com/video/example.mp4 diventa toopool2.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-226">For example, http://contoso.com/image/figure1.jpg goes toopool1 and http://contoso.com/video/example.mp4 goes toopool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="2aa8b-227">Se il percorso di hello non corrisponde a una delle regole di percorso predefinito di hello, configurazione della mappa di hello regola percorso consente di configurare anche un pool di indirizzi back-end di predefinito.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-227">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="2aa8b-228">Ad esempio, http://contoso.com/shoppingcart/test.html passa toopool1 con cui è definito come il pool predefinito hello per il traffico non corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-228">For example, http://contoso.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="2aa8b-229">Passaggio 8</span><span class="sxs-lookup"><span data-stu-id="2aa8b-229">Step 8</span></span>

<span data-ttu-id="2aa8b-230">Creare un'impostazione della regola.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-230">Create a rule setting.</span></span> <span data-ttu-id="2aa8b-231">Questo passaggio Configura hello applicazione gateway toouse basato sul percorso routing degli URL.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-231">This step configures hello application gateway toouse URL path-based routing.</span></span> <span data-ttu-id="2aa8b-232">Hello `$urlPathMap` variabile definita in hello passaggio precedente è la regola adesso toocreate utilizzati hello basata sul percorso.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-232">hello `$urlPathMap` variable defined in hello earlier step is now used toocreate hello path-based rule.</span></span> <span data-ttu-id="2aa8b-233">In questo passaggio, Associamo regola hello con un listener e il mapping del percorso url hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-233">In this step, we associate hello rule with a listener and hello url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="2aa8b-234">Passaggio 9:</span><span class="sxs-lookup"><span data-stu-id="2aa8b-234">Step 9</span></span>

<span data-ttu-id="2aa8b-235">Configurare hello numero di istanze e le dimensioni per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-235">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="2aa8b-236">Creare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="2aa8b-236">Create Application Gateway</span></span>

<span data-ttu-id="2aa8b-237">Creare un gateway applicazione con tutti gli oggetti di configurazione da hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-237">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="2aa8b-238">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="2aa8b-238">Get application gateway DNS name</span></span>

<span data-ttu-id="2aa8b-239">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-239">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="2aa8b-240">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="2aa8b-241">gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-241">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="2aa8b-242">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2aa8b-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="2aa8b-243">front-end hello tooconfigure record CNAME IP, recuperare i dettagli del gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-243">tooconfigure hello frontend IP CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="2aa8b-244">nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-244">hello application gateway's DNS name should be used toocreate a CNAME record.</span></span> <span data-ttu-id="2aa8b-245">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2aa8b-245">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="2aa8b-246">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2aa8b-246">Next steps</span></span>

<span data-ttu-id="2aa8b-247">Se si desidera toolearn offload Secure Sockets Layer (SSL), vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2aa8b-247">If you want toolearn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

