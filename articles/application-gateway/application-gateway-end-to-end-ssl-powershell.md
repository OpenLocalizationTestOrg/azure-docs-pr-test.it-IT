---
title: aaaConfigure fine tooend SSL con Gateway applicazione Azure | Documenti Microsoft
description: In questo articolo viene descritto come tooconfigure terminare tooend SSL con il Gateway applicazione usando Gestione risorse di Azure PowerShell
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="9bebc-103">Configurare tooend fine SSL con il Gateway applicazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bebc-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="9bebc-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9bebc-104">Overview</span></span>

<span data-ttu-id="9bebc-105">Supporta Gateway applicazione finale tooend la crittografia del traffico.</span><span class="sxs-lookup"><span data-stu-id="9bebc-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="9bebc-106">Gateway applicazione esegue questa operazione terminerà hello di connessione SSL al gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="9bebc-107">gateway Hello Applica regole di routing hello traffico toohello, crittografare nuovamente i pacchetti hello e inoltra hello pacchetto toohello back-end appropriati in base alle regole di routing hello definite.</span><span class="sxs-lookup"><span data-stu-id="9bebc-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="9bebc-108">Le risposte dal server web hello attraversa hello stessa procedura adottata toohello back-end utente.</span><span class="sxs-lookup"><span data-stu-id="9bebc-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="9bebc-109">Un'altra funzionalità supportata dal gateway applicazione è la definizione delle opzioni SSL personalizzate.</span><span class="sxs-lookup"><span data-stu-id="9bebc-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="9bebc-110">Gateway applicazione supporta hello disabilitando la seguente versione di protocollo. **TLSv1.0**, **TLSv1.1**, e **TLSv1.2** anche la definizione di hello che codifica ordine toouse e hello di gruppi di preferenza.</span><span class="sxs-lookup"><span data-stu-id="9bebc-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="9bebc-111">toolearn più sulle opzioni configurabili SSL, visitare [Panoramica criteri SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9bebc-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9bebc-112">SSL 2.0 e SSL 3.0 sono disabilitati per impostazione predefinita e non possono essere abilitati.</span><span class="sxs-lookup"><span data-stu-id="9bebc-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="9bebc-113">Questi sono considerati non sicuri e non sono in grado di toobe utilizzato con Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![immagine dello scenario][scenario]

## <a name="scenario"></a><span data-ttu-id="9bebc-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="9bebc-115">Scenario</span></span>

<span data-ttu-id="9bebc-116">In questo scenario viene illustrato come toocreate gateway un'applicazione che utilizza end tooend SSL tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bebc-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="9bebc-117">Questo scenario illustrerà come:</span><span class="sxs-lookup"><span data-stu-id="9bebc-117">This scenario will:</span></span>

* <span data-ttu-id="9bebc-118">Creare un gruppo di risorse denominato **appgw-rg**</span><span class="sxs-lookup"><span data-stu-id="9bebc-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="9bebc-119">Creare una rete virtuale denominata **appgwvnet** con uno spazio indirizzi 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="9bebc-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="9bebc-120">Creare due subnet denominate **appgwsubnet** e **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="9bebc-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="9bebc-121">Creare una piccola applicazione gateway supporto end tooend la crittografia SSL che limiti versioni di protocolli SSL e i pacchetti di crittografia.</span><span class="sxs-lookup"><span data-stu-id="9bebc-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9bebc-122">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="9bebc-122">Before you begin</span></span>

<span data-ttu-id="9bebc-123">fine tooconfigure tooend SSL con un gateway applicazione, è necessario per il gateway hello un certificato e i certificati sono necessari per i server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="9bebc-124">certificato di gateway Hello è utilizzato tooencrypt e decrittografia hello il traffico inviato tooit mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="9bebc-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="9bebc-125">certificato di gateway Hello deve toobe nel formato di scambio di informazioni personali (pfx).</span><span class="sxs-lookup"><span data-stu-id="9bebc-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="9bebc-126">Questo formato di file consente di hello privata toobe chiave esportato richiesto dal hello applicazione gateway tooperform hello crittografia e decrittografia del traffico.</span><span class="sxs-lookup"><span data-stu-id="9bebc-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="9bebc-127">Per end tooend SSL crittografia hello back-end deve essere abilitata con gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="9bebc-128">Questa operazione viene eseguita dal caricamento hello certificato pubblico del gateway applicazione toohello di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="9bebc-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="9bebc-129">In questo modo si garantisce che il gateway applicazione hello comunica solo con istanze di back-end noti.</span><span class="sxs-lookup"><span data-stu-id="9bebc-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="9bebc-130">Questo protegge ulteriormente la comunicazione di tooend end hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="9bebc-131">Questo processo è descritto in hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9bebc-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="9bebc-132">Creare hello gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="9bebc-132">Create hello Resource Group</span></span>

<span data-ttu-id="9bebc-133">Questa sezione viene illustrata la creazione di un gruppo di risorse, che contiene i gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="9bebc-134">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="9bebc-134">Step 1</span></span>

<span data-ttu-id="9bebc-135">Accedi tooyour Account Azure.</span><span class="sxs-lookup"><span data-stu-id="9bebc-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="9bebc-136">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="9bebc-136">Step 2</span></span>

<span data-ttu-id="9bebc-137">Selezionare hello toouse di sottoscrizione per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="9bebc-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="9bebc-138">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="9bebc-138">Step 3</span></span>

<span data-ttu-id="9bebc-139">Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="9bebc-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="9bebc-140">Creare una rete virtuale e una subnet per il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="9bebc-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="9bebc-141">Hello seguente viene creata una rete virtuale e due subnet.</span><span class="sxs-lookup"><span data-stu-id="9bebc-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="9bebc-142">Gateway applicazione hello di toohold usato è una subnet.</span><span class="sxs-lookup"><span data-stu-id="9bebc-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="9bebc-143">le altre subnet Hello viene utilizzato per hello back-end web hosting hello applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="9bebc-144">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="9bebc-144">Step 1</span></span>

<span data-ttu-id="9bebc-145">Assegnare un intervallo di indirizzi per subnet hello da utilizzare per hello Gateway applicazione stessa.</span><span class="sxs-lookup"><span data-stu-id="9bebc-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="9bebc-146">Le subnet configurate per il gateway applicazione devono essere ridimensionate in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="9bebc-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="9bebc-147">Un gateway applicazione può essere configurato per le istanze di too10.</span><span class="sxs-lookup"><span data-stu-id="9bebc-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="9bebc-148">Ogni istanza richiede un indirizzo IP dalla subnet hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="9bebc-149">Le dimensioni eccessivamente piccole di una subnet possono influire negativamente sull'aumento del numero di istanze di un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="9bebc-150">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="9bebc-150">Step 2</span></span>

<span data-ttu-id="9bebc-151">Assegnare un toobe intervallo di indirizzi utilizzato per il pool di indirizzi back-end hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="9bebc-152">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="9bebc-152">Step 3</span></span>

<span data-ttu-id="9bebc-153">Creare una rete virtuale con subnet hello definita in hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="9bebc-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="9bebc-154">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="9bebc-154">Step 4</span></span>

<span data-ttu-id="9bebc-155">Recuperare hello rete virtuale risorse e la subnet risorse toobe utilizzato in hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9bebc-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="9bebc-156">Creare un indirizzo IP pubblico per la configurazione front-end hello</span><span class="sxs-lookup"><span data-stu-id="9bebc-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="9bebc-157">Creare un toobe di risorsa IP pubblica utilizzata per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="9bebc-158">Questo indirizzo IP pubblico viene usato in uno dei prossimi passaggi.</span><span class="sxs-lookup"><span data-stu-id="9bebc-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="9bebc-159">Gateway applicazione non supporta l'utilizzo di hello di un indirizzo IP pubblico creato con un'etichetta di dominio definita.</span><span class="sxs-lookup"><span data-stu-id="9bebc-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="9bebc-160">È supportato solo un indirizzo IP pubblico con etichetta di dominio creata in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="9bebc-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="9bebc-161">Se è necessario un nome descrittivo di dns per il gateway applicazione hello, si consiglia di registrare un record CNAME toouse come alias.</span><span class="sxs-lookup"><span data-stu-id="9bebc-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="9bebc-162">Creare un oggetto di configurazione gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="9bebc-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="9bebc-163">Tutti gli elementi di configurazione vengono impostati prima di creare i gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="9bebc-164">Hello seguenti passaggi necessari per creare hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="9bebc-165">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="9bebc-165">Step 1</span></span>

<span data-ttu-id="9bebc-166">Creare una configurazione IP del gateway applicazione, questa impostazione configura utilizzi gateway applicazione hello subnet.</span><span class="sxs-lookup"><span data-stu-id="9bebc-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="9bebc-167">Avvio di gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e lo indirizza gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="9bebc-168">Tenere presente che ogni istanza ha un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="9bebc-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="9bebc-169">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="9bebc-169">Step 2</span></span>

<span data-ttu-id="9bebc-170">Creare una configurazione IP front-end, questa impostazione esegue il mapping di un ip pubblico o privato indirizzo toohello front-end del gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="9bebc-171">Hello riportata dopo il passaggio Associa indirizzo IP pubblico hello nel precedente passaggio con configurazione IP front-end hello hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="9bebc-172">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="9bebc-172">Step 3</span></span>

<span data-ttu-id="9bebc-173">Configurare i pool di indirizzi IP di hello back-end con indirizzi IP hello del server web back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="9bebc-174">Questi indirizzi IP sono gli indirizzi IP hello che ricevono il traffico di rete hello proveniente dall'endpoint IP front-end hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="9bebc-175">Sostituire hello seguente tooadd gli indirizzi IP endpoint dell'indirizzo IP la propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="9bebc-176">Un nome di dominio completo (FQDN) è un valore valido al posto di un indirizzo ip per i server back-end hello tramite commutatore - BackendFqdns hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="9bebc-177">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="9bebc-177">Step 4</span></span>

<span data-ttu-id="9bebc-178">Configurare una porta IP front-end di hello per endpoint IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="9bebc-179">Questa porta è porta hello in grado di connettersi agli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="9bebc-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="9bebc-180">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="9bebc-180">Step 5</span></span>

<span data-ttu-id="9bebc-181">Configurare hello certificato per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="9bebc-182">Questo certificato viene utilizzato toodecrypt e crittografa nuovamente traffico hello gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="9bebc-183">Questo esempio Configura certificato hello utilizzato per la connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="9bebc-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="9bebc-184">certificato Hello deve toobe in formato PFX e password hello deve essere compresa tra 4 too12 caratteri.</span><span class="sxs-lookup"><span data-stu-id="9bebc-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="9bebc-185">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="9bebc-185">Step 6</span></span>

<span data-ttu-id="9bebc-186">Creare il listener HTTP hello per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="9bebc-187">Assegnare una configurazione ip front-end di hello, porta e toouse certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="9bebc-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="9bebc-188">Passaggio 7</span><span class="sxs-lookup"><span data-stu-id="9bebc-188">Step 7</span></span>

<span data-ttu-id="9bebc-189">Caricare il certificato di hello toobe utilizzato su hello SSL abilitato risorse del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="9bebc-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="9bebc-190">probe predefinito Hello Ottiene la chiave pubblica di hello da hello **predefinito** associazione SSL per l'indirizzo IP hello back-end e confronta hello valore della chiave pubblica riceve toohello valore della chiave pubblica qui.</span><span class="sxs-lookup"><span data-stu-id="9bebc-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="9bebc-191">Hello recuperata la chiave pubblica potrebbe non essere necessariamente flussi di traffico hello destinato sito toowhich **se** si utilizzano intestazioni host e SNI hello back-end.</span><span class="sxs-lookup"><span data-stu-id="9bebc-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="9bebc-192">In caso di dubbio, visitare https://127.0.0.1/ tooconfirm back-end hello quale certificato viene utilizzato per hello **predefinito** binding SSL.</span><span class="sxs-lookup"><span data-stu-id="9bebc-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="9bebc-193">Utilizzare una chiave pubblica di hello dalla richiesta in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="9bebc-194">Se si utilizzano intestazioni host e SNI associazioni HTTPS e non si riceve una risposta e il certificato da un toohttps://127.0.0.1/ richiesta browser manuale in hello back-end, è necessario configurare un binding SSL predefinito in hello back-end.</span><span class="sxs-lookup"><span data-stu-id="9bebc-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="9bebc-195">Se non, probe esito negativo e hello back-end non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="9bebc-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="9bebc-196">certificato Hello fornito in questo passaggio deve essere una chiave pubblica di hello del certificato pfx hello presente nel back-end hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="9bebc-197">Esportare il certificato di hello (non certificato radice hello) installato nel server back-end hello in. CER formattare e utilizzarlo in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="9bebc-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="9bebc-198">Delle whitelist passaggio hello back-end con gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="9bebc-199">Passaggio 8</span><span class="sxs-lookup"><span data-stu-id="9bebc-199">Step 8</span></span>

<span data-ttu-id="9bebc-200">Configurare le impostazioni http back-end di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="9bebc-201">Assegnare il certificato di hello caricato nel precedente passaggio toohello http impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="9bebc-202">Passaggio 9:</span><span class="sxs-lookup"><span data-stu-id="9bebc-202">Step 9</span></span>

<span data-ttu-id="9bebc-203">Creare una regola di routing bilanciamento del carico che configura il comportamento del servizio di bilanciamento carico di hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="9bebc-204">In questo esempio viene creata una regola round robin di base.</span><span class="sxs-lookup"><span data-stu-id="9bebc-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="9bebc-205">Passaggio 10</span><span class="sxs-lookup"><span data-stu-id="9bebc-205">Step 10</span></span>

<span data-ttu-id="9bebc-206">Configurare le dimensioni di istanza hello del gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="9bebc-207">sono di dimensioni disponibili Hello **Standard\_Small**, **Standard\_Media**, e **Standard\_grande**.</span><span class="sxs-lookup"><span data-stu-id="9bebc-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="9bebc-208">Per la capacità, i valori disponibili hello sono 1 e 10.</span><span class="sxs-lookup"><span data-stu-id="9bebc-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="9bebc-209">A scopo di test si può scegliere 1 come numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="9bebc-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="9bebc-210">È importante che tutte le istanze in due istanze di contare tooknow non coperto da hello contratto di servizio e pertanto non sono consigliati.</span><span class="sxs-lookup"><span data-stu-id="9bebc-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="9bebc-211">Gateway di piccole dimensioni sono toobe utilizzato per il test di sviluppo e non per scopi di produzione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="9bebc-212">Passaggio 11</span><span class="sxs-lookup"><span data-stu-id="9bebc-212">Step 11</span></span>

<span data-ttu-id="9bebc-213">Configurare hello SSL criteri toobe utilizzato su hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="9bebc-214">Gateway applicazione supporta hello possibilità tooset una versione minima per le versioni protocollo SSL.</span><span class="sxs-lookup"><span data-stu-id="9bebc-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="9bebc-215">Hello i valori seguenti sono un elenco delle versioni del protocollo che possono essere definiti.</span><span class="sxs-lookup"><span data-stu-id="9bebc-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="9bebc-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="9bebc-216">**TLSv1_0**</span></span>
* <span data-ttu-id="9bebc-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="9bebc-217">**TLSv1_1**</span></span>
* <span data-ttu-id="9bebc-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="9bebc-218">**TLSv1_2**</span></span>

<span data-ttu-id="9bebc-219">Set di hello versione del protocollo minimo troppo**TLSv1_2** ed **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**e **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** solo.</span><span class="sxs-lookup"><span data-stu-id="9bebc-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="9bebc-220">Creare hello Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="9bebc-220">Create hello Application Gateway</span></span>

<span data-ttu-id="9bebc-221">Utilizzando hello tutti i passaggi precedenti, creare hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="9bebc-222">creazione di Hello del gateway hello è un processo a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="9bebc-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="9bebc-223">Limitare le versioni del protocollo SSL in un gateway applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="9bebc-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="9bebc-224">Hello passaggi precedenti consentono di creazione di un'applicazione con tooend fine SSL e la disabilitazione di alcune versioni del protocollo SSL.</span><span class="sxs-lookup"><span data-stu-id="9bebc-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="9bebc-225">Hello seguente disabilita determinati criteri SSL un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="9bebc-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="9bebc-226">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="9bebc-226">Step 1</span></span>

<span data-ttu-id="9bebc-227">Recuperare tooupdate di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="9bebc-228">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="9bebc-228">Step 2</span></span>

<span data-ttu-id="9bebc-229">Definire un criterio SSL.</span><span class="sxs-lookup"><span data-stu-id="9bebc-229">Define an SSL policy.</span></span> <span data-ttu-id="9bebc-230">Nell'esempio seguente di hello, TLSv1.0 e TLSv1.1 sono disattivati e hello pacchetti di crittografia **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, e  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** è hello soli quelli consentiti.</span><span class="sxs-lookup"><span data-stu-id="9bebc-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="9bebc-231">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="9bebc-231">Step 3</span></span>

<span data-ttu-id="9bebc-232">Infine, aggiornare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-232">Finally, update hello gateway.</span></span> <span data-ttu-id="9bebc-233">È importante toonote che quest'ultimo passaggio è un'attività a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="9bebc-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="9bebc-234">Al termine, terminare tooend che SSL configurato nel gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="9bebc-235">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="9bebc-235">Get application gateway DNS name</span></span>

<span data-ttu-id="9bebc-236">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="9bebc-237">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="9bebc-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="9bebc-238">gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9bebc-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="9bebc-239">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9bebc-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="9bebc-240">toodo, dettagli recuperare di gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="9bebc-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="9bebc-241">nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis.</span><span class="sxs-lookup"><span data-stu-id="9bebc-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="9bebc-242">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bebc-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9bebc-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9bebc-243">Next steps</span></span>

<span data-ttu-id="9bebc-244">Informazioni sulla protezione avanzata di sicurezza hello delle applicazioni web con Web Application Firewall tramite il Gateway applicazione visitando [Panoramica del Firewall applicazione Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9bebc-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
