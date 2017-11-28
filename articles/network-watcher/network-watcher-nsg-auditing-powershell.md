---
title: aaaAutomate NSG funzioni di controllo di visualizzazione del gruppo di sicurezza di controllo rete di Azure | Documenti Microsoft
description: Questa pagina vengono fornite istruzioni su come tooconfigure il controllo di un gruppo di sicurezza di rete
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="b39ae-103">Automatizzare il controllo del gruppo di sicurezza di rete con la visualizzazione del gruppo di sicurezza di rete di Network Watcher di Azure</span><span class="sxs-lookup"><span data-stu-id="b39ae-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="b39ae-104">I clienti devono spesso affrontare challenge hello di verifica delle condizioni di sicurezza hello dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="b39ae-104">Customers are often faced with hello challenge of verifying hello security posture of their infrastructure.</span></span> <span data-ttu-id="b39ae-105">Lo stesso problema si pone per le macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="b39ae-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="b39ae-106">È importante toohave un profilo di protezione simili in base alle regole di sicurezza gruppo (rete) hello applicate.</span><span class="sxs-lookup"><span data-stu-id="b39ae-106">It is important toohave a similar security profile based on hello Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="b39ae-107">Utilizza hello visualizzazione del gruppo di sicurezza, è possibile ottenere elenco hello delle regole applicate tooa VM all'interno di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="b39ae-107">Using hello Security Group View, you can now get hello list of rules applied tooa VM within an NSG.</span></span> <span data-ttu-id="b39ae-108">È possibile definire un profilo di sicurezza gruppo finale e avviare la visualizzazione del gruppo di sicurezza a un ritmo settimana e confrontare hello output finale toohello profilo e creare un report.</span><span class="sxs-lookup"><span data-stu-id="b39ae-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare hello output toohello golden profile and create a report.</span></span> <span data-ttu-id="b39ae-109">In questo modo è possibile identificare con facilità tutte le macchine virtuali hello conformi toohello previsto il profilo di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b39ae-109">This way you can identify with ease all hello VMs that do not conform toohello prescribed security profile.</span></span>

<span data-ttu-id="b39ae-110">Se non si ha familiarità con i gruppi di sicurezza di rete, visitare [Controllare il flusso del traffico di rete con i gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="b39ae-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b39ae-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b39ae-111">Before you begin</span></span>

<span data-ttu-id="b39ae-112">In questo scenario, si confronta un gruppo di sicurezza noti buona base di riferimento toohello visualizzare i risultati restituiti per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b39ae-112">In this scenario, you compare a known good baseline toohello security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="b39ae-113">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="b39ae-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="b39ae-114">scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="b39ae-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="b39ae-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="b39ae-115">Scenario</span></span>

<span data-ttu-id="b39ae-116">scenario di Hello illustrato in questo articolo Ottiene vista gruppo di sicurezza hello per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b39ae-116">hello scenario covered in this article gets hello security group view for a virtual machine.</span></span>

<span data-ttu-id="b39ae-117">In questo scenario si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="b39ae-117">In this scenario, you will:</span></span>

- <span data-ttu-id="b39ae-118">Recuperare un set di buone regole noto</span><span class="sxs-lookup"><span data-stu-id="b39ae-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="b39ae-119">Recuperare una macchina virtuale con l'API REST</span><span class="sxs-lookup"><span data-stu-id="b39ae-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="b39ae-120">Ottenere la visualizzazione del gruppo di sicurezza per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b39ae-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="b39ae-121">Valutare la risposta</span><span class="sxs-lookup"><span data-stu-id="b39ae-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="b39ae-122">Recuperare il set di regole</span><span class="sxs-lookup"><span data-stu-id="b39ae-122">Retrieve rule set</span></span>

<span data-ttu-id="b39ae-123">primo passaggio di Hello in questo esempio è toowork con una linea di base esistente.</span><span class="sxs-lookup"><span data-stu-id="b39ae-123">hello first step in this example is toowork with an existing baseline.</span></span> <span data-ttu-id="b39ae-124">esempio Hello è alcuni json estratto da un gruppo di sicurezza di rete esistente utilizzando hello `Get-AzureRmNetworkSecurityGroup` cmdlet che viene utilizzata come linea di base hello per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="b39ae-124">hello following example is some json extracted from an existing Network Security Group using hello `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as hello baseline for this example.</span></span>

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-toopowershell-objects"></a><span data-ttu-id="b39ae-125">Convertire gli oggetti tooPowerShell set di regole</span><span class="sxs-lookup"><span data-stu-id="b39ae-125">Convert rule set tooPowerShell objects</span></span>

<span data-ttu-id="b39ae-126">In questo passaggio, venga letto un file json che è stato creato in precedenza con le regole hello toobe previsto su hello il gruppo di sicurezza di rete per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="b39ae-126">In this step, we are reading a json file that was created earlier with hello rules that are expected toobe on hello Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="b39ae-127">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="b39ae-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="b39ae-128">passaggio successivo Hello è istanza di tooretrieve hello Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="b39ae-128">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="b39ae-129">Hello `$networkWatcher` variabile viene passata toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b39ae-129">hello `$networkWatcher` variable is passed toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="b39ae-130">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b39ae-130">Get a VM</span></span>

<span data-ttu-id="b39ae-131">Una macchina virtuale è obbligatorio toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet di base.</span><span class="sxs-lookup"><span data-stu-id="b39ae-131">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="b39ae-132">Hello di esempio seguente ottiene un oggetto macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b39ae-132">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="b39ae-133">Recuperare la visualizzazione del gruppo di sicurezza</span><span class="sxs-lookup"><span data-stu-id="b39ae-133">Retrieve security group view</span></span>

<span data-ttu-id="b39ae-134">passaggio successivo Hello è tooretrieve hello sicurezza gruppo Visualizza il risultato.</span><span class="sxs-lookup"><span data-stu-id="b39ae-134">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="b39ae-135">Questo risultato viene confrontato toohello "base" json che è stato illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b39ae-135">This result is compared toohello "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a><span data-ttu-id="b39ae-136">Analisi dei risultati di hello</span><span class="sxs-lookup"><span data-stu-id="b39ae-136">Analyzing hello results</span></span>

<span data-ttu-id="b39ae-137">risposta Hello è raggruppato per interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="b39ae-137">hello response is grouped by Network interfaces.</span></span> <span data-ttu-id="b39ae-138">Hello diversi tipi di regole restituite sono efficaci e regole di sicurezza predefinite.</span><span class="sxs-lookup"><span data-stu-id="b39ae-138">hello different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="b39ae-139">risultato Hello viene ulteriormente suddiviso da come viene applicata, su una subnet o una scheda di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b39ae-139">hello result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="b39ae-140">Hello script PowerShell riportato di seguito vengono confrontati hello risultati di hello output esistente tooan di visualizzazione di gruppo di sicurezza di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="b39ae-140">hello following PowerShell script compares hello results of hello Security Group View tooan existing output of an NSG.</span></span> <span data-ttu-id="b39ae-141">esempio Hello è un semplice esempio di come è possibile confrontare i risultati di hello con `Compare-Object` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b39ae-141">hello following example is a simple example of how hello results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="b39ae-142">Hello di esempio seguente è risultato hello.</span><span class="sxs-lookup"><span data-stu-id="b39ae-142">hello following example is hello result.</span></span> <span data-ttu-id="b39ae-143">È possibile visualizzare due delle regole di hello nel primo set di regole hello non erano presenti in confronto hello.</span><span class="sxs-lookup"><span data-stu-id="b39ae-143">You can see two of hello rules that were in hello first rule set were not present in hello comparison.</span></span>

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a><span data-ttu-id="b39ae-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b39ae-144">Next steps</span></span>

<span data-ttu-id="b39ae-145">Se sono state modificate le impostazioni, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza che sono in questione.</span><span class="sxs-lookup"><span data-stu-id="b39ae-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are in question.</span></span>













