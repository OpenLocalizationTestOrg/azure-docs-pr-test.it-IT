---
title: 'Creare e modificare un circuito Azure ExpressRoute: interfaccia della riga di comando | Microsoft Docs'
description: In questo articolo viene descritto come toocreate, eseguire il provisioning, verificare, aggiornare, eliminare e il deprovisioning di un circuito ExpressRoute tramite CLI.
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
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="a7ab0-103">Creare e modificare un circuito ExpressRoute tramite l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="a7ab0-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="a7ab0-104">In questo articolo viene descritto come toocreate un circuito ExpressRoute di Azure tramite hello interfaccia della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="a7ab0-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="a7ab0-105">Mostra anche come stato hello toocheck, aggiornare, o eliminare e il deprovisioning di un circuito.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="a7ab0-106">Se si desidera toouse toowork un metodo diverso con circuiti ExpressRoute, è possibile selezionare l'articolo hello da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7ab0-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a7ab0-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="a7ab0-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7ab0-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="a7ab0-109">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a7ab0-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="a7ab0-110">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a7ab0-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="a7ab0-111">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="a7ab0-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="a7ab0-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a7ab0-112">Before you begin</span></span>

* <span data-ttu-id="a7ab0-113">Prima di iniziare, installare hello versione i comandi CLI hello (2.0 o versione successivo).</span><span class="sxs-lookup"><span data-stu-id="a7ab0-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="a7ab0-114">Per informazioni sull'installazione di comandi CLI hello, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli) e [Introduzione a Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a7ab0-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="a7ab0-115">Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="a7ab0-116">Creare un circuito ExpressRoute ed eseguirne il provisioning</span><span class="sxs-lookup"><span data-stu-id="a7ab0-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="a7ab0-117">1. Accedi tooyour account Azure e selezionare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="a7ab0-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="a7ab0-118">toobegin della configurazione, accedi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="a7ab0-119">Hello seguenti esempi toohelp che ci si connette, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="a7ab0-120">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="a7ab0-121">Selezionare la sottoscrizione di hello per cui si desidera toocreate un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="a7ab0-122">2. Ottenere l'elenco di hello di provider supportati, posizioni e delle larghezze di banda</span><span class="sxs-lookup"><span data-stu-id="a7ab0-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="a7ab0-123">Prima di creare un circuito ExpressRoute, è necessario l'elenco di hello del provider di connettività supportate, località e le opzioni di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="a7ab0-124">Hello CLI comando 'az express route elenco-servizio-provider di rete' Restituisce queste informazioni, che verranno usati nei passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="a7ab0-125">risposta Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-125">hello response is similar toohello following example:</span></span>

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

<span data-ttu-id="a7ab0-126">Controllare hello risposta toosee se è elencato il provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="a7ab0-127">Prendere nota di hello informazioni, è necessario quando si crea un circuito di seguito:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="a7ab0-128">Nome</span><span class="sxs-lookup"><span data-stu-id="a7ab0-128">Name</span></span>
* <span data-ttu-id="a7ab0-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="a7ab0-129">PeeringLocations</span></span>
* <span data-ttu-id="a7ab0-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="a7ab0-130">BandwidthsOffered</span></span>

<span data-ttu-id="a7ab0-131">Si è ora pronto toocreate un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="a7ab0-132">3. Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7ab0-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7ab0-133">Il circuito ExpressRoute viene fatturato dall'istante hello che viene eseguita una chiave del servizio.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="a7ab0-134">Eseguire questa operazione quando il provider di connettività hello è circuito hello tooprovision pronto.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="a7ab0-135">Se non si ha già un gruppo di risorse, è necessario crearne uno prima di creare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="a7ab0-136">È possibile creare un gruppo di risorse eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="a7ab0-137">Hello di esempio seguente viene illustrato come un ExpressRoute a 200 Mbps toocreate circuit tramite Equinix Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="a7ab0-138">Se si usa un altro provider e impostazioni diverse, sostituire tali informazioni al momento della richiesta.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="a7ab0-139">Assicurarsi di specificare hello corretto dello SKU e famiglia di SKU:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="a7ab0-140">Il livello SKU determina se deve essere abilitato il componente aggiuntivo ExpressRoute Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="a7ab0-141">È possibile specificare 'Standard' tooget hello SKU standard o 'Premium' per il componente aggiuntivo di hello premium.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="a7ab0-142">Famiglia di SKU determina tipo fatturazione hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="a7ab0-143">Specificare 'Metereddata' per un piano dati a consumo e 'Unlimiteddata' per un piano dati senza limiti.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="a7ab0-144">È possibile modificare il tipo fatturazione di hello da 'Metereddata 'too'Unlimiteddata', ma è possibile modificare il tipo di hello da too'Metereddata 'Unlimiteddata' '.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="a7ab0-145">Il circuito ExpressRoute viene fatturato dall'istante hello che viene eseguita una chiave del servizio.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="a7ab0-146">Hello di esempio seguente è una richiesta per una nuova chiave di servizio:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="a7ab0-147">risposta Hello contiene una chiave del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="a7ab0-148">4. Elencare tutti i circuiti ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7ab0-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="a7ab0-149">tooget un elenco di tutti i circuiti ExpressRoute hello creato, eseguire il comando di 'list express route di rete az' hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="a7ab0-150">È possibile recuperare queste informazioni in qualsiasi momento usando questo comando.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="a7ab0-151">toolist tutti i circuiti, effettuare hello chiamata senza parametri.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="a7ab0-152">La chiave del servizio è elencata nella hello *ServiceKey* campo della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

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

<span data-ttu-id="a7ab0-153">È possibile ottenere una descrizione dettagliata di tutti i parametri di hello comando hello utilizzando hello '-h' parametro.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="a7ab0-154">5. Inviare i provider di connettività di hello servizio tooyour chiave per il provisioning</span><span class="sxs-lookup"><span data-stu-id="a7ab0-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="a7ab0-155">'ServiceProviderProvisioningState' vengono fornite informazioni sullo stato corrente di hello del provisioning sul lato di provider di servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="a7ab0-156">stato Hello fornisce lo stato di hello in hello lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="a7ab0-157">Per ulteriori informazioni, vedere hello [articolo flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="a7ab0-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="a7ab0-158">Quando si crea un nuovo circuito ExpressRoute, hello circuito si trova in hello seguente stato:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="a7ab0-159">circuito Hello modifica toohello seguente lo stato quando il provider di connettività hello è in corso di hello di abilitarlo per l'utente:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="a7ab0-160">Per è toobe in grado di toouse un circuito ExpressRoute, deve essere nel seguente stato hello:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="a7ab0-161">6. Controllare periodicamente hello stato della chiave circuito hello e hello</span><span class="sxs-lookup"><span data-stu-id="a7ab0-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="a7ab0-162">Controllo stato hello della chiave circuito hello e hello consente di sapere quando il circuito viene abilitato il provider.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="a7ab0-163">Dopo aver configurato il circuito hello, 'ServiceProviderProvisioningState' viene visualizzato come "Provisioning eseguito", come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="a7ab0-164">risposta Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-164">hello response is similar toohello following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="a7ab0-165">7. Creare la configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="a7ab0-165">7. Create your routing configuration</span></span>

<span data-ttu-id="a7ab0-166">Per istruzioni dettagliate, vedere hello [configurazione del routing circuito ExpressRoute](howto-routing-cli.md) toocreate dell'articolo e modificare peering di circuito.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7ab0-167">Queste istruzioni si applicano solo toocircuits creati con i provider di servizi che offrono servizi di livello 2 di connettività.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="a7ab0-168">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito una VPN IP, come MPLS), il provider di connettività configura e gestisce il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="a7ab0-169">8. Collegare un circuito ExpressRoute di tooan rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a7ab0-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="a7ab0-170">Successivamente, collegare un circuito ExpressRoute di tooyour rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="a7ab0-171">Hello utilizzare [collegamento virtuale reti circuiti tooExpressRoute](howto-linkvnet-cli.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="a7ab0-172"><a name="modify"></a>Modifica di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7ab0-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="a7ab0-173">È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="a7ab0-174">È possibile apportare hello dopo le modifiche senza tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="a7ab0-175">Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="a7ab0-176">È possibile aumentare la larghezza di banda hello del circuito ExpressRoute purché vi sia la capacità disponibile sulla porta hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="a7ab0-177">Tuttavia, non è supportato il downgrade della larghezza di banda hello di un circuito.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="a7ab0-178">È possibile modificare piano controllo hello da dati a consumo tooUnlimited dati.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="a7ab0-179">Tuttavia, la modifica hello misurazione piano da dati senza limiti tooMetered che dati non è supportata.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="a7ab0-180">È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).</span><span class="sxs-lookup"><span data-stu-id="a7ab0-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="a7ab0-181">Per ulteriori informazioni su limiti e limitazioni, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a7ab0-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="a7ab0-182">componente aggiuntivo di tooenable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="a7ab0-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="a7ab0-183">È possibile abilitare il componente aggiuntivo di hello ExpressRoute premium per il circuito esistente utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="a7ab0-184">circuito Hello dispone ora di funzionalità aggiuntive di hello ExpressRoute premium abilitata.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="a7ab0-185">Per iniziare, si fatturazione per la funzionalità di componente aggiuntivo di hello premium come comando hello è stata eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="a7ab0-186">componente aggiuntivo di toodisable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="a7ab0-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7ab0-187">Questa operazione può non riuscire se si utilizza le risorse che sono maggiori di ciò che è consentito per il circuito standard hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="a7ab0-188">Prima di disabilitare i componenti aggiuntivi di hello ExpressRoute premium, comprendere hello seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="a7ab0-189">Prima effettuare il downgrade da premium toostandard, assicurarsi di disporre di meno di 10 reti virtuali collegate toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="a7ab0-190">Se sono più di 10, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="a7ab0-191">È necessario scollegare tutte le reti virtuali in altre aree geopolitiche.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="a7ab0-192">Se non si scollegano tutte le reti virtuali, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="a7ab0-193">La tabella di route deve includere meno di 4.000 route per il peering privato.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="a7ab0-194">Se le dimensioni di tabella di route sono maggiore di 4.000 route, sessione BGP hello Elimina.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="a7ab0-195">non verrà riabilitata sessione Hello fino a quando il numero di hello di prefissi annunciati è inferiore a 4.000.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="a7ab0-196">È possibile disabilitare componente aggiuntivo di hello ExpressRoute premium per il circuito esistente hello utilizzando hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="a7ab0-197">larghezza di banda circuito ExpressRoute hello tooupdate</span><span class="sxs-lookup"><span data-stu-id="a7ab0-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="a7ab0-198">Per le opzioni di larghezza di banda hello è supportato per il provider, controllare hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a7ab0-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="a7ab0-199">È possibile scegliere qualsiasi dimensione maggiore della dimensione hello del circuito esistente.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7ab0-200">Se sulla porta esistente hello capacità insufficiente, è possibile circuito ExpressRoute di toorecreate hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="a7ab0-201">Se non è presente capacità aggiuntive disponibili in tale posizione non è possibile aggiornare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="a7ab0-202">È possibile ridurre la larghezza di banda hello di un circuito ExpressRoute senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="a7ab0-203">Il downgrade della larghezza di banda richiede si toodeprovision hello circuito ExpressRoute e quindi ripetere il provisioning di un nuovo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="a7ab0-204">Dopo aver stabilito dimensioni hello che è necessario, utilizzare il circuito hello tooresize di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="a7ab0-205">Il circuito viene ridimensionato sul lato Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="a7ab0-206">Successivamente, è necessario contattare le configurazioni di tooupdate provider di connettività nella loro toomatch lato questa modifica.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="a7ab0-207">Dopo aver apportato questa notifica, iniziamo è fatturazione per l'opzione di hello aggiornato della larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="a7ab0-208">toomove hello SKU da toounlimited a consumo</span><span class="sxs-lookup"><span data-stu-id="a7ab0-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="a7ab0-209">È possibile modificare hello SKU di un circuito ExpressRoute tramite hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="a7ab0-210">classica di toohello toocontrol accesso e gli ambienti di gestione risorse</span><span class="sxs-lookup"><span data-stu-id="a7ab0-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="a7ab0-211">Rivedere le istruzioni di hello in [circuiti ExpressRoute spostare dal modello di distribuzione di gestione risorse toohello classico hello](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a7ab0-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="a7ab0-212">Deprovisioning ed eliminazione di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7ab0-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="a7ab0-213">toodeprovision ed eliminare un circuito ExpressRoute, assicurarsi di comprendere hello seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="a7ab0-214">È necessario scollegare tutte le reti virtuali da hello circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="a7ab0-215">Se questa operazione non riesce, controllare toosee se sono configurate reti virtuali collegate toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="a7ab0-216">Se il provider del servizio di circuito ExpressRoute di hello lo stato di provisioning **Provisioning** o **provisioning eseguito**, è necessario collaborare con il circuito di hello toodeprovision provider del servizio sul relativo lato.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="a7ab0-217">Abbiamo continuare tooreserve risorse e fatturate fino a quando il provider di servizi di hello completa deprovisioning circuito hello e invia una notifica di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="a7ab0-218">È possibile eliminare il circuito hello se il provider di servizi di hello è deprovisioning circuito hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="a7ab0-219">Quando viene effettuato il deprovisioning un circuito, il provider di servizi hello lo stato di provisioning è stato impostato troppo**non è stato eseguito il provisioning**.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="a7ab0-220">Viene arrestata la fatturazione per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="a7ab0-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="a7ab0-221">È possibile eliminare il circuito ExpressRoute eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a7ab0-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7ab0-222">Next steps</span></span>

<span data-ttu-id="a7ab0-223">Dopo aver creato il circuito, assicurarsi che hello quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a7ab0-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="a7ab0-224">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a7ab0-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="a7ab0-225">Collegamento del circuito ExpressRoute di tooyour di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a7ab0-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
