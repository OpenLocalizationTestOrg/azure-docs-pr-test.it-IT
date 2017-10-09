---
title: aaaCreate un Gateway di applicazione di Azure - CLI di Azure 2.0 | Documenti Microsoft
description: Informazioni su come toocreate un Gateway applicazione utilizzando hello Azure CLI 2.0 in Gestione risorse
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="3c8d6-103">Creare un gateway applicazione hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3c8d6-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c8d6-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3c8d6-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="3c8d6-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3c8d6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="3c8d6-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="3c8d6-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="3c8d6-107">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3c8d6-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="3c8d6-108">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="3c8d6-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="3c8d6-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="3c8d6-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="3c8d6-110">Il gateway applicazione è un'appliance virtuale dedicata che offre un servizio di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller) e varie funzionalità di bilanciamento del carico di livello 7 per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3c8d6-111">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="3c8d6-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="3c8d6-112">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="3c8d6-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="3c8d6-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -nostri CLI per hello classic e risorse Gestione modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="3c8d6-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="3c8d6-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="3c8d6-115">Prerequisito: Installare hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3c8d6-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="3c8d6-116">hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="3c8d6-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="3c8d6-117">Se non si dispone di un account Azure, è necessario procurarsene uno.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="3c8d6-118">Usare la [versione di valutazione gratuita](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="3c8d6-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="3c8d6-119">Scenario</span><span class="sxs-lookup"><span data-stu-id="3c8d6-119">Scenario</span></span>

<span data-ttu-id="3c8d6-120">In questo scenario viene illustrato come gateway un'applicazione utilizzando toocreate hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="3c8d6-121">Questo scenario illustrerà come:</span><span class="sxs-lookup"><span data-stu-id="3c8d6-121">This scenario will:</span></span>

* <span data-ttu-id="3c8d6-122">Creare un gateway applicazione Medium con due istanze.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="3c8d6-123">Creare una rete virtuale denominata AdatumAppGatewayVNET con un blocco CIDR riservato 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="3c8d6-124">Creare una subnet denominata Appgatewaysubnet che usa 10.0.0.0/28 come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="3c8d6-125">Le ricerche di configurazione aggiuntiva di gateway applicazione hello, inclusi stato personalizzato, gli indirizzi del pool back-end e regole aggiuntive vengono configurati dopo la configurazione di gateway applicazione hello e non durante la distribuzione iniziale.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3c8d6-126">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3c8d6-126">Before you begin</span></span>

<span data-ttu-id="3c8d6-127">Il gateway applicazione di Azure richiede una propria subnet.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="3c8d6-128">Quando si crea una rete virtuale, assicurarsi di lasciare sufficiente toohave spazio di indirizzi più subnet.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="3c8d6-129">Dopo aver distribuito una subnet tooa di gateway applicazione, i gateway applicazione aggiuntiva solo è possibile aggiungere subnet toohello.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="3c8d6-130">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="3c8d6-130">Log in tooAzure</span></span>

<span data-ttu-id="3c8d6-131">Aprire hello **prompt dei comandi di Microsoft Azure**ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="3c8d6-132">È inoltre possibile utilizzare `az login` senza l'opzione per l'accesso di dispositivo che richiede l'immissione di un codice di aka.ms/devicelogin hello.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="3c8d6-133">Una volta digitato hello sopra riportato, viene fornito un codice.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="3c8d6-134">Spostarsi in un processo di accesso browser hello toocontinue toohttps://aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![Comando che illustra l'accesso al dispositivo][1]

<span data-ttu-id="3c8d6-136">Nel browser hello immettere codice hello ricevuto.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="3c8d6-137">Si è reindirizzato tooa nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-137">You are redirected tooa sign-in page.</span></span>

![codice tooenter browser][2]

<span data-ttu-id="3c8d6-139">Dopo aver immesso il codice hello si è connessi, hello Chiudi browser toocontinue scenario hello.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![Accesso eseguito][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="3c8d6-141">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="3c8d6-141">Create hello resource group</span></span>

<span data-ttu-id="3c8d6-142">Prima di creare i gateway applicazione hello, un gruppo di risorse viene creato toocontain gateway di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="3c8d6-143">Hello seguito è riportato il comando hello.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="3c8d6-144">Creare il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="3c8d6-144">Create hello application gateway</span></span>

<span data-ttu-id="3c8d6-145">gli indirizzi IP di Hello usati per back-end hello sono gli indirizzi IP hello del server back-end.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="3c8d6-146">Questi valori possono essere entrambi indirizzi IP privati nella rete virtuale hello, gli indirizzi IP pubblici o nomi di dominio completo per i server back-end.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="3c8d6-147">Hello seguente viene creato un gateway applicazione con le impostazioni di configurazione aggiuntive per le impostazioni http, porte e le regole.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="3c8d6-148">Hello precedente esempio vengono illustrate molte proprietà che non sono necessari durante la creazione di un gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="3c8d6-149">Hello esempio di codice seguente crea un gateway applicazione con le informazioni necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-149">hello following code example creates an application gateway with hello required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="3c8d6-150">Per un elenco di parametri che possono essere forniti durante hello creazione eseguire comando seguente: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="3c8d6-151">Questo esempio crea un gateway applicazione basic con le impostazioni predefinite per il listener hello, pool back-end, le impostazioni http back-end e regole.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="3c8d6-152">È possibile modificare la distribuzione toosuit queste impostazioni dopo il provisioning di hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="3c8d6-153">Se si dispone già di un'applicazione web definita con il pool back-end hello in hello precedenti passaggi, una volta creati, il bilanciamento del carico ha inizio.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="3c8d6-154">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="3c8d6-154">Get application gateway DNS name</span></span>

<span data-ttu-id="3c8d6-155">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="3c8d6-156">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="3c8d6-157">gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="3c8d6-158">[Configurazione di un nome di dominio personalizzato in Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3c8d6-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="3c8d6-159">tooconfigure un alias, recuperare i dettagli del gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="3c8d6-160">nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="3c8d6-161">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3c8d6-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="delete-all-resources"></a><span data-ttu-id="3c8d6-162">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="3c8d6-162">Delete all resources</span></span>

<span data-ttu-id="3c8d6-163">toodelete tutte le risorse create in questo articolo, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3c8d6-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="3c8d6-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c8d6-164">Next steps</span></span>

<span data-ttu-id="3c8d6-165">Informazioni su come probe di integrità personalizzato toocreate visitando [per creare un probe di integrità personalizzato](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3c8d6-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="3c8d6-166">Informazioni su come tooconfigure offload SSL e la decrittografia SSL costosa di intraprendere hello off i server web, visitare il sito [configurare Offload SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="3c8d6-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
