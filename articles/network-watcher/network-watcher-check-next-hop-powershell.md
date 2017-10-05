---
title: Individuare l'hop successivo con Network Watcher di Azure - PowerShell | Documentazione Microsoft
description: "Questo articolo descrive come individuare il tipo di hop successivo e l'indirizzo IP tramite la funzionalità Hop successivo usando PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 00161e7c6fb4becdb7d8eab266fa27128e50f8ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="1db5d-103">Individuare il tipo di hop successivo tramite la funzionalità Hop successivo di Network Watcher di Azure usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="1db5d-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1db5d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1db5d-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="1db5d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1db5d-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="1db5d-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="1db5d-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="1db5d-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="1db5d-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="1db5d-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="1db5d-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="1db5d-109">Hop successivo è una funzionalità di Network Watcher che consente di recuperare il tipo di hop successivo e l'indirizzo IP in base a una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="1db5d-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="1db5d-110">La funzionalità è utile per determinare se il traffico in uscita da una macchina virtuale attraversa gateway, Internet o reti virtuali per arrivare alla propria destinazione.</span><span class="sxs-lookup"><span data-stu-id="1db5d-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1db5d-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="1db5d-111">Before you begin</span></span>

<span data-ttu-id="1db5d-112">In questo scenario viene usato il portale di Azure per trovare il tipo di hop successivo e l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="1db5d-112">In this scenario, you will use the Azure portal to find the next hop type and IP address.</span></span>

<span data-ttu-id="1db5d-113">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="1db5d-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="1db5d-114">Lo scenario presuppone inoltre che esista e possa essere usato un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="1db5d-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="1db5d-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="1db5d-115">Scenario</span></span>

<span data-ttu-id="1db5d-116">Lo scenario illustrato in questo articolo usa la funzionalità Hop successivo di Network Watcher che rileva il tipo di hop successivo e l'indirizzo IP di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="1db5d-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="1db5d-117">Per altre informazioni sulla funzionalità di individuazione dell'hop successivo, consultare la [panoramica sulla funzionalità Hop successivo](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1db5d-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="1db5d-118">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="1db5d-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="1db5d-119">Il primo passaggio consente di recuperare l'istanza di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="1db5d-119">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="1db5d-120">La variabile `$networkWatcher` viene passata al cmdlet di verifica dell'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="1db5d-120">The `$networkWatcher` variable is passed to the next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="1db5d-121">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1db5d-121">Get a virtual machine</span></span>

<span data-ttu-id="1db5d-122">La funzionalità Hop successivo restituisce l'hop successivo e l'indirizzo IP dell'hop successivo da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1db5d-122">Next hop returns the next hop and the IP address of the next hop from a virtual machine.</span></span> <span data-ttu-id="1db5d-123">Il cmdlet richiede un ID di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1db5d-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="1db5d-124">Se l'ID della macchina virtuale da usare è già noto, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="1db5d-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="1db5d-125">La funzionalità Hop successivo richiede che la risorsa VM sia allocata.</span><span class="sxs-lookup"><span data-stu-id="1db5d-125">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="get-the-network-interfaces"></a><span data-ttu-id="1db5d-126">Ottenere le interfacce di rete</span><span class="sxs-lookup"><span data-stu-id="1db5d-126">Get the network interfaces</span></span>

<span data-ttu-id="1db5d-127">È necessario l'indirizzo IP di una scheda di rete nella macchina virtuale. In questo esempio vengono recuperate le schede NIC in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1db5d-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="1db5d-128">Se l'indirizzo IP da testare nella macchina virtuale è già noto, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="1db5d-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="1db5d-129">Ottenere l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="1db5d-129">Get Next Hop</span></span>

<span data-ttu-id="1db5d-130">Ora chiamiamo il cmdlet `Get-AzureRmNetworkWatcherNextHop`.</span><span class="sxs-lookup"><span data-stu-id="1db5d-130">Now we call the `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="1db5d-131">Al cmdlet vengono passati il Network Watcher, l'ID della macchina virtuale, l'indirizzo IP di origine e l'indirizzo IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1db5d-131">We pass the cmdlet the Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="1db5d-132">Nell'esempio seguente l'indirizzo IP di destinazione corrisponde a una macchina virtuale in un'altra rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1db5d-132">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="1db5d-133">Tra le due reti virtuali esiste un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1db5d-133">There is a virtual network gateway between the two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="1db5d-134">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="1db5d-134">Review results</span></span>

<span data-ttu-id="1db5d-135">Al termine vengono forniti i risultati.</span><span class="sxs-lookup"><span data-stu-id="1db5d-135">When complete, the results are provided.</span></span> <span data-ttu-id="1db5d-136">Viene inoltre restituito l'indirizzo IP dell'hop successivo e il tipo di risorsa corrispondente.</span><span class="sxs-lookup"><span data-stu-id="1db5d-136">The next hop IP address is returned as well as the type of resource it is.</span></span> <span data-ttu-id="1db5d-137">In questo scenario è l'indirizzo IP pubblico del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1db5d-137">In this scenario, it is the public IP address of the virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="1db5d-138">L'elenco seguente mostra i valori NextHopType attualmente disponibili:</span><span class="sxs-lookup"><span data-stu-id="1db5d-138">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="1db5d-139">**Tipo di hop successivo**</span><span class="sxs-lookup"><span data-stu-id="1db5d-139">**Next Hop Type**</span></span>

* <span data-ttu-id="1db5d-140">Internet</span><span class="sxs-lookup"><span data-stu-id="1db5d-140">Internet</span></span>
* <span data-ttu-id="1db5d-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="1db5d-141">VirtualAppliance</span></span>
* <span data-ttu-id="1db5d-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="1db5d-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="1db5d-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="1db5d-143">VnetLocal</span></span>
* <span data-ttu-id="1db5d-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="1db5d-144">HyperNetGateway</span></span>
* <span data-ttu-id="1db5d-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="1db5d-145">VnetPeering</span></span>
* <span data-ttu-id="1db5d-146">None</span><span class="sxs-lookup"><span data-stu-id="1db5d-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="1db5d-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1db5d-147">Next steps</span></span>

<span data-ttu-id="1db5d-148">Per altre informazioni su come verificare le impostazioni del gruppo di sicurezza di rete a livello di codice, consultare l'articolo su come [verificare i gruppi di sicurezza di rete con Network Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="1db5d-148">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















