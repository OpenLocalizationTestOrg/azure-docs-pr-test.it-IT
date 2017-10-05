---
title: Analizzare la protezione di rete con la visualizzazione del gruppo di sicurezza di rete di Network Watcher di Azure - PowerShell | Documentazione Microsoft
description: Questo articolo descrive come usare PowerShell per analizzare la protezione di macchine virtuali con la visualizzazione di un gruppo di sicurezza.
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
ms.openlocfilehash: 363fdd9f1de933bb4050f91e1e111aaf3e419058
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="80488-103">Analizzare la protezione della macchina virtuale visualizzando un gruppo di sicurezza con PowerShell</span><span class="sxs-lookup"><span data-stu-id="80488-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="80488-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80488-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="80488-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="80488-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="80488-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="80488-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="80488-107">API REST</span><span class="sxs-lookup"><span data-stu-id="80488-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="80488-108">La visualizzazione di un gruppo di sicurezza consente di recuperare le regole di sicurezza di rete configurate ed effettive applicate a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="80488-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="80488-109">Questa funzionalità è utile per controllare e diagnosticare i gruppi di sicurezza di rete e le regole configurate in una macchina virtuale per verificare che il traffico viene consentito o negato in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="80488-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="80488-110">Questo articolo illustra come recuperare le regole di sicurezza configurate ed effettive applicate a una macchina virtuale tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="80488-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="80488-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="80488-111">Before you begin</span></span>

<span data-ttu-id="80488-112">In questo scenario, il cmdlet `Get-AzureRmNetworkWatcherSecurityGroupView` viene eseguito per recuperare le informazioni sulla regola di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="80488-112">In this scenario, you run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet to retrieve the security rule information.</span></span>

<span data-ttu-id="80488-113">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="80488-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="80488-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="80488-114">Scenario</span></span>

<span data-ttu-id="80488-115">Lo scenario illustrato in questo articolo recupera le regole di sicurezza configurate ed effettive applicate a una determinata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="80488-115">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="80488-116">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="80488-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="80488-117">Il primo passaggio consente di recuperare l'istanza di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="80488-117">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="80488-118">Questa variabile viene passata al cmdlet `Get-AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="80488-118">This variable is passed to the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="80488-119">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="80488-119">Get a VM</span></span>

<span data-ttu-id="80488-120">È necessario che una macchina virtuale esegua il cmdlet `Get-AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="80488-120">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="80488-121">Nell'esempio seguente viene ottenuto un oggetto macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="80488-121">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="80488-122">Recuperare la visualizzazione del gruppo di sicurezza</span><span class="sxs-lookup"><span data-stu-id="80488-122">Retrieve security group view</span></span>

<span data-ttu-id="80488-123">Il passaggio successivo prevede il recupero del risultato della visualizzazione del gruppo di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="80488-123">The next step is to retrieve the security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-the-results"></a><span data-ttu-id="80488-124">Visualizzazione dei risultati</span><span class="sxs-lookup"><span data-stu-id="80488-124">Viewing the results</span></span>

<span data-ttu-id="80488-125">L'esempio seguente è una risposta abbreviata dei risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="80488-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="80488-126">I risultati mostrano tutte le regole di sicurezza effettive e applicate alla macchina virtuale, suddivise nei gruppi **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** e **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="80488-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="80488-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="80488-127">Next steps</span></span>

<span data-ttu-id="80488-128">Consultare [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Verifica dei gruppi di sicurezza di rete con Network Watcher) per informazioni su come automatizzare la verifica dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="80488-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


