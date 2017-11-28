---
title: topologia Watcher di rete di Azure aaaView - CLI di Azure 1.0 | Documenti Microsoft
description: "In questo articolo descriverà come tooquery toouse CLI di Azure 1.0 la topologia di rete."
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
ms.openlocfilehash: 30679d6dc74e85bacfc86c63bd1afa873893c772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="78fdf-103">Visualizzare la topologia di Network Watcher con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="78fdf-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="78fdf-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="78fdf-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="78fdf-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="78fdf-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="78fdf-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="78fdf-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="78fdf-107">API REST</span><span class="sxs-lookup"><span data-stu-id="78fdf-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="78fdf-108">funzionalità di topologia Hello del controllo di rete fornisce una rappresentazione visiva delle risorse di rete hello in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="78fdf-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="78fdf-109">Nel portale di hello, questa visualizzazione viene presentata tooyou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="78fdf-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="78fdf-110">informazioni Hello dietro vista della topologia hello nel portale di hello è possibile recuperare tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78fdf-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="78fdf-111">Questa funzionalità rende più versatile come hello dati possono essere utilizzati da altri strumenti toobuild out visualizzazione hello informazioni sulla topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="78fdf-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="78fdf-112">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="78fdf-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="78fdf-113">interconnessione Hello viene modellata in due relazioni.</span><span class="sxs-lookup"><span data-stu-id="78fdf-113">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="78fdf-114">**Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda NIC</span><span class="sxs-lookup"><span data-stu-id="78fdf-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="78fdf-115">**Associazione** - Esempio: la scheda NIC è associata a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="78fdf-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="78fdf-116">Hello seguito sono le proprietà restituite quando si eseguono query hello API REST di topologia.</span><span class="sxs-lookup"><span data-stu-id="78fdf-116">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="78fdf-117">**nome** : hello nome della risorsa hello</span><span class="sxs-lookup"><span data-stu-id="78fdf-117">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="78fdf-118">**ID** -hello uri della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="78fdf-118">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="78fdf-119">**percorso** -hello percorso in cui risiede la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="78fdf-119">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="78fdf-120">**le associazioni** -un elenco di associazioni toohello fa riferimento a oggetto.</span><span class="sxs-lookup"><span data-stu-id="78fdf-120">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="78fdf-121">**nome** -nome hello di hello risorsa a cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="78fdf-121">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="78fdf-122">**resourceId** -resourceId hello è hello uri della risorsa hello a cui fa riferimento nell'associazione hello.</span><span class="sxs-lookup"><span data-stu-id="78fdf-122">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="78fdf-123">**associationType** -relazione hello tra l'oggetto figlio hello e padre hello fa riferimento a questo valore.</span><span class="sxs-lookup"><span data-stu-id="78fdf-123">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="78fdf-124">I valori validi sono **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="78fdf-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="78fdf-125">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="78fdf-125">Before you begin</span></span>

<span data-ttu-id="78fdf-126">In questo scenario, si usa hello `network watcher topology` informazioni sulla topologia di cmdlet tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="78fdf-126">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="78fdf-127">È inoltre disponibile un articolo su come troppo[recuperare la topologia di rete con l'API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="78fdf-127">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="78fdf-128">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="78fdf-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="78fdf-129">Scenario</span><span class="sxs-lookup"><span data-stu-id="78fdf-129">Scenario</span></span>

<span data-ttu-id="78fdf-130">scenario di Hello illustrato in questo articolo recupera risposta topologia hello per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="78fdf-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="78fdf-131">Recuperare una topologia</span><span class="sxs-lookup"><span data-stu-id="78fdf-131">Retrieve topology</span></span>

<span data-ttu-id="78fdf-132">Hello `network watcher topology` cmdlet recupera la topologia di hello per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="78fdf-132">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="78fdf-133">Aggiunto argomento hello "--json" tooview hello oput in formato json</span><span class="sxs-lookup"><span data-stu-id="78fdf-133">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="78fdf-134">Risultati</span><span class="sxs-lookup"><span data-stu-id="78fdf-134">Results</span></span>

<span data-ttu-id="78fdf-135">Hello risultati restituiti hanno una proprietà nome "Resources", che contiene corpo della risposta json hello per hello `network watcher topology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="78fdf-135">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="78fdf-136">risposta Hello contiene risorse hello hello il gruppo di sicurezza di rete e le relative associazioni (vale a dire, Contains, associate).</span><span class="sxs-lookup"><span data-stu-id="78fdf-136">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="78fdf-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78fdf-137">Next steps</span></span>

<span data-ttu-id="78fdf-138">Ulteriori informazioni sulle regole di sicurezza hello che sono risorse di rete applicati tooyour visitando [Visualizza panoramica gruppo di sicurezza](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="78fdf-138">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
