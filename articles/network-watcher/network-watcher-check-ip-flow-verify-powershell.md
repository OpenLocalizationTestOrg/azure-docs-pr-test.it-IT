---
title: Verificare il traffico con la verifica del flusso IP di Azure Network Watcher - PowerShell | Microsoft Docs
description: "Questo articolo descrive come verificare se il traffico da o verso una macchina virtuale è consentito o negato usando PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: bf0c01a9af0e28647d11ad89a9d164716d5c8312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="4f940-103">Controllare se il traffico da o verso una macchina virtuale è consentito o negato con la verifica del flusso IP, una funzionalità di Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="4f940-103">Check if traffic is allowed or denied to or from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4f940-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4f940-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="4f940-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f940-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="4f940-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="4f940-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="4f940-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="4f940-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="4f940-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="4f940-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="4f940-109">La verifica del flusso IP è una funzionalità di Network Watcher che consente di verificare se il traffico da o verso una macchina virtuale è consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="4f940-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="4f940-110">Questo scenario è utile per stabilire se una macchina virtuale può comunicare con una risorsa esterna o back-end.</span><span class="sxs-lookup"><span data-stu-id="4f940-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="4f940-111">La funzionalità può essere usata per verificare se le regole del gruppo di sicurezza di rete sono configurate correttamente e per risolvere i problemi dei flussi bloccati da tali regole.</span><span class="sxs-lookup"><span data-stu-id="4f940-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="4f940-112">La verifica del flusso IP consente inoltre di verificare che il traffico che si vuole bloccare sia correttamente bloccato dal gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="4f940-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4f940-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4f940-113">Before you begin</span></span>

<span data-ttu-id="4f940-114">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher o aprire un'istanza esistente di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="4f940-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="4f940-115">Lo scenario presuppone inoltre che esista e possa essere usato un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="4f940-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="4f940-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="4f940-116">Scenario</span></span>

<span data-ttu-id="4f940-117">Questo scenario usa la verifica del flusso IP per verificare se una macchina virtuale può comunicare con un indirizzo IP Bing noto.</span><span class="sxs-lookup"><span data-stu-id="4f940-117">This scenario uses IP flow verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="4f940-118">Se il traffico viene negato, restituisce la regola di sicurezza che nega il traffico.</span><span class="sxs-lookup"><span data-stu-id="4f940-118">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="4f940-119">Per altre informazioni sulla verifica del flusso IP, leggere la [panoramica sulla verifica del flusso IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4f940-119">To learn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="4f940-120">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="4f940-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="4f940-121">Il primo passaggio consente di recuperare l'istanza di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="4f940-121">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="4f940-122">La variabile `$networkWatcher` viene passata al cmdlet di verifica del flusso IP.</span><span class="sxs-lookup"><span data-stu-id="4f940-122">The `$networkWatcher` variable is passed to the IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="4f940-123">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4f940-123">Get a VM</span></span>

<span data-ttu-id="4f940-124">La verifica del flusso IP esegue il test del traffico da o verso un indirizzo IP su una macchina virtuale da o verso una destinazione remota.</span><span class="sxs-lookup"><span data-stu-id="4f940-124">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="4f940-125">Il cmdlet richiede un ID di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f940-125">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="4f940-126">Se l'ID della macchina virtuale da usare è già noto, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="4f940-126">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-the-nics"></a><span data-ttu-id="4f940-127">Ottenere le schede NIC</span><span class="sxs-lookup"><span data-stu-id="4f940-127">Get the NICS</span></span>

<span data-ttu-id="4f940-128">È necessario l'indirizzo IP di una scheda di rete nella macchina virtuale. In questo esempio vengono recuperate le schede NIC in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f940-128">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="4f940-129">Se l'indirizzo IP da testare nella macchina virtuale è già noto, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="4f940-129">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="4f940-130">Eseguire la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="4f940-130">Run IP flow verify</span></span>

<span data-ttu-id="4f940-131">Dopo aver ottenuto le informazioni necessarie per eseguire il cmdlet, eseguire il cmdlet `Test-AzureRmNetworkWatcherIPFlow` per testare il traffico.</span><span class="sxs-lookup"><span data-stu-id="4f940-131">Now that we have the information needed to run the cmdlet, we run the `Test-AzureRmNetworkWatcherIPFlow` cmdlet to test the traffic.</span></span> <span data-ttu-id="4f940-132">In questo esempio, viene usato il primo indirizzo IP nella prima scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="4f940-132">In this example, we are using the first IP address on the first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="4f940-133">Per eseguire la verifica del flusso IP è necessario che la risorsa della macchina virtuale sia allocata.</span><span class="sxs-lookup"><span data-stu-id="4f940-133">IP flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="4f940-134">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="4f940-134">Review Results</span></span>

<span data-ttu-id="4f940-135">Dopo aver eseguito `Test-AzureRmNetworkWatcherIPFlow` vengono restituiti i risultati. L'esempio seguente mostra i risultati restituiti nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="4f940-135">After running `Test-AzureRmNetworkWatcherIPFlow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="4f940-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f940-136">Next steps</span></span>

<span data-ttu-id="4f940-137">Se il traffico risulta bloccato e non dovrebbe esserlo, vedere [Gestire i gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) per individuare il gruppo di sicurezza di rete e le relative regole di sicurezza definite.</span><span class="sxs-lookup"><span data-stu-id="4f940-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













