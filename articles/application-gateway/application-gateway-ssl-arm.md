---
title: -Gateway applicazione Azure - PowerShell di offload SSL aaaConfigure | Documenti Microsoft
description: Questa pagina fornisce istruzioni toocreate un gateway applicazione con SSL offload usando Gestione risorse di Azure
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
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="a489d-103">Configurare un gateway applicazione per l'offload SSL con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a489d-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a489d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a489d-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="a489d-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a489d-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="a489d-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="a489d-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="a489d-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a489d-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="a489d-108">Gateway applicazione Azure può essere configurato tooterminate hello Secure Sockets Layer (SSL) sessione hello gateway tooavoid costosi SSL decrittografia attività toohappen alla farm web hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="a489d-109">Offload SSL semplifica anche l'installazione di server front-end di hello e gestione di un'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a489d-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a489d-110">Before you begin</span></span>

1. <span data-ttu-id="a489d-111">Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="a489d-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="a489d-112">È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a489d-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="a489d-113">Creare una rete virtuale e una subnet per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="a489d-114">Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="a489d-115">Il gateway applicazione deve essere da solo in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a489d-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="a489d-116">server di Hello è configurare gateway di applicazione hello toouse deve essere presente o i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="a489d-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="a489d-117">Che cos'è toocreate necessario un gateway applicazione?</span><span class="sxs-lookup"><span data-stu-id="a489d-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="a489d-118">**Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="a489d-119">gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="a489d-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="a489d-120">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="a489d-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="a489d-121">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="a489d-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="a489d-122">**Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="a489d-123">Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="a489d-124">**Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, queste impostazioni sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="a489d-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="a489d-125">**Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="a489d-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="a489d-126">Attualmente, solo hello *base* regola supportata.</span><span class="sxs-lookup"><span data-stu-id="a489d-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="a489d-127">Hello *base* regola è una distribuzione del carico round robin.</span><span class="sxs-lookup"><span data-stu-id="a489d-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="a489d-128">**Note aggiuntive sulla configurazione**</span><span class="sxs-lookup"><span data-stu-id="a489d-128">**Additional configuration notes**</span></span>

<span data-ttu-id="a489d-129">Per la configurazione di certificati SSL, hello protocollo **HttpListener** deve modificare troppo*Https* (maiuscole / minuscole).</span><span class="sxs-lookup"><span data-stu-id="a489d-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="a489d-130">Hello **SslCertificate** elemento viene aggiunto troppo**HttpListener** con valore della variabile hello configurato per il certificato SSL hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="a489d-131">porta front-end di Hello deve essere aggiornato too443.</span><span class="sxs-lookup"><span data-stu-id="a489d-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="a489d-132">**affinità basato su cookie tooenable**: un gateway applicazione può essere configurato tooensure che una richiesta da una sessione client è sempre toohello diretto stessa macchina virtuale nella farm web hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="a489d-133">Questo scenario viene eseguito dall'inserimento di un cookie di sessione che consenta il traffico di toodirect di hello gateway in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="a489d-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="a489d-134">impostata l'affinità basato su cookie tooenable, **CookieBasedAffinity** troppo*abilitato* in hello **BackendHttpSettings** elemento.</span><span class="sxs-lookup"><span data-stu-id="a489d-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="a489d-135">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="a489d-135">Create an application gateway</span></span>

<span data-ttu-id="a489d-136">differenza Hello tra il modello di distribuzione di Azure classico hello e Gestione risorse di Azure è ordine hello che si crea un'applicazione gateway e hello gli elementi che devono toobe configurato.</span><span class="sxs-lookup"><span data-stu-id="a489d-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="a489d-137">Gestione risorse di tutti i componenti di gateway applicazione sono configurati singolarmente e quindi inserire toocreate insieme una risorsa di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="a489d-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="a489d-138">Di seguito è hello passaggi necessari toocreate un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="a489d-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="a489d-139">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="a489d-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="a489d-140">Creare una rete virtuale, subnet e indirizzo IP pubblico per il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a489d-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="a489d-141">Creare un oggetto di configurazione gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="a489d-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="a489d-142">Creare una risorsa del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="a489d-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="a489d-143">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="a489d-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="a489d-144">Assicurarsi che si passa in modalità toouse hello Azure Resource Manager cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a489d-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="a489d-145">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a489d-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="a489d-146">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="a489d-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="a489d-147">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="a489d-147">Step 2</span></span>

<span data-ttu-id="a489d-148">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a489d-149">Si è tooauthenticate richiesta con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="a489d-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="a489d-150">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="a489d-150">Step 3</span></span>

<span data-ttu-id="a489d-151">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a489d-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="a489d-152">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="a489d-152">Step 4</span></span>

<span data-ttu-id="a489d-153">Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="a489d-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="a489d-154">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="a489d-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="a489d-155">Questa impostazione viene utilizzata come posizione predefinita hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a489d-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="a489d-156">Assicurarsi che tutti i comandi toocreate utilizza un gateway applicazione hello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a489d-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="a489d-157">Nell'esempio hello sopra, è stato creato un gruppo di risorse denominato **appgw-RG** e il percorso **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="a489d-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="a489d-158">Creare una rete virtuale e una subnet per il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a489d-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="a489d-159">Hello seguente esempio viene illustrato come toocreate una rete virtuale usando Gestione risorse:</span><span class="sxs-lookup"><span data-stu-id="a489d-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="a489d-160">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="a489d-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="a489d-161">In questo esempio assegna hello indirizzo intervallo 10.0.0.0/24 tooa subnet toobe variabile utilizzata toocreate una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a489d-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="a489d-162">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="a489d-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="a489d-163">In questo esempio crea una rete virtuale denominata **appgwvnet** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello con hello prefisso 10.0.0.0/16 10.0.0.0/24 subnet.</span><span class="sxs-lookup"><span data-stu-id="a489d-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="a489d-164">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="a489d-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="a489d-165">In questo esempio assegna hello subnet oggetto toovariable $subnet per i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="a489d-166">Creare un indirizzo IP pubblico per la configurazione front-end hello</span><span class="sxs-lookup"><span data-stu-id="a489d-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="a489d-167">In questo esempio crea una risorsa IP pubblica **publicIP01** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="a489d-168">Creare un oggetto di configurazione gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="a489d-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="a489d-169">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="a489d-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="a489d-170">Questo esempio crea una configurazione IP del gateway applicazione denominata **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="a489d-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="a489d-171">Avvio di Gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="a489d-172">Tenere presente che ogni istanza ha un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="a489d-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="a489d-173">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="a489d-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="a489d-174">Questo esempio Configura pool indirizzi IP back-end di hello denominato **pool01** con indirizzi IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="a489d-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="a489d-175">Tali valori sono gli indirizzi IP hello che ricevono il traffico di rete hello proveniente dall'endpoint IP front-end hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="a489d-176">Sostituire gli indirizzi IP hello hello sopra riportato con indirizzi IP hello degli endpoint dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="a489d-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="a489d-177">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="a489d-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="a489d-178">In questo esempio consente di configurare impostazioni del gateway applicazione **poolsetting01** il traffico di rete bilanciato tooload nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="a489d-179">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="a489d-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="a489d-180">Questo esempio Configura porta IP front-end hello denominata **frontendport01** per endpoint IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="a489d-181">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="a489d-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="a489d-182">Questo esempio Configura certificato hello utilizzato per la connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="a489d-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="a489d-183">certificato Hello deve toobe in formato PFX e password hello deve essere compresa tra 4 too12 caratteri.</span><span class="sxs-lookup"><span data-stu-id="a489d-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="a489d-184">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="a489d-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="a489d-185">In questo esempio Crea configurazione IP front-end di hello denominata **fipconfig01** e lo associa hello indirizzo IP pubblico con configurazione IP front-end hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="a489d-186">Passaggio 7</span><span class="sxs-lookup"><span data-stu-id="a489d-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="a489d-187">Questo esempio viene creato il nome del listener hello **listener01** e lo associa hello configurazione IP front-end di porte front-end toohello e il certificato.</span><span class="sxs-lookup"><span data-stu-id="a489d-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="a489d-188">Passaggio 8</span><span class="sxs-lookup"><span data-stu-id="a489d-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="a489d-189">In questo esempio crea hello regola bilanciamento del carico routing denominata **rule01** che configura il comportamento del servizio di bilanciamento carico di hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="a489d-190">Passaggio 9:</span><span class="sxs-lookup"><span data-stu-id="a489d-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="a489d-191">In questo esempio consente di configurare dimensioni di istanza hello del gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="a489d-192">il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10.</span><span class="sxs-lookup"><span data-stu-id="a489d-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="a489d-193">il valore predefinito per Hello *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="a489d-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="a489d-194">È possibile scegliere tra Standard_Small, Standard_Medium e Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="a489d-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="a489d-195">Passaggio 10</span><span class="sxs-lookup"><span data-stu-id="a489d-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="a489d-196">Questo passaggio definisce hello SSL criteri toouse gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="a489d-197">Visitare [le versioni dei criteri configurare SSL e pacchetti di crittografia nel Gateway applicazione](application-gateway-configure-ssl-policy-powershell.md) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="a489d-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="a489d-198">Creare un gateway applicazione usando New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="a489d-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="a489d-199">Questo esempio viene creato un gateway applicazione con tutti gli elementi di configurazione da hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="a489d-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="a489d-200">Nell'esempio hello, viene chiamato gateway applicazione hello **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="a489d-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="a489d-201">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="a489d-201">Get application gateway DNS name</span></span>

<span data-ttu-id="a489d-202">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="a489d-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="a489d-203">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="a489d-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="a489d-204">gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a489d-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="a489d-205">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a489d-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="a489d-206">toodo, dettagli recuperare di gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="a489d-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="a489d-207">nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis.</span><span class="sxs-lookup"><span data-stu-id="a489d-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="a489d-208">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="a489d-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="a489d-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a489d-209">Next steps</span></span>

<span data-ttu-id="a489d-210">Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno (ILB), vedere [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="a489d-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="a489d-211">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="a489d-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="a489d-212">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="a489d-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="a489d-213">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="a489d-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

