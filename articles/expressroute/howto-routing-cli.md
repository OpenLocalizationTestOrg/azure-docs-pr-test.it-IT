---
title: 'Come tooconfigure routing per un circuito ExpressRoute di Azure: CLI | Documenti Microsoft'
description: In questo articolo consente di creare ed eseguire il provisioning di hello privato, pubblico e peering Microsoft di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornamento o eliminazione di peering per il circuito.
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="eeac5-104">Creare e modificare il routing per un circuito ExpressRoute con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="eeac5-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="eeac5-105">In questo articolo consente di creare e gestire la configurazione di routing per un circuito ExpressRoute nel modello di distribuzione di gestione risorse hello utilizzando CLI.</span><span class="sxs-lookup"><span data-stu-id="eeac5-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="eeac5-106">È anche possibile controllare lo stato di hello, update o delete e deprovisioning peering per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eeac5-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="eeac5-107">Se si desidera toouse toowork un metodo diverso con il circuito, selezionare un articolo da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="eeac5-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eeac5-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="eeac5-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eeac5-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="eeac5-110">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="eeac5-111">Video - Peering privato</span><span class="sxs-lookup"><span data-stu-id="eeac5-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="eeac5-112">Video - Peering pubblico</span><span class="sxs-lookup"><span data-stu-id="eeac5-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="eeac5-113">Video - Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="eeac5-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="eeac5-114">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="eeac5-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="eeac5-115">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="eeac5-115">Configuration prerequisites</span></span>

* <span data-ttu-id="eeac5-116">Prima di iniziare, installare hello versione i comandi CLI hello (2.0 o versione successivo).</span><span class="sxs-lookup"><span data-stu-id="eeac5-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="eeac5-117">Per informazioni sull'installazione di comandi CLI hello, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eeac5-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="eeac5-118">Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flusso di lavoro](expressroute-workflows.md) pagine prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="eeac5-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="eeac5-119">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="eeac5-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="eeac5-120">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](howto-circuit-cli.md) e circuito hello abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="eeac5-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="eeac5-121">Hello circuito ExpressRoute deve essere in uno stato di provisioning e attivato per consentire i comandi di hello in grado di toorun toobe in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="eeac5-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="eeac5-122">Queste istruzioni si applicano solo toocircuits creato con il provider di servizi che offre servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="eeac5-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="eeac5-123">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (in genere una VPN IP, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="eeac5-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="eeac5-124">Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="eeac5-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="eeac5-125">È possibile configurare i peering nell'ordine desiderato.</span><span class="sxs-lookup"><span data-stu-id="eeac5-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="eeac5-126">Tuttavia, è necessario assicurarsi completare hello configurazione di ogni peer uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="eeac5-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="eeac5-127">Peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-127">Azure private peering</span></span>

<span data-ttu-id="eeac5-128">In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione peering privata per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eeac5-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="eeac5-129">toocreate peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="eeac5-130">Installare hello l'ultima versione di CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="eeac5-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="eeac5-131">È necessario utilizzare una versione più recente di hello di hello Azure interfaccia della riga di comando (CLI). * hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="eeac5-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="eeac5-132">Selezionare la sottoscrizione di hello da circuito ExpressRoute toocreate</span><span class="sxs-lookup"><span data-stu-id="eeac5-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="eeac5-133">Creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eeac5-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="eeac5-134">Seguire hello istruzioni toocreate un [circuito ExpressRoute](howto-circuit-cli.md) e fare in modo fornito dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="eeac5-135">Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure.</span><span class="sxs-lookup"><span data-stu-id="eeac5-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="eeac5-136">In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="eeac5-137">Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="eeac5-138">Controllare toomake di circuito ExpressRoute hello assicurarsi che sia stato eseguito il provisioning e inoltre abilitato.</span><span class="sxs-lookup"><span data-stu-id="eeac5-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="eeac5-139">Utilizzare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="eeac5-140">risposta Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-140">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="eeac5-141">Configurare peering privato di Azure per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="eeac5-142">Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:</span><span class="sxs-lookup"><span data-stu-id="eeac5-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="eeac5-143">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="eeac5-144">subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="eeac5-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="eeac5-145">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="eeac5-146">subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="eeac5-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="eeac5-147">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="eeac5-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="eeac5-148">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="eeac5-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="eeac5-149">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="eeac5-149">AS number for peering.</span></span> <span data-ttu-id="eeac5-150">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="eeac5-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="eeac5-151">È possibile usare il numero AS privato per questo peering.</span><span class="sxs-lookup"><span data-stu-id="eeac5-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="eeac5-152">Assicurarsi di non usare il numero 65515.</span><span class="sxs-lookup"><span data-stu-id="eeac5-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="eeac5-153">**Facoltativo:** un hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="eeac5-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="eeac5-154">Utilizzare hello seguente esempio tooconfigure privata peering per il circuito di Azure:</span><span class="sxs-lookup"><span data-stu-id="eeac5-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="eeac5-155">Se si sceglie toouse un hash MD5, usare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="eeac5-156">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="eeac5-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="eeac5-157">tooview dettagli di peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-157">tooview Azure private peering details</span></span>

<span data-ttu-id="eeac5-158">È possibile ottenere i dettagli di configurazione utilizzando hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="eeac5-159">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="eeac5-159">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="eeac5-160">configurazione di peering privato Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="eeac5-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="eeac5-161">È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="eeac5-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="eeac5-162">In questo esempio hello ID VLAN del circuito hello viene aggiornato da too500 100.</span><span class="sxs-lookup"><span data-stu-id="eeac5-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="eeac5-163">toodelete peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-163">toodelete Azure private peering</span></span>

<span data-ttu-id="eeac5-164">È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="eeac5-165">È necessario assicurarsi che tutte le reti virtuali vengono scollegate dal hello circuito ExpressRoute prima di eseguire questo esempio.</span><span class="sxs-lookup"><span data-stu-id="eeac5-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="eeac5-166">Peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-166">Azure public peering</span></span>

<span data-ttu-id="eeac5-167">In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione di peering pubblico per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eeac5-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="eeac5-168">toocreate peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="eeac5-169">Installare hello l'ultima versione di CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="eeac5-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="eeac5-170">È necessario utilizzare una versione più recente di hello di hello Azure interfaccia della riga di comando (CLI). * hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="eeac5-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="eeac5-171">Selezionare la sottoscrizione di hello per cui si desidera circuito ExpressRoute toocreate.</span><span class="sxs-lookup"><span data-stu-id="eeac5-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="eeac5-172">Creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eeac5-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="eeac5-173">Seguire hello istruzioni toocreate un [circuito ExpressRoute](howto-circuit-cli.md) e fare in modo fornito dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="eeac5-174">Se il provider di connettività offre servizi gestiti di livello 3, è possibile chiedere al provider di connettività di abilitare il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="eeac5-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="eeac5-175">In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="eeac5-176">Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="eeac5-177">Controllare hello ExpressRoute circuito tooensure che sia stato eseguito il provisioning e inoltre abilitato.</span><span class="sxs-lookup"><span data-stu-id="eeac5-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="eeac5-178">Utilizzare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="eeac5-179">risposta Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-179">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="eeac5-180">Configurare peering pubblico di Azure per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="eeac5-181">Assicurarsi di avere le seguenti informazioni prima di continuare ulteriormente hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="eeac5-182">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="eeac5-183">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="eeac5-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="eeac5-184">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="eeac5-185">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="eeac5-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="eeac5-186">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="eeac5-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="eeac5-187">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="eeac5-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="eeac5-188">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="eeac5-188">AS number for peering.</span></span> <span data-ttu-id="eeac5-189">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="eeac5-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="eeac5-190">**Facoltativo:** un hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="eeac5-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="eeac5-191">Eseguire hello seguente esempio tooconfigure pubblici di peering per il circuito di Azure:</span><span class="sxs-lookup"><span data-stu-id="eeac5-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="eeac5-192">Se si sceglie toouse un hash MD5, usare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="eeac5-193">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="eeac5-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="eeac5-194">tooview dettagli di peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-194">tooview Azure public peering details</span></span>

<span data-ttu-id="eeac5-195">È possibile ottenere i dettagli di configurazione mediante hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="eeac5-196">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="eeac5-196">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="eeac5-197">configurazione di peering pubblico Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="eeac5-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="eeac5-198">È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="eeac5-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="eeac5-199">In questo esempio hello ID VLAN del circuito hello viene aggiornato da too600 200.</span><span class="sxs-lookup"><span data-stu-id="eeac5-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="eeac5-200">toodelete peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="eeac5-200">toodelete Azure public peering</span></span>

<span data-ttu-id="eeac5-201">È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="eeac5-202">Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="eeac5-202">Microsoft peering</span></span>

<span data-ttu-id="eeac5-203">In questa sezione consente di creare, ottenere, aggiornare ed eliminare le configurazioni di peering Microsoft hello per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eeac5-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eeac5-204">Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite hello peering Microsoft, anche se non sono definiti i filtri di route.</span><span class="sxs-lookup"><span data-stu-id="eeac5-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="eeac5-205">Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="eeac5-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="eeac5-206">Per altre informazioni, vedere [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurare un filtro di route per il peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="eeac5-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="eeac5-207">toocreate peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="eeac5-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="eeac5-208">Installare hello l'ultima versione di CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="eeac5-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="eeac5-209">Utilizzare hello più recente di hello Azure interfaccia della riga di comando (CLI). * hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="eeac5-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="eeac5-210">Selezionare la sottoscrizione di hello per cui si desidera circuito ExpressRoute toocreate.</span><span class="sxs-lookup"><span data-stu-id="eeac5-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="eeac5-211">Creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eeac5-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="eeac5-212">Seguire hello istruzioni toocreate un [circuito ExpressRoute](howto-circuit-cli.md) e fare in modo fornito dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="eeac5-213">Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure.</span><span class="sxs-lookup"><span data-stu-id="eeac5-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="eeac5-214">In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="eeac5-215">Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="eeac5-216">Controllare toomake di circuito ExpressRoute hello assicurarsi che sia stato eseguito il provisioning e inoltre abilitato.</span><span class="sxs-lookup"><span data-stu-id="eeac5-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="eeac5-217">Utilizzare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="eeac5-218">risposta Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-218">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="eeac5-219">Configurare Microsoft peering per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="eeac5-220">Assicurarsi di aver hello le seguenti informazioni prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="eeac5-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="eeac5-221">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="eeac5-222">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="eeac5-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="eeac5-223">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="eeac5-224">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="eeac5-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="eeac5-225">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="eeac5-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="eeac5-226">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="eeac5-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="eeac5-227">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="eeac5-227">AS number for peering.</span></span> <span data-ttu-id="eeac5-228">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="eeac5-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="eeac5-229">I prefissi annunciati: È necessario fornire un elenco di tutti i prefissi Prevedi tooadvertise sessione BGP hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="eeac5-230">Sono accettati solo prefissi di indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="eeac5-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="eeac5-231">Se si prevede un set di prefissi toosend, è possibile inviare un elenco delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="eeac5-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="eeac5-232">I prefissi devono essere registrati tooyou in un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="eeac5-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="eeac5-233">**Facoltativo:** cliente ASN: nel caso di annunci con prefissi non registrato toohello peering sotto forma di numero, è possibile specificare hello come numero toowhich sono registrati.</span><span class="sxs-lookup"><span data-stu-id="eeac5-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="eeac5-234">Nome del Registro di sistema di routing: È possibile specificare hello RIR / IRR contro cui hello come numero e i prefissi sono registrati.</span><span class="sxs-lookup"><span data-stu-id="eeac5-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="eeac5-235">**Facoltativo:** un hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="eeac5-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="eeac5-236">Eseguire hello seguendo l'esempio tooconfigure peering Microsoft per il circuito:</span><span class="sxs-lookup"><span data-stu-id="eeac5-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="eeac5-237">dettagli di peering Microsoft tooget</span><span class="sxs-lookup"><span data-stu-id="eeac5-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="eeac5-238">È possibile ottenere i dettagli di configurazione utilizzando hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="eeac5-239">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="eeac5-239">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="eeac5-240">configurazione di peering Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="eeac5-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="eeac5-241">È possibile aggiornare qualsiasi parte della configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="eeac5-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="eeac5-242">Hello annunciati prefissi del circuito hello in corso l'aggiornamento da too124.1.0.0/24 123.1.0.0/24 nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="eeac5-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="eeac5-243">toodelete peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="eeac5-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="eeac5-244">È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeac5-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="eeac5-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eeac5-245">Next steps</span></span>

<span data-ttu-id="eeac5-246">Passaggio successivo, [collegare un circuito ExpressRoute di tooan rete virtuale](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="eeac5-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="eeac5-247">Per ulteriori informazioni sui flussi di lavoro ExpressRoute, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="eeac5-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="eeac5-248">Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="eeac5-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="eeac5-249">Per ulteriori informazioni sull’uso delle reti virtuali, vedere [Panoramica sulla rete virtuale](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eeac5-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>