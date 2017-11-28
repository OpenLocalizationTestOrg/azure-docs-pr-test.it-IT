---
title: firewall di applicazione web aaaConfigure - Gateway applicazione Azure | Documenti Microsoft
description: In questo articolo vengono fornite indicazioni su come toostart tramite web firewall applicazione su un gateway applicazione nuova o esistente.
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
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="f6294-103">Configurare un web application firewall in un gateway applicazione nuovo o esistente con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f6294-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6294-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f6294-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="f6294-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6294-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="f6294-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f6294-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="f6294-107">Informazioni su come toocreate un firewall applicazione web abilitata gateway applicazione oppure aggiungere web application firewall tooan applicazione gateway esistente.</span><span class="sxs-lookup"><span data-stu-id="f6294-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="f6294-108">firewall applicazione web di Hello (WAF) nel Gateway di applicazione di Azure consente di proteggere le applicazioni web da attacchi basati sul web comuni quali attacchi SQL injection, attacchi di script e assume il controllo di sessione.</span><span class="sxs-lookup"><span data-stu-id="f6294-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="f6294-109">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="f6294-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="f6294-110">Fornisce il failover, le prestazioni di routing di richieste HTTP tra server diversi, che si trovino in locale o cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f6294-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="f6294-111">Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f6294-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="f6294-112">toofind un elenco completo delle funzionalità supportate, visitare: [Panoramica del Gateway applicazione](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f6294-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="f6294-113">Hello articolo seguente viene illustrato come troppo[aggiungere web application firewall tooan esistente gateway applicazione](#add-web-application-firewall-to-an-existing-application-gateway) e [creare un gateway di applicazione che utilizza firewall applicazione web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="f6294-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![immagine dello scenario][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="f6294-115">Prerequisito: Installare hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f6294-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="f6294-116">hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f6294-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="f6294-117">Differenze di configurazione dei WAF</span><span class="sxs-lookup"><span data-stu-id="f6294-117">WAF configuration differences</span></span>

<span data-ttu-id="f6294-118">Se si è letto [creare un Gateway applicazione con Azure CLI](application-gateway-create-gateway-cli.md), comprendere hello SKU impostazioni tooconfigure durante la creazione di un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6294-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="f6294-119">WAF fornisce toodefine impostazioni aggiuntive quando si configurano hello SKU di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6294-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="f6294-120">Non sono presenti modifiche aggiuntive che verranno apportate gateway applicazione hello stesso.</span><span class="sxs-lookup"><span data-stu-id="f6294-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="f6294-121">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="f6294-121">**Setting**</span></span> | <span data-ttu-id="f6294-122">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="f6294-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="f6294-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="f6294-123">**SKU**</span></span> |<span data-ttu-id="f6294-124">Un gateway applicazione normale senza WAF supporta le dimensioni **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="f6294-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="f6294-125">Introduzione di hello di WAF, non vi sono due SKU aggiuntive, **WAF\_Media** e **WAF\_grande**.</span><span class="sxs-lookup"><span data-stu-id="f6294-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="f6294-126">WAF non è supportato sui gateway applicazione di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="f6294-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="f6294-127">**Modalità**</span><span class="sxs-lookup"><span data-stu-id="f6294-127">**Mode**</span></span> | <span data-ttu-id="f6294-128">Questa impostazione è la modalità di WAF hello.</span><span class="sxs-lookup"><span data-stu-id="f6294-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="f6294-129">I valori consentiti sono **Rilevamento** e **Prevenzione**.</span><span class="sxs-lookup"><span data-stu-id="f6294-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="f6294-130">Quando il firewall WAF è configurato in modalità di rilevamento, tutte le minacce vengono archiviate in un file di log.</span><span class="sxs-lookup"><span data-stu-id="f6294-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="f6294-131">In modalità di prevenzione, gli eventi vengono comunque registrati ma autore dell'attacco hello riceve una risposta di non autorizzato 403 dal gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f6294-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="f6294-132">Aggiungere web application firewall tooan esistente gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f6294-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="f6294-133">Hello seguire le modifiche dei comandi di un gateway applicazione abilitato tooa WAF di gateway applicazione standard esistente.</span><span class="sxs-lookup"><span data-stu-id="f6294-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="f6294-134">Questo comando Aggiorna gateway applicazione hello con firewall applicazione web.</span><span class="sxs-lookup"><span data-stu-id="f6294-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="f6294-135">Visitare [diagnostica del Gateway applicazione](application-gateway-diagnostics.md) toounderstand come tooview Registra per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6294-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="f6294-136">A causa di toohello sicurezza natura WAF, registri necessità toobe rivisto regolarmente condizioni di sicurezza hello toounderstand delle applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="f6294-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="f6294-137">Creare un gateway applicazione con il web application firewall</span><span class="sxs-lookup"><span data-stu-id="f6294-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="f6294-138">Hello comando seguente crea un Gateway applicazione con firewall applicazione web.</span><span class="sxs-lookup"><span data-stu-id="f6294-138">hello following command creates an Application Gateway with web application firewall.</span></span>

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
> <span data-ttu-id="f6294-139">Gateway applicazione creati con configurazione del firewall applicazione web di base hello sono configurati con CRS 3.0 per la protezione.</span><span class="sxs-lookup"><span data-stu-id="f6294-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="f6294-140">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f6294-140">Get application gateway DNS name</span></span>

<span data-ttu-id="f6294-141">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="f6294-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="f6294-142">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="f6294-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="f6294-143">gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f6294-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="f6294-144">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f6294-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="f6294-145">tooconfigure un record CNAME, recuperare i dettagli del gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="f6294-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="f6294-146">nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis.</span><span class="sxs-lookup"><span data-stu-id="f6294-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="f6294-147">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6294-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f6294-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6294-148">Next steps</span></span>

<span data-ttu-id="f6294-149">Informazioni su come toocustomize WAF regole visitando: [personalizzare le regole di firewall applicazione web mediante Azure CLI 2.0 hello](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f6294-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
