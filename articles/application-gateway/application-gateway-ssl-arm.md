---
title: Configurare l'offload SSL - Gateway applicazione di Azure - PowerShell | Documentazione Microsoft
description: Questa pagina fornisce istruzioni per creare un gateway applicazione con offload SSL usando Gestione risorse di Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="8f5da-103">Configurare un gateway applicazione per l'offload SSL con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f5da-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f5da-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8f5da-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="8f5da-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f5da-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="8f5da-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="8f5da-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="8f5da-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8f5da-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="8f5da-108">Il gateway applicazione di Azure può essere configurato per terminare la sessione Secure Sockets Layer (SSL) nel gateway ed evitare costose attività di decrittografia SSL nella Web farm.</span><span class="sxs-lookup"><span data-stu-id="8f5da-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="8f5da-109">L'offload SSL semplifica anche la configurazione e la gestione del server front-end dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="8f5da-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8f5da-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8f5da-110">Before you begin</span></span>

1. <span data-ttu-id="8f5da-111">Installare la versione più recente dei cmdlet di Azure PowerShell usando l'Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="8f5da-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="8f5da-112">È possibile scaricare e installare la versione più recente dalla sezione **Windows PowerShell** della [Pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8f5da-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="8f5da-113">Creare una rete virtuale e una subnet per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f5da-113">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="8f5da-114">Assicurarsi che nessuna macchina virtuale o distribuzione cloud stia usando la subnet.</span><span class="sxs-lookup"><span data-stu-id="8f5da-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="8f5da-115">Il gateway applicazione deve essere da solo in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8f5da-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="8f5da-116">È necessario che i server configurati per l'uso del gateway applicazione esistano oppure che i relativi endpoint siano stati creati nella rete virtuale o con un indirizzo IP/VIP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="8f5da-116">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="8f5da-117">Elementi necessari per creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="8f5da-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="8f5da-118">**Pool di server back-end:** elenco di indirizzi IP dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="8f5da-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="8f5da-119">Gli indirizzi IP elencati devono appartenere alla subnet della rete virtuale o devono essere indirizzi IP/VIP pubblici.</span><span class="sxs-lookup"><span data-stu-id="8f5da-119">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="8f5da-120">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni come porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="8f5da-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="8f5da-121">Queste impostazioni sono associate a un pool e vengono applicate a tutti i server nel pool.</span><span class="sxs-lookup"><span data-stu-id="8f5da-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="8f5da-122">**Porta front-end:** porta pubblica aperta sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f5da-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="8f5da-123">Il traffico raggiunge questa porta e quindi viene reindirizzato a uno dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="8f5da-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="8f5da-124">**Listener** : ha una porta front-end, un protocollo (Http o Https, queste impostazioni fanno distinzione tra maiuscole e minuscole) e il nome del certificato SSL (se si configura l'offload SSL).</span><span class="sxs-lookup"><span data-stu-id="8f5da-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="8f5da-125">**Regola** : associa il listener e il pool di server back-end e definisce il pool di server back-end a cui deve essere indirizzato il traffico quando raggiunge un listener specifico.</span><span class="sxs-lookup"><span data-stu-id="8f5da-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="8f5da-126">È attualmente supportata solo la regola *basic* .</span><span class="sxs-lookup"><span data-stu-id="8f5da-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="8f5da-127">La regola *basic* è una distribuzione del carico di tipo round robin.</span><span class="sxs-lookup"><span data-stu-id="8f5da-127">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="8f5da-128">**Note aggiuntive sulla configurazione**</span><span class="sxs-lookup"><span data-stu-id="8f5da-128">**Additional configuration notes**</span></span>

<span data-ttu-id="8f5da-129">Per la configurazione dei certificati SSL, il protocollo in **HttpListener** deve essere sostituito con *Https* (distinzione tra maiuscole e minuscole).</span><span class="sxs-lookup"><span data-stu-id="8f5da-129">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="8f5da-130">L'elemento **SslCertificate** viene aggiunto ad **HttpListener** con il valore della variabile configurato per il certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="8f5da-130">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="8f5da-131">La porta front-end deve essere impostata su 443.</span><span class="sxs-lookup"><span data-stu-id="8f5da-131">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="8f5da-132">**Per abilitare l'affinità basata sui cookie**: è possibile configurare un gateway applicazione per fare in modo che una richiesta proveniente da una sessione client sia sempre diretta alla stessa macchina virtuale nella Web farm.</span><span class="sxs-lookup"><span data-stu-id="8f5da-132">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="8f5da-133">Questo scenario viene realizzato aggiungendo un cookie di sessione che consente al gateway di indirizzare il traffico in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="8f5da-133">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="8f5da-134">Per abilitare l'affinità basata sui cookie, impostare **CookieBasedAffinity** su *Enabled* nell'elemento **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="8f5da-134">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="8f5da-135">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="8f5da-135">Create an application gateway</span></span>

<span data-ttu-id="8f5da-136">La differenza tra l'uso del modello di distribuzione classica di Azure e di Azure Resource Manager risiede nell'ordine in cui vengono creati un gateway applicazione e gli elementi da configurare.</span><span class="sxs-lookup"><span data-stu-id="8f5da-136">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="8f5da-137">Con Resource Manager, tutti gli elementi di un gateway applicazione vengono configurati singolarmente e quindi combinati per creare una risorsa gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f5da-137">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="8f5da-138">Per creare un gateway applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8f5da-138">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="8f5da-139">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="8f5da-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="8f5da-140">Creare una rete virtuale, una subnet e un indirizzo IP pubblico per il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="8f5da-140">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="8f5da-141">Creare un oggetto di configurazione gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="8f5da-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="8f5da-142">Creare una risorsa del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="8f5da-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="8f5da-143">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="8f5da-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="8f5da-144">Assicurarsi di passare alla modalità PowerShell per usare i cmdlet di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5da-144">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="8f5da-145">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8f5da-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="8f5da-146">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="8f5da-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="8f5da-147">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="8f5da-147">Step 2</span></span>

<span data-ttu-id="8f5da-148">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="8f5da-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="8f5da-149">Verrà richiesto di eseguire l'autenticazione con le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="8f5da-149">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="8f5da-150">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="8f5da-150">Step 3</span></span>

<span data-ttu-id="8f5da-151">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="8f5da-151">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="8f5da-152">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="8f5da-152">Step 4</span></span>

<span data-ttu-id="8f5da-153">Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="8f5da-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="8f5da-154">Azure Resource Manager richiede che tutti i gruppi di risorse specifichino una località.</span><span class="sxs-lookup"><span data-stu-id="8f5da-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="8f5da-155">Questa impostazione viene usata come località predefinita per le risorse presenti nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8f5da-155">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="8f5da-156">Assicurarsi che tutti i comandi per creare un gateway applicazione usino lo stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8f5da-156">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="8f5da-157">Nell'esempio precedente è stato creato un gruppo di risorse denominato **appgw-RG** e l'area **West US**.</span><span class="sxs-lookup"><span data-stu-id="8f5da-157">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="8f5da-158">Creare una rete virtuale e una subnet per il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="8f5da-158">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="8f5da-159">L'esempio seguente illustra come creare una rete virtuale usando Gestione risorse:</span><span class="sxs-lookup"><span data-stu-id="8f5da-159">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="8f5da-160">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="8f5da-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="8f5da-161">Questo esempio assegna l'intervallo di indirizzi 10.0.0.0/24 a una variabile di subnet da usare per creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8f5da-161">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="8f5da-162">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="8f5da-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="8f5da-163">Questo esempio crea una rete virtuale denominata **appgwvnet** nel gruppo di risorse **appgw-rg** per l'area Stati Uniti occidentali usando il prefisso 10.0.0.0/16 con subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="8f5da-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="8f5da-164">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="8f5da-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="8f5da-165">Questo esempio assegna l'oggetto subnet alla variabile $subnet per i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="8f5da-165">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="8f5da-166">Creare un indirizzo IP pubblico per la configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="8f5da-166">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="8f5da-167">Questo esempio crea una risorsa IP pubblica **publicIP01** nel gruppo di risorse **appgw-rg** per l'area Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="8f5da-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="8f5da-168">Creare un oggetto di configurazione gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="8f5da-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="8f5da-169">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="8f5da-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="8f5da-170">Questo esempio crea una configurazione IP del gateway applicazione denominata **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="8f5da-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="8f5da-171">All'avvio, il gateway applicazione seleziona un indirizzo IP dalla subnet configurata e instrada il traffico di rete agli indirizzi IP nel pool di indirizzi IP back-end.</span><span class="sxs-lookup"><span data-stu-id="8f5da-171">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="8f5da-172">Tenere presente che ogni istanza ha un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="8f5da-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="8f5da-173">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="8f5da-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="8f5da-174">Questo esempio configura il pool di indirizzi IP back-end denominato **pool01** con gli indirizzi IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="8f5da-174">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="8f5da-175">Tali valori saranno gli indirizzi IP che ricevono il traffico di rete proveniente dall'endpoint IP front-end.</span><span class="sxs-lookup"><span data-stu-id="8f5da-175">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="8f5da-176">Sostituire gli indirizzi IP dell'esempio precedente con gli indirizzi IP degli endpoint dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="8f5da-176">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="8f5da-177">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="8f5da-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="8f5da-178">Questo esempio configura l'impostazione **poolsetting01** del gateway applicazione per il traffico di rete con bilanciamento del carico nel pool back-end.</span><span class="sxs-lookup"><span data-stu-id="8f5da-178">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="8f5da-179">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="8f5da-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="8f5da-180">Questo esempio configura la porta IP front-end denominata **frontendport01** per l'endpoint IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="8f5da-180">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="8f5da-181">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="8f5da-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="8f5da-182">Questo esempio configura il certificato usato per la connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="8f5da-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="8f5da-183">Il certificato deve essere in formato PFX e la password deve essere compresa tra 4 e 12 caratteri.</span><span class="sxs-lookup"><span data-stu-id="8f5da-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="8f5da-184">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="8f5da-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="8f5da-185">Questo esempio crea la configurazione IP front-end denominata **fipconfig01** e associa l'indirizzo IP pubblico alla configurazione IP front-end.</span><span class="sxs-lookup"><span data-stu-id="8f5da-185">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="8f5da-186">Passaggio 7</span><span class="sxs-lookup"><span data-stu-id="8f5da-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="8f5da-187">Questo esempio crea il listener denominato **listener01** e associa la porta front-end al certificato e alla configurazione IP front-end.</span><span class="sxs-lookup"><span data-stu-id="8f5da-187">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="8f5da-188">Passaggio 8</span><span class="sxs-lookup"><span data-stu-id="8f5da-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="8f5da-189">Questo esempio crea la regola di routing del servizio di bilanciamento del carico denominata **rule01** che configura il comportamento di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="8f5da-189">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="8f5da-190">Passaggio 9:</span><span class="sxs-lookup"><span data-stu-id="8f5da-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="8f5da-191">Questo esempio configura le dimensioni dell'istanza del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f5da-191">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="8f5da-192">Il valore predefinito per *InstanceCount* è 2, con un valore massimo pari a 10.</span><span class="sxs-lookup"><span data-stu-id="8f5da-192">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="8f5da-193">Il valore predefinito per *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="8f5da-193">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="8f5da-194">È possibile scegliere tra Standard_Small, Standard_Medium e Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="8f5da-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="8f5da-195">Passaggio 10</span><span class="sxs-lookup"><span data-stu-id="8f5da-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="8f5da-196">Questo passaggio definisce i criteri SSL da usare sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f5da-196">This step defines the SSL policy to use on the application gateway.</span></span> <span data-ttu-id="8f5da-197">Per altre informazioni, vedere [Configurare i pacchetti di crittografia e le versioni dei criteri SSL nel gateway applicazione](application-gateway-configure-ssl-policy-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8f5da-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="8f5da-198">Creare un gateway applicazione usando New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="8f5da-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="8f5da-199">Questo esempio crea un gateway applicazione con tutti gli elementi di configurazione illustrati nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="8f5da-199">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="8f5da-200">Nell'esempio il gateway applicazione è denominato **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="8f5da-200">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="8f5da-201">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="8f5da-201">Get application gateway DNS name</span></span>

<span data-ttu-id="8f5da-202">Dopo avere creato il gateway, il passaggio successivo prevede la configurazione del front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="8f5da-202">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="8f5da-203">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="8f5da-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="8f5da-204">Per assicurarsi che gli utenti finali possano raggiungere il gateway applicazione, è possibile usare un record CNAME per fare riferimento all'endpoint pubblico del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f5da-204">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="8f5da-205">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8f5da-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="8f5da-206">A questo scopo, recuperare i dettagli del gateway applicazione e il nome DNS e l'IP associati, usando l'elemento PublicIPAddress collegato al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f5da-206">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="8f5da-207">Il nome DNS del gateway applicazione dovrà essere usato per creare un record CNAME che associa le due applicazioni Web a questo nome DNS.</span><span class="sxs-lookup"><span data-stu-id="8f5da-207">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="8f5da-208">Non è consigliabile usare record A perché l'indirizzo VIP può cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f5da-208">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="8f5da-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f5da-209">Next steps</span></span>

<span data-ttu-id="8f5da-210">Per configurare un gateway applicazione da usare con un servizio di bilanciamento del carico interno, vedere [Creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="8f5da-210">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="8f5da-211">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="8f5da-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="8f5da-212">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="8f5da-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="8f5da-213">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="8f5da-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

