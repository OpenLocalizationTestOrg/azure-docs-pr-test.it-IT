---
title: Creare un gateway applicazione con le regole per il routing basato su URL | Microsoft Docs
description: Questa pagina fornisce istruzioni per la creazione e la configurazione di un gateway applicazione di Azure con le regole per il routing basato su URL
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
ms.openlocfilehash: ba756d3262b9780c5701e69faad860ba32bba08b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="4754f-103">Creare un gateway applicazione con il routing basato sul percorso</span><span class="sxs-lookup"><span data-stu-id="4754f-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4754f-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4754f-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="4754f-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4754f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="4754f-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4754f-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="4754f-107">Il routing basato sul percorso dell'URL consente di associare le route in base al percorso dell'URL di una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="4754f-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="4754f-108">Verifica se è disponibile una route per il pool back-end configurato per l'URL presentato nel gateway applicazione,</span><span class="sxs-lookup"><span data-stu-id="4754f-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway.</span></span> <span data-ttu-id="4754f-109">quindi invia il traffico di rete al pool back-end definito.</span><span class="sxs-lookup"><span data-stu-id="4754f-109">It then sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="4754f-110">In genere il routing basato su URL viene usato per le richieste di bilanciamento del carico per diversi tipi di contenuto tra vari pool di server back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-110">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="4754f-111">Il routing basato su URL introduce un nuovo tipo di regola per i gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-111">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="4754f-112">Per il gateway applicazione sono disponibili due tipi di regole: basic e PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="4754f-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="4754f-113">Il tipo di regola basic fornisce un servizio di tipo round robin per i pool back-end, mentre la regola PathBasedRouting oltre alla distribuzione round robin tiene conto del modello di percorso dell'URL della richiesta per la scelta del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-113">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="4754f-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="4754f-114">Scenario</span></span>

<span data-ttu-id="4754f-115">Nell'esempio seguente il gateway applicazione gestisce il traffico per contoso.com con due pool di server back-end: pool di server video e pool di server immagini.</span><span class="sxs-lookup"><span data-stu-id="4754f-115">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="4754f-116">Le richieste per http://contoso.com/image* vengono instradate al pool di server di immagini (pool1), mentre quelle per http://contoso.com/video* vengono instradate al pool di server di video (pool2).</span><span class="sxs-lookup"><span data-stu-id="4754f-116">Requests for http://contoso.com/image* are routed to image server pool (pool1), and http://contoso.com/video* are routed to video server pool (pool2).</span></span> <span data-ttu-id="4754f-117">In caso di mancata corrispondenza dei modelli di percorso, viene selezionato un pool di server predefinito (pool1).</span><span class="sxs-lookup"><span data-stu-id="4754f-117">if none of the path patterns match, a default server pool (pool1) is selected.</span></span>

![route dell'URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="4754f-119">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4754f-119">Before you begin</span></span>

1. <span data-ttu-id="4754f-120">Installare la versione più recente dei cmdlet di Azure PowerShell usando l'Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="4754f-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="4754f-121">È possibile scaricare e installare la versione più recente dalla sezione **Windows PowerShell** della [Pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4754f-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="4754f-122">Creare una rete virtuale e una subnet per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="4754f-123">Assicurarsi che nessuna macchina virtuale o distribuzione cloud stia usando la subnet.</span><span class="sxs-lookup"><span data-stu-id="4754f-123">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="4754f-124">Il gateway applicazione deve essere da solo in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4754f-124">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="4754f-125">È necessario che i server aggiunti al pool back-end per l'uso del gateway applicazione esistano oppure che i relativi endpoint siano stati creati nella rete virtuale o che sia stato assegnato loro un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="4754f-125">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="4754f-126">Elementi necessari per creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4754f-126">What is required to create an application gateway?</span></span>

* <span data-ttu-id="4754f-127">**Pool di server back-end:** elenco di indirizzi IP dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="4754f-128">Gli indirizzi IP elencati devono appartenere alla subnet della rete virtuale o devono essere indirizzi IP/VIP pubblici.</span><span class="sxs-lookup"><span data-stu-id="4754f-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="4754f-129">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni come porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="4754f-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4754f-130">Queste impostazioni sono associate a un pool e vengono applicate a tutti i server nel pool.</span><span class="sxs-lookup"><span data-stu-id="4754f-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="4754f-131">**Porta front-end:** porta pubblica aperta sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="4754f-132">Il traffico raggiunge questa porta e quindi viene reindirizzato a uno dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="4754f-133">**Listener** : ha una porta front-end, un protocollo (Http o Https, con distinzione tra maiuscole e minuscole) e il nome del certificato SSL (se si configura l'offload SSL).</span><span class="sxs-lookup"><span data-stu-id="4754f-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4754f-134">**Regola** : associa il listener e il pool di server back-end e definisce il pool di server back-end a cui deve essere indirizzato il traffico quando raggiunge un listener specifico.</span><span class="sxs-lookup"><span data-stu-id="4754f-134">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="4754f-135">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4754f-135">Create an application gateway</span></span>

<span data-ttu-id="4754f-136">La differenza tra l'uso di Azure classico e di Azure Resource Manager risiede nell'ordine in cui vengono creati il gateway applicazione e gli elementi da configurare.</span><span class="sxs-lookup"><span data-stu-id="4754f-136">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="4754f-137">Con Resource Manager, tutti gli elementi che costituiscono un gateway applicazione vengono configurati singolarmente e quindi combinati per creare la risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-137">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="4754f-138">Per creare un gateway applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4754f-138">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="4754f-139">Creare un gruppo di risorse per Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="4754f-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="4754f-140">Creare una rete virtuale, una subnet e un indirizzo IP pubblico per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-140">Create a virtual network, subnet, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="4754f-141">Creare un oggetto di configurazione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="4754f-142">Creare una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="4754f-143">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="4754f-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="4754f-144">Assicurarsi di usare la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4754f-144">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="4754f-145">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4754f-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="4754f-146">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="4754f-146">Step 1</span></span>

<span data-ttu-id="4754f-147">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="4754f-147">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="4754f-148">Verrà richiesto di eseguire l'autenticazione con le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="4754f-148">You are prompted to authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="4754f-149">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="4754f-149">Step 2</span></span>

<span data-ttu-id="4754f-150">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="4754f-150">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="4754f-151">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="4754f-151">Step 3</span></span>

<span data-ttu-id="4754f-152">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="4754f-152">Choose which of your Azure subscriptions to use.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="4754f-153">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="4754f-153">Step 4</span></span>

<span data-ttu-id="4754f-154">Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="4754f-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="4754f-155">In alternativa, è anche possibile creare tag del gruppo di risorse per il gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="4754f-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="4754f-156">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="4754f-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="4754f-157">Questo gruppo di risorse viene usato come percorso predefinito per le risorse presenti nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4754f-157">This resource group is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="4754f-158">Assicurarsi che tutti i comandi per creare un gateway applicazione usino lo stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4754f-158">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="4754f-159">Nell'esempio precedente è stato creato un gruppo di risorse denominato "appgw-RG" e la località "West US".</span><span class="sxs-lookup"><span data-stu-id="4754f-159">In the example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="4754f-160">Se è necessario configurare un probe personalizzato per il gateway applicazione, vedere [Creare un probe personalizzato per il gateway applicazione di Azure con PowerShell per Azure Resource Manager](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4754f-160">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="4754f-161">Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="4754f-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="4754f-162">Creare una rete virtuale e una subnet per il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4754f-162">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="4754f-163">L'esempio seguente illustra come creare una rete virtuale usando Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="4754f-163">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="4754f-164">Questo esempio crea una rete virtuale per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-164">This example creates a VNET for the Application Gateway.</span></span> <span data-ttu-id="4754f-165">Il gateway applicazione richiede la propria subnet, per questo motivo la subnet creata per il gateway applicazione è più piccola dello spazio degli indirizzi della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4754f-165">Application Gateway requires its own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span></span> <span data-ttu-id="4754f-166">Ciò consente alle altre risorse, inclusi ma non limitati i server Web, di essere configurate nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4754f-166">This allows for other resources, including but not limited to web servers to be configured in the same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="4754f-167">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="4754f-167">Step 1</span></span>

<span data-ttu-id="4754f-168">Assegnare l'intervallo di indirizzi 10.0.0.0/24 alla variabile di subnet da usare per creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4754f-168">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span></span>  <span data-ttu-id="4754f-169">Questo passaggio crea l'oggetto di configurazione della subnet per il gateway applicazione usato nell'esempio successivo.</span><span class="sxs-lookup"><span data-stu-id="4754f-169">This creates the subnet configuration object for the Application Gateway, which is used in the next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="4754f-170">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="4754f-170">Step 2</span></span>

<span data-ttu-id="4754f-171">Creare una rete virtuale denominata **appgwvnet** nel gruppo di risorse **appgw-rg** per l'area Stati Uniti occidentali usando il prefisso 10.0.0.0/16 con subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="4754f-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="4754f-172">Questo passaggio completa la configurazione della rete virtuale con una singola subnet per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-172">This completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="4754f-173">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="4754f-173">Step 3</span></span>

<span data-ttu-id="4754f-174">Assegnare la variabile di subnet per i passaggi successivi. Questa variabile viene passata al cmdlet `New-AzureRMApplicationGateway` in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="4754f-174">Assign the subnet variable for the next steps, this is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="4754f-175">Creare un indirizzo IP pubblico per la configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="4754f-175">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="4754f-176">Creare una risorsa IP pubblica denominata **publicIP01** nel gruppo di risorse **appgw-rg** per l'area Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="4754f-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="4754f-177">Il gateway applicazione può usare un indirizzo IP pubblico, un interno indirizzo IP o entrambi per ricevere le richieste di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="4754f-177">Application Gateway can use a public IP address, internal IP address or both to receive requests for load balancing.</span></span>  <span data-ttu-id="4754f-178">Per questo esempio è stato usato solo un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="4754f-178">This example only uses a public IP address.</span></span> <span data-ttu-id="4754f-179">Nell'esempio seguente, nessun nome DNS è configurato per la creazione dell'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="4754f-179">In the following example, no DNS name is configured for creating the Public IP address.</span></span>  <span data-ttu-id="4754f-180">Il gateway applicazione non supporta i nomi DNS personalizzati negli indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="4754f-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="4754f-181">Se per l'endpoint pubblico è necessario un nome personalizzato, è necessario creare un record CNAME per fare riferimento al nome DNS generato automaticamente per l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="4754f-181">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="4754f-182">All'avvio del servizio viene assegnato un indirizzo IP al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-182">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="4754f-183">Creare la configurazione del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4754f-183">Create application gateway configuration</span></span>

<span data-ttu-id="4754f-184">Prima di creare il gateway applicazione, è necessario impostare tutti gli elementi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-184">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="4754f-185">La procedura seguente consente di creare gli elementi di configurazione necessari per una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-185">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="4754f-186">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="4754f-186">Step 1</span></span>

<span data-ttu-id="4754f-187">Creare una configurazione IP del gateway applicazione denominata **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="4754f-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="4754f-188">All'avvio, il gateway applicazione seleziona un indirizzo IP dalla subnet configurata e instrada il traffico di rete agli indirizzi IP nel pool di indirizzi IP back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-188">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="4754f-189">Tenere presente che ogni istanza ha un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="4754f-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="4754f-190">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="4754f-190">Step 2</span></span>

<span data-ttu-id="4754f-191">Configurare il pool di indirizzi IP back-end denominato **pool01** e **pool2** con indirizzi IP per **pool1** e **pool2**.</span><span class="sxs-lookup"><span data-stu-id="4754f-191">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="4754f-192">Questi indirizzi sono gli indirizzi IP delle risorse che ospitano l'applicazione Web da proteggere con il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-192">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span></span> <span data-ttu-id="4754f-193">Tutti questi membri del pool back-end vengono convalidati come integri mediante i probe, che siano probe di base o personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4754f-193">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="4754f-194">Il traffico viene instradato verso di loro quando le richieste arrivano al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-194">Traffic is then routed to them when requests come into the application gateway.</span></span> <span data-ttu-id="4754f-195">I pool di back-end possono essere usati dalle regole multiple all'interno del gateway applicazione, ovvero un pool di back-end può essere usato per più applicazioni Web che si trovano nello stesso host.</span><span class="sxs-lookup"><span data-stu-id="4754f-195">Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="4754f-196">Questo esempio mostra due pool back-end che indirizzano il traffico di rete in base al percorso dell'URL.</span><span class="sxs-lookup"><span data-stu-id="4754f-196">In this example, there are two back-end pools to route network traffic based on the URL path.</span></span> <span data-ttu-id="4754f-197">Un pool riceve il traffico dal percorso dell'URL "/video" e l'altro riceve il traffico dal percorso "/image".</span><span class="sxs-lookup"><span data-stu-id="4754f-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="4754f-198">Sostituire gli indirizzi IP precedenti e aggiungere gli endpoint di indirizzi IP dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-198">Replace the preceding IP addresses to add your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="4754f-199">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="4754f-199">Step 3</span></span>

<span data-ttu-id="4754f-200">Configurare le impostazioni **poolsetting01** e **poolsetting02** del gateway applicazione per il traffico di rete con carico bilanciato nel pool back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="4754f-201">In questo esempio vengono configurate diverse impostazioni per i pool back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-201">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="4754f-202">Ogni pool back-end può avere un'impostazione del pool back-end dedicata.</span><span class="sxs-lookup"><span data-stu-id="4754f-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="4754f-203">Le impostazioni HTTP back-end vengono usate dalle regole per instradare il traffico verso i membri del pool di back-end corretti.</span><span class="sxs-lookup"><span data-stu-id="4754f-203">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="4754f-204">Ciò determina il protocollo e la porta usati durante l'invio di traffico ai membri del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-204">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="4754f-205">Anche le sessioni basate sui cookie sono determinate dalle impostazioni HTTP di back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-205">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="4754f-206">Se abilitata, l'affinità di sessione basata su cookie invia traffico allo stesso back-end sotto forma di richieste precedenti per ogni pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4754f-206">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="4754f-207">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="4754f-207">Step 4</span></span>

<span data-ttu-id="4754f-208">Configurare l'indirizzo IP front-end con l'endpoint di indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="4754f-208">Configure the front-end IP with public IP endpoint.</span></span> <span data-ttu-id="4754f-209">L'oggetto di configurazione IP front-end viene usato da un listener per correlare l'indirizzo IP rivolto all'esterno con il listener.</span><span class="sxs-lookup"><span data-stu-id="4754f-209">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="4754f-210">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="4754f-210">Step 5</span></span>

<span data-ttu-id="4754f-211">Configurare la porta front-end per un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-211">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="4754f-212">L'oggetto di configurazione della porta front-end viene usato da un listener per definire la porta del gateway applicazione in ascolto del traffico nel listener.</span><span class="sxs-lookup"><span data-stu-id="4754f-212">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="4754f-213">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="4754f-213">Step 6</span></span>

<span data-ttu-id="4754f-214">Configurare il listener.</span><span class="sxs-lookup"><span data-stu-id="4754f-214">Configure the listener.</span></span> <span data-ttu-id="4754f-215">Questo passaggio configura il listener per l'indirizzo IP pubblico e la porta usata per ricevere il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="4754f-215">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="4754f-216">L'esempio seguente prende in considerazione la configurazione IP front-end configurata in precedenza, la configurazione della porta front-end e un protocollo (HTTP o HTTPS) e configura il listener.</span><span class="sxs-lookup"><span data-stu-id="4754f-216">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="4754f-217">In questo esempio, il listener è in ascolto per il traffico HTTP sulla porta 80 all'indirizzo IP pubblico che è stato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4754f-217">In this example, the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="4754f-218">Passaggio 7</span><span class="sxs-lookup"><span data-stu-id="4754f-218">Step 7</span></span>

<span data-ttu-id="4754f-219">Configurare i percorsi della regola per gli URL per i pool back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-219">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="4754f-220">Questo passaggio configura il percorso relativo usato dal gateway applicazione e definisce il mapping tra il percorso dell'URL e il pool back-end assegnato per gestire il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="4754f-220">This step configures the relative path used by application gateway and defines the mapping between the URL path and the back-end pool that is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4754f-221">Ogni percorso deve iniziare con una barra / e l'unica posizione in cui è consentito il carattere "\*" è alla fine.</span><span class="sxs-lookup"><span data-stu-id="4754f-221">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="4754f-222">Esempi validi sono /xyz, /xyz* or /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="4754f-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="4754f-223">La stringa inviata al selettore di percorsi non include alcun testo dopo il primo carattere "?" o "#" e questi caratteri non sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="4754f-223">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="4754f-224">L'esempio seguente crea due regole: una per il percorso "/image" che instrada il traffico al pool back-end "pool1" e un'altra per il percorso "/video/" che instrada il traffico al pool back-end "pool2".</span><span class="sxs-lookup"><span data-stu-id="4754f-224">The following example creates two rules: one for "/image/" path routing traffic to back-end "pool1" and another one for "/video/" path routing traffic to back-end "pool2."</span></span> <span data-ttu-id="4754f-225">Queste regole assicurano che il traffico per ogni set di URL viene indirizzato al back-end.</span><span class="sxs-lookup"><span data-stu-id="4754f-225">These rules ensure that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="4754f-226">Ad esempio, http://contoso.com/image/figure1.jpg passa al pool1 e http://contoso.com/video/example.mp4 al pool2.</span><span class="sxs-lookup"><span data-stu-id="4754f-226">For example, http://contoso.com/image/figure1.jpg goes to pool1 and http://contoso.com/video/example.mp4 goes to pool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="4754f-227">In caso di mancata corrispondenza con le regole di percorso predefinite, la configurazione del mapping dei percorsi della regola configura anche un pool di indirizzi back-end predefinito.</span><span class="sxs-lookup"><span data-stu-id="4754f-227">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="4754f-228">Ad esempio, http://contoso.com/shoppingcart/test.html passa al pool1 definito come pool predefinito per il traffico senza corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="4754f-228">For example, http://contoso.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="4754f-229">Passaggio 8</span><span class="sxs-lookup"><span data-stu-id="4754f-229">Step 8</span></span>

<span data-ttu-id="4754f-230">Creare un'impostazione della regola.</span><span class="sxs-lookup"><span data-stu-id="4754f-230">Create a rule setting.</span></span> <span data-ttu-id="4754f-231">Questo passaggio configura il gateway applicazione per l'uso del routing basato sul percorso dell'URL.</span><span class="sxs-lookup"><span data-stu-id="4754f-231">This step configures the application gateway to use URL path-based routing.</span></span> <span data-ttu-id="4754f-232">La variabile `$urlPathMap` definita nel passaggio precedente viene ora usata per creare la regola basata sul percorso.</span><span class="sxs-lookup"><span data-stu-id="4754f-232">The `$urlPathMap` variable defined in the earlier step is now used to create the path-based rule.</span></span> <span data-ttu-id="4754f-233">In questo passaggio la regola viene associata a un listener e al mapping del percorso URL creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4754f-233">In this step, we associate the rule with a listener and the url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="4754f-234">Passaggio 9:</span><span class="sxs-lookup"><span data-stu-id="4754f-234">Step 9</span></span>

<span data-ttu-id="4754f-235">Configurare il numero di istanze e le dimensioni per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-235">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="4754f-236">Creare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4754f-236">Create Application Gateway</span></span>

<span data-ttu-id="4754f-237">Creare un gateway applicazione con tutti gli oggetti di configurazione illustrati nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="4754f-237">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="4754f-238">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4754f-238">Get application gateway DNS name</span></span>

<span data-ttu-id="4754f-239">Dopo avere creato il gateway, il passaggio successivo prevede la configurazione del front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-239">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="4754f-240">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="4754f-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="4754f-241">Per assicurarsi che gli utenti finali possano raggiungere il gateway applicazione, è possibile usare un record CNAME per fare riferimento all'endpoint pubblico del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-241">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="4754f-242">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4754f-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="4754f-243">Per configurare il record CNAME per l'IP front-end, recuperare i dettagli del gateway applicazione e il nome DNS e l'IP associati usando l'elemento PublicIPAddress collegato al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-243">To configure the frontend IP CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="4754f-244">Il nome DNS del gateway applicazione dovrà essere usato per creare un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="4754f-244">The application gateway's DNS name should be used to create a CNAME record.</span></span> <span data-ttu-id="4754f-245">Non è consigliabile usare record A perché l'indirizzo VIP può cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4754f-245">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4754f-246">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4754f-246">Next steps</span></span>

<span data-ttu-id="4754f-247">Per informazioni sull'offload SSL (Secure Sockets Layer), vedere [Configurare un gateway applicazione per l'offload SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="4754f-247">If you want to learn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

