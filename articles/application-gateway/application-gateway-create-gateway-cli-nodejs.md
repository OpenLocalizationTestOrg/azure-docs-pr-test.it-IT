---
title: Creare un gateway applicazione di Azure - Interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Informazioni su come creare un gateway applicazione usando l'interfaccia della riga di comando di Azure 1.0 in Resource Manager
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: e7b16e789e0f241aa8ca2292aacb2bccde8777ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli"></a><span data-ttu-id="06acf-103">Creare un gateway applicazione con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="06acf-103">Create an application gateway by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="06acf-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="06acf-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="06acf-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="06acf-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="06acf-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="06acf-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="06acf-107">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="06acf-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="06acf-108">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="06acf-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="06acf-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="06acf-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="06acf-110">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="06acf-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="06acf-111">Fornisce richieste HTTP con routing delle prestazioni e failover tra server diversi, sia nel cloud che in locale.</span><span class="sxs-lookup"><span data-stu-id="06acf-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="06acf-112">Il gateway applicazione offre le seguenti funzionalità di distribuzione delle applicazioni: bilanciamento del carico HTTP, affinità di sessione basata sui cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati e supporto per più siti.</span><span class="sxs-lookup"><span data-stu-id="06acf-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-the-azure-cli"></a><span data-ttu-id="06acf-113">Prerequisito: installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="06acf-113">Prerequisite: Install the Azure CLI</span></span>

<span data-ttu-id="06acf-114">Per eseguire i passaggi in questo articolo, è necessario [installare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows (interfaccia della riga di comando di Azure)](../xplat-cli-install.md) ed è necessario [accedere ad Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="06acf-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="06acf-115">Se non si dispone di un account Azure, è necessario procurarsene uno.</span><span class="sxs-lookup"><span data-stu-id="06acf-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="06acf-116">Usare la [versione di valutazione gratuita](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="06acf-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="06acf-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="06acf-117">Scenario</span></span>

<span data-ttu-id="06acf-118">Questo scenario mostra come creare un gateway applicazione usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="06acf-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="06acf-119">Questo scenario illustrerà come:</span><span class="sxs-lookup"><span data-stu-id="06acf-119">This scenario will:</span></span>

* <span data-ttu-id="06acf-120">Creare un gateway applicazione Medium con due istanze.</span><span class="sxs-lookup"><span data-stu-id="06acf-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="06acf-121">Creare una rete virtuale denominata ContosoVNET con un blocco CIDR riservato di 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="06acf-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="06acf-122">Creare una subnet denominata subnet01 che usa 10.0.0.0/28 come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="06acf-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="06acf-123">La configurazione aggiuntiva del gateway applicazione, che include i probe di integrità personalizzati, gli indirizzi del pool back-end e le regole aggiuntive, viene definita dopo la configurazione del gateway applicazione e non durante la distribuzione iniziale.</span><span class="sxs-lookup"><span data-stu-id="06acf-123">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="06acf-124">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="06acf-124">Before you begin</span></span>

<span data-ttu-id="06acf-125">Il gateway applicazione di Azure richiede una propria subnet.</span><span class="sxs-lookup"><span data-stu-id="06acf-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="06acf-126">Quando si crea una rete virtuale, assicurarsi di lasciare uno spazio indirizzi sufficiente per più subnet.</span><span class="sxs-lookup"><span data-stu-id="06acf-126">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="06acf-127">Dopo che un gateway applicazione è stato distribuito in una subnet, alla subnet possono essere aggiunti solo altri gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="06acf-127">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="06acf-128">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="06acf-128">Log in to Azure</span></span>

<span data-ttu-id="06acf-129">Aprire il **prompt dei comandi di Microsoft Azure**ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="06acf-129">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="06acf-130">Dopo avere digitato l'esempio precedente, viene fornito un codice.</span><span class="sxs-lookup"><span data-stu-id="06acf-130">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="06acf-131">Passare a https://aka.ms/devicelogin in un browser per continuare il processo di accesso.</span><span class="sxs-lookup"><span data-stu-id="06acf-131">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![Comando che illustra l'accesso al dispositivo][1]

<span data-ttu-id="06acf-133">Nel browser immettere il codice ricevuto.</span><span class="sxs-lookup"><span data-stu-id="06acf-133">In the browser, enter the code you received.</span></span> <span data-ttu-id="06acf-134">Si verrà reindirizzati a una pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="06acf-134">You are redirected to a sign-in page.</span></span>

![Browser in cui immettere il codice][2]

<span data-ttu-id="06acf-136">Dopo avere immesso il codice ed effettuato l'accesso, chiudere il browser per continuare con lo scenario.</span><span class="sxs-lookup"><span data-stu-id="06acf-136">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![Accesso eseguito][3]

## <a name="switch-to-resource-manager-mode"></a><span data-ttu-id="06acf-138">Passare alla modalità Resource Manager</span><span class="sxs-lookup"><span data-stu-id="06acf-138">Switch to Resource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-the-resource-group"></a><span data-ttu-id="06acf-139">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="06acf-139">Create the resource group</span></span>

<span data-ttu-id="06acf-140">Prima di creare il gateway applicazione viene creato un gruppo di risorse che contenga il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="06acf-140">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="06acf-141">Di seguito è riportato il comando.</span><span class="sxs-lookup"><span data-stu-id="06acf-141">The following shows the command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="06acf-142">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="06acf-142">Create a virtual network</span></span>

<span data-ttu-id="06acf-143">Dopo aver creato il gruppo di risorse, viene creata una rete virtuale per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="06acf-143">Once the resource group is created, a virtual network is created for the application gateway.</span></span>  <span data-ttu-id="06acf-144">Nell'esempio seguente, lo spazio degli indirizzi era 10.0.0.0/16 come definito nelle note sullo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="06acf-144">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="06acf-145">Creare una subnet</span><span class="sxs-lookup"><span data-stu-id="06acf-145">Create a subnet</span></span>

<span data-ttu-id="06acf-146">Dopo aver creato la rete virtuale, viene aggiunta una subnet per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="06acf-146">After the virtual network is created, a subnet is added for the application gateway.</span></span>  <span data-ttu-id="06acf-147">Se si intende usare il gateway applicazione con un'app Web ospitata nella stessa rete virtuale del gateway applicazione, assicurarsi di lasciare spazio sufficiente per un'altra subnet.</span><span class="sxs-lookup"><span data-stu-id="06acf-147">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="06acf-148">Creare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="06acf-148">Create the application gateway</span></span>

<span data-ttu-id="06acf-149">Dopo aver creato la rete virtuale e la subnet, i prerequisiti per il gateway applicazione sono soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="06acf-149">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="06acf-150">Per il passaggio seguente sono necessari anche un certificato PFX esportato prima e la password del certificato. Gli indirizzi IP usati per il back-end sono gli indirizzi IP per il server back-end.</span><span class="sxs-lookup"><span data-stu-id="06acf-150">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="06acf-151">Questi valori possono essere indirizzi IP privati nella rete virtuale, indirizzi IP pubblici o nomi di dominio completi per i server back-end.</span><span class="sxs-lookup"><span data-stu-id="06acf-151">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="06acf-152">Per un elenco di parametri che possono essere specificati durante la creazione, eseguire questo comando: **azure network application-gateway create --help**.</span><span class="sxs-lookup"><span data-stu-id="06acf-152">For a list of parameters that can be provided during creation run the following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="06acf-153">Questo esempio crea un gateway applicazione di base con le impostazioni predefinite per il listener, il pool back-end, le impostazioni HTTP back-end e le regole.</span><span class="sxs-lookup"><span data-stu-id="06acf-153">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="06acf-154">Queste impostazioni possono essere modificate in base alla propria distribuzione dopo che è stato completato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="06acf-154">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="06acf-155">Se l'applicazione Web è già stata definita con il pool back-end nei passaggi precedenti, dopo la creazione, inizia il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="06acf-155">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06acf-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06acf-156">Next steps</span></span>

<span data-ttu-id="06acf-157">Per informazioni su come creare probe di integrità personalizzati, vedere [Creare un probe personalizzato per un gateway applicazione con il portale](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="06acf-157">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="06acf-158">Per informazioni su come configurare l'offload SSL ed evitare costose attività di decrittografia SSL nei server Web, vedere [Configurare un gateway applicazione per l'offload SSL con Azure Resource Manager](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="06acf-158">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
