---
title: Gateway applicazione Azure con bilanciamento del carico interno aaaUsing | Documenti Microsoft
description: Questa pagina fornisce istruzioni tooconfigure un Gateway applicazione Azure con un endpoint con bilanciamento del carico interno
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="9843a-103">Creare un gateway applicazione con un dispositivo di bilanciamento del carico interno (ILB)</span><span class="sxs-lookup"><span data-stu-id="9843a-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9843a-104">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="9843a-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="9843a-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9843a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="9843a-106">Gateway applicazione può essere configurato con un indirizzo IP virtuale è connessa a internet o con toohello un endpoint interno non è esposta internet, noto anche come endpoint di servizio di bilanciamento di carico interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="9843a-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="9843a-107">Configurazione di gateway hello con un bilanciamento del carico interno è utile per applicazioni line-of-business interne non esposte toointernet.</span><span class="sxs-lookup"><span data-stu-id="9843a-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="9843a-108">È inoltre utile per i servizi o livelli all'interno di un'applicazione multilivello, che si trova in un toointernet limite non esposti di sicurezza, ma ancora richiede la distribuzione del carico round robin, aderenza sessione o la terminazione SSL.</span><span class="sxs-lookup"><span data-stu-id="9843a-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="9843a-109">In questo articolo illustra i passaggi di hello tooconfigure un gateway applicazione con un bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="9843a-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9843a-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="9843a-110">Before you begin</span></span>

1. <span data-ttu-id="9843a-111">Installare la versione più recente dei cmdlet di Azure PowerShell hello utilizzando hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="9843a-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="9843a-112">È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di Download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9843a-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9843a-113">Assicurarsi di avere una rete virtuale funzionante con una subnet valida.</span><span class="sxs-lookup"><span data-stu-id="9843a-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="9843a-114">Verificare di disporre di server back-end nella rete virtuale hello o con un indirizzo IP/VIP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="9843a-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="9843a-115">toocreate un gateway di applicazione, eseguire hello seguendo i passaggi nell'ordine di hello elencati.</span><span class="sxs-lookup"><span data-stu-id="9843a-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="9843a-116">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="9843a-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="9843a-117">Configurare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="9843a-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="9843a-118">Configurazione del gateway hello set</span><span class="sxs-lookup"><span data-stu-id="9843a-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="9843a-119">Avviare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="9843a-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="9843a-120">Verificare i gateway hello</span><span class="sxs-lookup"><span data-stu-id="9843a-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="9843a-121">Creare un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="9843a-121">Create an application gateway:</span></span>

<span data-ttu-id="9843a-122">**gateway hello toocreate**, utilizzare hello `New-AzureApplicationGateway` cmdlet, sostituendo i valori hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="9843a-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="9843a-123">Si noti che la fatturazione per il gateway hello non viene avviato a questo punto.</span><span class="sxs-lookup"><span data-stu-id="9843a-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="9843a-124">La fatturazione inizia in un passaggio successivo, quando il gateway hello sia stato avviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="9843a-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="9843a-125">**toovalidate** che gateway hello è stato creato, è possibile usare hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9843a-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="9843a-126">Nell'esempio hello *descrizione*, *InstanceCount*, e *GatewaySize* sono parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="9843a-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="9843a-127">il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10.</span><span class="sxs-lookup"><span data-stu-id="9843a-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="9843a-128">il valore predefinito per Hello *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="9843a-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="9843a-129">Small e Large sono altri valori disponibili.</span><span class="sxs-lookup"><span data-stu-id="9843a-129">Small and Large are other available values.</span></span> <span data-ttu-id="9843a-130">*VIP* e *DnsName* vengono visualizzati come vuoto perché non è ancora iniziata gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9843a-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="9843a-131">Vengono creati una volta hello gateway si trova in stato di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="9843a-131">These are created once hello gateway is in hello running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a><span data-ttu-id="9843a-132">Configurare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="9843a-132">Configure hello gateway</span></span>
<span data-ttu-id="9843a-133">La configurazione di un gateway applicazione è costituita da più valori.</span><span class="sxs-lookup"><span data-stu-id="9843a-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="9843a-134">possono essere associati i valori Hello configurazione hello tooconstruct insieme.</span><span class="sxs-lookup"><span data-stu-id="9843a-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="9843a-135">i valori Hello sono:</span><span class="sxs-lookup"><span data-stu-id="9843a-135">hello values are:</span></span>

* <span data-ttu-id="9843a-136">**Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="9843a-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="9843a-137">gli indirizzi IP Hello elencati devono appartenere toohello subnet di rete virtuale oppure devono essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="9843a-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="9843a-138">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni come porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="9843a-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9843a-139">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="9843a-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="9843a-140">**Porta front-end:** questa porta è aperta nel gateway applicazione hello la porta pubblica hello.</span><span class="sxs-lookup"><span data-stu-id="9843a-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="9843a-141">Traffico raggiunge questa porta e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="9843a-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="9843a-142">**Listener:** listener hello dispone di una porta di front-end, un protocollo (Http o Https, si tratta tra maiuscole e minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="9843a-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="9843a-143">**Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="9843a-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="9843a-144">Attualmente, solo hello *base* regola supportata.</span><span class="sxs-lookup"><span data-stu-id="9843a-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="9843a-145">Hello *base* regola è una distribuzione del carico round robin.</span><span class="sxs-lookup"><span data-stu-id="9843a-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="9843a-146">È possibile definire la configurazione creando un oggetto di configurazione oppure usando un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9843a-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="9843a-147">tooconstruct la configurazione utilizzando un file XML di configurazione, utilizzare hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="9843a-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="9843a-148">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="9843a-148">Note hello following:</span></span>

* <span data-ttu-id="9843a-149">Hello *Frontendipconfiguration* elemento descrive i dettagli di bilanciamento del carico interno hello rilevanti per la configurazione di Gateway applicazione con un bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="9843a-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="9843a-150">IP di front-end Hello *tipo* deve essere impostato too'Private'</span><span class="sxs-lookup"><span data-stu-id="9843a-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="9843a-151">Hello *StaticIPAddress* deve essere impostato su quale hello gateway riceve il traffico di indirizzo IP interno toohello desiderato.</span><span class="sxs-lookup"><span data-stu-id="9843a-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="9843a-152">Si noti che hello *StaticIPAddress* elemento è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="9843a-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="9843a-153">Se non impostato, viene scelto un indirizzo IP interno disponibili dalla subnet hello distribuito.</span><span class="sxs-lookup"><span data-stu-id="9843a-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="9843a-154">valore di hello Hello *nome* specificato nell'elemento *FrontendIPConfiguration* deve essere utilizzato in HTTPListener hello *FrontendIP* toohello toorefer elemento FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="9843a-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="9843a-155">**Esempio di file XML di configurazione**</span><span class="sxs-lookup"><span data-stu-id="9843a-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="9843a-156">Configurazione del gateway hello set</span><span class="sxs-lookup"><span data-stu-id="9843a-156">Set hello gateway configuration</span></span>
<span data-ttu-id="9843a-157">Successivamente, impostare gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9843a-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="9843a-158">È possibile utilizzare hello `Set-AzureApplicationGatewayConfig` cmdlet con un oggetto di configurazione o con un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9843a-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a><span data-ttu-id="9843a-159">Avviare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="9843a-159">Start hello gateway</span></span>

<span data-ttu-id="9843a-160">Una volta configurato il gateway di hello, utilizzare hello `Start-AzureApplicationGateway` gateway hello toostart di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9843a-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="9843a-161">La fatturazione per un gateway applicazione inizia dopo il gateway hello è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="9843a-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="9843a-162">Hello `Start-AzureApplicationGateway` cmdlet può richiedere toocomplete too15-20 minuti.</span><span class="sxs-lookup"><span data-stu-id="9843a-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="9843a-163">Verificare lo stato del gateway hello</span><span class="sxs-lookup"><span data-stu-id="9843a-163">Verify hello gateway status</span></span>

<span data-ttu-id="9843a-164">Hello utilizzare `Get-AzureApplicationGateway` stato hello toocheck di cmdlet del gateway.</span><span class="sxs-lookup"><span data-stu-id="9843a-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="9843a-165">Se `Start-AzureApplicationGateway` ha avuto esito positivo nel passaggio precedente hello, deve essere stato hello *esecuzione*, hello Vip e DnsName dovrebbe avere voci valide.</span><span class="sxs-lookup"><span data-stu-id="9843a-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="9843a-166">In questo esempio viene illustrato il cmdlet hello hello della prima riga, seguito dall'output di hello.</span><span class="sxs-lookup"><span data-stu-id="9843a-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="9843a-167">In questo esempio, hello gateway è in esecuzione e di traffico tootake pronto.</span><span class="sxs-lookup"><span data-stu-id="9843a-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="9843a-168">gateway applicazione Hello è configurato il traffico tooaccept hello configurato l'endpoint di bilanciamento del carico interno 10.0.0.10 in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="9843a-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="9843a-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9843a-169">Next steps</span></span>
<span data-ttu-id="9843a-170">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="9843a-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="9843a-171">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="9843a-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="9843a-172">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="9843a-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

