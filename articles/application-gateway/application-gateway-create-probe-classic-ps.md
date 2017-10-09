---
title: un classico PowerShell probe personalizzato - Gateway applicazione Azure - aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate personalizzato probe per il Gateway applicazione usando PowerShell in modello di distribuzione classica hello
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="c3042-103">Creare un probe personalizzato per il gateway applicazione di Azure (classico) con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3042-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3042-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c3042-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="c3042-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c3042-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="c3042-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="c3042-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="c3042-107">In questo articolo aggiungere un gateway di applicazione esistente probe personalizzato tooan con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3042-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="c3042-108">Probe personalizzati sono utili per le applicazioni che dispone di una pagina di controllo di integrità specifico o per le applicazioni che non forniscono una risposta corretta in un'applicazione web predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="c3042-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3042-109">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c3042-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c3042-110">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="c3042-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c3042-111">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="c3042-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c3042-112">Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c3042-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="c3042-113">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c3042-113">Create an application gateway</span></span>

<span data-ttu-id="c3042-114">toocreate un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="c3042-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="c3042-115">Creare una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3042-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="c3042-116">Creare un file XML di configurazione o un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c3042-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="c3042-117">Eseguire il commit toohello configurazione hello appena creati risorsa per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3042-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="c3042-118">Creare una risorsa del gateway applicazione con un probe personalizzato</span><span class="sxs-lookup"><span data-stu-id="c3042-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="c3042-119">gateway hello toocreate, utilizzare hello `New-AzureApplicationGateway` cmdlet, sostituendo i valori hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="c3042-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="c3042-120">La fatturazione per il gateway hello non inizia a questo punto.</span><span class="sxs-lookup"><span data-stu-id="c3042-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="c3042-121">La fatturazione inizia in un passaggio successivo, quando il gateway hello sia stato avviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c3042-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="c3042-122">Hello seguente viene creato un gateway applicazione tramite una rete virtuale denominata "testvnet1" e una subnet denominata "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="c3042-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="c3042-123">toovalidate che hello gateway è stato creato, è possibile usare hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c3042-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="c3042-124">il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10.</span><span class="sxs-lookup"><span data-stu-id="c3042-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="c3042-125">il valore predefinito per Hello *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="c3042-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="c3042-126">È possibile scegliere tra Small, Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="c3042-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="c3042-127">*Gli IP virtuali* e *DnsName* vengono visualizzati come vuoto perché non è ancora iniziata gateway hello.</span><span class="sxs-lookup"><span data-stu-id="c3042-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="c3042-128">Questi valori vengono creati una volta hello gateway si trova in stato di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="c3042-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="c3042-129">Configurare un gateway applicazione usando XML</span><span class="sxs-lookup"><span data-stu-id="c3042-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="c3042-130">Nell'esempio seguente di hello, un tooconfigure file XML tutte le impostazioni di gateway applicazione e di eseguirne il commit toohello risorsa per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3042-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="c3042-131">Copiare hello tooNotepad testo seguente.</span><span class="sxs-lookup"><span data-stu-id="c3042-131">Copy hello following text tooNotepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="c3042-132">Modificare i valori hello tra parentesi hello hello degli elementi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c3042-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="c3042-133">Salvare hello file con estensione XML.</span><span class="sxs-lookup"><span data-stu-id="c3042-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="c3042-134">Hello seguente viene illustrato come un tooset di file di configurazione di tooload di gateway applicazione hello toouse bilanciare il traffico HTTP sulla porta pubblica 80 e inviare il traffico di rete porta tooback fine 80 tra due indirizzi IP utilizzando un probe personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c3042-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3042-135">Hello protocollo Http o Https è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="c3042-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="c3042-136">Un nuovo elemento di configurazione \<Probe\> viene aggiunto probe personalizzato tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c3042-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="c3042-137">parametri di configurazione di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="c3042-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="c3042-138">.</span><span class="sxs-lookup"><span data-stu-id="c3042-138">Parameter</span></span>|<span data-ttu-id="c3042-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c3042-139">Description</span></span>|
|---|---|
|<span data-ttu-id="c3042-140">**Nome**</span><span class="sxs-lookup"><span data-stu-id="c3042-140">**Name**</span></span> |<span data-ttu-id="c3042-141">Nome di riferimento del probe personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c3042-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="c3042-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="c3042-142">* **Protocol**</span></span> | <span data-ttu-id="c3042-143">Protocollo usato. I valori possibili sono HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c3042-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="c3042-144">**Host** e **Path**</span><span class="sxs-lookup"><span data-stu-id="c3042-144">**Host** and **Path**</span></span> | <span data-ttu-id="c3042-145">Percorso URL completo che viene richiamato dall'integrità hello applicazione gateway toodetermine hello dell'istanza di hello.</span><span class="sxs-lookup"><span data-stu-id="c3042-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="c3042-146">Ad esempio, se si dispone di http://contoso.com/ un sito Web, quindi probe personalizzato hello può essere configurate per "http://contoso.com/path/custompath.htm" per il probe controlla toohave una risposta HTTP ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="c3042-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="c3042-147">**Interval**</span><span class="sxs-lookup"><span data-stu-id="c3042-147">**Interval**</span></span> | <span data-ttu-id="c3042-148">Consente di configurare i controlli di intervallo di probe hello in secondi.</span><span class="sxs-lookup"><span data-stu-id="c3042-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="c3042-149">**Timeout**</span><span class="sxs-lookup"><span data-stu-id="c3042-149">**Timeout**</span></span> | <span data-ttu-id="c3042-150">Definisce il periodo di timeout di hello probe per un controllo della risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3042-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="c3042-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="c3042-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="c3042-152">Hello numero di risposte HTTP non riuscite necessari tooflag hello back-end dell'istanza come *integro*.</span><span class="sxs-lookup"><span data-stu-id="c3042-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="c3042-153">nome di probe Hello viene fatto riferimento in hello \<BackendHttpSettings\> tooassign configurazione quale pool back-end Usa le impostazioni di tipo probe personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c3042-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="c3042-154">Aggiungere un gateway di applicazione esistente tooan probe personalizzato</span><span class="sxs-lookup"><span data-stu-id="c3042-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="c3042-155">La modifica della configurazione corrente hello di un gateway applicazione sono necessari tre passaggi: ottenere i file di configurazione XML corrente hello, modificare toohave un probe personalizzato e configurare gateway applicazione hello con le nuove impostazioni XML hello.</span><span class="sxs-lookup"><span data-stu-id="c3042-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="c3042-156">Ottenere i file XML di hello utilizzando `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="c3042-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="c3042-157">Questo toobe XML di configurazione di cmdlet esportazioni hello modificato tooadd un'impostazione probe.</span><span class="sxs-lookup"><span data-stu-id="c3042-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="c3042-158">Aprire il file XML di hello in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="c3042-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="c3042-159">Aggiungere una sezione `<probe>` dopo `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="c3042-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="c3042-160">Nella sezione di backendHttpSettings hello di hello XML, aggiungere il nome di probe hello come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c3042-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="c3042-161">Salvare il file XML di hello.</span><span class="sxs-lookup"><span data-stu-id="c3042-161">Save hello XML file.</span></span>

1. <span data-ttu-id="c3042-162">Configurazione di gateway applicazione hello aggiornamento con nuovo file XML hello utilizzando `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="c3042-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="c3042-163">Questo cmdlet aggiorna il gateway applicazione con una nuova configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="c3042-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="c3042-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3042-164">Next steps</span></span>

<span data-ttu-id="c3042-165">Se si desidera tooconfigure offload Secure Sockets Layer (SSL), vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="c3042-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="c3042-166">Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno, vedere [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="c3042-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

