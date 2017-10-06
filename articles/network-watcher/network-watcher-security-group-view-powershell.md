---
title: sicurezza di rete aaaAnalyze con visualizzazione gruppo di sicurezza di controllo di rete di Azure - PowerShell | Documenti Microsoft
description: In questo articolo viene descritto come toouse PowerShell tooanalyze un virtuale macchine protezione con visualizzazione del gruppo di sicurezza.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="870fb-103">Analizzare la protezione della macchina virtuale visualizzando un gruppo di sicurezza con PowerShell</span><span class="sxs-lookup"><span data-stu-id="870fb-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="870fb-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="870fb-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="870fb-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="870fb-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="870fb-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="870fb-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="870fb-107">API REST</span><span class="sxs-lookup"><span data-stu-id="870fb-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="870fb-108">Visualizzazione del gruppo di sicurezza restituisce regole di sicurezza di rete configurate ed efficace di macchina virtuale tooa applicato.</span><span class="sxs-lookup"><span data-stu-id="870fb-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="870fb-109">Questa funzionalità è utile tooaudit e diagnosticare i gruppi di sicurezza di rete e le regole configurate per il traffico tooensure una macchina virtuale viene correttamente consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="870fb-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="870fb-110">In questo articolo viene illustrata la modalità di configurazione tooretrieve hello e sicurezza efficace regole tooa macchina virtuale mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="870fb-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="870fb-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="870fb-111">Before you begin</span></span>

<span data-ttu-id="870fb-112">In questo scenario, si esegue hello `Get-AzureRmNetworkWatcherSecurityGroupView` informazioni sulle regole di sicurezza di cmdlet tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="870fb-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="870fb-113">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="870fb-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="870fb-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="870fb-114">Scenario</span></span>

<span data-ttu-id="870fb-115">scenario di Hello illustrato in questo articolo recupera hello configurato e le regole di sicurezza efficace per una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="870fb-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="870fb-116">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="870fb-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="870fb-117">innanzitutto Hello è l'istanza di tooretrieve hello Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="870fb-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="870fb-118">Questa variabile viene passata toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="870fb-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="870fb-119">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="870fb-119">Get a VM</span></span>

<span data-ttu-id="870fb-120">Una macchina virtuale è obbligatorio toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet di base.</span><span class="sxs-lookup"><span data-stu-id="870fb-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="870fb-121">Hello di esempio seguente ottiene un oggetto macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="870fb-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="870fb-122">Recuperare la visualizzazione del gruppo di sicurezza</span><span class="sxs-lookup"><span data-stu-id="870fb-122">Retrieve security group view</span></span>

<span data-ttu-id="870fb-123">passaggio successivo Hello è tooretrieve hello sicurezza gruppo Visualizza il risultato.</span><span class="sxs-lookup"><span data-stu-id="870fb-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="870fb-124">Visualizzazione dei risultati hello</span><span class="sxs-lookup"><span data-stu-id="870fb-124">Viewing hello results</span></span>

<span data-ttu-id="870fb-125">Hello seguito è riportata una risposta abbreviata di hello risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="870fb-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="870fb-126">Hello risultati mostrano tutte le regole di sicurezza efficace e applicato hello nella macchina virtuale hello suddiviso in gruppi di **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="870fb-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="870fb-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="870fb-127">Next steps</span></span>

<span data-ttu-id="870fb-128">Visitare [il controllo di sicurezza gruppi (rete) con Watcher di rete](network-watcher-nsg-auditing-powershell.md) toolearn come tooautomate convalida dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="870fb-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


