---
title: aaaHow toouse gestione API di Azure nella rete virtuale con Gateway applicazione | Documenti Microsoft
description: Informazioni su come toosetup e configurare Gestione API di Azure in rete virtuale interna con applicazioni Gateway (WAF) come front-end
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="c76cc-103">Integrare Gestione API in una rete virtuale interna con un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c76cc-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="c76cc-104"><a name="overview"></a> Panoramica</span><span class="sxs-lookup"><span data-stu-id="c76cc-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="c76cc-105">Hello servizio Gestione API può essere configurato in una rete virtuale in modalità interna che rende accessibile solo dall'interno hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c76cc-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="c76cc-106">Il gateway applicazione di Azure è un servizio PAAS con bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="c76cc-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="c76cc-107">Funge da servizio proxy inverso e offre anche un Web application firewall (WAF).</span><span class="sxs-lookup"><span data-stu-id="c76cc-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="c76cc-108">La combinazione di gestione API, il provisioning in una rete virtuale interna con front-end di Gateway applicazione hello consente hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="c76cc-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="c76cc-109">Utilizzare hello stessa risorsa di gestione API per l'utilizzo dal consumer interno sia utenti esterni.</span><span class="sxs-lookup"><span data-stu-id="c76cc-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="c76cc-110">Uso di una singola risorsa di Gestione API e disponibilità di un sottoinsieme di API definite in Gestione API per gli utenti esterni.</span><span class="sxs-lookup"><span data-stu-id="c76cc-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="c76cc-111">Fornire un tooAPI di accesso di tooswitch Gestione chiavi in modo da hello rete Internet pubblica e disattivare.</span><span class="sxs-lookup"><span data-stu-id="c76cc-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="c76cc-112"><a name="scenario"> </a> Scenario</span><span class="sxs-lookup"><span data-stu-id="c76cc-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="c76cc-113">In questo articolo verrà coprire come toouse un singolo Management API del servizio per i consumer interni ed esterni e consentono di agire come un singolo server front-end per entrambi locale e le API del cloud.</span><span class="sxs-lookup"><span data-stu-id="c76cc-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="c76cc-114">Verrà visualizzato anche come tooexpose solo un subset delle API (nell'esempio hello vengono evidenziati in verde) per l'utilizzo esterno utilizzando hello PathBasedRouting funzionalità disponibili in Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="c76cc-115">Nel primo esempio il programma di installazione di hello tutte le API vengono gestite solo dall'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c76cc-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="c76cc-116">Gli utenti interni (evidenziati in arancione) possono accedere a tutte le API interne ed esterne.</span><span class="sxs-lookup"><span data-stu-id="c76cc-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="c76cc-117">Il traffico non viene mai salvato tooInternet che viene recapitato un ad alte prestazioni tramite circuiti Expressroute.</span><span class="sxs-lookup"><span data-stu-id="c76cc-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![route dell'URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="c76cc-119"><a name="before-you-begin"></a> Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c76cc-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="c76cc-120">Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="c76cc-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="c76cc-121">È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c76cc-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="c76cc-122">Creare una rete virtuale e subnet separate per Gestione API e il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="c76cc-123">Se si prevede un server DNS personalizzato per la rete virtuale hello toocreate, è possibile farlo prima di avviare la distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="c76cc-124">Verificare che funziona garantendo una macchina virtuale creata in una nuova subnet nella rete virtuale hello può risolvere e accedere a tutti gli endpoint di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="c76cc-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="c76cc-125">Che cos'è obbligatorio toocreate un'integrazione tra gestione API e di Gateway applicazione?</span><span class="sxs-lookup"><span data-stu-id="c76cc-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="c76cc-126">**Pool di server back-end:** tratta hello interno indirizzo IP virtuale del servizio Gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="c76cc-127">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="c76cc-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="c76cc-128">Queste impostazioni sono applicate tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="c76cc-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="c76cc-129">**Porta front-end:** porta pubblica di hello che viene aperta su gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="c76cc-130">Traffico raggiungimento di si ottiene tooone reindirizzato di hello server back-end.</span><span class="sxs-lookup"><span data-stu-id="c76cc-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="c76cc-131">**Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="c76cc-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="c76cc-132">**Regola:** regola hello associa un pool di server back-end tooa listener.</span><span class="sxs-lookup"><span data-stu-id="c76cc-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="c76cc-133">**Probe di integrità personalizzato:** Gateway applicazione, per impostazione predefinita, utilizza IP indirizzo basato su probe toofigure out server hello BackendAddressPool sono attivi.</span><span class="sxs-lookup"><span data-stu-id="c76cc-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="c76cc-134">Servizio gestione API Hello risponde solo toorequests che presenta l'intestazione host corretto hello, pertanto probe predefiniti hello avere esito negativo.</span><span class="sxs-lookup"><span data-stu-id="c76cc-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="c76cc-135">Un probe di integrità personalizzato deve toobe definito gateway applicazione toohelp determinare che il servizio hello è attivo e inoltra le richieste.</span><span class="sxs-lookup"><span data-stu-id="c76cc-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="c76cc-136">**Certificato di dominio personalizzato:** tooaccess gestione API da hello internet è necessario toocreate un mapping CNAME del nome host toohello Gateway applicazione front-end nome DNS.</span><span class="sxs-lookup"><span data-stu-id="c76cc-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="c76cc-137">Questo assicura che hello hostname intestazione e il certificato inviato tooApplication Gateway inoltrati tooAPI gestione sia uno in grado di riconoscere ruoli come valido.</span><span class="sxs-lookup"><span data-stu-id="c76cc-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="c76cc-138"><a name="overview-steps"> </a> Passaggi necessari per l'integrazione di Gestione API e il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c76cc-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="c76cc-139">Creare un gruppo di risorse per Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="c76cc-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="c76cc-140">Creare una rete virtuale, subnet e l'indirizzo IP pubblico per hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="c76cc-141">Creare un'altra subnet per Gestione API.</span><span class="sxs-lookup"><span data-stu-id="c76cc-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="c76cc-142">Creare un servizio di gestione API in subnet di rete virtuale hello creato in precedenza e accertarsi di utilizzare la modalità interna hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="c76cc-143">Nome di dominio personalizzato hello in hello servizio Gestione API del programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="c76cc-144">Creare un oggetto di configurazione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="c76cc-145">Creare una risorsa gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="c76cc-146">Creare un record CNAME dal nome DNS pubblico hello nomehost hello Gateway applicazione toohello gestione API proxy.</span><span class="sxs-lookup"><span data-stu-id="c76cc-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="c76cc-147">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="c76cc-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="c76cc-148">Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c76cc-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="c76cc-149">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c76cc-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="c76cc-150">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="c76cc-150">Step 1</span></span>

<span data-ttu-id="c76cc-151">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="c76cc-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="c76cc-152">Eseguire l'autenticazione con le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="c76cc-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="c76cc-153">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="c76cc-153">Step 2</span></span>

<span data-ttu-id="c76cc-154">Controllare le sottoscrizioni di hello per account hello e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="c76cc-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="c76cc-155">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="c76cc-155">Step 3</span></span>

<span data-ttu-id="c76cc-156">Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="c76cc-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="c76cc-157">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="c76cc-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="c76cc-158">Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c76cc-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="c76cc-159">Assicurarsi che tutti i comandi toocreate un hello di uso di gateway applicazione stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c76cc-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="c76cc-160">Creare una rete virtuale e una subnet per il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="c76cc-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="c76cc-161">Hello di esempio seguente viene illustrato come una rete virtuale utilizzando toocreate hello Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="c76cc-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="c76cc-162">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="c76cc-162">Step 1</span></span>

<span data-ttu-id="c76cc-163">Assegnare hello indirizzo intervallo 10.0.0.0/24 toohello subnet variabile toobe utilizzato per il Gateway applicazione durante la creazione di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c76cc-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="c76cc-164">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="c76cc-164">Step 2</span></span>

<span data-ttu-id="c76cc-165">Assegnare hello indirizzo intervallo 10.0.1.0/24 toohello subnet variabile toobe utilizzato per l'API di gestione durante la creazione di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c76cc-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="c76cc-166">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="c76cc-166">Step 3</span></span>

<span data-ttu-id="c76cc-167">Creare una rete virtuale denominata **appgwvnet** nel gruppo di risorse **ruoli-appGw-RG** per area Stati Uniti occidentali hello utilizzando hello prefisso 10.0.0.0/16 con subnet 10.0.0.0/24 e 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="c76cc-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="c76cc-168">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="c76cc-168">Step 4</span></span>

<span data-ttu-id="c76cc-169">Assegnare una variabile di subnet per i passaggi successivi hello</span><span class="sxs-lookup"><span data-stu-id="c76cc-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="c76cc-170">Creare un servizio Gestione API in una rete virtuale configurata in modalità interna</span><span class="sxs-lookup"><span data-stu-id="c76cc-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="c76cc-171">Hello esempio seguente viene illustrato come toocreate un servizio di gestione API in una rete virtuale configurato per il solo accesso interno.</span><span class="sxs-lookup"><span data-stu-id="c76cc-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="c76cc-172">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="c76cc-172">Step 1</span></span>
<span data-ttu-id="c76cc-173">Creare un oggetto di rete virtuale di gestione API mediante subnet hello $apimsubnetdata creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c76cc-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="c76cc-174">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="c76cc-174">Step 2</span></span>
<span data-ttu-id="c76cc-175">Creare un servizio di gestione API all'interno di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c76cc-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="c76cc-176">Dopo hello sopra comando ha esito positivo, consultare troppo[necessaria una configurazione DNS del servizio Gestione API di rete virtuale interno tooaccess](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess è.</span><span class="sxs-lookup"><span data-stu-id="c76cc-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="c76cc-177">Configurare un nome di dominio personalizzato in Gestione API</span><span class="sxs-lookup"><span data-stu-id="c76cc-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="c76cc-178">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="c76cc-178">Step 1</span></span>
<span data-ttu-id="c76cc-179">Caricare il certificato di hello con la chiave privata per il dominio hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="c76cc-180">Per questo esempio sarà `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="c76cc-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="c76cc-181">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="c76cc-181">Step 2</span></span>
<span data-ttu-id="c76cc-182">Una volta caricato il certificato di hello, creare un oggetto di configurazione di nome host per il proxy di hello con un nome host di `api.contoso.net`, come certificato di esempio hello fornisce autorità per hello `*.contoso.net` dominio.</span><span class="sxs-lookup"><span data-stu-id="c76cc-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="c76cc-183">Creare un indirizzo IP pubblico per la configurazione front-end hello</span><span class="sxs-lookup"><span data-stu-id="c76cc-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="c76cc-184">Creare una risorsa IP pubblica **publicIP01** nel gruppo di risorse **ruoli-appGw-RG** per area Stati Uniti occidentali hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="c76cc-185">Viene assegnato a un indirizzo IP gateway applicazione toohello all'avvio del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="c76cc-186">Creare la configurazione del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c76cc-186">Create application gateway configuration</span></span>

<span data-ttu-id="c76cc-187">Tutti gli elementi di configurazione necessario impostare prima di creare i gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="c76cc-188">Hello seguenti passaggi necessari per creare hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="c76cc-189">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="c76cc-189">Step 1</span></span>

<span data-ttu-id="c76cc-190">Creare una configurazione IP del gateway applicazione denominata **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="c76cc-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="c76cc-191">Avvio di Gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="c76cc-192">Tenere presente che ogni istanza ha un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="c76cc-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="c76cc-193">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="c76cc-193">Step 2</span></span>

<span data-ttu-id="c76cc-194">Configurare una porta IP front-end di hello per endpoint IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="c76cc-195">Questa porta è porta hello in grado di connettersi agli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="c76cc-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="c76cc-196">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="c76cc-196">Step 3</span></span>

<span data-ttu-id="c76cc-197">Configurazione IP front-end hello con endpoint IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="c76cc-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="c76cc-198">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="c76cc-198">Step 4</span></span>

<span data-ttu-id="c76cc-199">Configurare il certificato di hello per Gateway di applicazione, hello utilizzato toodecrypt e crittografa nuovamente traffico hello passano attraverso.</span><span class="sxs-lookup"><span data-stu-id="c76cc-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="c76cc-200">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="c76cc-200">Step 5</span></span>

<span data-ttu-id="c76cc-201">Creare il listener HTTP hello per hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="c76cc-202">Assegnare una configurazione IP front-end hello, porta e tooit certificato ssl.</span><span class="sxs-lookup"><span data-stu-id="c76cc-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="c76cc-203">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="c76cc-203">Step 6</span></span>

<span data-ttu-id="c76cc-204">Creare un servizio di gestione API di toohello probe personalizzato `ContosoApi` endpoint proxy per dominio.</span><span class="sxs-lookup"><span data-stu-id="c76cc-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="c76cc-205">percorso Hello `/status-0123456789abcdef` è ospitato in tutti i servizi di gestione API hello un endpoint di integrità predefinito.</span><span class="sxs-lookup"><span data-stu-id="c76cc-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="c76cc-206">Impostare `api.contoso.net` come un toosecure nome host di tipo probe personalizzato con certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="c76cc-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="c76cc-207">Hello hostname `contosoapi.azure-api.net` nome host di proxy predefinito hello configurato quando un servizio denominato `contosoapi` creato in Azure pubblica.</span><span class="sxs-lookup"><span data-stu-id="c76cc-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="c76cc-208">Passaggio 7</span><span class="sxs-lookup"><span data-stu-id="c76cc-208">Step 7</span></span>

<span data-ttu-id="c76cc-209">Caricare il certificato di hello toobe utilizzato per le risorse di pool di hello SSL abilitato back-end.</span><span class="sxs-lookup"><span data-stu-id="c76cc-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="c76cc-210">Si tratta di hello stesso certificato che è fornito nel passaggio 4 precedente.</span><span class="sxs-lookup"><span data-stu-id="c76cc-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="c76cc-211">Passaggio 8</span><span class="sxs-lookup"><span data-stu-id="c76cc-211">Step 8</span></span>

<span data-ttu-id="c76cc-212">Configurare le impostazioni HTTP back-end hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="c76cc-213">Questo passaggio include l'impostazione di un limite di timeout per la richiesta del back-end, raggiunto il quale verrà annullata.</span><span class="sxs-lookup"><span data-stu-id="c76cc-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="c76cc-214">Questo valore è diverso dal timeout probe hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="c76cc-215">Passaggio 9:</span><span class="sxs-lookup"><span data-stu-id="c76cc-215">Step 9</span></span>

<span data-ttu-id="c76cc-216">Configurare un pool di indirizzi IP back-end denominato **apimbackend** con indirizzo IP virtuale interno hello indirizzo del servizio Gestione API hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c76cc-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="c76cc-217">Passaggio 10</span><span class="sxs-lookup"><span data-stu-id="c76cc-217">Step 10</span></span>

<span data-ttu-id="c76cc-218">Creare le impostazioni per un back-end fittizio (inesistente).</span><span class="sxs-lookup"><span data-stu-id="c76cc-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="c76cc-219">I percorsi di tooAPI di richieste che non si desidera tooexpose da Gestione API tramite il Gateway applicazione verranno raggiunto questo back-end e restituire l'errore 404.</span><span class="sxs-lookup"><span data-stu-id="c76cc-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="c76cc-220">Configurare le impostazioni HTTP back-end fittizio di hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="c76cc-221">Configurare un back-end fittizio **dummyBackendPool**, vale a dire indirizzo FQDN tooa **dummybackend.com**. Questo indirizzo FQDN non esiste nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="c76cc-222">Creare una regola di impostazione che hello Gateway applicazione utilizzerà per impostazione predefinita che punta back-end inesistente toohello **dummybackend.com** in hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c76cc-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="c76cc-223">Passaggio 11</span><span class="sxs-lookup"><span data-stu-id="c76cc-223">Step 11</span></span>

<span data-ttu-id="c76cc-224">Configurare i percorsi di regola di URL per il pool di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="c76cc-225">In questo modo selezionando solo alcune delle hello le API di gestione API per essere esposte toohello pubblico.</span><span class="sxs-lookup"><span data-stu-id="c76cc-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="c76cc-226">Ad esempio, se esistono `Echo API` (/echo/), `Calculator API` (/calc/) e così via, è possibile rendere accessibile da Internet solo `Echo API`.</span><span class="sxs-lookup"><span data-stu-id="c76cc-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="c76cc-227">Hello esempio seguente viene creata una semplice regola per hello "echo /" percorso routing del traffico toohello back-end "apimProxyBackendPool".</span><span class="sxs-lookup"><span data-stu-id="c76cc-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="c76cc-228">Se non corrisponde a percorso hello percorso hello regole desideriamo tooenable dalla gestione API, regola hello configurazione mappa percorso consente di configurare anche un pool di indirizzi back-end di predefinito denominato **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="c76cc-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="c76cc-229">Ad esempio, http://api.contoso.net/calc/ * diventa troppo**dummyBackendPool** con cui è definito come il pool predefinito hello per il traffico senza corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="c76cc-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="c76cc-230">Hello sopra passaggio garantisce che solo le richieste per il percorso di hello "/ echo" siano consentiti attraverso il Gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="c76cc-231">Tooother richieste che API configurate in Gestione API genererà 404 errori dal Gateway applicazione quando si accede da hello Internet.</span><span class="sxs-lookup"><span data-stu-id="c76cc-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="c76cc-232">Passaggio 12</span><span class="sxs-lookup"><span data-stu-id="c76cc-232">Step 12</span></span>

<span data-ttu-id="c76cc-233">Creare un'impostazione di regole per hello Gateway applicazione toouse basato sul percorso routing degli URL.</span><span class="sxs-lookup"><span data-stu-id="c76cc-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="c76cc-234">Passaggio 13</span><span class="sxs-lookup"><span data-stu-id="c76cc-234">Step 13</span></span>

<span data-ttu-id="c76cc-235">Configurare hello numero di istanze e le dimensioni per hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="c76cc-236">Qui utilizziamo hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) per aumentare la protezione di hello risorse di gestione API.</span><span class="sxs-lookup"><span data-stu-id="c76cc-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="c76cc-237">Passaggio 14</span><span class="sxs-lookup"><span data-stu-id="c76cc-237">Step 14</span></span>

<span data-ttu-id="c76cc-238">Configurare WAF toobe in modalità "Programmi".</span><span class="sxs-lookup"><span data-stu-id="c76cc-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="c76cc-239">Creare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c76cc-239">Create Application Gateway</span></span>

<span data-ttu-id="c76cc-240">Creare un Gateway applicazione con tutti gli oggetti di configurazione hello da hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="c76cc-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="c76cc-241">CNAME hello gestione API proxy hostname toohello nome DNS pubblico del hello risorse Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c76cc-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="c76cc-242">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="c76cc-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="c76cc-243">Quando si utilizza un indirizzo IP pubblico, Gateway applicazione richiede un nome DNS assegnato dinamicamente, che potrebbe non essere toouse semplice.</span><span class="sxs-lookup"><span data-stu-id="c76cc-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="c76cc-244">Hello nome DNS del Gateway applicazione deve essere utilizzato toocreate un record CNAME che punta nome host di hello ruoli proxy (ad esempio `api.contoso.net` negli esempi di hello sopra) toothis il nome DNS.</span><span class="sxs-lookup"><span data-stu-id="c76cc-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="c76cc-245">front-end hello tooconfigure record CNAME IP, recuperare i dettagli di hello di Gateway applicazione hello e il relativo nome IP/DNS associato utilizzando l'elemento PublicIPAddress hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="c76cc-246">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway.</span><span class="sxs-lookup"><span data-stu-id="c76cc-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="c76cc-247"><a name="summary"></a> Riepilogo</span><span class="sxs-lookup"><span data-stu-id="c76cc-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="c76cc-248">Gestione API di Azure configurato in una rete virtuale fornisce un'interfaccia di gateway singolo per tutte le API configurate, se sono ospitati in locale o nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="c76cc-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="c76cc-249">L'integrazione di Gateway applicazione con l'API di gestione offre la flessibilità di hello di attivazione selettiva particolare toobe di API accessibile su Internet hello, nonché di fornire un Firewall applicazione Web come un'istanza di gestione API tooyour front-end.</span><span class="sxs-lookup"><span data-stu-id="c76cc-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="c76cc-250"><a name="next-steps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c76cc-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="c76cc-251">Altre informazioni sul gateway applicazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c76cc-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="c76cc-252">Panoramica del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c76cc-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="c76cc-253">Web application firewall del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c76cc-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="c76cc-254">Creare un gateway applicazione con il routing basato sul percorso</span><span class="sxs-lookup"><span data-stu-id="c76cc-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="c76cc-255">Altre informazioni su Gestione API e reti virtuali</span><span class="sxs-lookup"><span data-stu-id="c76cc-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="c76cc-256">Utilizzo di gestione API disponibile solo all'interno di hello rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c76cc-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="c76cc-257">Usare Gestione API in una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c76cc-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
