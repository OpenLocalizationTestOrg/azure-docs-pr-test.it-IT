---
title: aaaFind Hop successivo con Azure rete Watcher Hop successivo - REST | Documenti Microsoft
description: "In questo articolo descrive come è possibile trovare quale hello tipo dell'hop successivo è e indirizzo ip utilizzando di Hop successivo hello API REST di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="ac9da-103">Individuare il tipo dell'hop successivo hello sta utilizzando funzionalità Hop successivo hello in Watcher di rete di Azure utilizzando l'API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="ac9da-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ac9da-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ac9da-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="ac9da-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac9da-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="ac9da-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="ac9da-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="ac9da-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="ac9da-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="ac9da-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="ac9da-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="ac9da-109">Hop successivo è una funzionalità di controllo di rete che consente di hello ottenere il tipo dell'hop successivo di hello e l'indirizzo IP in base a una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="ac9da-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="ac9da-110">Questa funzionalità è utile per determinare se il traffico da una macchina virtuale consente di scorrere un gateway, internet o reti virtuali tooget tooits destinazione.</span><span class="sxs-lookup"><span data-stu-id="ac9da-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ac9da-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ac9da-111">Before you begin</span></span>

<span data-ttu-id="ac9da-112">ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac9da-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="ac9da-113">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="ac9da-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="ac9da-114">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="ac9da-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="ac9da-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="ac9da-115">Scenario</span></span>

<span data-ttu-id="ac9da-116">scenario di Hello illustrato in questo articolo Usa Hop successivo, una funzionalità del controllo di rete che consente di trovare il tipo dell'hop successivo hello e indirizzo IP per una risorsa.</span><span class="sxs-lookup"><span data-stu-id="ac9da-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="ac9da-117">toolearn su più Hop successivo, visitare [panoramica dell'Hop successivo](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac9da-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="ac9da-118">In questo scenario si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="ac9da-118">In this scenario, you will:</span></span>

* <span data-ttu-id="ac9da-119">Recuperare l'hop successivo di hello per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ac9da-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="ac9da-120">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="ac9da-120">Log in with ARMClient</span></span>

<span data-ttu-id="ac9da-121">Accedi tooarmclient con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac9da-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="ac9da-122">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ac9da-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="ac9da-123">Eseguire hello seguenti script tooreturn una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ac9da-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="ac9da-124">Queste informazioni sono necessarie per eseguire l'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="ac9da-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="ac9da-125">Hello seguente di codice deve valori per hello seguenti variabili:</span><span class="sxs-lookup"><span data-stu-id="ac9da-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="ac9da-126">**subscriptionId** -hello toouse Id sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ac9da-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="ac9da-127">**resourceGroupName** : hello nome di un gruppo di risorse contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ac9da-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="ac9da-128">Dall'output seguente hello, id di hello della macchina virtuale hello viene utilizzato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="ac9da-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a><span data-ttu-id="ac9da-129">Ottenere l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="ac9da-129">Get Next Hop</span></span>

<span data-ttu-id="ac9da-130">Dopo aver creata un'intestazione authorization hello, hop successivo di hello da una macchina virtuale può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="ac9da-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="ac9da-131">Hello valori seguenti devono essere sostituiti per toowork di esempio di codice hello.</span><span class="sxs-lookup"><span data-stu-id="ac9da-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="ac9da-132">Per l'API REST di controllo rete chiamate hello Nome gruppo di risorse nella richiesta di hello che URI è gruppo di risorse hello contenente hello Watcher di rete, non le risorse hello si eseguono operazioni di diagnostica hello in.</span><span class="sxs-lookup"><span data-stu-id="ac9da-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="ac9da-133">Hop successivo è necessario che risorsa macchina virtuale hello è allocato toorun.</span><span class="sxs-lookup"><span data-stu-id="ac9da-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="ac9da-134">Risultati</span><span class="sxs-lookup"><span data-stu-id="ac9da-134">Results</span></span>

<span data-ttu-id="ac9da-135">Hello frammento di codice seguente è riportato un esempio dell'output di hello ricevuto.</span><span class="sxs-lookup"><span data-stu-id="ac9da-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="ac9da-136">risultati di Hello contengono hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="ac9da-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="ac9da-137">**nextHopType** -questo valore è uno dei seguenti valori hello: Internet, VirtualAppliance, gateway di rete virtuale, VnetLocal, HyperNetGateway o nessuno.</span><span class="sxs-lookup"><span data-stu-id="ac9da-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="ac9da-138">**nextHopIpAddress** -indirizzo IP dell'hop successivo hello hello.</span><span class="sxs-lookup"><span data-stu-id="ac9da-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="ac9da-139">**routeTableId** - valore hello è l'uri per la tabella di route hello associato hello route o se non definita dall'utente route è il valore di hello definito di *sistema Route* viene restituito.</span><span class="sxs-lookup"><span data-stu-id="ac9da-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="ac9da-140">di seguito Hello sono risultati hello in formato json.</span><span class="sxs-lookup"><span data-stu-id="ac9da-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="ac9da-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac9da-141">Next steps</span></span>

<span data-ttu-id="ac9da-142">Una volta che è stato in grado di toofind all'hop successivo di hello per una macchina virtuale, è possibile visualizzare sicurezza hello delle risorse di rete, visitare il sito [Panoramica di vista della sicurezza](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ac9da-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














