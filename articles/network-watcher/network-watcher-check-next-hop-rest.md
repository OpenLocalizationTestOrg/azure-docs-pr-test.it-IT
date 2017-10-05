---
title: "Individuare l'hop successivo con la funzionalità Hop successivo di Network Watcher di Azure - REST | Documentazione Microsoft"
description: "Questo articolo descrive come individuare il tipo di hop successivo e l'indirizzo IP mediante la funzionalità Hop successivo usando l'API REST di Azure"
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
ms.openlocfilehash: 644713d365191bf5e51517d0cc565efbc2abc144
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="6cff9-103">Individuare il tipo di hop successivo tramite la funzionalità Hop successivo di Network Watcher di Azure usando l'API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="6cff9-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6cff9-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6cff9-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="6cff9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cff9-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="6cff9-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="6cff9-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="6cff9-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="6cff9-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="6cff9-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="6cff9-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="6cff9-109">Hop successivo è una funzionalità di Network Watcher che consente di recuperare il tipo di hop successivo e l'indirizzo IP in base a una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="6cff9-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="6cff9-110">La funzionalità è utile per determinare se il traffico in uscita da una macchina virtuale attraversa gateway, Internet o reti virtuali per arrivare alla propria destinazione.</span><span class="sxs-lookup"><span data-stu-id="6cff9-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6cff9-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="6cff9-111">Before you begin</span></span>

<span data-ttu-id="6cff9-112">ARMclient viene usato per chiamare l'API REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6cff9-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="6cff9-113">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="6cff9-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="6cff9-114">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="6cff9-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="6cff9-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="6cff9-115">Scenario</span></span>

<span data-ttu-id="6cff9-116">Lo scenario illustrato in questo articolo usa la funzionalità Hop successivo di Network Watcher che rileva il tipo di hop successivo e l'indirizzo IP di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="6cff9-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="6cff9-117">Per altre informazioni sulla funzionalità di individuazione dell'hop successivo, consultare la [panoramica sulla funzionalità Hop successivo](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6cff9-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="6cff9-118">In questo scenario si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="6cff9-118">In this scenario, you will:</span></span>

* <span data-ttu-id="6cff9-119">Recuperare l'hop successivo per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6cff9-119">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="6cff9-120">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="6cff9-120">Log in with ARMClient</span></span>

<span data-ttu-id="6cff9-121">Accedere ad armclient con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cff9-121">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="6cff9-122">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6cff9-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="6cff9-123">Eseguire lo script seguente per restituire la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6cff9-123">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="6cff9-124">Queste informazioni sono necessarie per eseguire l'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="6cff9-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="6cff9-125">Il codice seguente richiede i valori per le variabili seguenti:</span><span class="sxs-lookup"><span data-stu-id="6cff9-125">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="6cff9-126">**subscriptionId**: l'ID sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="6cff9-126">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="6cff9-127">**resourceGroupName**: il nome di un gruppo di risorse contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6cff9-127">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="6cff9-128">L'ID della macchina virtuale dell'output seguente viene usato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cff9-128">From the following output, the id of the virtual machine is used in the following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="6cff9-129">Ottenere l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="6cff9-129">Get Next Hop</span></span>

<span data-ttu-id="6cff9-130">Dopo aver creato l'intestazione di autorizzazione, è possibile recuperare l'hop successivo da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6cff9-130">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="6cff9-131">Perché l'esempio di codice funzioni devono essere sostituiti i valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="6cff9-131">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> <span data-ttu-id="6cff9-132">Per le chiamate dell'API REST di Network Watcher, il nome del gruppo di risorse nell'URI della richiesta è il gruppo di risorse che contiene Network Watcher, non le risorse su cui eseguono le azioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="6cff9-132">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

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
> <span data-ttu-id="6cff9-133">La funzionalità Hop successivo richiede che la risorsa VM sia allocata.</span><span class="sxs-lookup"><span data-stu-id="6cff9-133">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="results"></a><span data-ttu-id="6cff9-134">Risultati</span><span class="sxs-lookup"><span data-stu-id="6cff9-134">Results</span></span>

<span data-ttu-id="6cff9-135">Il seguente frammento di codice è un esempio dell'output ricevuto.</span><span class="sxs-lookup"><span data-stu-id="6cff9-135">The following snippet is an example of the output received.</span></span> <span data-ttu-id="6cff9-136">I risultati contengono i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="6cff9-136">The results contain the following values:</span></span>

* <span data-ttu-id="6cff9-137">**nextHopType**: questo è uno dei seguenti valori: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway o None.</span><span class="sxs-lookup"><span data-stu-id="6cff9-137">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="6cff9-138">**nextHopIpAddress**: l'indirizzo IP dell'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="6cff9-138">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="6cff9-139">**routeTableId**: il valore è un URI per la tabella di route associata alla route oppure, se non ci sono route definite dall'utente, viene restituito il valore *System Route*.</span><span class="sxs-lookup"><span data-stu-id="6cff9-139">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="6cff9-140">Di seguito sono riportati i risultati in formato json.</span><span class="sxs-lookup"><span data-stu-id="6cff9-140">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="6cff9-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6cff9-141">Next steps</span></span>

<span data-ttu-id="6cff9-142">Dopo aver scoperto l'hop successivo per una macchina virtuale, è possibile visualizzare le informazioni sulla sicurezza delle risorse di rete visitando [Security View overview](network-watcher-security-group-view-overview.md) (Panoramica della visualizzazione della sicurezza)</span><span class="sxs-lookup"><span data-stu-id="6cff9-142">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














