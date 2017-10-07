---
title: "un gateway applicazione per ospitare più siti aaaCreate | Documenti Microsoft"
description: "Questa pagina fornisce istruzioni toocreate, configurare un gateway applicazione Azure per ospitare più applicazioni web su hello stesso gateway."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="78352-103">Creare un gateway applicazione per l'hosting di più applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="78352-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="78352-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="78352-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="78352-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="78352-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="78352-106">Hosting di più siti consente toodeploy più di una sola applicazione web su hello stesso gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="78352-107">Si basa su presenza dell'intestazione host nella richiesta HTTP in ingresso hello, toodetermine quali listener riceve traffico.</span><span class="sxs-lookup"><span data-stu-id="78352-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="78352-108">listener di Hello indirizza quindi il pool back-end tooappropriate traffico come configurato nella definizione delle regole hello del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="78352-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="78352-109">Nelle applicazioni web SSL abilitato, i gateway applicazione si basa su hello indicazione nome Server (SNI) estensione toochoose hello corretto del listener per il traffico web hello.</span><span class="sxs-lookup"><span data-stu-id="78352-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="78352-110">Viene in genere utilizzata per l'hosting del sito più tooload bilanciamento delle richieste per i pool di server back-end web diversi domini toodifferent.</span><span class="sxs-lookup"><span data-stu-id="78352-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="78352-111">Analogamente, più sottodomini del dominio radice della stessa può essere ospitato su hello hello stesso gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="78352-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="78352-112">Scenario</span></span>

<span data-ttu-id="78352-113">Nell'esempio seguente di hello, gateway applicazione gestisce il traffico per contoso.com e fabrikam.com con due pool di server back-end: contoso pool di server e il pool di server di fabrikam.</span><span class="sxs-lookup"><span data-stu-id="78352-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="78352-114">Il programma di installazione simile potrebbe essere sottodomini toohost usato come app.contoso.com e blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="78352-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="78352-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="78352-116">Before you begin</span></span>

1. <span data-ttu-id="78352-117">Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="78352-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="78352-118">È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="78352-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="78352-119">server Hello aggiunto deve essere presente il gateway applicazione hello di toohello pool back-end toouse o i relativi endpoint creato in una rete virtuale di hello in una subnet distinta o con un indirizzo IP/VIP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="78352-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="78352-120">Requisiti</span><span class="sxs-lookup"><span data-stu-id="78352-120">Requirements</span></span>

* <span data-ttu-id="78352-121">**Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="78352-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="78352-122">gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="78352-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="78352-123">È possibile usare anche FQDN.</span><span class="sxs-lookup"><span data-stu-id="78352-123">FQDN can also be used.</span></span>
* <span data-ttu-id="78352-124">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="78352-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="78352-125">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="78352-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="78352-126">**Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="78352-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="78352-127">Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="78352-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="78352-128">**Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="78352-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="78352-129">Per i gateway applicazione abilitati per più siti vengono aggiunti anche indicatori SNI e nome host.</span><span class="sxs-lookup"><span data-stu-id="78352-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="78352-130">**Regola:** regola hello associa listener hello, pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="78352-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="78352-131">Le regole vengono elaborate in ordine di hello che sono elencati e il traffico verrà indirizzato tramite hello prima regola che corrisponde indipendentemente dal fatto di specificità.</span><span class="sxs-lookup"><span data-stu-id="78352-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="78352-132">Ad esempio, se si dispone di una regola di utilizzo di un listener di base e una regola di utilizzo di un listener multisito entrambi nella stessa regola di porta, hello con hello listener multisito hello deve essere elencato prima regola hello con listener di base hello affinché hello multisito regola toofunction come previsto.</span><span class="sxs-lookup"><span data-stu-id="78352-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="78352-133">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="78352-133">Create an application gateway</span></span>

<span data-ttu-id="78352-134">di seguito Hello sono passaggi hello necessari toocreate un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="78352-135">Creare un gruppo di risorse per Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="78352-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="78352-136">Creare una rete virtuale, subnet e indirizzo IP pubblico per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="78352-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="78352-137">Creare un oggetto di configurazione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="78352-138">Creare una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="78352-139">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="78352-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="78352-140">Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78352-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="78352-141">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="78352-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="78352-142">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="78352-142">Step 1</span></span>

<span data-ttu-id="78352-143">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="78352-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="78352-144">Si è tooauthenticate richiesta con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="78352-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="78352-145">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="78352-145">Step 2</span></span>

<span data-ttu-id="78352-146">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="78352-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="78352-147">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="78352-147">Step 3</span></span>

<span data-ttu-id="78352-148">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="78352-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="78352-149">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="78352-149">Step 4</span></span>

<span data-ttu-id="78352-150">Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="78352-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="78352-151">In alternativa, è anche possibile creare tag del gruppo di risorse per il gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="78352-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="78352-152">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="78352-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="78352-153">Questo percorso viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="78352-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="78352-154">Assicurarsi che tutti i comandi toocreate un hello di uso di gateway applicazione stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="78352-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="78352-155">Nell'esempio hello sopra, è stato creato un gruppo di risorse denominato **appgw-RG** con un percorso di **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="78352-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="78352-156">Se è necessario tooconfigure un probe personalizzato per il gateway applicazione, vedere [creare un gateway applicazione con probe personalizzati usando PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="78352-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="78352-157">Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="78352-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="78352-158">Creare una rete virtuale e le subnet</span><span class="sxs-lookup"><span data-stu-id="78352-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="78352-159">Hello seguente esempio viene illustrato come toocreate una rete virtuale usando Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="78352-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="78352-160">In questo passaggio vengono create due subnet.</span><span class="sxs-lookup"><span data-stu-id="78352-160">Two subnets are created in this step.</span></span> <span data-ttu-id="78352-161">prima di subnet Hello è per il gateway applicazione hello stesso.</span><span class="sxs-lookup"><span data-stu-id="78352-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="78352-162">Gateway applicazione richiede il proprio toohold subnet delle istanze.</span><span class="sxs-lookup"><span data-stu-id="78352-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="78352-163">In tale subnet possono essere distribuiti solo altri gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="78352-164">subnet secondo Hello è server back-end di applicazione hello toohold utilizzato.</span><span class="sxs-lookup"><span data-stu-id="78352-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="78352-165">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="78352-165">Step 1</span></span>

<span data-ttu-id="78352-166">Assegnare hello indirizzo intervallo 10.0.0.0/24 toohello subnet toobe variabile toohold utilizzati hello gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="78352-167">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="78352-167">Step 2</span></span>

<span data-ttu-id="78352-168">Assegnare hello indirizzo intervallo 10.0.1.0/24 toohello subnet2 variabile toobe utilizzato per il pool di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="78352-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="78352-169">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="78352-169">Step 3</span></span>

<span data-ttu-id="78352-170">Creare una rete virtuale denominata **appgwvnet** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello con hello prefisso 10.0.0.0/16 10.0.0.0/24 subnet e 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="78352-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="78352-171">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="78352-171">Step 4</span></span>

<span data-ttu-id="78352-172">Assegnare una variabile di subnet per i passaggi successivi hello, che consente di creare un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="78352-173">Creare un indirizzo IP pubblico per la configurazione front-end hello</span><span class="sxs-lookup"><span data-stu-id="78352-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="78352-174">Creare una risorsa IP pubblica **publicIP01** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello.</span><span class="sxs-lookup"><span data-stu-id="78352-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="78352-175">Viene assegnato a un indirizzo IP gateway applicazione toohello all'avvio del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="78352-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="78352-176">Creare la configurazione del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="78352-176">Create application gateway configuration</span></span>

<span data-ttu-id="78352-177">Hai tooset backup di tutti gli elementi di configurazione prima di creare i gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="78352-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="78352-178">Hello seguenti passaggi necessari per creare hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="78352-179">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="78352-179">Step 1</span></span>

<span data-ttu-id="78352-180">Creare una configurazione IP del gateway applicazione denominata **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="78352-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="78352-181">Avvio di gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello.</span><span class="sxs-lookup"><span data-stu-id="78352-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="78352-182">Tenere presente che ogni istanza ha un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="78352-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="78352-183">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="78352-183">Step 2</span></span>

<span data-ttu-id="78352-184">Configurare hello pool di indirizzi IP back-end denominato **pool01** e **pool2** con indirizzi IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** per **pool1** e **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  per **pool2**.</span><span class="sxs-lookup"><span data-stu-id="78352-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="78352-185">In questo esempio, sono disponibili due pool back-end tooroute il traffico di rete basato su sito richiesto hello.</span><span class="sxs-lookup"><span data-stu-id="78352-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="78352-186">Un pool riceve il traffico dal sito "contoso.com" e l'altro riceve il traffico dal sito "fabrikam.com".</span><span class="sxs-lookup"><span data-stu-id="78352-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="78352-187">È necessario hello tooreplace precedente tooadd gli indirizzi IP endpoint dell'indirizzo IP la propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="78352-188">Al posto di indirizzi IP interni si potrebbero usare per le istanze back-end anche indirizzi IP pubblici, FQDN o la scheda di interfaccia di rete di una VM.</span><span class="sxs-lookup"><span data-stu-id="78352-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="78352-189">toospecify FQDN anziché gli indirizzi IP in uso di PowerShell "-BackendFQDNs" parametro.</span><span class="sxs-lookup"><span data-stu-id="78352-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="78352-190">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="78352-190">Step 3</span></span>

<span data-ttu-id="78352-191">Configurare impostazioni del gateway applicazione **poolsetting01** e **poolsetting02** hello con bilanciamento del carico del traffico di rete nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="78352-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="78352-192">In questo esempio, configurare le impostazioni del pool back-end diverso per il pool di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="78352-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="78352-193">Ogni pool back-end può avere un'impostazione del pool back-end dedicata.</span><span class="sxs-lookup"><span data-stu-id="78352-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="78352-194">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="78352-194">Step 4</span></span>

<span data-ttu-id="78352-195">Configurazione IP front-end hello con endpoint IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="78352-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="78352-196">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="78352-196">Step 5</span></span>

<span data-ttu-id="78352-197">Configurare hello porta front-end per un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="78352-198">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="78352-198">Step 6</span></span>

<span data-ttu-id="78352-199">Configurare due i certificati SSL per i siti Web hello due verrà toosupport in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="78352-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="78352-200">È un certificato per il traffico di contoso.com e altri hello è per il traffico fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="78352-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="78352-201">Questi certificati per i siti Web devono essere rilasciati da un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="78352-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="78352-202">I certificati autofirmati sono supportati, ma non sono consigliati per il traffico di produzione.</span><span class="sxs-lookup"><span data-stu-id="78352-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="78352-203">Passaggio 7</span><span class="sxs-lookup"><span data-stu-id="78352-203">Step 7</span></span>

<span data-ttu-id="78352-204">In questo esempio, configurare due listener per hello due siti web.</span><span class="sxs-lookup"><span data-stu-id="78352-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="78352-205">Questo passaggio consente di configurare i listener di hello per host, porta e indirizzo IP pubblico usato tooreceive il traffico in entrata.</span><span class="sxs-lookup"><span data-stu-id="78352-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="78352-206">Parametro HostName è obbligatorio per il supporto del sito e deve essere toohello appropriato siti Web per cui hello ricezione del traffico.</span><span class="sxs-lookup"><span data-stu-id="78352-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="78352-207">Parametro RequireServerNameIndication deve essere impostato tootrue per i siti Web che necessitano di supporto per SSL in uno scenario con più host.</span><span class="sxs-lookup"><span data-stu-id="78352-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="78352-208">Se è richiesto il supporto SSL, è necessario anche toospecify hello SSL certificato traffico toosecure utilizzato per l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="78352-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="78352-209">combinazione di Hello di FrontendIPConfiguration front-end e il nome host deve essere univoco tooa listener.</span><span class="sxs-lookup"><span data-stu-id="78352-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="78352-210">Ogni listener può supportare un certificato.</span><span class="sxs-lookup"><span data-stu-id="78352-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="78352-211">Passaggio 8</span><span class="sxs-lookup"><span data-stu-id="78352-211">Step 8</span></span>

<span data-ttu-id="78352-212">Creare due regola impostazione per hello due applicazioni web in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="78352-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="78352-213">Una regola collega listener, pool back-end e impostazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="78352-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="78352-214">Questo passaggio Configura hello applicazione gateway toouse base regola di routing, uno per ogni sito Web.</span><span class="sxs-lookup"><span data-stu-id="78352-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="78352-215">Sito Web tooeach il traffico viene ricevuto dal relativo listener configurato e viene quindi indirizzato tooits configurato pool back-end, utilizzando le proprietà di hello specificate in hello BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="78352-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="78352-216">Passaggio 9:</span><span class="sxs-lookup"><span data-stu-id="78352-216">Step 9</span></span>

<span data-ttu-id="78352-217">Configurare hello numero di istanze e le dimensioni per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="78352-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="78352-218">Creare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="78352-218">Create application gateway</span></span>

<span data-ttu-id="78352-219">Creare un gateway applicazione con tutti gli oggetti di configurazione da hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="78352-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="78352-220">Provisioning di Gateway applicazione è un'operazione a esecuzione prolungata e potrebbe richiedere alcuni toocomplete ora.</span><span class="sxs-lookup"><span data-stu-id="78352-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="78352-221">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="78352-221">Get application gateway DNS name</span></span>

<span data-ttu-id="78352-222">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="78352-223">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="78352-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="78352-224">gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="78352-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="78352-225">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78352-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="78352-226">toodo, dettagli recuperare di gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="78352-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="78352-227">nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis.</span><span class="sxs-lookup"><span data-stu-id="78352-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="78352-228">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="78352-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="78352-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78352-229">Next steps</span></span>

<span data-ttu-id="78352-230">Informazioni su come tooprotect i siti Web con [Gateway applicazione - Firewall applicazione Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="78352-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

