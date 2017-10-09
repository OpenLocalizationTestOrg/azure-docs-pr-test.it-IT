---
title: topologia Watcher di rete di Azure aaaView - PowerShell | Documenti Microsoft
description: "In questo articolo descriverà come toouse PowerShell tooquery la topologia di rete."
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
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="abf72-103">Visualizzare la topologia di Network Watcher con PowerShell</span><span class="sxs-lookup"><span data-stu-id="abf72-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="abf72-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="abf72-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="abf72-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="abf72-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="abf72-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="abf72-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="abf72-107">API REST</span><span class="sxs-lookup"><span data-stu-id="abf72-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="abf72-108">funzionalità di topologia Hello del controllo di rete fornisce una rappresentazione visiva delle risorse di rete hello in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="abf72-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="abf72-109">Nel portale di hello, questa visualizzazione viene presentata tooyou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="abf72-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="abf72-110">informazioni Hello dietro vista della topologia hello nel portale di hello è possibile recuperare tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abf72-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="abf72-111">Questa funzionalità rende più versatile come hello dati possono essere utilizzati da altri strumenti toobuild out visualizzazione hello informazioni sulla topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="abf72-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="abf72-112">interconnessione Hello viene modellata in due relazioni.</span><span class="sxs-lookup"><span data-stu-id="abf72-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="abf72-113">**Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda NIC</span><span class="sxs-lookup"><span data-stu-id="abf72-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="abf72-114">**Associazione** - Esempio: la scheda NIC è associata a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="abf72-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="abf72-115">Hello seguito sono le proprietà restituite quando si eseguono query hello API REST di topologia.</span><span class="sxs-lookup"><span data-stu-id="abf72-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="abf72-116">**nome** : hello nome della risorsa hello</span><span class="sxs-lookup"><span data-stu-id="abf72-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="abf72-117">**ID** -hello uri della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="abf72-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="abf72-118">**percorso** -hello percorso in cui risiede la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="abf72-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="abf72-119">**le associazioni** -un elenco di associazioni toohello fa riferimento a oggetto.</span><span class="sxs-lookup"><span data-stu-id="abf72-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="abf72-120">**nome** -nome hello di hello risorsa a cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="abf72-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="abf72-121">**resourceId** -resourceId hello è hello uri della risorsa hello a cui fa riferimento nell'associazione hello.</span><span class="sxs-lookup"><span data-stu-id="abf72-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="abf72-122">**associationType** -relazione hello tra l'oggetto figlio hello e padre hello fa riferimento a questo valore.</span><span class="sxs-lookup"><span data-stu-id="abf72-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="abf72-123">I valori validi sono **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="abf72-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="abf72-124">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="abf72-124">Before you begin</span></span>

<span data-ttu-id="abf72-125">In questo scenario, si usa hello `Get-AzureRmNetworkWatcherTopology` informazioni sulla topologia di cmdlet tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="abf72-125">In this scenario, you use hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="abf72-126">È inoltre disponibile un articolo su come troppo[recuperare la topologia di rete con l'API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="abf72-126">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="abf72-127">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="abf72-127">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="abf72-128">Scenario</span><span class="sxs-lookup"><span data-stu-id="abf72-128">Scenario</span></span>

<span data-ttu-id="abf72-129">scenario di Hello illustrato in questo articolo recupera risposta topologia hello per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="abf72-129">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="abf72-130">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="abf72-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="abf72-131">innanzitutto Hello è l'istanza di tooretrieve hello Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="abf72-131">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="abf72-132">Hello `$networkWatcher` variabile viene passata toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="abf72-132">hello `$networkWatcher` variable is passed toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="abf72-133">Recuperare una topologia</span><span class="sxs-lookup"><span data-stu-id="abf72-133">Retrieve topology</span></span>

<span data-ttu-id="abf72-134">Hello `Get-AzureRmNetworkWatcherTopology` cmdlet recupera la topologia di hello per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="abf72-134">hello `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves hello topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="abf72-135">Risultati</span><span class="sxs-lookup"><span data-stu-id="abf72-135">Results</span></span>

<span data-ttu-id="abf72-136">Hello risultati restituiti hanno una proprietà nome "Resources", che contiene corpo della risposta json hello per hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="abf72-136">hello results returned have a property name "Resources", which contains hello json response body for hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="abf72-137">risposta Hello contiene risorse hello hello il gruppo di sicurezza di rete e le relative associazioni (vale a dire, Contains, associate).</span><span class="sxs-lookup"><span data-stu-id="abf72-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="abf72-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="abf72-138">Next steps</span></span>

<span data-ttu-id="abf72-139">Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="abf72-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


