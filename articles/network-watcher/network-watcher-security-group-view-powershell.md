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
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a>Analizzare la protezione della macchina virtuale visualizzando un gruppo di sicurezza con PowerShell

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-security-group-view-cli.md)
> - [API REST](network-watcher-security-group-view-rest.md)

Visualizzazione del gruppo di sicurezza restituisce regole di sicurezza di rete configurate ed efficace di macchina virtuale tooa applicato. Questa funzionalità è utile tooaudit e diagnosticare i gruppi di sicurezza di rete e le regole configurate per il traffico tooensure una macchina virtuale viene correttamente consentito o negato. In questo articolo viene illustrata la modalità di configurazione tooretrieve hello e sicurezza efficace regole tooa macchina virtuale mediante PowerShell

## <a name="before-you-begin"></a>Prima di iniziare

In questo scenario, si esegue hello `Get-AzureRmNetworkWatcherSecurityGroupView` informazioni sulle regole di sicurezza di cmdlet tooretrieve hello.

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.

## <a name="scenario"></a>Scenario

scenario di Hello illustrato in questo articolo recupera hello configurato e le regole di sicurezza efficace per una macchina virtuale specificata.

## <a name="retrieve-network-watcher"></a>Recuperare Network Watcher

innanzitutto Hello è l'istanza di tooretrieve hello Watcher di rete. Questa variabile viene passata toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a>Ottenere una macchina virtuale

Una macchina virtuale è obbligatorio toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet di base. Hello di esempio seguente ottiene un oggetto macchina virtuale.

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a>Recuperare la visualizzazione del gruppo di sicurezza

passaggio successivo Hello è tooretrieve hello sicurezza gruppo Visualizza il risultato.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a>Visualizzazione dei risultati hello

Hello seguito è riportata una risposta abbreviata di hello risultati restituiti. Hello risultati mostrano tutte le regole di sicurezza efficace e applicato hello nella macchina virtuale hello suddiviso in gruppi di **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.

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

## <a name="next-steps"></a>Passaggi successivi

Visitare [il controllo di sicurezza gruppi (rete) con Watcher di rete](network-watcher-nsg-auditing-powershell.md) toolearn come tooautomate convalida dei gruppi di sicurezza di rete.


