---
title: Creare un probe personalizzato - Gateway applicazione di Azure - PowerShell versione classica | Microsoft Docs
description: Informazioni su come creare un probe personalizzato per il gateway applicazione usando PowerShell nel modello di distribuzione classica
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
ms.openlocfilehash: bf190741b10c10e885d927ad21a9f2b25107943f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="f36f2-103">Creare un probe personalizzato per il gateway applicazione di Azure (classico) con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f36f2-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f36f2-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f36f2-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="f36f2-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f36f2-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="f36f2-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="f36f2-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="f36f2-107">Questo articolo illustra come aggiungere un probe personalizzato a un gateway applicazione esistente con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f36f2-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="f36f2-108">I probe personalizzati sono utili per le applicazioni che dispongono di una pagina di controllo dell'integrità specifica o per quelle che non rispondono in modo corretto all'applicazione Web predefinita.</span><span class="sxs-lookup"><span data-stu-id="f36f2-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f36f2-109">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f36f2-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f36f2-110">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="f36f2-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f36f2-111">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="f36f2-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f36f2-112">Informazioni su come [eseguire questa procedura con il modello di Resource Manager](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f36f2-112">Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="f36f2-113">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f36f2-113">Create an application gateway</span></span>

<span data-ttu-id="f36f2-114">Per creare un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="f36f2-114">To create an application gateway:</span></span>

1. <span data-ttu-id="f36f2-115">Creare una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="f36f2-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="f36f2-116">Creare un file XML di configurazione o un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f36f2-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="f36f2-117">Eseguire il commit della configurazione nella risorsa del gateway applicazione appena creata.</span><span class="sxs-lookup"><span data-stu-id="f36f2-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="f36f2-118">Creare una risorsa del gateway applicazione con un probe personalizzato</span><span class="sxs-lookup"><span data-stu-id="f36f2-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="f36f2-119">Per creare il gateway, usare il cmdlet `New-AzureApplicationGateway`, sostituendo i valori esistenti con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="f36f2-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="f36f2-120">La fatturazione per il gateway non viene applicata a partire da questo punto.</span><span class="sxs-lookup"><span data-stu-id="f36f2-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="f36f2-121">La fatturazione viene applicata a partire da un passaggio successivo, dopo l'avvio corretto del gateway.</span><span class="sxs-lookup"><span data-stu-id="f36f2-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="f36f2-122">L'esempio seguente mostra come creare un gateway applicazione usando una rete virtuale denominata "testvnet1" e una subnet denominata "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="f36f2-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="f36f2-123">Per convalidare la creazione del gateway, è possibile usare il cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="f36f2-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="f36f2-124">Il valore predefinito per *InstanceCount* è 2, con un valore massimo di 10.</span><span class="sxs-lookup"><span data-stu-id="f36f2-124">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="f36f2-125">Il valore predefinito per *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="f36f2-125">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="f36f2-126">È possibile scegliere tra Small, Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="f36f2-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="f36f2-127">*VirtualIPs* e *DnsName* vengono visualizzati vuoti perché il gateway non è stato ancora avviato.</span><span class="sxs-lookup"><span data-stu-id="f36f2-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="f36f2-128">Questi valori vengono creati quando il gateway è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f36f2-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="f36f2-129">Configurare un gateway applicazione usando XML</span><span class="sxs-lookup"><span data-stu-id="f36f2-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="f36f2-130">Nell'esempio seguente viene usato un file XML per configurare tutte le impostazioni del gateway applicazione ed eseguirne il commit nella risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="f36f2-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="f36f2-131">Copiare il testo seguente in Blocco note.</span><span class="sxs-lookup"><span data-stu-id="f36f2-131">Copy the following text to Notepad.</span></span>

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

<span data-ttu-id="f36f2-132">Modificare i valori tra parentesi per gli elementi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f36f2-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="f36f2-133">Salvare il file con estensione XML.</span><span class="sxs-lookup"><span data-stu-id="f36f2-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="f36f2-134">L'esempio seguente mostra come usare un file di configurazione per impostare il gateway applicazione per il bilanciamento del carico del traffico HTTP sulla porta pubblica 80 e inviare il traffico di rete alla porta back-end 80 tra due indirizzi IP usando un probe personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f36f2-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f36f2-135">L'elemento del protocollo HTTP o HTTPS deve rispettare la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="f36f2-135">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="f36f2-136">Viene aggiunto un nuovo elemento di configurazione \<Probe\> per configurare i probe personalizzati.</span><span class="sxs-lookup"><span data-stu-id="f36f2-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="f36f2-137">I parametri di configurazione sono:</span><span class="sxs-lookup"><span data-stu-id="f36f2-137">The configuration parameters are:</span></span>

|<span data-ttu-id="f36f2-138">Parametro</span><span class="sxs-lookup"><span data-stu-id="f36f2-138">Parameter</span></span>|<span data-ttu-id="f36f2-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f36f2-139">Description</span></span>|
|---|---|
|<span data-ttu-id="f36f2-140">**Nome**</span><span class="sxs-lookup"><span data-stu-id="f36f2-140">**Name**</span></span> |<span data-ttu-id="f36f2-141">Nome di riferimento del probe personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f36f2-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="f36f2-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="f36f2-142">* **Protocol**</span></span> | <span data-ttu-id="f36f2-143">Protocollo usato. I valori possibili sono HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f36f2-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="f36f2-144">**Host** e **Path**</span><span class="sxs-lookup"><span data-stu-id="f36f2-144">**Host** and **Path**</span></span> | <span data-ttu-id="f36f2-145">Percorso URL completo richiamato dal gateway applicazione per determinare l'integrità dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="f36f2-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="f36f2-146">Se si ha un sito Web http://contoso.com/, ad esempio, il probe personalizzato può essere configurato per "http://contoso.com/path/custompath.htm" in modo che i controlli del probe ottengano una risposta HTTP corretta.</span><span class="sxs-lookup"><span data-stu-id="f36f2-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="f36f2-147">**Interval**</span><span class="sxs-lookup"><span data-stu-id="f36f2-147">**Interval**</span></span> | <span data-ttu-id="f36f2-148">Configura i controlli dell'intervallo di probe, in secondi.</span><span class="sxs-lookup"><span data-stu-id="f36f2-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="f36f2-149">**Timeout**</span><span class="sxs-lookup"><span data-stu-id="f36f2-149">**Timeout**</span></span> | <span data-ttu-id="f36f2-150">Definisce il timeout del probe per un controllo della risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="f36f2-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="f36f2-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="f36f2-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="f36f2-152">Numero di risposte HTTP non riuscite necessario per contrassegnare l'istanza back-end come *non integra*.</span><span class="sxs-lookup"><span data-stu-id="f36f2-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="f36f2-153">Nella configurazione \<BackendHttpSettings\> viene fatto riferimento al nome del probe per assegnare il pool back-end che userà le impostazioni del probe personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f36f2-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="f36f2-154">Aggiungere un probe personalizzato a un gateway applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="f36f2-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="f36f2-155">Per modificare la configurazione corrente di un gateway applicazione sono necessari tre passaggi: ottenere il file di configurazione XML corrente, apportare modifiche per avere un probe personalizzato e configurare il gateway applicazione con le nuove impostazioni XML.</span><span class="sxs-lookup"><span data-stu-id="f36f2-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="f36f2-156">Ottenere il file XML usando `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="f36f2-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="f36f2-157">Questo cmdlet esporta il file XML di configurazione, che potrà quindi essere modificato per aggiungere un'impostazione di probe.</span><span class="sxs-lookup"><span data-stu-id="f36f2-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="f36f2-158">Aprire il file XML in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="f36f2-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="f36f2-159">Aggiungere una sezione `<probe>` dopo `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="f36f2-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="f36f2-160">Nella sezione backendHttpSettings del file XML aggiungere il nome del probe, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f36f2-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

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

  <span data-ttu-id="f36f2-161">Salvare il file XML.</span><span class="sxs-lookup"><span data-stu-id="f36f2-161">Save the XML file.</span></span>

1. <span data-ttu-id="f36f2-162">Aggiornare la configurazione del gateway applicazione con il nuovo file XML usando `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="f36f2-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="f36f2-163">Questo cmdlet aggiorna il gateway applicazione con la nuova configurazione.</span><span class="sxs-lookup"><span data-stu-id="f36f2-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="f36f2-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f36f2-164">Next steps</span></span>

<span data-ttu-id="f36f2-165">Per configurare l'offload SSL (Secure Sockets Layer), vedere [Configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="f36f2-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="f36f2-166">Per configurare un gateway applicazione da usare con un servizio di bilanciamento del carico interno, vedere [Creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="f36f2-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

