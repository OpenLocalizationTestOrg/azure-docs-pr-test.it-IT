---
title: Creare un'istanza di Azure Network Watcher | Microsoft Docs
description: Questa pagina illustra la procedura per la creazione di un'istanza di Network Watcher tramite il portale di Azure e l'API REST
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2aeaffdd5ab552e18677cbd1a24a748dd14bf172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="828c1-103">Creare un'istanza di Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="828c1-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="828c1-104">Network Watcher è un servizio a livello di area che permette di monitorare e diagnosticare le condizioni al livello di scenario di rete da, verso e all'interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="828c1-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="828c1-105">Il monitoraggio a livello di scenario permette di diagnosticare i problemi in una visualizzazione completa a livello di rete.</span><span class="sxs-lookup"><span data-stu-id="828c1-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span></span> <span data-ttu-id="828c1-106">Gli strumenti di visualizzazione e diagnostica di rete disponibili in Network Watcher permettono di comprendere, diagnosticare e ottenere informazioni dettagliate sulla rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="828c1-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="828c1-107">Dato che Network Watcher supporta attualmente solo l'interfaccia della riga di comando 1.0, le istruzioni fornite per creare una nuova istanza di Network Watcher sono quelle per l'interfaccia della riga di comando 1.0.</span><span class="sxs-lookup"><span data-stu-id="828c1-107">As Network Watcher currently only supports CLI 1.0, the instructions to create a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-the-portal"></a><span data-ttu-id="828c1-108">Creare un'istanza di Network Watcher nel portale</span><span class="sxs-lookup"><span data-stu-id="828c1-108">Create a Network Watcher in the portal</span></span>

<span data-ttu-id="828c1-109">Passare ad **Altri servizi** > **Rete** > **Network Watcher**.</span><span class="sxs-lookup"><span data-stu-id="828c1-109">Navigate to **More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="828c1-110">È possibile selezionare tutte le sottoscrizioni per cui si vuole abilitare Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="828c1-110">You can select all the subscriptions you want to enable Network Watcher for.</span></span> <span data-ttu-id="828c1-111">Questa azione crea un'istanza di Network Watcher in ogni area in cui è disponibile.</span><span class="sxs-lookup"><span data-stu-id="828c1-111">This action creates a Network Watcher in every region that is available.</span></span>

![Creare un'istanza di Network Watcher][1]

<span data-ttu-id="828c1-113">Quando si abilita Network Watcher tramite il portale, il nome dell'istanza di Network Watcher verrà impostato automaticamente su NetworkWatcher_region_name dove region_name corrisponde all'area di Azure in cui l'istanza è stata abilitata.</span><span class="sxs-lookup"><span data-stu-id="828c1-113">When you enable Network Watcher using the Portal, the name of the Network Watcher instance will automatically be set to NetworkWatcher_region_name where region_name corresponds to the Azure Region where the instance was enabled.</span></span>  <span data-ttu-id="828c1-114">Ad esempio, un Network Watcher abilitato nell'area centro-occidentale degli Stati Uniti verrà denominato NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="828c1-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="828c1-115">Inoltre, l'istanza di Network Watcher verrà automaticamente aggiunta in un gruppo di risorse denominato NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="828c1-115">Additionally, the Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="828c1-116">Questo gruppo di risorse verrà creato se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="828c1-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="828c1-117">Se si desidera personalizzare il nome di un'istanza di Network Watcher e il gruppo di risorse in cui è inserito, è possibile usare Powershell, l'API REST o i metodi ARMClient descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="828c1-117">If you wish to customize the name of a Network Watcher instance and the Resource Group it's placed into, you can use Powershell, the REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="828c1-118">Per ogni opzione, il gruppo di risorse deve esistere prima di inserirvi Network Watcher all'interno.</span><span class="sxs-lookup"><span data-stu-id="828c1-118">In each option, the Resource Group must exist before you place the Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="828c1-119">Creare un'istanza di Network Watcher con PowerShell</span><span class="sxs-lookup"><span data-stu-id="828c1-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="828c1-120">Per creare un'istanza di Network Watcher, eseguire questo esempio:</span><span class="sxs-lookup"><span data-stu-id="828c1-120">To create an instance of Network Watcher, run the following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-rest-api"></a><span data-ttu-id="828c1-121">Creare un'istanza di Network Watcher con l'API REST</span><span class="sxs-lookup"><span data-stu-id="828c1-121">Create a Network Watcher with the REST API</span></span>

<span data-ttu-id="828c1-122">ARMclient viene usato per chiamare l'API REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="828c1-122">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="828c1-123">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="828c1-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="828c1-124">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="828c1-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a><span data-ttu-id="828c1-125">Creare l'istanza di Network Watcher</span><span class="sxs-lookup"><span data-stu-id="828c1-125">Create the network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="828c1-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="828c1-126">Next steps</span></span>

<span data-ttu-id="828c1-127">Dopo aver creato un'istanza di Network Watcher, è possibile approfondire le funzionalità disponibili, indicate di seguito:</span><span class="sxs-lookup"><span data-stu-id="828c1-127">Now that you have an instance of Network Watcher, learn about the features available:</span></span>

* [<span data-ttu-id="828c1-128">Topologia</span><span class="sxs-lookup"><span data-stu-id="828c1-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="828c1-129">Acquisizione pacchetti</span><span class="sxs-lookup"><span data-stu-id="828c1-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="828c1-130">Verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="828c1-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="828c1-131">Hop successivo</span><span class="sxs-lookup"><span data-stu-id="828c1-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="828c1-132">Visualizzazione di un gruppo di sicurezza</span><span class="sxs-lookup"><span data-stu-id="828c1-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="828c1-133">Registrazione dei flussi dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="828c1-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="828c1-134">Risoluzione dei problemi del gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="828c1-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="828c1-135">Dopo aver creato un'istanza di Network Watcher, è possibile configurare l'acquisizione pacchetti in base a quanto indicato nell'articolo relativo alla [creazione dell'acquisizione pacchetti attivata da avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="828c1-135">Once a Network Watcher instance has been created, package capture can be configured by following the article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











