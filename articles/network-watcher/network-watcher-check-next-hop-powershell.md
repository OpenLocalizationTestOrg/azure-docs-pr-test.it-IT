---
title: aaaFind hop successivo con rete Azure Watcher Hop successivo - PowerShell | Documenti Microsoft
description: "In questo articolo viene descritto come è possibile trovare quale hello tipo dell'hop successivo è e tramite indirizzo ip dell'Hop successivo utilizzo di PowerShell."
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
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="2f816-103">Individuare il tipo dell'hop successivo hello sta utilizzando funzionalità Hop successivo hello in Watcher di rete di Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f816-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2f816-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2f816-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="2f816-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f816-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="2f816-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="2f816-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="2f816-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="2f816-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="2f816-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="2f816-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="2f816-109">Hop successivo è una funzionalità di controllo di rete che consente di hello ottenere il tipo dell'hop successivo di hello e l'indirizzo IP in base a una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="2f816-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="2f816-110">Questa funzionalità è utile per determinare se il traffico da una macchina virtuale consente di scorrere un gateway, internet o reti virtuali tooget tooits destinazione.</span><span class="sxs-lookup"><span data-stu-id="2f816-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2f816-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2f816-111">Before you begin</span></span>

<span data-ttu-id="2f816-112">In questo scenario, si utilizzerà il tipo dell'hop successivo di toofind portale Azure hello hello e l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="2f816-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="2f816-113">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="2f816-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="2f816-114">scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="2f816-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2f816-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="2f816-115">Scenario</span></span>

<span data-ttu-id="2f816-116">scenario di Hello illustrato in questo articolo Usa Hop successivo, una funzionalità del controllo di rete che consente di trovare il tipo dell'hop successivo hello e indirizzo IP per una risorsa.</span><span class="sxs-lookup"><span data-stu-id="2f816-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="2f816-117">toolearn su più Hop successivo, visitare [panoramica dell'Hop successivo](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f816-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="2f816-118">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="2f816-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="2f816-119">innanzitutto Hello è l'istanza di tooretrieve hello Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="2f816-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="2f816-120">Hello `$networkWatcher` variabile viene passata l'hop successivo toohello verificare cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f816-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="2f816-121">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2f816-121">Get a virtual machine</span></span>

<span data-ttu-id="2f816-122">Hop successivo restituisce hop successivo hello e hello l'indirizzo IP dell'hop successivo hello da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2f816-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="2f816-123">Un Id di una macchina virtuale è obbligatorio per i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="2f816-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="2f816-124">Se si conosce già ID hello di hello toouse di macchina virtuale, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="2f816-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="2f816-125">Hop successivo è necessario che risorsa macchina virtuale hello è allocato toorun.</span><span class="sxs-lookup"><span data-stu-id="2f816-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="2f816-126">Ottenere le interfacce di rete hello</span><span class="sxs-lookup"><span data-stu-id="2f816-126">Get hello network interfaces</span></span>

<span data-ttu-id="2f816-127">è necessario l'indirizzo IP Hello di una scheda di rete nella macchina virtuale hello, in questo esempio vengono recuperate le schede NIC hello in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2f816-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="2f816-128">Se si conosce già hello IP indirizzo che si desidera tootest sulla macchina virtuale hello, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="2f816-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="2f816-129">Ottenere l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="2f816-129">Get Next Hop</span></span>

<span data-ttu-id="2f816-130">Ora è chiamare hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f816-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="2f816-131">Abbiamo passare hello cmdlet hello Watcher di rete, la macchina virtuale Id, origine, indirizzo IP e indirizzo IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2f816-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="2f816-132">In questo esempio, indirizzo IP di destinazione hello è tooa macchina virtuale in un'altra rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2f816-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="2f816-133">È un gateway di rete virtuale tra due reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="2f816-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="2f816-134">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="2f816-134">Review results</span></span>

<span data-ttu-id="2f816-135">Al termine, vengono forniti i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="2f816-135">When complete, hello results are provided.</span></span> <span data-ttu-id="2f816-136">indirizzo IP dell'hop successivo Hello viene restituito nonché il tipo di hello della risorsa che è.</span><span class="sxs-lookup"><span data-stu-id="2f816-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="2f816-137">In questo scenario, è l'indirizzo IP pubblico di hello del gateway di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="2f816-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="2f816-138">Hello seguito sono elencati i valori NextHopType hello attualmente disponibili:</span><span class="sxs-lookup"><span data-stu-id="2f816-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="2f816-139">**Tipo di hop successivo**</span><span class="sxs-lookup"><span data-stu-id="2f816-139">**Next Hop Type**</span></span>

* <span data-ttu-id="2f816-140">Internet</span><span class="sxs-lookup"><span data-stu-id="2f816-140">Internet</span></span>
* <span data-ttu-id="2f816-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="2f816-141">VirtualAppliance</span></span>
* <span data-ttu-id="2f816-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="2f816-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="2f816-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="2f816-143">VnetLocal</span></span>
* <span data-ttu-id="2f816-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="2f816-144">HyperNetGateway</span></span>
* <span data-ttu-id="2f816-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="2f816-145">VnetPeering</span></span>
* <span data-ttu-id="2f816-146">None</span><span class="sxs-lookup"><span data-stu-id="2f816-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f816-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f816-147">Next steps</span></span>

<span data-ttu-id="2f816-148">Informazioni su come tooreview le impostazioni di gruppo di sicurezza di rete a livello di codice, visitare il sito [NSG il controllo con Watcher di rete](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="2f816-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















