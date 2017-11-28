---
title: aaaCreate un Gateway di applicazione di Azure - CLI di Azure 1.0 | Documenti Microsoft
description: Informazioni su come toocreate un Gateway applicazione utilizzando hello Azure CLI 1.0 in Gestione risorse
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
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="8d0f7-103">Creare un gateway applicazione hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="8d0f7-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8d0f7-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8d0f7-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="8d0f7-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8d0f7-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="8d0f7-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="8d0f7-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="8d0f7-107">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8d0f7-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="8d0f7-108">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="8d0f7-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="8d0f7-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8d0f7-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="8d0f7-110">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="8d0f7-111">Fornisce il failover, le prestazioni di routing di richieste HTTP tra server diversi, che si trovino in locale o cloud hello.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="8d0f7-112">Gateway applicazione ha seguendo le funzionalità di recapito dell'applicazione hello: caricare probe di integrità personalizzato di bilanciamento del carico, l'affinità di sessione basato su cookie e offload Secure Sockets Layer (SSL), HTTP e il supporto per più siti.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="8d0f7-113">Prerequisito: Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="8d0f7-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="8d0f7-114">hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](../xplat-cli-install.md) ed è necessario troppo[accedere tooAzure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8d0f7-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="8d0f7-115">Se non si dispone di un account Azure, è necessario procurarsene uno.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="8d0f7-116">Usare la [versione di valutazione gratuita](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="8d0f7-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="8d0f7-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="8d0f7-117">Scenario</span></span>

<span data-ttu-id="8d0f7-118">In questo scenario viene illustrato come gateway un'applicazione utilizzando toocreate hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="8d0f7-119">Questo scenario illustrerà come:</span><span class="sxs-lookup"><span data-stu-id="8d0f7-119">This scenario will:</span></span>

* <span data-ttu-id="8d0f7-120">Creare un gateway applicazione Medium con due istanze.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="8d0f7-121">Creare una rete virtuale denominata ContosoVNET con un blocco CIDR riservato di 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="8d0f7-122">Creare una subnet denominata subnet01 che usa 10.0.0.0/28 come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="8d0f7-123">Le ricerche di configurazione aggiuntiva di gateway applicazione hello, inclusi stato personalizzato, gli indirizzi del pool back-end e regole aggiuntive vengono configurati dopo la configurazione di gateway applicazione hello e non durante la distribuzione iniziale.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8d0f7-124">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8d0f7-124">Before you begin</span></span>

<span data-ttu-id="8d0f7-125">Il gateway applicazione di Azure richiede una propria subnet.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="8d0f7-126">Quando si crea una rete virtuale, assicurarsi di lasciare sufficiente toohave spazio di indirizzi più subnet.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="8d0f7-127">Dopo aver distribuito una subnet tooa di gateway applicazione, gateway di applicazione solo aggiuntive sono in grado di toobe aggiunto toohello subnet.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="8d0f7-128">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="8d0f7-128">Log in tooAzure</span></span>

<span data-ttu-id="8d0f7-129">Aprire hello **prompt dei comandi di Microsoft Azure**ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="8d0f7-130">Una volta digitato hello sopra riportato, viene fornito un codice.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="8d0f7-131">Spostarsi in un processo di accesso browser hello toocontinue toohttps://aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![Comando che illustra l'accesso al dispositivo][1]

<span data-ttu-id="8d0f7-133">Nel browser hello immettere codice hello ricevuto.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="8d0f7-134">Si è reindirizzato tooa nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-134">You are redirected tooa sign-in page.</span></span>

![codice tooenter browser][2]

<span data-ttu-id="8d0f7-136">Dopo aver immesso il codice hello si è connessi, hello Chiudi browser toocontinue scenario hello.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![Accesso eseguito][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="8d0f7-138">Passare tooResource modalità di gestione</span><span class="sxs-lookup"><span data-stu-id="8d0f7-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="8d0f7-139">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="8d0f7-139">Create hello resource group</span></span>

<span data-ttu-id="8d0f7-140">Prima di creare i gateway applicazione hello, un gruppo di risorse viene creato toocontain gateway di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="8d0f7-141">Hello seguito è riportato il comando hello.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="8d0f7-142">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8d0f7-142">Create a virtual network</span></span>

<span data-ttu-id="8d0f7-143">Una volta creato il gruppo di risorse hello, viene creata una rete virtuale per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="8d0f7-144">Nell'esempio seguente di hello, spazio degli indirizzi di hello era come 10.0.0.0/16 come definito in hello note scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="8d0f7-145">Creare una subnet</span><span class="sxs-lookup"><span data-stu-id="8d0f7-145">Create a subnet</span></span>

<span data-ttu-id="8d0f7-146">Dopo aver creata la rete virtuale hello, viene aggiunta una subnet per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="8d0f7-147">Se si prevede di gateway applicazione toouse con un'app web ospitato in hello stesso virtuale come gateway applicazione hello di rete, tooleave che lo spazio sia sufficiente per un'altra subnet.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="8d0f7-148">Creare il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="8d0f7-148">Create hello application gateway</span></span>

<span data-ttu-id="8d0f7-149">Dopo aver creati la rete virtuale hello e subnet, siano soddisfatti i prerequisiti per il gateway applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="8d0f7-150">Inoltre, una password di hello e di certificato PFX esportato in precedenza per il certificato di hello sono richieste per hello seguente passaggio: hello indirizzi utilizzati per back-end hello sono gli indirizzi IP hello del server back-end.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="8d0f7-151">Questi valori possono essere entrambi indirizzi IP privati nella rete virtuale hello, gli indirizzi IP pubblici o nomi di dominio completo per i server back-end.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

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
> <span data-ttu-id="8d0f7-152">Per un elenco di parametri che possono essere forniti durante la creazione eseguire hello comando seguente: **creare applicazione-gateway di rete di azure - Guida**.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="8d0f7-153">Questo esempio crea un gateway applicazione basic con le impostazioni predefinite per il listener hello, pool back-end, le impostazioni http back-end e regole.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="8d0f7-154">È possibile modificare la distribuzione toosuit queste impostazioni dopo il provisioning di hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="8d0f7-155">Se si dispone già di un'applicazione web definita con il pool back-end hello in hello precedenti passaggi, una volta creati, il bilanciamento del carico ha inizio.</span><span class="sxs-lookup"><span data-stu-id="8d0f7-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d0f7-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8d0f7-156">Next steps</span></span>

<span data-ttu-id="8d0f7-157">Informazioni su come probe di integrità personalizzato toocreate visitando [per creare un probe di integrità personalizzato](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8d0f7-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="8d0f7-158">Informazioni su come tooconfigure offload SSL e la decrittografia SSL costosa di intraprendere hello off i server web, visitare il sito [configurare Offload SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="8d0f7-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
