---
title: "Creare un gateway applicazione per l'hosting di più siti | Microsoft Docs"
description: "Questa pagina contiene istruzioni per creare e configurare un gateway applicazione di Azure per l'hosting di più applicazioni Web nello stesso gateway."
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
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="3748f-103">Creare un gateway applicazione per l'hosting di più applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="3748f-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3748f-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3748f-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="3748f-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3748f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="3748f-106">L'hosting di più siti consente di distribuire più applicazioni Web nello stesso gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="3748f-107">La presenza dell'intestazione host nella richiesta HTTP in ingresso consente di determinare il listener che riceverà il traffico.</span><span class="sxs-lookup"><span data-stu-id="3748f-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="3748f-108">Il listener indirizza quindi il traffico al pool back-end appropriato in base alla configurazione della definizione delle regole del gateway.</span><span class="sxs-lookup"><span data-stu-id="3748f-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="3748f-109">Nelle applicazioni Web abilitate per SSL il gateway applicazione sceglie il listener corretto per il traffico Web in base all'estensione dell'indicazione nome server (SNI).</span><span class="sxs-lookup"><span data-stu-id="3748f-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="3748f-110">L'hosting di più siti viene comunemente usato per bilanciare il carico delle richieste per diversi domini Web tra vari pool di server back-end.</span><span class="sxs-lookup"><span data-stu-id="3748f-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="3748f-111">Analogamente, lo stesso gateway applicazione potrebbe ospitare anche più sottodomini dello stesso dominio radice.</span><span class="sxs-lookup"><span data-stu-id="3748f-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="3748f-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="3748f-112">Scenario</span></span>

<span data-ttu-id="3748f-113">Nell'esempio seguente, il gateway applicazione gestisce il traffico per contoso.com e fabrikam.com con due pool di server back-end: il pool di server contoso e il pool di server fabrikam.</span><span class="sxs-lookup"><span data-stu-id="3748f-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="3748f-114">Una configurazione simile potrebbe essere usata per ospitare sottodomini come app.contoso.com e blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3748f-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="3748f-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3748f-116">Before you begin</span></span>

1. <span data-ttu-id="3748f-117">Installare la versione più recente dei cmdlet di Azure PowerShell usando l'Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="3748f-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="3748f-118">È possibile scaricare e installare la versione più recente dalla sezione **Windows PowerShell** della [Pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3748f-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="3748f-119">È necessario che i server aggiunti al pool back-end per l'uso del gateway applicazione esistano oppure che i relativi endpoint siano stati creati nella rete virtuale in una subnet separata o che sia stato assegnato loro un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="3748f-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="3748f-120">Requisiti</span><span class="sxs-lookup"><span data-stu-id="3748f-120">Requirements</span></span>

* <span data-ttu-id="3748f-121">**Pool di server back-end:** elenco di indirizzi IP dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="3748f-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="3748f-122">Gli indirizzi IP elencati devono appartenere alla subnet della rete virtuale o devono essere indirizzi IP/VIP pubblici.</span><span class="sxs-lookup"><span data-stu-id="3748f-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="3748f-123">È possibile usare anche FQDN.</span><span class="sxs-lookup"><span data-stu-id="3748f-123">FQDN can also be used.</span></span>
* <span data-ttu-id="3748f-124">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="3748f-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="3748f-125">Queste impostazioni sono associate a un pool e vengono applicate a tutti i server nel pool.</span><span class="sxs-lookup"><span data-stu-id="3748f-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="3748f-126">**Porta front-end:** porta pubblica aperta sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="3748f-127">Il traffico raggiunge questa porta e quindi viene reindirizzato a uno dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="3748f-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="3748f-128">**Listener** : ha una porta front-end, un protocollo (Http o Https, con distinzione tra maiuscole e minuscole) e il nome del certificato SSL (se si configura l'offload SSL).</span><span class="sxs-lookup"><span data-stu-id="3748f-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="3748f-129">Per i gateway applicazione abilitati per più siti vengono aggiunti anche indicatori SNI e nome host.</span><span class="sxs-lookup"><span data-stu-id="3748f-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="3748f-130">**Regola**: associa il listener e il pool di server back-end e definisce il pool di server back-end a cui deve essere indirizzato il traffico quando raggiunge un listener specifico.</span><span class="sxs-lookup"><span data-stu-id="3748f-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="3748f-131">Le regole vengono elaborate nell'ordine in cui sono elencate e il traffico verrà indirizzato tramite la prima regola corrispondente indipendentemente dalla specificità.</span><span class="sxs-lookup"><span data-stu-id="3748f-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="3748f-132">Se ad esempio si dispone di due regole, una che usa un listener di base e una che usa un listener multisito, entrambe sulla stessa porta, la regola con il listener multisito deve essere elencata prima della regola con il listener di base per funzionare come previsto.</span><span class="sxs-lookup"><span data-stu-id="3748f-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="3748f-133">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="3748f-133">Create an application gateway</span></span>

<span data-ttu-id="3748f-134">Per creare un gateway applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3748f-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="3748f-135">Creare un gruppo di risorse per Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="3748f-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="3748f-136">Creare una rete virtuale, le subnet e un indirizzo IP pubblico per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="3748f-137">Creare un oggetto di configurazione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="3748f-138">Creare una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="3748f-139">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="3748f-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="3748f-140">Assicurarsi di usare la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3748f-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="3748f-141">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3748f-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="3748f-142">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="3748f-142">Step 1</span></span>

<span data-ttu-id="3748f-143">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="3748f-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="3748f-144">Verrà richiesto di eseguire l'autenticazione con le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="3748f-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="3748f-145">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="3748f-145">Step 2</span></span>

<span data-ttu-id="3748f-146">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="3748f-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="3748f-147">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="3748f-147">Step 3</span></span>

<span data-ttu-id="3748f-148">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="3748f-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="3748f-149">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="3748f-149">Step 4</span></span>

<span data-ttu-id="3748f-150">Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="3748f-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="3748f-151">In alternativa, è anche possibile creare tag del gruppo di risorse per il gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="3748f-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="3748f-152">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="3748f-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="3748f-153">che viene usato come percorso predefinito per le risorse presenti in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3748f-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="3748f-154">Assicurarsi che tutti i comandi per creare un gateway applicazione usino lo stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3748f-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="3748f-155">Nell'esempio precedente è stato creato un gruppo di risorse denominato **appgw-RG** con la località **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="3748f-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="3748f-156">Se è necessario configurare un probe personalizzato per il gateway applicazione, vedere [Creare un probe personalizzato per il gateway applicazione di Azure con PowerShell per Azure Resource Manager](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3748f-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="3748f-157">Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="3748f-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="3748f-158">Creare una rete virtuale e le subnet</span><span class="sxs-lookup"><span data-stu-id="3748f-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="3748f-159">L'esempio seguente illustra come creare una rete virtuale usando Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="3748f-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="3748f-160">In questo passaggio vengono create due subnet.</span><span class="sxs-lookup"><span data-stu-id="3748f-160">Two subnets are created in this step.</span></span> <span data-ttu-id="3748f-161">La prima subnet è per il gateway applicazione stesso.</span><span class="sxs-lookup"><span data-stu-id="3748f-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="3748f-162">Il gateway applicazione richiede una propria subnet che deve contenere le sue istanze.</span><span class="sxs-lookup"><span data-stu-id="3748f-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="3748f-163">In tale subnet possono essere distribuiti solo altri gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="3748f-164">La seconda subnet viene usata per contenere i server back-end dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="3748f-165">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="3748f-165">Step 1</span></span>

<span data-ttu-id="3748f-166">Assegnare l'intervallo di indirizzi 10.0.0.0/24 alla variabile subnet da usare per contenere il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="3748f-167">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="3748f-167">Step 2</span></span>

<span data-ttu-id="3748f-168">Assegnare l'intervallo di indirizzi 10.0.1.0/24 alla variabile subnet2 da usare per i pool back-end.</span><span class="sxs-lookup"><span data-stu-id="3748f-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="3748f-169">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="3748f-169">Step 3</span></span>

<span data-ttu-id="3748f-170">Creare una rete virtuale denominata **appgwvnet** nel gruppo di risorse **appgw-rg** per l'area Stati Uniti occidentali usando il prefisso 10.0.0.0/16 con le subnet 10.0.0.0/24 e 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="3748f-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="3748f-171">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="3748f-171">Step 4</span></span>

<span data-ttu-id="3748f-172">Assegnare una variabile di subnet per la creazione di un gateway applicazione nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="3748f-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="3748f-173">Creare un indirizzo IP pubblico per la configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="3748f-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="3748f-174">Creare una risorsa IP pubblica denominata **publicIP01** nel gruppo di risorse **appgw-rg** per l'area Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="3748f-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="3748f-175">All'avvio del servizio viene assegnato un indirizzo IP al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="3748f-176">Creare la configurazione del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="3748f-176">Create application gateway configuration</span></span>

<span data-ttu-id="3748f-177">È necessario impostare tutti gli elementi di configurazione prima di creare il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="3748f-178">La procedura seguente consente di creare gli elementi di configurazione necessari per una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="3748f-179">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="3748f-179">Step 1</span></span>

<span data-ttu-id="3748f-180">Creare una configurazione IP del gateway applicazione denominata **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="3748f-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="3748f-181">All'avvio, il gateway applicazione seleziona un indirizzo IP dalla subnet configurata e instrada il traffico di rete agli indirizzi IP nel pool di indirizzi IP back-end.</span><span class="sxs-lookup"><span data-stu-id="3748f-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="3748f-182">Tenere presente che ogni istanza ha un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="3748f-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="3748f-183">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="3748f-183">Step 2</span></span>

<span data-ttu-id="3748f-184">Configurare i pool di indirizzi IP back-end denominati **pool01** e **pool2** con gli indirizzi IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** per **pool1** e **134.170.186.46**, **134.170.189.221**, **134.170.186.50** per **pool2**.</span><span class="sxs-lookup"><span data-stu-id="3748f-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="3748f-185">Questo esempio mostra due pool back-end che indirizzano il traffico di rete in base al sito richiesto.</span><span class="sxs-lookup"><span data-stu-id="3748f-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="3748f-186">Un pool riceve il traffico dal sito "contoso.com" e l'altro riceve il traffico dal sito "fabrikam.com".</span><span class="sxs-lookup"><span data-stu-id="3748f-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="3748f-187">È necessario sostituire gli indirizzi IP precedenti e aggiungere gli endpoint di indirizzi IP dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="3748f-188">Al posto di indirizzi IP interni si potrebbero usare per le istanze back-end anche indirizzi IP pubblici, FQDN o la scheda di interfaccia di rete di una VM.</span><span class="sxs-lookup"><span data-stu-id="3748f-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="3748f-189">Per specificare FQDN invece di indirizzi IP in PowerShell usare il parametro "-BackendFQDNs".</span><span class="sxs-lookup"><span data-stu-id="3748f-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="3748f-190">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="3748f-190">Step 3</span></span>

<span data-ttu-id="3748f-191">Configurare le impostazioni **poolsetting01** e **poolsetting02** del gateway applicazione per il traffico di rete con carico bilanciato nel pool back-end.</span><span class="sxs-lookup"><span data-stu-id="3748f-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="3748f-192">In questo esempio vengono configurate diverse impostazioni per i pool back-end.</span><span class="sxs-lookup"><span data-stu-id="3748f-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="3748f-193">Ogni pool back-end può avere un'impostazione del pool back-end dedicata.</span><span class="sxs-lookup"><span data-stu-id="3748f-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="3748f-194">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="3748f-194">Step 4</span></span>

<span data-ttu-id="3748f-195">Configurare l'indirizzo IP front-end con l'endpoint di indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="3748f-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="3748f-196">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="3748f-196">Step 5</span></span>

<span data-ttu-id="3748f-197">Configurare la porta front-end per un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="3748f-198">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="3748f-198">Step 6</span></span>

<span data-ttu-id="3748f-199">Configurare due certificati SSL per i due siti Web che verranno supportati in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="3748f-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="3748f-200">un certificato per il traffico di contoso.com e l'altro per il traffico di fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="3748f-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="3748f-201">Questi certificati per i siti Web devono essere rilasciati da un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="3748f-202">I certificati autofirmati sono supportati, ma non sono consigliati per il traffico di produzione.</span><span class="sxs-lookup"><span data-stu-id="3748f-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="3748f-203">Passaggio 7</span><span class="sxs-lookup"><span data-stu-id="3748f-203">Step 7</span></span>

<span data-ttu-id="3748f-204">Configurare due listener per i due siti Web dell'esempio.</span><span class="sxs-lookup"><span data-stu-id="3748f-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="3748f-205">Questo passaggio configura i listener per l'indirizzo IP pubblico, la porta e l'host usati per ricevere il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="3748f-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="3748f-206">Il parametro HostName è necessario per il supporto di più siti e deve essere impostato sul sito Web appropriato per cui viene ricevuto il traffico.</span><span class="sxs-lookup"><span data-stu-id="3748f-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="3748f-207">Il parametro RequireServerNameIndication dovrà essere impostato su true per i siti Web in cui è necessario il supporto per SSL per uno scenario di hosting multiplo.</span><span class="sxs-lookup"><span data-stu-id="3748f-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="3748f-208">Se è necessario il supporto per SSL, si deve specificare anche il certificato SSL che viene usato per proteggere il traffico per l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="3748f-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="3748f-209">La combinazione di FrontendIPConfiguration, FrontendPort e HostName deve essere univoca per un listener.</span><span class="sxs-lookup"><span data-stu-id="3748f-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="3748f-210">Ogni listener può supportare un certificato.</span><span class="sxs-lookup"><span data-stu-id="3748f-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="3748f-211">Passaggio 8</span><span class="sxs-lookup"><span data-stu-id="3748f-211">Step 8</span></span>

<span data-ttu-id="3748f-212">Creare l'impostazione di due regole per le due applicazioni Web di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="3748f-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="3748f-213">Una regola collega listener, pool back-end e impostazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="3748f-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="3748f-214">Questo passaggio configura il gateway applicazione per l'uso di una regola di routing Basic per ogni sito Web.</span><span class="sxs-lookup"><span data-stu-id="3748f-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="3748f-215">Il traffico verso ogni sito Web viene ricevuto dal rispettivo listener configurato e quindi indirizzato al pool back-end configurato usando le proprietà specificate in BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="3748f-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="3748f-216">Passaggio 9:</span><span class="sxs-lookup"><span data-stu-id="3748f-216">Step 9</span></span>

<span data-ttu-id="3748f-217">Configurare il numero di istanze e le dimensioni per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="3748f-218">Creare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="3748f-218">Create application gateway</span></span>

<span data-ttu-id="3748f-219">Creare un gateway applicazione con tutti gli oggetti di configurazione illustrati nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="3748f-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="3748f-220">Il provisioning del gateway applicazione è un'operazione con esecuzione prolungata il cui completamento può richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="3748f-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="3748f-221">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="3748f-221">Get application gateway DNS name</span></span>

<span data-ttu-id="3748f-222">Dopo avere creato il gateway, il passaggio successivo prevede la configurazione del front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="3748f-223">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="3748f-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="3748f-224">Per assicurarsi che gli utenti finali possano raggiungere il gateway applicazione, è possibile usare un record CNAME per fare riferimento all'endpoint pubblico del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="3748f-225">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3748f-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="3748f-226">A questo scopo, recuperare i dettagli del gateway applicazione e il nome DNS e l'IP associati, usando l'elemento PublicIPAddress collegato al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="3748f-227">Il nome DNS del gateway applicazione dovrà essere usato per creare un record CNAME che associa le due applicazioni Web a questo nome DNS.</span><span class="sxs-lookup"><span data-stu-id="3748f-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="3748f-228">Non è consigliabile usare record A perché l'indirizzo VIP può cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3748f-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3748f-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3748f-229">Next steps</span></span>

<span data-ttu-id="3748f-230">Informazioni su come proteggere i siti Web con [Gateway applicazione: firewall applicazione Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3748f-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

