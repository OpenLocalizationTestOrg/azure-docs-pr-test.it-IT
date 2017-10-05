---
title: Configurare un web application firewall - Gateway applicazione di Azure | Microsoft Docs
description: Questo articolo fornisce indicazioni su come iniziare a usare il firewall applicazione Web in un gateway applicazione nuovo o esistente.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: ac6c629ceaf1a8036643f593ce3d7ef9ea096ef8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="546b8-103">Configurare un web application firewall in un gateway applicazione nuovo o esistente con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="546b8-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="546b8-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="546b8-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="546b8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="546b8-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="546b8-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="546b8-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="546b8-107">Informazioni su come creare un gateway applicazione abilitato per un firewall applicazione Web o su come aggiungere un firewall applicazione Web a un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="546b8-107">Learn how to create a web application firewall enabled application gateway or add web application firewall to an existing application gateway.</span></span>

<span data-ttu-id="546b8-108">Il firewall applicazione Web (WAF) nel gateway applicazione di Azure protegge le applicazioni Web dai comuni attacchi basati sul Web, come ad esempio gli attacchi SQL injection, gli attacchi di scripting intersito e il controllo delle sessioni.</span><span class="sxs-lookup"><span data-stu-id="546b8-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="546b8-109">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="546b8-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="546b8-110">Fornisce richieste HTTP con routing delle prestazioni e failover tra server diversi, sia nel cloud che in locale.</span><span class="sxs-lookup"><span data-stu-id="546b8-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="546b8-111">Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="546b8-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="546b8-112">Per un elenco completo delle funzionalità supportate, vedere la [panoramica del gateway applicazione](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="546b8-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="546b8-113">L'articolo seguente illustra come [aggiungere il firewall applicazione Web a un gateway applicazione esistente](#add-web-application-firewall-to-an-existing-application-gateway) e [creare un gateway applicazione che usa il firewall applicazione Web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="546b8-113">The following article shows how to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![immagine dello scenario][scenario]

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="546b8-115">Prerequisito: installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="546b8-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="546b8-116">Per eseguire i passaggi indicati in questo articolo è necessario [installare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows (interfaccia della riga di comando di Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="546b8-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="546b8-117">Differenze di configurazione dei WAF</span><span class="sxs-lookup"><span data-stu-id="546b8-117">WAF configuration differences</span></span>

<span data-ttu-id="546b8-118">Se è stato letto l'argomento [Creare un gateway applicazione con l'interfaccia della riga di comando di Azure ](application-gateway-create-gateway-cli.md), si conoscono le impostazioni della SKU da configurare quando si crea un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="546b8-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand the SKU settings to configure when creating an application gateway.</span></span> <span data-ttu-id="546b8-119">WAF fornisce impostazioni aggiuntive da definire quando si configura la SKU su un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="546b8-119">WAF provides additional settings to define when configuring the SKU on an application gateway.</span></span> <span data-ttu-id="546b8-120">Non esistono altre modifiche aggiuntive da apportare sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="546b8-120">There are no additional changes that you make on the application gateway itself.</span></span>

| <span data-ttu-id="546b8-121">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="546b8-121">**Setting**</span></span> | <span data-ttu-id="546b8-122">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="546b8-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="546b8-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="546b8-123">**SKU**</span></span> |<span data-ttu-id="546b8-124">Un gateway applicazione normale senza WAF supporta le dimensioni **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="546b8-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="546b8-125">Con l'introduzione di WAF sono disponibili due SKU aggiuntive, **WAF\_Medium** e **WAF\_Large**.</span><span class="sxs-lookup"><span data-stu-id="546b8-125">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="546b8-126">WAF non è supportato sui gateway applicazione di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="546b8-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="546b8-127">**Modalità**</span><span class="sxs-lookup"><span data-stu-id="546b8-127">**Mode**</span></span> | <span data-ttu-id="546b8-128">Questa impostazione è la modalità di WAF.</span><span class="sxs-lookup"><span data-stu-id="546b8-128">This setting is the mode of WAF.</span></span> <span data-ttu-id="546b8-129">I valori consentiti sono **Rilevamento** e **Prevenzione**.</span><span class="sxs-lookup"><span data-stu-id="546b8-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="546b8-130">Quando il firewall WAF è configurato in modalità di rilevamento, tutte le minacce vengono archiviate in un file di log.</span><span class="sxs-lookup"><span data-stu-id="546b8-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="546b8-131">In modalità di prevenzione, gli eventi vengono comunque registrati, ma l'autore dell'attacco riceve una risposta di mancata autorizzazione 403 dal gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="546b8-131">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the application gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="546b8-132">Aggiungere un firewall applicazione Web a un gateway applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="546b8-132">Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="546b8-133">Il comando seguente modifica un gateway applicazione standard esistente in un gateway applicazione abilitato per WAF.</span><span class="sxs-lookup"><span data-stu-id="546b8-133">The follow command changes an existing standard application gateway to a WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="546b8-134">Questo comando aggiorna il gateway applicazione con il web application firewall.</span><span class="sxs-lookup"><span data-stu-id="546b8-134">This command updates the application gateway with web application firewall.</span></span> <span data-ttu-id="546b8-135">Per informazioni su come visualizzare i log per il gateway applicazione, vedere l'argomento relativo alla [diagnostica del gateway applicazione](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="546b8-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your application gateway.</span></span> <span data-ttu-id="546b8-136">Per le implicazioni di sicurezza del WAF, i log devono essere esaminati a intervalli regolari per essere aggiornati sulle condizioni di sicurezza delle applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="546b8-136">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="546b8-137">Creare un gateway applicazione con il web application firewall</span><span class="sxs-lookup"><span data-stu-id="546b8-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="546b8-138">Il comando seguente crea un gateway applicazione con web application firewall.</span><span class="sxs-lookup"><span data-stu-id="546b8-138">The following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="546b8-139">I gateway applicazione creati con la configurazione di base del web application firewall sono configurati con CRS 3.0 per la protezione.</span><span class="sxs-lookup"><span data-stu-id="546b8-139">Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="546b8-140">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="546b8-140">Get application gateway DNS name</span></span>

<span data-ttu-id="546b8-141">Dopo avere creato il gateway, il passaggio successivo prevede la configurazione del front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="546b8-141">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="546b8-142">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="546b8-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="546b8-143">Per assicurarsi che gli utenti finali possano raggiungere il gateway applicazione, è possibile usare un record CNAME per fare riferimento all'endpoint pubblico del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="546b8-143">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="546b8-144">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="546b8-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="546b8-145">Per configurare un record CNAME, recuperare i dettagli del gateway applicazione e il nome DNS e l'IP associati usando l'elemento PublicIPAddress collegato al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="546b8-145">To configure a CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="546b8-146">Il nome DNS del gateway applicazione dovrà essere usato per creare un record CNAME che associa le due applicazioni Web a questo nome DNS.</span><span class="sxs-lookup"><span data-stu-id="546b8-146">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="546b8-147">Non è consigliabile usare record A perché l'indirizzo VIP può cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="546b8-147">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="next-steps"></a><span data-ttu-id="546b8-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="546b8-148">Next steps</span></span>

<span data-ttu-id="546b8-149">Informazioni su come personalizzare le regole del WAF sono disponibili in [Customize web application firewall rules through the Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md) (Personalizzare le regole del web application firewall con l'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="546b8-149">Learn how to customize WAF rules by visiting: [Customize web application firewall rules through the Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
