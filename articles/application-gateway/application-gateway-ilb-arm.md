---
title: Gateway applicazione Azure con bilanciamento del carico interno - PowerShell aaaUsing | Documenti Microsoft
description: Questa pagina vengono fornite istruzioni toocreate, configurare, avviare ed eliminare un gateway applicazione Azure con bilanciamento del carico interno (ILB) per Gestione risorse di Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="e4b90-103">Creare un gateway applicazione con un dispositivo di bilanciamento del carico interno (ILB) tramite Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="e4b90-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4b90-104">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="e4b90-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="e4b90-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e4b90-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="e4b90-106">Gateway applicazione Azure può essere configurato con un indirizzo VIP rivolto a Internet o con un endpoint interno non è esposto toohello Internet, noto anche come un endpoint di (ILB) del servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="e4b90-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed toohello Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="e4b90-107">Configurazione di gateway hello con un bilanciamento del carico interno è utile per applicazioni line-of-business interne che non sono esposto toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="e4b90-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications that are not exposed toohello Internet.</span></span> <span data-ttu-id="e4b90-108">È inoltre utile per i servizi e i livelli all'interno di un'applicazione multilivello che si trovano in un limite di sicurezza che non è esposto toohello Internet, ma richiedono comunque round-robin caricano distribuzione, l'aderenza sessione o terminazione Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="e4b90-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed toohello Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="e4b90-109">In questo articolo illustra i passaggi di hello tooconfigure un gateway applicazione con un bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="e4b90-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e4b90-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e4b90-110">Before you begin</span></span>

1. <span data-ttu-id="e4b90-111">Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="e4b90-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="e4b90-112">È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e4b90-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="e4b90-113">Creare una rete virtuale e una subnet per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="e4b90-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="e4b90-114">Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="e4b90-115">Il gateway applicazione deve essere da solo in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e4b90-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="e4b90-116">deve esistere server Hello configurare gateway di applicazione hello toouse o disporre i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="e4b90-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="e4b90-117">Che cos'è toocreate necessario un gateway applicazione?</span><span class="sxs-lookup"><span data-stu-id="e4b90-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="e4b90-118">**Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="e4b90-119">Hello indirizzi IP elencati devono appartenere toohello di rete virtuale, ma in un'altra subnet per il gateway applicazione hello o deve essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="e4b90-119">hello IP addresses listed should either belong toohello virtual network but in a different subnet for hello application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="e4b90-120">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="e4b90-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="e4b90-121">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="e4b90-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="e4b90-122">**Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="e4b90-123">Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="e4b90-124">**Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, si tratta tra maiuscole e minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="e4b90-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="e4b90-125">**Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="e4b90-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="e4b90-126">Attualmente, solo hello *base* regola supportata.</span><span class="sxs-lookup"><span data-stu-id="e4b90-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="e4b90-127">Hello *base* regola è una distribuzione del carico round robin.</span><span class="sxs-lookup"><span data-stu-id="e4b90-127">hello *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="e4b90-128">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="e4b90-128">Create an application gateway</span></span>

<span data-ttu-id="e4b90-129">differenza Hello tra l'utilizzo di Azure classico e Gestione risorse di Azure è ordine hello in cui è stato creato il gateway di applicazione hello e gli elementi hello necessario toobe configurato.</span><span class="sxs-lookup"><span data-stu-id="e4b90-129">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>
<span data-ttu-id="e4b90-130">Gestione risorse di tutti gli elementi che costituiscono un gateway applicazione viene configurata singolarmente e riunire risorsa per il gateway applicazione toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-130">With Resource Manager, all items that make an application gateway is configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="e4b90-131">Ecco i passaggi hello toocreate necessario un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="e4b90-131">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="e4b90-132">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="e4b90-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="e4b90-133">Creare una rete virtuale e una subnet per il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e4b90-133">Create a virtual network and a subnet for hello application gateway</span></span>
3. <span data-ttu-id="e4b90-134">Creare un oggetto di configurazione gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="e4b90-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="e4b90-135">Creare una risorsa del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="e4b90-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="e4b90-136">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="e4b90-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="e4b90-137">Assicurarsi che si passa in modalità toouse hello Azure Resource Manager cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e4b90-137">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="e4b90-138">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e4b90-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="e4b90-139">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e4b90-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="e4b90-140">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e4b90-140">Step 2</span></span>

<span data-ttu-id="e4b90-141">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-141">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="e4b90-142">Si è tooauthenticate richiesta con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="e4b90-142">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="e4b90-143">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="e4b90-143">Step 3</span></span>

<span data-ttu-id="e4b90-144">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4b90-144">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="e4b90-145">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="e4b90-145">Step 4</span></span>

<span data-ttu-id="e4b90-146">Creare un nuovo gruppo di risorse. Ignorare questo passaggio se si sta usando un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="e4b90-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="e4b90-147">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="e4b90-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="e4b90-148">Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e4b90-148">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="e4b90-149">Assicurarsi che tutti i comandi toocreate utilizza un gateway applicazione hello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e4b90-149">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="e4b90-150">In hello sopra riportato, è stato creato un gruppo di risorse denominato "Appgw-rg" e il percorso "Stati Uniti occidentali".</span><span class="sxs-lookup"><span data-stu-id="e4b90-150">In hello preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="e4b90-151">Creare una rete virtuale e una subnet per il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e4b90-151">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="e4b90-152">Hello seguente esempio viene illustrato come toocreate una rete virtuale usando Gestione risorse:</span><span class="sxs-lookup"><span data-stu-id="e4b90-152">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="e4b90-153">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e4b90-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="e4b90-154">Questo passaggio assegna hello indirizzo intervallo 10.0.0.0/24 tooa subnet toobe variabile utilizzata toocreate una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e4b90-154">This step assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="e4b90-155">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e4b90-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="e4b90-156">Questo passaggio viene creata una rete virtuale denominata "appgwvnet" nella risorsa gruppo "appgw-rg" per area Stati Uniti occidentali hello con hello prefisso 10.0.0.0/16 10.0.0.0/24 subnet.</span><span class="sxs-lookup"><span data-stu-id="e4b90-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="e4b90-157">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="e4b90-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="e4b90-158">Questo passaggio assegna hello subnet oggetto toovariable $subnet per i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-158">This step assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="e4b90-159">Creare un oggetto di configurazione gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="e4b90-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="e4b90-160">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e4b90-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="e4b90-161">Questo passaggio crea una configurazione IP del gateway applicazione denominata "gatewayIP01".</span><span class="sxs-lookup"><span data-stu-id="e4b90-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="e4b90-162">Avvio di Gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-162">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="e4b90-163">Tenere presente che ogni istanza ha un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="e4b90-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="e4b90-164">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e4b90-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="e4b90-165">Questo passaggio consente di configurare pool indirizzi IP back-end di hello denominato "pool01" con IP indirizzi "10.1.1.8, 10.1.1.9, 10.1.1.10".</span><span class="sxs-lookup"><span data-stu-id="e4b90-165">This step configures hello back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="e4b90-166">Questi sono gli indirizzi IP hello che ricevono il traffico di rete hello proveniente dall'endpoint IP front-end hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-166">Those are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="e4b90-167">Sostituire hello precedente tooadd gli indirizzi IP endpoint dell'indirizzo IP la propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="e4b90-167">You replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="e4b90-168">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="e4b90-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="e4b90-169">Questo passaggio consente di configurare applicazioni gateway impostazione "poolsetting01" per il carico hello con bilanciati del traffico di rete nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-169">This step configures application gateway setting "poolsetting01" for hello load balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="e4b90-170">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="e4b90-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="e4b90-171">Questo passaggio Configura porta IP front-end hello denominata "frontendport01" per hello bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="e4b90-171">This step configures hello front-end IP port named "frontendport01" for hello ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="e4b90-172">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="e4b90-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="e4b90-173">Questo passaggio Crea una configurazione IP front-end hello chiamata "fipconfig01" e lo associa a un indirizzo IP dalla subnet di rete virtuale corrente hello privato.</span><span class="sxs-lookup"><span data-stu-id="e4b90-173">This step creates hello front-end IP configuration called "fipconfig01" and associates it with a private IP from hello current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="e4b90-174">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="e4b90-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="e4b90-175">Questo passaggio consente di creare listener hello chiamato "listener01" e associa una configurazione IP front-end di hello porta front-end toohello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-175">This step creates hello listener called "listener01" and associates hello front-end port toohello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="e4b90-176">Passaggio 7</span><span class="sxs-lookup"><span data-stu-id="e4b90-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="e4b90-177">Questo passaggio Crea hello regola bilanciamento del carico routing chiamato "rule01" che configura il comportamento del servizio di bilanciamento carico di hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-177">This step creates hello load balancer routing rule called "rule01" that configures hello load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="e4b90-178">Passaggio 8</span><span class="sxs-lookup"><span data-stu-id="e4b90-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="e4b90-179">Questo passaggio consente di configurare dimensioni di istanza hello del gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-179">This step configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="e4b90-180">il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10.</span><span class="sxs-lookup"><span data-stu-id="e4b90-180">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="e4b90-181">il valore predefinito per Hello *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="e4b90-181">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="e4b90-182">È possibile scegliere tra Standard_Small, Standard_Medium e Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="e4b90-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="e4b90-183">Creare un gateway applicazione usando New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="e4b90-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="e4b90-184">Crea un gateway applicazione con tutti gli elementi di configurazione da hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="e4b90-184">Creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="e4b90-185">In questo esempio, i gateway applicazione hello viene chiamato "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="e4b90-185">In this example, hello application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="e4b90-186">Questo passaggio Crea un gateway applicazione con tutti gli elementi di configurazione da hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="e4b90-186">This step creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="e4b90-187">Nell'esempio hello gateway applicazione hello viene chiamato "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="e4b90-187">In hello example, hello application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="e4b90-188">Eliminare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="e4b90-188">Delete an application gateway</span></span>

<span data-ttu-id="e4b90-189">toodelete un gateway applicazione, è necessario hello toodo procedura nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="e4b90-189">toodelete an application gateway, you need toodo hello following steps in order:</span></span>

1. <span data-ttu-id="e4b90-190">Hello utilizzare `Stop-AzureRmApplicationGateway` gateway hello toostop di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e4b90-190">Use hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="e4b90-191">Hello utilizzare `Remove-AzureRmApplicationGateway` gateway hello tooremove di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e4b90-191">Use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="e4b90-192">Verificare che gateway hello è stato rimosso utilizzando hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e4b90-192">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="e4b90-193">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e4b90-193">Step 1</span></span>

<span data-ttu-id="e4b90-194">Ottenere l'oggetto di gateway applicazione hello e associarlo variabile tooa "$getgw".</span><span class="sxs-lookup"><span data-stu-id="e4b90-194">Get hello application gateway object and associate it tooa variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="e4b90-195">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e4b90-195">Step 2</span></span>

<span data-ttu-id="e4b90-196">Utilizzare `Stop-AzureRmApplicationGateway` toostop gateway di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-196">Use `Stop-AzureRmApplicationGateway` toostop hello application gateway.</span></span> <span data-ttu-id="e4b90-197">In questo esempio viene hello `Stop-AzureRmApplicationGateway` cmdlet hello della prima riga, seguito dall'output di hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-197">This sample shows hello `Stop-AzureRmApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="e4b90-198">Una volta gateway applicazione hello in stato di interruzione, utilizzare hello `Remove-AzureRmApplicationGateway` servizio hello tooremove di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e4b90-198">Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="e4b90-199">Hello **-force** switch possono essere messaggio di conferma rimozione hello toosuppress utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e4b90-199">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="e4b90-200">tooverify che hello servizio è stato rimosso, è possibile usare hello `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e4b90-200">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="e4b90-201">Questo passaggio non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="e4b90-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="e4b90-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e4b90-202">Next steps</span></span>

<span data-ttu-id="e4b90-203">Se si desidera tooconfigure offload SSL, vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="e4b90-203">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="e4b90-204">Se si desidera tooconfigure un toouse di gateway applicazione con un bilanciamento del carico interno, vedere [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="e4b90-204">If you want tooconfigure an application gateway toouse with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="e4b90-205">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="e4b90-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="e4b90-206">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="e4b90-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="e4b90-207">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="e4b90-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

