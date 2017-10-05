---
title: Visualizzare la topologia con Network Watcher di Azure - PowerShell | Documentazione Microsoft
description: Questo articolo descrive come usare PowerShell per eseguire una query relativa alla topologia di rete.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 40e01a7a6a2ea6127ab725f04649cec47b9d9422
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="fb13f-103">Visualizzare la topologia di Network Watcher con PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb13f-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="fb13f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb13f-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="fb13f-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="fb13f-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="fb13f-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="fb13f-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="fb13f-107">API REST</span><span class="sxs-lookup"><span data-stu-id="fb13f-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="fb13f-108">La funzionalità per la visualizzazione della topologia di Network Watcher offre una rappresentazione visiva delle risorse di rete in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fb13f-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="fb13f-109">Nel portale, questa visualizzazione è automatica.</span><span class="sxs-lookup"><span data-stu-id="fb13f-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="fb13f-110">È possibile recuperare le informazioni sottostanti alla visualizzazione della topologia nel portale usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb13f-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="fb13f-111">Questa funzionalità rende le informazioni sulla topologia più versatili, poiché i dati possono essere usati anche da altri strumenti per compilare la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="fb13f-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="fb13f-112">L'interconnessione è modellata in due relazioni.</span><span class="sxs-lookup"><span data-stu-id="fb13f-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="fb13f-113">**Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda NIC</span><span class="sxs-lookup"><span data-stu-id="fb13f-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="fb13f-114">**Associazione** - Esempio: la scheda NIC è associata a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fb13f-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="fb13f-115">L'elenco include le proprietà restituite quando si esegue una query all'API REST della topologia.</span><span class="sxs-lookup"><span data-stu-id="fb13f-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="fb13f-116">**name** - Il nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="fb13f-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="fb13f-117">**id** - L'URI della risorsa.</span><span class="sxs-lookup"><span data-stu-id="fb13f-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="fb13f-118">**location** - La località in cui si risiede la risorsa.</span><span class="sxs-lookup"><span data-stu-id="fb13f-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="fb13f-119">**associations** - Un elenco di associazioni all'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="fb13f-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="fb13f-120">**name** - Il nome della risorsa di riferimento.</span><span class="sxs-lookup"><span data-stu-id="fb13f-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="fb13f-121">**resourceId** - ResourceId è l'URI della risorsa di riferimento nell'associazione.</span><span class="sxs-lookup"><span data-stu-id="fb13f-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="fb13f-122">**associationType** - Il valore fa riferimento alla relazione tra l'oggetto figlio e l'oggetto padre.</span><span class="sxs-lookup"><span data-stu-id="fb13f-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="fb13f-123">I valori validi sono **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="fb13f-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fb13f-124">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="fb13f-124">Before you begin</span></span>

<span data-ttu-id="fb13f-125">In questo scenario, il cmdlet `Get-AzureRmNetworkWatcherTopology` viene usato per recuperare le informazioni sulla topologia.</span><span class="sxs-lookup"><span data-stu-id="fb13f-125">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="fb13f-126">È anche disponibile un articolo che illustra come [recuperare una topologia di rete con l'API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="fb13f-126">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="fb13f-127">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="fb13f-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="fb13f-128">Scenario</span><span class="sxs-lookup"><span data-stu-id="fb13f-128">Scenario</span></span>

<span data-ttu-id="fb13f-129">Lo scenario illustrato in questo articolo consente di recuperare la risposta relativa alla topologia per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="fb13f-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="fb13f-130">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="fb13f-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="fb13f-131">Il primo passaggio consente di recuperare l'istanza di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="fb13f-131">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="fb13f-132">La variabile `$networkWatcher` viene passata al cmdlet `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="fb13f-132">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="fb13f-133">Recuperare una topologia</span><span class="sxs-lookup"><span data-stu-id="fb13f-133">Retrieve topology</span></span>

<span data-ttu-id="fb13f-134">Il cmdlet `Get-AzureRmNetworkWatcherTopology` recupera la topologia per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="fb13f-134">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="fb13f-135">Risultati</span><span class="sxs-lookup"><span data-stu-id="fb13f-135">Results</span></span>

<span data-ttu-id="fb13f-136">I risultati restituiti hanno il nome proprietà "Resources", che contiene il corpo della risposta in formato JSON per il cmdlet `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="fb13f-136">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="fb13f-137">La risposta contiene le risorse nel gruppo di sicurezza di rete e le relative associazioni (vale a dire, Contains, Associated).</span><span class="sxs-lookup"><span data-stu-id="fb13f-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="fb13f-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb13f-138">Next steps</span></span>

<span data-ttu-id="fb13f-139">Per informazioni su come visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI, vedere [Visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="fb13f-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


