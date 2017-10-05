---
title: Creare un gateway applicazione di Azure - Interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Informazioni su come creare un gateway applicazione usando l'interfaccia della riga di comando di Azure 2.0 in Resource Manager
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
ms.openlocfilehash: 052410db8c7619c7990dc319951a55663f2c2ba1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli-20"></a><span data-ttu-id="e3187-103">Creare un gateway applicazione con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e3187-103">Create an application gateway by using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3187-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e3187-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="e3187-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3187-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="e3187-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="e3187-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="e3187-107">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3187-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="e3187-108">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e3187-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="e3187-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e3187-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="e3187-110">Il gateway applicazione è un'appliance virtuale dedicata che offre un servizio di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller) e varie funzionalità di bilanciamento del carico di livello 7 per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3187-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e3187-111">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="e3187-111">CLI versions to complete the task</span></span>

<span data-ttu-id="e3187-112">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="e3187-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="e3187-113">[Interfaccia della riga di comando di Azure 1.0](application-gateway-create-gateway-cli-nodejs.md): l'interfaccia della riga di comando per il modello di distribuzione classico e di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="e3187-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="e3187-114">[Interfaccia della riga di comando di Azure 2.0](application-gateway-create-gateway-cli.md): interfaccia avanzata per il modello di distribuzione di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="e3187-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="e3187-115">Prerequisito: installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e3187-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="e3187-116">Per eseguire i passaggi indicati in questo articolo è necessario [installare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows (interfaccia della riga di comando di Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e3187-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="e3187-117">Se non si dispone di un account Azure, è necessario procurarsene uno.</span><span class="sxs-lookup"><span data-stu-id="e3187-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="e3187-118">Usare la [versione di valutazione gratuita](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="e3187-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="e3187-119">Scenario</span><span class="sxs-lookup"><span data-stu-id="e3187-119">Scenario</span></span>

<span data-ttu-id="e3187-120">Questo scenario mostra come creare un gateway applicazione usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3187-120">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="e3187-121">Questo scenario illustrerà come:</span><span class="sxs-lookup"><span data-stu-id="e3187-121">This scenario will:</span></span>

* <span data-ttu-id="e3187-122">Creare un gateway applicazione Medium con due istanze.</span><span class="sxs-lookup"><span data-stu-id="e3187-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="e3187-123">Creare una rete virtuale denominata AdatumAppGatewayVNET con un blocco CIDR riservato 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="e3187-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="e3187-124">Creare una subnet denominata Appgatewaysubnet che usa 10.0.0.0/28 come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="e3187-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="e3187-125">La configurazione aggiuntiva del gateway applicazione, che include i probe di integrità personalizzati, gli indirizzi del pool back-end e le regole aggiuntive, viene definita dopo la configurazione del gateway applicazione e non durante la distribuzione iniziale.</span><span class="sxs-lookup"><span data-stu-id="e3187-125">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e3187-126">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e3187-126">Before you begin</span></span>

<span data-ttu-id="e3187-127">Il gateway applicazione di Azure richiede una propria subnet.</span><span class="sxs-lookup"><span data-stu-id="e3187-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="e3187-128">Quando si crea una rete virtuale, assicurarsi di lasciare uno spazio indirizzi sufficiente per più subnet.</span><span class="sxs-lookup"><span data-stu-id="e3187-128">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="e3187-129">Dopo che un gateway applicazione è stato distribuito in una subnet, alla subnet possono essere aggiunti solo altri gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3187-129">Once you deploy an application gateway to a subnet, only additional application gateways can be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="e3187-130">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="e3187-130">Log in to Azure</span></span>

<span data-ttu-id="e3187-131">Aprire il **prompt dei comandi di Microsoft Azure**ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="e3187-131">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="e3187-132">È anche possibile usare `az login` senza l'opzione per l'accesso del dispositivo che richiede l'immissione di un codice in aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="e3187-132">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="e3187-133">Dopo avere digitato l'esempio precedente, viene fornito un codice.</span><span class="sxs-lookup"><span data-stu-id="e3187-133">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="e3187-134">Passare a https://aka.ms/devicelogin in un browser per continuare il processo di accesso.</span><span class="sxs-lookup"><span data-stu-id="e3187-134">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![Comando che illustra l'accesso al dispositivo][1]

<span data-ttu-id="e3187-136">Nel browser immettere il codice ricevuto.</span><span class="sxs-lookup"><span data-stu-id="e3187-136">In the browser, enter the code you received.</span></span> <span data-ttu-id="e3187-137">Si verrà reindirizzati a una pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="e3187-137">You are redirected to a sign-in page.</span></span>

![Browser in cui immettere il codice][2]

<span data-ttu-id="e3187-139">Dopo avere immesso il codice ed effettuato l'accesso, chiudere il browser per continuare con lo scenario.</span><span class="sxs-lookup"><span data-stu-id="e3187-139">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![Accesso eseguito][3]

## <a name="create-the-resource-group"></a><span data-ttu-id="e3187-141">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e3187-141">Create the resource group</span></span>

<span data-ttu-id="e3187-142">Prima di creare il gateway applicazione viene creato un gruppo di risorse che contenga il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3187-142">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="e3187-143">Di seguito è riportato il comando.</span><span class="sxs-lookup"><span data-stu-id="e3187-143">The following shows the command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="e3187-144">Creare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="e3187-144">Create the application gateway</span></span>

<span data-ttu-id="e3187-145">Gli indirizzi IP usati per il back-end sono gli indirizzi IP per il server back-end.</span><span class="sxs-lookup"><span data-stu-id="e3187-145">The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="e3187-146">Questi valori possono essere indirizzi IP privati nella rete virtuale, indirizzi IP pubblici o nomi di dominio completi per i server back-end.</span><span class="sxs-lookup"><span data-stu-id="e3187-146">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="e3187-147">L'esempio seguente crea un gateway applicazione con impostazioni di configurazione aggiuntive per le impostazioni HTTP, le porte e le regole.</span><span class="sxs-lookup"><span data-stu-id="e3187-147">The following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

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

<span data-ttu-id="e3187-148">L'esempio precedente mostra molte proprietà non necessarie durante la creazione di un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3187-148">The preceding example shows many properties that are not required during the creation of an application gateway.</span></span> <span data-ttu-id="e3187-149">L'esempio di codice seguente crea un gateway applicazione con le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="e3187-149">The following code example creates an application gateway with the required information.</span></span>

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
> <span data-ttu-id="e3187-150">Per un elenco dei parametri che possono essere specificati durante la creazione, eseguire questo comando: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="e3187-150">For a list of parameters that can be provided during creation run the following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="e3187-151">Questo esempio crea un gateway applicazione di base con le impostazioni predefinite per il listener, il pool back-end, le impostazioni HTTP back-end e le regole.</span><span class="sxs-lookup"><span data-stu-id="e3187-151">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="e3187-152">Queste impostazioni possono essere modificate in base alla propria distribuzione dopo che è stato completato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="e3187-152">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="e3187-153">Se l'applicazione Web è già stata definita con il pool back-end nei passaggi precedenti, dopo la creazione, inizia il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e3187-153">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="e3187-154">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="e3187-154">Get application gateway DNS name</span></span>

<span data-ttu-id="e3187-155">Dopo avere creato il gateway, il passaggio successivo prevede la configurazione del front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="e3187-155">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="e3187-156">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="e3187-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="e3187-157">Per assicurarsi che gli utenti finali possano raggiungere il gateway applicazione, è possibile usare un record CNAME per fare riferimento all'endpoint pubblico del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3187-157">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="e3187-158">[Configurazione di un nome di dominio personalizzato in Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="e3187-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="e3187-159">Per configurare un alias, recuperare i dettagli del gateway applicazione e il nome DNS e l'IP associati usando l'elemento PublicIPAddress collegato al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3187-159">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="e3187-160">Il nome DNS del gateway applicazione dovrà essere usato per creare un record CNAME che associa le due applicazioni Web a questo nome DNS.</span><span class="sxs-lookup"><span data-stu-id="e3187-160">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="e3187-161">Non è consigliabile usare record A perché l'indirizzo VIP può cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3187-161">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="delete-all-resources"></a><span data-ttu-id="e3187-162">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="e3187-162">Delete all resources</span></span>

<span data-ttu-id="e3187-163">Per eliminare tutte le risorse create nell'esecuzione dell'esercizio, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e3187-163">To delete all resources created in this article, complete the following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="e3187-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3187-164">Next steps</span></span>

<span data-ttu-id="e3187-165">Per informazioni su come creare probe di integrità personalizzati, vedere [Creare un probe personalizzato per un gateway applicazione con il portale](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e3187-165">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="e3187-166">Per informazioni su come configurare l'offload SSL ed evitare costose attività di decrittografia SSL nei server Web, vedere [Configurare un gateway applicazione per l'offload SSL con Azure Resource Manager](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="e3187-166">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
