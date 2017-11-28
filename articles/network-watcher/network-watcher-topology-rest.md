---
title: topologia Watcher di rete di Azure aaaView - API REST | Documenti Microsoft
description: In questo articolo viene descritto come toouse REST API tooquery la topologia di rete.
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
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="64b06-103">Visualizzare la topologia di Network Watcher con l'API REST</span><span class="sxs-lookup"><span data-stu-id="64b06-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="64b06-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64b06-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="64b06-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="64b06-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="64b06-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="64b06-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="64b06-107">API REST</span><span class="sxs-lookup"><span data-stu-id="64b06-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="64b06-108">funzionalità di topologia Hello del controllo di rete fornisce una rappresentazione visiva delle risorse di rete hello in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="64b06-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="64b06-109">Nel portale di hello, questa visualizzazione viene presentata tooyou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="64b06-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="64b06-110">informazioni Hello dietro vista della topologia hello nel portale di hello è possibile recuperare tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64b06-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="64b06-111">Questa funzionalità rende più versatile come hello dati possono essere utilizzati da altri strumenti toobuild out visualizzazione hello informazioni sulla topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="64b06-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="64b06-112">interconnessione Hello viene modellata in due relazioni.</span><span class="sxs-lookup"><span data-stu-id="64b06-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="64b06-113">**Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda NIC</span><span class="sxs-lookup"><span data-stu-id="64b06-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="64b06-114">**Associazione** - Esempio: la scheda NIC è associata a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="64b06-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="64b06-115">Hello seguito sono le proprietà restituite quando si eseguono query hello API REST di topologia.</span><span class="sxs-lookup"><span data-stu-id="64b06-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="64b06-116">**nome** : hello nome della risorsa hello</span><span class="sxs-lookup"><span data-stu-id="64b06-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="64b06-117">**ID** -hello uri della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="64b06-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="64b06-118">**percorso** -hello percorso in cui risiede la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="64b06-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="64b06-119">**le associazioni** -un elenco di associazioni toohello fa riferimento a oggetto.</span><span class="sxs-lookup"><span data-stu-id="64b06-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="64b06-120">**nome** -nome hello di hello risorsa a cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="64b06-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="64b06-121">**resourceId** -resourceId hello è hello uri della risorsa hello a cui fa riferimento nell'associazione hello.</span><span class="sxs-lookup"><span data-stu-id="64b06-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="64b06-122">**associationType** -relazione hello tra l'oggetto figlio hello e padre hello fa riferimento a questo valore.</span><span class="sxs-lookup"><span data-stu-id="64b06-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="64b06-123">I valori validi sono **Contains** o **Associated**.</span><span class="sxs-lookup"><span data-stu-id="64b06-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="64b06-124">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="64b06-124">Before you begin</span></span>

<span data-ttu-id="64b06-125">In questo scenario è recuperare le informazioni sulla topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="64b06-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="64b06-126">ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64b06-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="64b06-127">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="64b06-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="64b06-128">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="64b06-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="64b06-129">Scenario</span><span class="sxs-lookup"><span data-stu-id="64b06-129">Scenario</span></span>

<span data-ttu-id="64b06-130">scenario di Hello illustrato in questo articolo recupera risposta topologia hello per un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="64b06-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="64b06-131">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="64b06-131">Log in with ARMClient</span></span>

<span data-ttu-id="64b06-132">Accedi tooarmclient con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="64b06-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="64b06-133">Recuperare una topologia</span><span class="sxs-lookup"><span data-stu-id="64b06-133">Retrieve topology</span></span>

<span data-ttu-id="64b06-134">Hello di esempio seguente richiede topologia hello hello API REST.</span><span class="sxs-lookup"><span data-stu-id="64b06-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="64b06-135">esempio Hello è tooallow con parametri per la flessibilità per la creazione di un esempio.</span><span class="sxs-lookup"><span data-stu-id="64b06-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="64b06-136">Sostituire tutti i valori con \< \> intorno a essi.</span><span class="sxs-lookup"><span data-stu-id="64b06-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="64b06-137">Hello risposta seguente è riportato un esempio di una risposta abbreviato che viene restituito quando recuperare topologia per un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="64b06-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="64b06-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64b06-138">Next steps</span></span>

<span data-ttu-id="64b06-139">Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="64b06-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

