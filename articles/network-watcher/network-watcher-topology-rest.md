---
title: Visualizzare la topologia con Network Watcher di Azure - API REST | Documentazione Microsoft
description: Questo articolo descrive come usare l'API REST per eseguire una query relativa alla topologia di rete.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 568f3060da372f4a08cec342e04359172522cb69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="7acca-103">Visualizzare la topologia di Network Watcher con l'API REST</span><span class="sxs-lookup"><span data-stu-id="7acca-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7acca-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7acca-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="7acca-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="7acca-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="7acca-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="7acca-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="7acca-107">API REST</span><span class="sxs-lookup"><span data-stu-id="7acca-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="7acca-108">La funzionalità per la visualizzazione della topologia di Network Watcher offre una rappresentazione visiva delle risorse di rete in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7acca-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="7acca-109">Nel portale, questa visualizzazione è automatica.</span><span class="sxs-lookup"><span data-stu-id="7acca-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="7acca-110">È possibile recuperare le informazioni sottostanti alla visualizzazione della topologia nel portale usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7acca-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="7acca-111">Questa funzionalità rende le informazioni sulla topologia più versatili, poiché i dati possono essere usati anche da altri strumenti per compilare la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="7acca-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="7acca-112">L'interconnessione è modellata in due relazioni.</span><span class="sxs-lookup"><span data-stu-id="7acca-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="7acca-113">**Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda NIC</span><span class="sxs-lookup"><span data-stu-id="7acca-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="7acca-114">**Associazione** - Esempio: la scheda NIC è associata a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7acca-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="7acca-115">L'elenco include le proprietà restituite quando si esegue una query all'API REST della topologia.</span><span class="sxs-lookup"><span data-stu-id="7acca-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="7acca-116">**name** - Il nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="7acca-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="7acca-117">**id** - L'URI della risorsa.</span><span class="sxs-lookup"><span data-stu-id="7acca-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="7acca-118">**location** - La località in cui si risiede la risorsa.</span><span class="sxs-lookup"><span data-stu-id="7acca-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="7acca-119">**associations** - Un elenco di associazioni all'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="7acca-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="7acca-120">**name** - Il nome della risorsa di riferimento.</span><span class="sxs-lookup"><span data-stu-id="7acca-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="7acca-121">**resourceId** - ResourceId è l'URI della risorsa di riferimento nell'associazione.</span><span class="sxs-lookup"><span data-stu-id="7acca-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="7acca-122">**associationType** - Il valore fa riferimento alla relazione tra l'oggetto figlio e l'oggetto padre.</span><span class="sxs-lookup"><span data-stu-id="7acca-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="7acca-123">I valori validi sono **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="7acca-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7acca-124">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7acca-124">Before you begin</span></span>

<span data-ttu-id="7acca-125">In questo scenario, vengono recuperate le informazioni sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="7acca-125">In this scenario, you retrieve the topology information.</span></span> <span data-ttu-id="7acca-126">ARMclient viene usato per chiamare l'API REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7acca-126">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="7acca-127">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="7acca-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="7acca-128">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="7acca-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="7acca-129">Scenario</span><span class="sxs-lookup"><span data-stu-id="7acca-129">Scenario</span></span>

<span data-ttu-id="7acca-130">Lo scenario illustrato in questo articolo consente di recuperare la risposta relativa alla topologia per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="7acca-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="7acca-131">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="7acca-131">Log in with ARMClient</span></span>

<span data-ttu-id="7acca-132">Accedere ad armclient con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="7acca-132">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="7acca-133">Recuperare una topologia</span><span class="sxs-lookup"><span data-stu-id="7acca-133">Retrieve topology</span></span>

<span data-ttu-id="7acca-134">L'esempio seguente richiede la topologia dall'API REST.</span><span class="sxs-lookup"><span data-stu-id="7acca-134">The following example requests the topology from the REST API.</span></span>  <span data-ttu-id="7acca-135">Nell'esempio vengono impostati parametri per consentire flessibilità nella creazione di un esempio.</span><span class="sxs-lookup"><span data-stu-id="7acca-135">The example is parameterized to allow for flexibility in creating an example.</span></span>  <span data-ttu-id="7acca-136">Sostituire tutti i valori con \< \> intorno a essi.</span><span class="sxs-lookup"><span data-stu-id="7acca-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name to run topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="7acca-137">La risposta seguente è un esempio di risposta abbreviata che viene restituita quando si recupera la topologia per un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="7acca-137">The following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="7acca-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7acca-138">Next steps</span></span>

<span data-ttu-id="7acca-139">Per informazioni su come visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI, vedere [Visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="7acca-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

