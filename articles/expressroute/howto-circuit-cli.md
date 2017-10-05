---
title: 'Creare e modificare un circuito Azure ExpressRoute: interfaccia della riga di comando | Microsoft Docs'
description: Questo articolo descrive le procedure di creazione, provisioning, verifica, aggiornamento, eliminazione e deprovisioning di un circuito ExpressRoute tramite l'interfaccia della riga di comando.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 1a1c9a96b772868e2c832e9ff57874038c0db2d4
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="c2c71-103">Creare e modificare un circuito ExpressRoute tramite l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="c2c71-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="c2c71-104">Questo articolo descrive la procedura di creazione di un circuito di Azure ExpressRoute usando l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="c2c71-104">This article describes how to create an Azure ExpressRoute circuit by using the Command Line Interface (CLI).</span></span> <span data-ttu-id="c2c71-105">Questo articolo descrive anche come controllare lo stato, eseguire l'aggiornamento o effettuare l'eliminazione e il deprovisioning di un circuito.</span><span class="sxs-lookup"><span data-stu-id="c2c71-105">This article also shows you how to check the status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="c2c71-106">Se si vuole usare un metodo diverso per operare con circuiti ExpressRoute, è possibile selezionare l'articolo appropriato nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-106">If you want to use a different method to work with ExpressRoute circuits, you can select the article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2c71-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c2c71-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="c2c71-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2c71-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="c2c71-109">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c2c71-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="c2c71-110">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c2c71-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="c2c71-111">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="c2c71-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="c2c71-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c2c71-112">Before you begin</span></span>

* <span data-ttu-id="c2c71-113">Prima di iniziare, installare la versione più recente dei comandi dell'interfaccia della riga di comando (2.0 o successiva).</span><span class="sxs-lookup"><span data-stu-id="c2c71-113">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="c2c71-114">Per informazioni sull'installazione dei comandi dell'interfaccia della riga di comando, vedere [Install Azure CLI 2.0](/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0) e [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) (Introduzione all'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="c2c71-114">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="c2c71-115">Prima di iniziare la configurazione, verificare i [prerequisiti](expressroute-prerequisites.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="c2c71-115">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="c2c71-116">Creare un circuito ExpressRoute ed eseguirne il provisioning</span><span class="sxs-lookup"><span data-stu-id="c2c71-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="c2c71-117">1. Accedere al proprio account Azure e selezionare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="c2c71-117">1. Sign in to your Azure account and select your subscription</span></span>

<span data-ttu-id="c2c71-118">Per iniziare la configurazione, accedere al proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="c2c71-118">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="c2c71-119">Per eseguire la connessione, usare gli esempi che seguono:</span><span class="sxs-lookup"><span data-stu-id="c2c71-119">Use the following examples to help you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="c2c71-120">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="c2c71-120">Check the subscriptions for the account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="c2c71-121">Selezionare la sottoscrizione per la quale si vuole creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2c71-121">Select the subscription for which you want to create an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="c2c71-122">2. Ottenere l'elenco dei provider, delle località e delle larghezze di banda supportate</span><span class="sxs-lookup"><span data-stu-id="c2c71-122">2. Get the list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="c2c71-123">Prima di creare un circuito ExpressRoute, è necessario avere l'elenco delle località, delle opzioni di larghezza di banda e dei provider di connettività supportati.</span><span class="sxs-lookup"><span data-stu-id="c2c71-123">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="c2c71-124">Il comando 'az network express-route list-service-providers' dell'interfaccia della riga di comando restituisce queste informazioni, che verranno usate nei passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="c2c71-124">The CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="c2c71-125">La risposta restituita è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-125">The response is similar to the following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="c2c71-126">Controllare la riposta per verificare se è presente il proprio provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="c2c71-126">Check the response to see if your connectivity provider is listed.</span></span> <span data-ttu-id="c2c71-127">Prendere nota delle informazioni seguenti, perché saranno necessarie al momento della creazione di un circuito:</span><span class="sxs-lookup"><span data-stu-id="c2c71-127">Make a note of the following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="c2c71-128">Nome</span><span class="sxs-lookup"><span data-stu-id="c2c71-128">Name</span></span>
* <span data-ttu-id="c2c71-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="c2c71-129">PeeringLocations</span></span>
* <span data-ttu-id="c2c71-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="c2c71-130">BandwidthsOffered</span></span>

<span data-ttu-id="c2c71-131">È ora possibile creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2c71-131">You're now ready to create an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="c2c71-132">3. Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c71-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2c71-133">Il circuito ExpressRoute viene addebitato dal momento in cui viene emessa una chiave di servizio.</span><span class="sxs-lookup"><span data-stu-id="c2c71-133">Your ExpressRoute circuit is billed from the moment a service key is issued.</span></span> <span data-ttu-id="c2c71-134">Eseguire l'operazione quando il provider di connettività è pronto a effettuare il provisioning del circuito.</span><span class="sxs-lookup"><span data-stu-id="c2c71-134">Perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="c2c71-135">Se non si ha già un gruppo di risorse, è necessario crearne uno prima di creare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2c71-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="c2c71-136">È possibile creare un gruppo di risorse eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-136">You can create a resource group by running the following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="c2c71-137">L'esempio seguente illustra come creare un circuito ExpressRoute a 200 Mbps tramite Equinix nella Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="c2c71-137">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="c2c71-138">Se si usa un altro provider e impostazioni diverse, sostituire tali informazioni al momento della richiesta.</span><span class="sxs-lookup"><span data-stu-id="c2c71-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="c2c71-139">Verificare di aver specificato il livello e la famiglia SKU corretti:</span><span class="sxs-lookup"><span data-stu-id="c2c71-139">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="c2c71-140">Il livello SKU determina se deve essere abilitato il componente aggiuntivo ExpressRoute Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="c2c71-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="c2c71-141">È possibile specificare 'Standard' per ottenere lo SKU Standard o 'Premium' per il componente aggiuntivo Premium.</span><span class="sxs-lookup"><span data-stu-id="c2c71-141">You can specify 'Standard' to get the standard SKU or 'Premium' for the premium add-on.</span></span>
* <span data-ttu-id="c2c71-142">La famiglia SKU determina il tipo di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="c2c71-142">SKU family determines the billing type.</span></span> <span data-ttu-id="c2c71-143">Specificare 'Metereddata' per un piano dati a consumo e 'Unlimiteddata' per un piano dati senza limiti.</span><span class="sxs-lookup"><span data-stu-id="c2c71-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="c2c71-144">È possibile modificare il tipo di fatturazione da 'Metereddata' a 'Unlimiteddata', ma non è possibile eseguire il passaggio inverso.</span><span class="sxs-lookup"><span data-stu-id="c2c71-144">You can change the billing type from 'Metereddata' to 'Unlimiteddata', but you can't change the type from 'Unlimiteddata' to 'Metereddata'.</span></span>


<span data-ttu-id="c2c71-145">Il circuito ExpressRoute viene addebitato dal momento in cui viene emessa una chiave di servizio.</span><span class="sxs-lookup"><span data-stu-id="c2c71-145">Your ExpressRoute circuit is billed from the moment a service key is issued.</span></span> <span data-ttu-id="c2c71-146">Di seguito è riportato un esempio di richiesta di una nuova chiave di servizio:</span><span class="sxs-lookup"><span data-stu-id="c2c71-146">The following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="c2c71-147">La risposta contiene la chiave di servizio.</span><span class="sxs-lookup"><span data-stu-id="c2c71-147">The response contains the service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="c2c71-148">4. Elencare tutti i circuiti ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c71-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="c2c71-149">Per ottenere un elenco di tutti i circuiti ExpressRoute creati, eseguire il comando 'az network express-route list'.</span><span class="sxs-lookup"><span data-stu-id="c2c71-149">To get a list of all the ExpressRoute circuits that you created, run the 'az network express-route list' command.</span></span> <span data-ttu-id="c2c71-150">È possibile recuperare queste informazioni in qualsiasi momento usando questo comando.</span><span class="sxs-lookup"><span data-stu-id="c2c71-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="c2c71-151">Per ottenere un elenco di tutti i circuiti, effettuare la chiamata senza parametri.</span><span class="sxs-lookup"><span data-stu-id="c2c71-151">To list all circuits, make the call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="c2c71-152">La chiave di servizio è indicata nel campo *ServiceKey* della risposta.</span><span class="sxs-lookup"><span data-stu-id="c2c71-152">Your service key is listed in the *ServiceKey* field of the response.</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="c2c71-153">È possibile ottenere descrizioni dettagliate di tutti i parametri eseguendo il comando con il parametro '-h'.</span><span class="sxs-lookup"><span data-stu-id="c2c71-153">You can get detailed descriptions of all the parameters by running the command using the '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="c2c71-154">5. Inviare la chiave di servizio al provider di connettività per il provisioning</span><span class="sxs-lookup"><span data-stu-id="c2c71-154">5. Send the service key to your connectivity provider for provisioning</span></span>

<span data-ttu-id="c2c71-155">'ServiceProviderProvisioningState' offre informazioni sullo stato di provisioning corrente sul lato provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="c2c71-155">'ServiceProviderProvisioningState' provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="c2c71-156">Le informazioni di stato indicano lo stato sul lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c2c71-156">The status provides the state on the Microsoft side.</span></span> <span data-ttu-id="c2c71-157">Per altre informazioni, vedere [l'articolo sui flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="c2c71-157">For more information, see the [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="c2c71-158">Quando si crea un nuovo circuito ExpressRoute, il circuito ha lo stato seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-158">When you create a new ExpressRoute circuit, the circuit is in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="c2c71-159">Il circuito passa allo stato seguente quando è in corso l'abilitazione da parte del provider di connettività:</span><span class="sxs-lookup"><span data-stu-id="c2c71-159">The circuit changes to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="c2c71-160">Per poterlo usare, un circuito ExpressRoute deve avere lo stato seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-160">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="c2c71-161">6. Controllare periodicamente lo stato e la condizione della chiave del circuito</span><span class="sxs-lookup"><span data-stu-id="c2c71-161">6. Periodically check the status and the state of the circuit key</span></span>

<span data-ttu-id="c2c71-162">La verifica dello stato e della condizione della chiave del circuito comunicano all'utente quando il provider ha abilitato il circuito.</span><span class="sxs-lookup"><span data-stu-id="c2c71-162">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="c2c71-163">Dopo la configurazione del circuito, lo stato di 'ServiceProviderProvisioningState' visualizzato è 'Provisioned', come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-163">After the circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in the following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="c2c71-164">La risposta restituita è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-164">The response is similar to the following example:</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="c2c71-165">7. Creare la configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="c2c71-165">7. Create your routing configuration</span></span>

<span data-ttu-id="c2c71-166">Per istruzioni dettagliate, vedere l'articolo relativo alla [configurazione del routing per un circuito ExpressRoute](howto-routing-cli.md) per creare e modificare i peering del circuito.</span><span class="sxs-lookup"><span data-stu-id="c2c71-166">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](howto-routing-cli.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2c71-167">Queste istruzioni si applicano solo ai circuiti creati con provider di servizi che offrono servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="c2c71-167">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="c2c71-168">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito una VPN IP, come MPLS), il provider di connettività configura e gestisce il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c2c71-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="c2c71-169">8. Collegare una rete virtuale a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c71-169">8. Link a virtual network to an ExpressRoute circuit</span></span>

<span data-ttu-id="c2c71-170">Collegare quindi una rete virtuale al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2c71-170">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="c2c71-171">Fare riferimento all'articolo [Collegare una rete virtuale a un circuito ExpressRoute](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c2c71-171">Use the [Linking virtual networks to ExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="c2c71-172"><a name="modify"></a>Modifica di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c71-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="c2c71-173">È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.</span><span class="sxs-lookup"><span data-stu-id="c2c71-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="c2c71-174">È possibile apportare le modifiche seguenti senza tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="c2c71-174">You can make the following changes with no downtime:</span></span>

* <span data-ttu-id="c2c71-175">Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2c71-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="c2c71-176">Aumentare la larghezza di banda del circuito ExpressRoute, a condizione che sulla porta sia disponibile capacità.</span><span class="sxs-lookup"><span data-stu-id="c2c71-176">You can increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="c2c71-177">Il downgrade della larghezza di banda di un circuito non è tuttavia supportato.</span><span class="sxs-lookup"><span data-stu-id="c2c71-177">However, downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="c2c71-178">Modificare il piano di misurazione da Dati a consumo a Dati senza limiti.</span><span class="sxs-lookup"><span data-stu-id="c2c71-178">You can change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="c2c71-179">La modifica del piano di misurazione da Dati senza limiti a Dati a consumo non è tuttavia supportata.</span><span class="sxs-lookup"><span data-stu-id="c2c71-179">However, changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="c2c71-180">È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).</span><span class="sxs-lookup"><span data-stu-id="c2c71-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="c2c71-181">Per altre informazioni su limiti e limitazioni, vedere [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="c2c71-181">For more information on limits and limitations, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="c2c71-182">Per abilitare il componente aggiuntivo ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="c2c71-182">To enable the ExpressRoute premium add-on</span></span>

<span data-ttu-id="c2c71-183">È possibile abilitare il componente aggiuntivo ExpressRoute Premium per il circuito esistente usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-183">You can enable the ExpressRoute premium add-on for your existing circuit by using the following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="c2c71-184">Le funzionalità del componente aggiuntivo ExpressRoute Premium sono così abilitate nel circuito.</span><span class="sxs-lookup"><span data-stu-id="c2c71-184">The circuit now has the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="c2c71-185">La fatturazione della funzionalità del componente aggiuntivo Premium inizia non appena il comando viene eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="c2c71-185">We begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="c2c71-186">Per disabilitare il componente aggiuntivo ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="c2c71-186">To disable the ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2c71-187">Questa operazione può avere esito negativo se si usano più risorse di quelle consentite per il circuito standard.</span><span class="sxs-lookup"><span data-stu-id="c2c71-187">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

<span data-ttu-id="c2c71-188">Prima di disabilitare il componente aggiuntivo ExpressRoute Premium, tenere conto dei criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2c71-188">Before disabling the ExpressRoute premium add-on, understand the following criteria:</span></span>

* <span data-ttu-id="c2c71-189">Prima di effettuare il downgrade da Premium a Standard, è necessario assicurarsi che il numero di reti virtuali collegate al circuito sia minore di 10.</span><span class="sxs-lookup"><span data-stu-id="c2c71-189">Before you downgrade from premium to standard, you must make sure that you have fewer than 10 virtual networks linked to the circuit.</span></span> <span data-ttu-id="c2c71-190">Se sono più di 10, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="c2c71-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="c2c71-191">È necessario scollegare tutte le reti virtuali in altre aree geopolitiche.</span><span class="sxs-lookup"><span data-stu-id="c2c71-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="c2c71-192">Se non si scollegano tutte le reti virtuali, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="c2c71-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="c2c71-193">La tabella di route deve includere meno di 4.000 route per il peering privato.</span><span class="sxs-lookup"><span data-stu-id="c2c71-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="c2c71-194">Se le dimensioni della tabella di route sono maggiori di 4.000 route, la sessione BGP viene interrotta.</span><span class="sxs-lookup"><span data-stu-id="c2c71-194">If your route table size is greater than 4,000 routes, the BGP session drops.</span></span> <span data-ttu-id="c2c71-195">La sessione non potrà essere riabilitata fino a quando il numero di prefissi annunciati non diventa inferiore a 4.000.</span><span class="sxs-lookup"><span data-stu-id="c2c71-195">The session won't be reenabled until the number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="c2c71-196">È possibile disabilitare il componente aggiuntivo ExpressRoute Premium per il circuito esistente usando l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-196">You can disable the ExpressRoute premium add-on for the existing circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="c2c71-197">Per aggiornare la larghezza di banda del circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c71-197">To update the ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="c2c71-198">Per le opzioni relative alla larghezza di banda supportate per il provider, vedere [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="c2c71-198">For the supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="c2c71-199">È possibile scegliere qualsiasi dimensione maggiore della dimensione del circuito esistente.</span><span class="sxs-lookup"><span data-stu-id="c2c71-199">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2c71-200">Se la capacità sulla porta esistente non è sufficiente, potrebbe essere necessario ricreare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2c71-200">If there is inadequate capacity on the existing port, you may have to recreate the ExpressRoute circuit.</span></span> <span data-ttu-id="c2c71-201">Il circuito non può essere aggiornato se in tale posizione non è disponibile capacità aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="c2c71-201">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="c2c71-202">Non è possibile ridurre la larghezza di banda di un circuito ExpressRoute senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="c2c71-202">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="c2c71-203">Il downgrade della larghezza di banda richiede il deprovisioning del circuito ExpressRoute e quindi il provisioning di un nuovo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2c71-203">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="c2c71-204">Una volta stabilite le dimensioni necessarie, usare il comando seguente per ridimensionare il circuito:</span><span class="sxs-lookup"><span data-stu-id="c2c71-204">After you decide the size you need, use the following command to resize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="c2c71-205">Il circuito viene ridimensionato su lato di competenza di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c2c71-205">Your circuit is sized up on the Microsoft side.</span></span> <span data-ttu-id="c2c71-206">Sarà poi necessario contattare il provider di connettività perché aggiorni le configurazioni corrispondenti in base a questa modifica.</span><span class="sxs-lookup"><span data-stu-id="c2c71-206">Next, you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="c2c71-207">In seguito alla notifica, Microsoft inizia la fatturazione in base all'opzione relativa alla larghezza di banda aggiornata.</span><span class="sxs-lookup"><span data-stu-id="c2c71-207">After you make this notification, we begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="c2c71-208">Per passare lo SKU dal piano a consumo al piano senza limiti</span><span class="sxs-lookup"><span data-stu-id="c2c71-208">To move the SKU from metered to unlimited</span></span>

<span data-ttu-id="c2c71-209">È possibile modificare lo SKU di un circuito ExpressRoute usando l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c2c71-209">You can change the SKU of an ExpressRoute circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="c2c71-210">Per controllare l'accesso all'ambiente classico e all'ambiente Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c2c71-210">To control access to the classic and Resource Manager environments</span></span>

<span data-ttu-id="c2c71-211">Vedere le istruzioni contenute in [Spostare i circuiti ExpressRoute dal modello di distribuzione classica a quello Resource Manager](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c2c71-211">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="c2c71-212">Deprovisioning ed eliminazione di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c71-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="c2c71-213">Per effettuare il deprovisioning e l'eliminazione di un circuito ExpressRoute, assicurarsi di comprendere i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2c71-213">To deprovision and delete an ExpressRoute circuit, make sure you understand the following criteria:</span></span>

* <span data-ttu-id="c2c71-214">È necessario scollegare tutte le reti virtuali dal circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2c71-214">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="c2c71-215">Se l'operazione non riesce, controllare se sono presenti reti virtuali collegate al circuito.</span><span class="sxs-lookup"><span data-stu-id="c2c71-215">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="c2c71-216">Se lo stato di provisioning del provider del servizio del circuito ExpressRoute è **Provisioning in corso** o **Provisioning eseguito**, è necessario collaborare con il provider di servizi per eseguire il deprovisioning del circuito sul lato del provider.</span><span class="sxs-lookup"><span data-stu-id="c2c71-216">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="c2c71-217">Le risorse continuano a essere riservate e la fatturazione continuerà a essere applicata finché il provider di servizi non avrà completato il deprovisioning del circuito e inviato una notifica a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c2c71-217">We continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="c2c71-218">È possibile eliminare il circuito se il provider del servizio ne ha effettuato il deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="c2c71-218">You can delete the circuit if the service provider has deprovisioned the circuit.</span></span> <span data-ttu-id="c2c71-219">Dopo il deprovisioning di un circuito, lo stato di provisioning del provider di servizio è impostato su **Senza provisioning**.</span><span class="sxs-lookup"><span data-stu-id="c2c71-219">When a circuit is deprovisioned, the service provider provisioning state is set to **Not provisioned**.</span></span> <span data-ttu-id="c2c71-220">Viene così interrotta la fatturazione per il circuito.</span><span class="sxs-lookup"><span data-stu-id="c2c71-220">This stops billing for the circuit.</span></span>

<span data-ttu-id="c2c71-221">È possibile eliminare un circuito ExpressRoute eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="c2c71-221">You can delete your ExpressRoute circuit by running the following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c2c71-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2c71-222">Next steps</span></span>

<span data-ttu-id="c2c71-223">Dopo aver creato il circuito, verificare di eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2c71-223">After you create your circuit, make sure that you do the following tasks:</span></span>

* [<span data-ttu-id="c2c71-224">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c71-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="c2c71-225">Collegare la rete virtuale al circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c71-225">Link your virtual network to your ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)