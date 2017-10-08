---
title: -Gateway applicazione Azure - CLI di Azure 2.0 di offload SSL aaaConfigure | Documenti Microsoft
description: Questa pagina fornisce istruzioni toocreate offload un gateway applicazione con SSL 2.0 CLI di Azure
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
ms.openlocfilehash: f8d50e0c6ffef17c807938d816410e6d85321c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="6c9c6-103">Configurare un gateway applicazione per l'offload SSL con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6c9c6-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c9c6-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6c9c6-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="6c9c6-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6c9c6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="6c9c6-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="6c9c6-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="6c9c6-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6c9c6-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="6c9c6-108">Gateway applicazione Azure può essere configurato tooterminate hello Secure Sockets Layer (SSL) sessione hello gateway tooavoid costosi SSL decrittografia attività toohappen alla farm web hello.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="6c9c6-109">Offload SSL semplifica anche la gestione dei certificati server front-end hello.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-109">SSL offload also simplifies certificate management at hello front-end server.</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="6c9c6-110">Prerequisito: Installare hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6c9c6-110">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="6c9c6-111">hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="6c9c6-111">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="6c9c6-112">Componenti richiesti</span><span class="sxs-lookup"><span data-stu-id="6c9c6-112">Required components</span></span>

* <span data-ttu-id="6c9c6-113">**Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-113">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="6c9c6-114">gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-114">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="6c9c6-115">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="6c9c6-116">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-116">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="6c9c6-117">**Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-117">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="6c9c6-118">Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-118">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="6c9c6-119">**Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, queste impostazioni sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="6c9c6-119">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="6c9c6-120">**Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-120">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="6c9c6-121">Attualmente, solo hello *base* regola supportata.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-121">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="6c9c6-122">Hello *base* regola è una distribuzione del carico round robin.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-122">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="6c9c6-123">**Note aggiuntive sulla configurazione**</span><span class="sxs-lookup"><span data-stu-id="6c9c6-123">**Additional configuration notes**</span></span>

<span data-ttu-id="6c9c6-124">Per la configurazione di certificati SSL, hello protocollo **HttpListener** deve modificare troppo*Https* (maiuscole / minuscole).</span><span class="sxs-lookup"><span data-stu-id="6c9c6-124">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="6c9c6-125">Hello **SslCertificate** elemento viene aggiunto troppo**HttpListener** con valore della variabile hello configurato per il certificato SSL hello.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-125">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="6c9c6-126">porta front-end di Hello deve essere aggiornato too443.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-126">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="6c9c6-127">**affinità basato su cookie tooenable**: un gateway applicazione può essere configurato tooensure che una richiesta da una sessione client è sempre toohello diretto stessa macchina virtuale nella farm web hello.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-127">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="6c9c6-128">Questo scenario viene eseguito dall'inserimento di un cookie di sessione che consenta il traffico di toodirect di hello gateway in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-128">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="6c9c6-129">impostata l'affinità basato su cookie tooenable, **CookieBasedAffinity** troppo*abilitato* in hello **BackendHttpSettings** elemento.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-129">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="6c9c6-130">Configurare l'offload SSL in un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="6c9c6-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port toobe used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload hello .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing hello port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool toobe used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using hello new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking hello listener toohello back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="6c9c6-131">Creare un gateway applicazione con l'offload SSL</span><span class="sxs-lookup"><span data-stu-id="6c9c6-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="6c9c6-132">Hello seguente esempio crea un gateway applicazione con offload SSL.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-132">hello following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="6c9c6-133">certificato Hello e la password del certificato deve essere aggiornato tooa la chiave privata valida.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-133">hello certificate and certificate password must be updated tooa valid private key.</span></span>

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

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="6c9c6-134">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="6c9c6-134">Get application gateway DNS name</span></span>

<span data-ttu-id="6c9c6-135">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-135">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="6c9c6-136">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="6c9c6-137">gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-137">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="6c9c6-138">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6c9c6-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="6c9c6-139">tooconfigure un alias, recuperare i dettagli del gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-139">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="6c9c6-140">nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-140">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="6c9c6-141">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c9c6-141">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="6c9c6-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c9c6-142">Next steps</span></span>

<span data-ttu-id="6c9c6-143">Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno (ILB), vedere [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="6c9c6-143">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="6c9c6-144">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="6c9c6-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="6c9c6-145">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="6c9c6-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="6c9c6-146">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="6c9c6-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
