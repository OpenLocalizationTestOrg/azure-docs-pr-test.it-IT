---
title: aaaCreate, avviare o eliminare un gateway applicazione | Documenti Microsoft
description: Questa pagina vengono fornite istruzioni toocreate, configurare, avviare ed eliminare un gateway applicazione Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="1ed3e-103">Creare, avviare o eliminare un gateway applicazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ed3e-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ed3e-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1ed3e-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="1ed3e-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1ed3e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="1ed3e-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="1ed3e-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="1ed3e-107">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1ed3e-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="1ed3e-108">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1ed3e-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="1ed3e-109">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="1ed3e-110">Fornisce il failover, le prestazioni di routing di richieste HTTP tra server diversi, che si trovino in locale o cloud hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="1ed3e-111">Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e molte altre.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="1ed3e-112">toofind un elenco completo delle funzionalità supportate, visitare [Panoramica di Gateway applicazione](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1ed3e-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="1ed3e-113">Questo articolo vengono illustrati toocreate passaggi hello, configurare, avviare ed eliminare un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1ed3e-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="1ed3e-114">Before you begin</span></span>

1. <span data-ttu-id="1ed3e-115">Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="1ed3e-116">È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1ed3e-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="1ed3e-117">Se si dispone di una rete virtuale esistente, selezionare una subnet vuota esistente o creare una nuova subnet nella rete virtuale esistente esclusivamente per l'utilizzo dal gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="1ed3e-118">Non è possibile distribuire hello applicazione gateway tooa rete virtuale diverso rispetto alle risorse di hello intendi toodeploy dietro gateway applicazione hello a meno che non peering reti virtuali viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="1ed3e-119">visitare più toolearn [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1ed3e-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="1ed3e-120">Assicurarsi di avere una rete virtuale funzionante con una subnet valida.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="1ed3e-121">Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="1ed3e-122">gateway applicazione Hello deve essere da solo in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="1ed3e-123">deve esistere server Hello configurare gateway di applicazione hello toouse o disporre i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="1ed3e-124">Che cos'è toocreate necessario un gateway applicazione?</span><span class="sxs-lookup"><span data-stu-id="1ed3e-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="1ed3e-125">Quando si utilizza hello `New-AzureApplicationGateway` gateway di applicazione hello toocreate comando, non è impostata una configurazione a questo punto e risorse hello appena creato sono configurati utilizzando XML o un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="1ed3e-126">i valori Hello sono:</span><span class="sxs-lookup"><span data-stu-id="1ed3e-126">hello values are:</span></span>

* <span data-ttu-id="1ed3e-127">**Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="1ed3e-128">gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="1ed3e-129">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="1ed3e-130">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="1ed3e-131">**Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="1ed3e-132">Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="1ed3e-133">**Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="1ed3e-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="1ed3e-134">**Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="1ed3e-135">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="1ed3e-135">Create an application gateway</span></span>

<span data-ttu-id="1ed3e-136">toocreate un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="1ed3e-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="1ed3e-137">Creare una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="1ed3e-138">Creare un file XML di configurazione o un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="1ed3e-139">Eseguire il commit toohello configurazione hello appena creati risorsa per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="1ed3e-140">Se è necessario tooconfigure un probe personalizzato per il gateway applicazione, vedere [creare un gateway applicazione con probe personalizzati usando PowerShell](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1ed3e-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="1ed3e-141">Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="1ed3e-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Esempio dello scenario][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="1ed3e-143">Creare una risorsa del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="1ed3e-143">Create an application gateway resource</span></span>

<span data-ttu-id="1ed3e-144">gateway hello toocreate, utilizzare hello `New-AzureApplicationGateway` cmdlet, sostituendo i valori hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="1ed3e-145">La fatturazione per il gateway hello non inizia a questo punto.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="1ed3e-146">La fatturazione inizia in un passaggio successivo, quando il gateway hello sia stato avviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="1ed3e-147">Hello esempio seguente viene creato un gateway applicazione tramite una rete virtuale denominata "testvnet1" e una subnet denominata "subnet-1":</span><span class="sxs-lookup"><span data-stu-id="1ed3e-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="1ed3e-148">*Description*, *InstanceCount* e *GatewaySize* sono parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="1ed3e-149">toovalidate che hello gateway è stato creato, è possibile usare hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="1ed3e-150">il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="1ed3e-151">il valore predefinito per Hello *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="1ed3e-152">È possibile scegliere tra Small, Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="1ed3e-153">*Gli IP virtuali* e *DnsName* vengono visualizzati come vuoto perché non è ancora iniziata gateway hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="1ed3e-154">Vengono creati una volta hello gateway si trova in stato di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="1ed3e-155">Configurare gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1ed3e-155">Configure hello application gateway</span></span>

<span data-ttu-id="1ed3e-156">È possibile configurare gateway applicazione hello utilizzando XML o un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="1ed3e-157">Configurazione di gateway applicazione hello tramite XML</span><span class="sxs-lookup"><span data-stu-id="1ed3e-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="1ed3e-158">Nell'esempio seguente di hello, un tooconfigure file XML tutte le impostazioni di gateway applicazione e di eseguirne il commit toohello risorsa per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="1ed3e-159">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="1ed3e-159">Step 1</span></span>

<span data-ttu-id="1ed3e-160">Copiare hello tooNotepad testo seguente.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-160">Copy hello following text tooNotepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="1ed3e-161">Modificare i valori hello tra parentesi hello hello degli elementi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="1ed3e-162">Salvare hello file con estensione XML.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ed3e-163">Hello protocollo Http o Https è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="1ed3e-164">Hello di esempio seguente viene illustrato come una configurazione toouse file tooset di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="1ed3e-165">il caricamento di esempio Hello bilancia il traffico HTTP sulla porta pubblica 80 e invia il traffico di rete porta tooback fine 80 tra due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a><span data-ttu-id="1ed3e-166">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="1ed3e-166">Step 2</span></span>

<span data-ttu-id="1ed3e-167">Quindi, impostare gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-167">Next, set hello application gateway.</span></span> <span data-ttu-id="1ed3e-168">Hello utilizzare `Set-AzureApplicationGatewayConfig` cmdlet con un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="1ed3e-169">Configurazione di gateway applicazione hello utilizzando un oggetto di configurazione</span><span class="sxs-lookup"><span data-stu-id="1ed3e-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="1ed3e-170">Hello di esempio seguente viene illustrato come tooconfigure hello gateway applicazione tramite gli oggetti di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="1ed3e-171">Tutti gli elementi di configurazione devono essere configurati singolarmente e quindi aggiunta oggetto di configurazione di gateway applicazione tooan.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="1ed3e-172">Dopo aver creato l'oggetto di configurazione di hello, utilizzare hello `Set-AzureApplicationGateway` comando toocommit hello configurazione toohello creato in precedenza di risorsa per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="1ed3e-173">Prima di assegnare un oggetto di configurazione tooeach valore, è necessario toodeclare il tipo di oggetto PowerShell utilizza per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="1ed3e-174">Hello prima toocreate hello singole voci definisce le azioni `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="1ed3e-175">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="1ed3e-175">Step 1</span></span>

<span data-ttu-id="1ed3e-176">Creare tutti i singoli elementi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-176">Create all individual configuration items.</span></span>

<span data-ttu-id="1ed3e-177">Creare l'indirizzo IP front-end hello come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="1ed3e-178">Creare la porta front-end di hello come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="1ed3e-179">Creare il pool di server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="1ed3e-180">Definire gli indirizzi IP hello aggiunti toohello pool di server back-end come mostrato nell'esempio riportato di seguito hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="1ed3e-181">Utilizzare hello $server tooadd hello valori toohello pool back-end dell'oggetto ($pool).</span><span class="sxs-lookup"><span data-stu-id="1ed3e-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="1ed3e-182">Creare l'impostazione del pool di server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="1ed3e-183">Creare listener hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="1ed3e-184">Creare una regola di hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="1ed3e-185">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="1ed3e-185">Step 2</span></span>

<span data-ttu-id="1ed3e-186">Assegnare tutti i singoli elementi tooan applicazione gateway configurazione oggetto di configurazione ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="1ed3e-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="1ed3e-187">Aggiungere la configurazione front-end IP toohello hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="1ed3e-188">Aggiunta una configurazione toohello hello porta front-end.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="1ed3e-189">Aggiungi configurazione toohello del pool di server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="1ed3e-190">Aggiungere toohello di configurazione di hello pool back-end.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="1ed3e-191">Aggiungere una configurazione di toohello hello del listener.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="1ed3e-192">Aggiungere hello regola toohello configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="1ed3e-193">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="1ed3e-193">Step 3</span></span>
<span data-ttu-id="1ed3e-194">Eseguire il commit utilizzando risorse di gateway applicazione hello configurazione oggetto toohello `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="1ed3e-195">Avviare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="1ed3e-195">Start hello gateway</span></span>

<span data-ttu-id="1ed3e-196">Una volta configurato il gateway di hello, utilizzare hello `Start-AzureApplicationGateway` gateway hello toostart di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="1ed3e-197">La fatturazione per un gateway applicazione inizia dopo il gateway hello è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="1ed3e-198">Hello `Start-AzureApplicationGateway` cmdlet può richiedere toofinish too15-20 minuti.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="1ed3e-199">Verificare lo stato del gateway hello</span><span class="sxs-lookup"><span data-stu-id="1ed3e-199">Verify hello gateway status</span></span>

<span data-ttu-id="1ed3e-200">Hello utilizzare `Get-AzureApplicationGateway` cmdlet toocheck hello stato gateway hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="1ed3e-201">Se `Start-AzureApplicationGateway` ha avuto esito positivo nel passaggio precedente hello *stato* deve essere in esecuzione, e *Vip* e *DnsName* dovrebbero avere voci valide.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="1ed3e-202">Hello esempio seguente viene illustrato un gateway di applicazione che è in esecuzione e pronto tootake il traffico destinato `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="1ed3e-203">Eliminare il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1ed3e-203">Delete hello application gateway</span></span>

<span data-ttu-id="1ed3e-204">gateway applicazione hello di toodelete:</span><span class="sxs-lookup"><span data-stu-id="1ed3e-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="1ed3e-205">Hello utilizzare `Stop-AzureApplicationGateway` gateway hello toostop di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="1ed3e-206">Hello utilizzare `Remove-AzureApplicationGateway` gateway hello tooremove di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="1ed3e-207">Verificare che gateway hello è stato rimosso utilizzando hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="1ed3e-208">Hello riportato di seguito hello `Stop-AzureApplicationGateway` cmdlet hello della prima riga, seguito dall'output di hello.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="1ed3e-209">Una volta gateway applicazione hello in stato di interruzione, utilizzare hello `Remove-AzureApplicationGateway` servizio hello tooremove di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="1ed3e-210">tooverify che hello servizio è stato rimosso, è possibile usare hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="1ed3e-211">Questo passaggio non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1ed3e-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="1ed3e-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1ed3e-212">Next steps</span></span>

<span data-ttu-id="1ed3e-213">Se si desidera tooconfigure offload SSL, vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="1ed3e-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="1ed3e-214">Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno, vedere [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="1ed3e-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="1ed3e-215">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="1ed3e-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="1ed3e-216">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="1ed3e-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="1ed3e-217">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="1ed3e-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
