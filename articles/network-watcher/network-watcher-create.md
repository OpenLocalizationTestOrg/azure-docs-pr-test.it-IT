---
title: aaaCreate un'istanza di controllo di rete di Azure | Documenti Microsoft
description: In questa pagina vengono hello passaggi toocreate un'istanza del controllo di rete tramite il portale di hello e API REST di Azure
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
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="adce0-103">Creare un'istanza di Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="adce0-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="adce0-104">Watcher di rete è un servizio internazionale che consente di toomonitor e diagnosticare le condizioni di livello rete scenario, a e da Azure.</span><span class="sxs-lookup"><span data-stu-id="adce0-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="adce0-105">Monitoraggio a livello di scenario consente problemi toodiagnose a una vista della rete tooend end livello.</span><span class="sxs-lookup"><span data-stu-id="adce0-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="adce0-106">Diagnostica di rete e gli strumenti di visualizzazione disponibili con Watcher di rete consentono di comprendere, diagnosticare e ottenere rete tooyour insights in Azure.</span><span class="sxs-lookup"><span data-stu-id="adce0-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="adce0-107">Watcher di rete supporta attualmente solo 1.0 CLI, hello istruzioni toocreate viene fornita una nuova istanza di controllo di rete per CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="adce0-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="adce0-108">Creare un controllo di rete nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="adce0-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="adce0-109">Passare troppo**più servizi** > **rete** > **Watcher di rete**.</span><span class="sxs-lookup"><span data-stu-id="adce0-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="adce0-110">È possibile selezionare tutte le sottoscrizioni di hello da tooenable Watcher di rete per.</span><span class="sxs-lookup"><span data-stu-id="adce0-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="adce0-111">Questa azione crea un'istanza di Network Watcher in ogni area in cui è disponibile.</span><span class="sxs-lookup"><span data-stu-id="adce0-111">This action creates a Network Watcher in every region that is available.</span></span>

![Creare un'istanza di Network Watcher][1]

<span data-ttu-id="adce0-113">Quando si abilita il Watcher di rete utilizzando hello portale, hello nome dell'istanza di hello Watcher di rete verrà automaticamente impostato tooNetworkWatcher_region_name dove region_name corrisponde toohello regione di Azure in cui è stata abilitata l'istanza di hello.</span><span class="sxs-lookup"><span data-stu-id="adce0-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="adce0-114">Ad esempio, un Network Watcher abilitato nell'area centro-occidentale degli Stati Uniti verrà denominato NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="adce0-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="adce0-115">Inoltre, istanza Watcher di rete hello verrà automaticamente aggiunto in un gruppo di risorse denominato NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="adce0-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="adce0-116">Questo gruppo di risorse verrà creato se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="adce0-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="adce0-117">Se si desidera nome hello toocustomize di un'istanza del controllo di rete e hello gruppo di risorse viene inserito in, è possibile usare Powershell, hello API REST o ARMClient metodi descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="adce0-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="adce0-118">Per ogni opzione, hello gruppo di risorse deve essere presente prima di effettuare hello Watcher di rete al suo interno.</span><span class="sxs-lookup"><span data-stu-id="adce0-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="adce0-119">Creare un'istanza di Network Watcher con PowerShell</span><span class="sxs-lookup"><span data-stu-id="adce0-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="adce0-120">toocreate un'istanza del controllo di rete, eseguire hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="adce0-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="adce0-121">Creare un controllo di rete con hello API REST</span><span class="sxs-lookup"><span data-stu-id="adce0-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="adce0-122">ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adce0-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="adce0-123">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="adce0-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="adce0-124">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="adce0-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="adce0-125">Creare il watcher di rete hello</span><span class="sxs-lookup"><span data-stu-id="adce0-125">Create hello network watcher</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="adce0-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="adce0-126">Next steps</span></span>

<span data-ttu-id="adce0-127">Dopo aver creato un'istanza del controllo di rete, informazioni sulle funzionalità di hello disponibili:</span><span class="sxs-lookup"><span data-stu-id="adce0-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="adce0-128">Topologia</span><span class="sxs-lookup"><span data-stu-id="adce0-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="adce0-129">Acquisizione pacchetti</span><span class="sxs-lookup"><span data-stu-id="adce0-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="adce0-130">Verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="adce0-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="adce0-131">Hop successivo</span><span class="sxs-lookup"><span data-stu-id="adce0-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="adce0-132">Visualizzazione di un gruppo di sicurezza</span><span class="sxs-lookup"><span data-stu-id="adce0-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="adce0-133">Registrazione dei flussi dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="adce0-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="adce0-134">Risoluzione dei problemi del gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="adce0-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="adce0-135">Dopo aver creata un'istanza del controllo di rete, l'acquisizione pacchetto può essere configurato dal seguente hello: [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="adce0-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











