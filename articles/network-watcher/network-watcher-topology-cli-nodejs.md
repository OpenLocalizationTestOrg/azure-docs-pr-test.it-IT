---
title: Visualizzare la topologia di Azure Network Watcher - Interfaccia della riga di comando di Azure 1.0 | Microsoft Docs
description: Questo articolo descrive come usare l'interfaccia della riga di comando di Azure 1.0 per eseguire una query sulla topologia di rete.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9178c485a92e04564c95dae8073f045b5c639bb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="aef0f-103">Visualizzare la topologia di Network Watcher con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="aef0f-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="aef0f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aef0f-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="aef0f-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="aef0f-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="aef0f-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="aef0f-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="aef0f-107">API REST</span><span class="sxs-lookup"><span data-stu-id="aef0f-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="aef0f-108">La funzionalità per la visualizzazione della topologia di Network Watcher offre una rappresentazione visiva delle risorse di rete in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="aef0f-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="aef0f-109">Nel portale, questa visualizzazione è automatica.</span><span class="sxs-lookup"><span data-stu-id="aef0f-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="aef0f-110">È possibile recuperare le informazioni sottostanti alla visualizzazione della topologia nel portale usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aef0f-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="aef0f-111">Questa funzionalità rende le informazioni sulla topologia più versatili, poiché i dati possono essere usati anche da altri strumenti per compilare la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="aef0f-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="aef0f-112">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="aef0f-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="aef0f-113">L'interconnessione è modellata in due relazioni.</span><span class="sxs-lookup"><span data-stu-id="aef0f-113">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="aef0f-114">**Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda NIC</span><span class="sxs-lookup"><span data-stu-id="aef0f-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="aef0f-115">**Associazione** - Esempio: la scheda NIC è associata a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="aef0f-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="aef0f-116">L'elenco include le proprietà restituite quando si esegue una query all'API REST della topologia.</span><span class="sxs-lookup"><span data-stu-id="aef0f-116">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="aef0f-117">**name** - Il nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="aef0f-117">**name** - The name of the resource</span></span>
* <span data-ttu-id="aef0f-118">**id** - L'URI della risorsa.</span><span class="sxs-lookup"><span data-stu-id="aef0f-118">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="aef0f-119">**location** - La località in cui si risiede la risorsa.</span><span class="sxs-lookup"><span data-stu-id="aef0f-119">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="aef0f-120">**associations** - Un elenco di associazioni all'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="aef0f-120">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="aef0f-121">**name** - Il nome della risorsa di riferimento.</span><span class="sxs-lookup"><span data-stu-id="aef0f-121">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="aef0f-122">**resourceId** - ResourceId è l'URI della risorsa di riferimento nell'associazione.</span><span class="sxs-lookup"><span data-stu-id="aef0f-122">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="aef0f-123">**associationType** - Il valore fa riferimento alla relazione tra l'oggetto figlio e l'oggetto padre.</span><span class="sxs-lookup"><span data-stu-id="aef0f-123">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="aef0f-124">I valori validi sono **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="aef0f-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="aef0f-125">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="aef0f-125">Before you begin</span></span>

<span data-ttu-id="aef0f-126">In questo scenario, il cmdlet `network watcher topology` viene usato per recuperare le informazioni sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="aef0f-126">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="aef0f-127">È anche disponibile un articolo che illustra come [recuperare una topologia di rete con l'API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="aef0f-127">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="aef0f-128">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="aef0f-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="aef0f-129">Scenario</span><span class="sxs-lookup"><span data-stu-id="aef0f-129">Scenario</span></span>

<span data-ttu-id="aef0f-130">Lo scenario illustrato in questo articolo consente di recuperare la risposta relativa alla topologia per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="aef0f-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="aef0f-131">Recuperare una topologia</span><span class="sxs-lookup"><span data-stu-id="aef0f-131">Retrieve topology</span></span>

<span data-ttu-id="aef0f-132">Il cmdlet `network watcher topology` recupera la topologia per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="aef0f-132">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span></span> <span data-ttu-id="aef0f-133">Aggiungere l'argomento "-json" per visualizzare l'output in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="aef0f-133">Add the argument "--json" to view the oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="aef0f-134">Risultati</span><span class="sxs-lookup"><span data-stu-id="aef0f-134">Results</span></span>

<span data-ttu-id="aef0f-135">I risultati restituiti hanno il nome proprietà "Resources", che contiene il corpo della risposta in formato JSON per il cmdlet `network watcher topology`.</span><span class="sxs-lookup"><span data-stu-id="aef0f-135">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="aef0f-136">La risposta contiene le risorse nel gruppo di sicurezza di rete e le relative associazioni (vale a dire, Contains, Associated).</span><span class="sxs-lookup"><span data-stu-id="aef0f-136">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="aef0f-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aef0f-137">Next steps</span></span>

<span data-ttu-id="aef0f-138">Per altre informazioni sulle regole di sicurezza applicate alle risorse di rete, leggere la [panoramica sulla visualizzazione di gruppo di sicurezza](network-watcher-security-group-view-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aef0f-138">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
