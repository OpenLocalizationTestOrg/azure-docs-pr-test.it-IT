---
title: Verificare il traffico aaaverify con flusso di controllo indirizzo IP rete di Azure - PowerShell | Documenti Microsoft
description: "Questo articolo viene descritto come toocheck se tooor il traffico da una macchina virtuale è consentito o negato tramite PowerShell"
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
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="4ac2e-103">Verificare se il traffico è consentito o negato tooor da una macchina virtuale con flusso IP verificare un componente del controllo di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="4ac2e-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4ac2e-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4ac2e-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="4ac2e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ac2e-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="4ac2e-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="4ac2e-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="4ac2e-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="4ac2e-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="4ac2e-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="4ac2e-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="4ac2e-109">Verificare di flusso IP è una funzionalità di controllo di rete che consente tooverify se il traffico consentito tooor da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="4ac2e-110">Questo scenario è utile tooget uno stato corrente di fatto una macchina virtuale possono comunicare con la risorsa esterna tooan o back-end.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="4ac2e-111">Verificare di flusso IP può essere utilizzato tooverify se le regole di sicurezza gruppo (rete) sono configurate correttamente e risolvere i problemi di flussi che sono bloccati dalle regole di gruppo.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="4ac2e-112">Un altro motivo per l'uso di IP flusso verificare tooensure che si desidera bloccare il traffico viene bloccato correttamente dal gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4ac2e-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4ac2e-113">Before you begin</span></span>

<span data-ttu-id="4ac2e-114">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete o dispone di un'istanza esistente del controllo di rete.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="4ac2e-115">scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="4ac2e-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="4ac2e-116">Scenario</span></span>

<span data-ttu-id="4ac2e-117">Questo flusso di scenario utilizza IP verificare tooverify se una macchina virtuale possono comunicare con tooa noti indirizzo IP di Bing.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="4ac2e-118">Regola di sicurezza hello che nega il traffico viene restituito se il traffico hello viene negato.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="4ac2e-119">informazioni sul flusso IP verificare, visitare toolearn [flusso IP verificare Panoramica](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4ac2e-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="4ac2e-120">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="4ac2e-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="4ac2e-121">innanzitutto Hello è l'istanza di tooretrieve hello Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="4ac2e-122">Hello `$networkWatcher` variabile viene passata toohello IP flusso verificare cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="4ac2e-123">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4ac2e-123">Get a VM</span></span>

<span data-ttu-id="4ac2e-124">Flusso IP verificare tooor il traffico di test da un indirizzo IP su tooor una macchina virtuale da una destinazione remota.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="4ac2e-125">Un Id di una macchina virtuale è obbligatorio per i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="4ac2e-126">Se si conosce già ID hello di hello toouse di macchina virtuale, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="4ac2e-127">Ottenere hello NIC</span><span class="sxs-lookup"><span data-stu-id="4ac2e-127">Get hello NICS</span></span>

<span data-ttu-id="4ac2e-128">è necessario l'indirizzo IP Hello di una scheda di rete nella macchina virtuale hello, in questo esempio vengono recuperate le schede NIC hello in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="4ac2e-129">Se si conosce già hello IP indirizzo che si desidera tootest sulla macchina virtuale hello, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="4ac2e-130">Eseguire la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="4ac2e-130">Run IP flow verify</span></span>

<span data-ttu-id="4ac2e-131">Ora che si dispone di informazioni hello necessari toorun hello cmdlet, eseguiamo hello `Test-AzureRmNetworkWatcherIPFlow` traffico hello tootest di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="4ac2e-132">In questo esempio, utilizziamo primo indirizzo IP di hello in hello prima scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="4ac2e-133">Flusso IP verificare richiede che risorsa macchina virtuale hello è allocato toorun.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="4ac2e-134">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="4ac2e-134">Review Results</span></span>

<span data-ttu-id="4ac2e-135">Dopo aver eseguito `Test-AzureRmNetworkWatcherIPFlow` hello risultati vengono restituiti, esempio hello è risultato hello restituito da hello passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="4ac2e-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ac2e-136">Next steps</span></span>

<span data-ttu-id="4ac2e-137">Se il traffico viene bloccato e non può essere, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza definiti.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













