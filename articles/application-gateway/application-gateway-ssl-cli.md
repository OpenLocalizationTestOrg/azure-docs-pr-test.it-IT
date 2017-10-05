---
title: Configurare l'offload SSL - Gateway applicazione di Azure - Interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Questo articolo contiene le istruzioni per creare un gateway applicazione con l'offload SSL usando l'interfaccia della riga di comando di Azure 2.0
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: e8c1ba09daef09ef5002e33345905772961c1d93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="64c3d-103">Configurare un gateway applicazione per l'offload SSL con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="64c3d-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="64c3d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="64c3d-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="64c3d-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64c3d-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="64c3d-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="64c3d-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="64c3d-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="64c3d-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="64c3d-108">Il gateway applicazione di Azure può essere configurato per terminare la sessione Secure Sockets Layer (SSL) nel gateway ed evitare costose attività di decrittografia SSL nella Web farm.</span><span class="sxs-lookup"><span data-stu-id="64c3d-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="64c3d-109">L'offload SSL semplifica anche la gestione dei certificati nel server front-end.</span><span class="sxs-lookup"><span data-stu-id="64c3d-109">SSL offload also simplifies certificate management at the front-end server.</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="64c3d-110">Prerequisito: installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="64c3d-110">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="64c3d-111">Per eseguire i passaggi indicati in questo articolo è necessario [installare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows (interfaccia della riga di comando di Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="64c3d-111">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="64c3d-112">Componenti richiesti</span><span class="sxs-lookup"><span data-stu-id="64c3d-112">Required components</span></span>

* <span data-ttu-id="64c3d-113">**Pool di server back-end:** elenco di indirizzi IP dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="64c3d-113">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="64c3d-114">Gli indirizzi IP elencati devono appartenere alla subnet della rete virtuale o devono essere indirizzi IP/VIP pubblici.</span><span class="sxs-lookup"><span data-stu-id="64c3d-114">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="64c3d-115">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni come porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="64c3d-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="64c3d-116">Queste impostazioni sono associate a un pool e vengono applicate a tutti i server nel pool.</span><span class="sxs-lookup"><span data-stu-id="64c3d-116">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="64c3d-117">**Porta front-end:** porta pubblica aperta sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="64c3d-117">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="64c3d-118">Il traffico raggiunge questa porta e quindi viene reindirizzato a uno dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="64c3d-118">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="64c3d-119">**Listener** : ha una porta front-end, un protocollo (Http o Https, queste impostazioni fanno distinzione tra maiuscole e minuscole) e il nome del certificato SSL (se si configura l'offload SSL).</span><span class="sxs-lookup"><span data-stu-id="64c3d-119">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="64c3d-120">**Regola** : associa il listener e il pool di server back-end e definisce il pool di server back-end a cui deve essere indirizzato il traffico quando raggiunge un listener specifico.</span><span class="sxs-lookup"><span data-stu-id="64c3d-120">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="64c3d-121">È attualmente supportata solo la regola *basic* .</span><span class="sxs-lookup"><span data-stu-id="64c3d-121">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="64c3d-122">La regola *basic* è una distribuzione del carico di tipo round robin.</span><span class="sxs-lookup"><span data-stu-id="64c3d-122">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="64c3d-123">**Note aggiuntive sulla configurazione**</span><span class="sxs-lookup"><span data-stu-id="64c3d-123">**Additional configuration notes**</span></span>

<span data-ttu-id="64c3d-124">Per la configurazione dei certificati SSL, il protocollo in **HttpListener** deve essere sostituito con *Https* (distinzione tra maiuscole e minuscole).</span><span class="sxs-lookup"><span data-stu-id="64c3d-124">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="64c3d-125">L'elemento **SslCertificate** viene aggiunto ad **HttpListener** con il valore della variabile configurato per il certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="64c3d-125">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="64c3d-126">La porta front-end deve essere impostata su 443.</span><span class="sxs-lookup"><span data-stu-id="64c3d-126">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="64c3d-127">**Per abilitare l'affinità basata sui cookie**: è possibile configurare un gateway applicazione per fare in modo che una richiesta proveniente da una sessione client sia sempre diretta alla stessa macchina virtuale nella Web farm.</span><span class="sxs-lookup"><span data-stu-id="64c3d-127">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="64c3d-128">Questo scenario viene realizzato aggiungendo un cookie di sessione che consente al gateway di indirizzare il traffico in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="64c3d-128">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="64c3d-129">Per abilitare l'affinità basata sui cookie, impostare **CookieBasedAffinity** su *Enabled* nell'elemento **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="64c3d-129">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="64c3d-130">Configurare l'offload SSL in un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="64c3d-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port to be used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload the .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing the port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool to be used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using the new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking the listener to the back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="64c3d-131">Creare un gateway applicazione con l'offload SSL</span><span class="sxs-lookup"><span data-stu-id="64c3d-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="64c3d-132">L'esempio seguente crea un gateway applicazione con l'offload SSL.</span><span class="sxs-lookup"><span data-stu-id="64c3d-132">The following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="64c3d-133">Il certificato e la password del certificato devono essere aggiornati a una chiave privata valida.</span><span class="sxs-lookup"><span data-stu-id="64c3d-133">The certificate and certificate password must be updated to a valid private key.</span></span>

```azurecli-interactive
#!/bin/bash

# Creates an application gateway with SSL offload
az network application-gateway create \
  --name "AdatumAppGateway3" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG2" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet" \
  --subnet-address-prefix "10.0.0.0/28" \
  --frontend-port 443 \
  --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 \
  --sku "Standard_Small" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip" \
  --public-ip-address-allocation "dynamic"
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="64c3d-134">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="64c3d-134">Get application gateway DNS name</span></span>

<span data-ttu-id="64c3d-135">Dopo avere creato il gateway, il passaggio successivo prevede la configurazione del front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="64c3d-135">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="64c3d-136">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="64c3d-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="64c3d-137">Per assicurarsi che gli utenti finali possano raggiungere il gateway applicazione, è possibile usare un record CNAME per fare riferimento all'endpoint pubblico del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="64c3d-137">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="64c3d-138">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="64c3d-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="64c3d-139">Per configurare un alias, recuperare i dettagli del gateway applicazione e il nome DNS e l'IP associati usando l'elemento PublicIPAddress collegato al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="64c3d-139">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="64c3d-140">Il nome DNS del gateway applicazione dovrà essere usato per creare un record CNAME che associa le due applicazioni Web a questo nome DNS.</span><span class="sxs-lookup"><span data-stu-id="64c3d-140">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="64c3d-141">Non è consigliabile usare record A perché l'indirizzo VIP può cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="64c3d-141">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
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

## <a name="next-steps"></a><span data-ttu-id="64c3d-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64c3d-142">Next steps</span></span>

<span data-ttu-id="64c3d-143">Per configurare un gateway applicazione da usare con un servizio di bilanciamento del carico interno, vedere [Creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="64c3d-143">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="64c3d-144">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="64c3d-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="64c3d-145">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="64c3d-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="64c3d-146">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="64c3d-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
