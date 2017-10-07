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
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a>Automatizzare il controllo del gruppo di sicurezza di rete con la visualizzazione del gruppo di sicurezza di rete di Network Watcher di Azure

I clienti devono spesso affrontare challenge hello di verifica delle condizioni di sicurezza hello dell'infrastruttura. Lo stesso problema si pone per le macchine virtuali in Azure. È importante toohave un profilo di protezione simili in base alle regole di sicurezza gruppo (rete) hello applicate. Utilizza hello visualizzazione del gruppo di sicurezza, è possibile ottenere elenco hello delle regole applicate tooa VM all'interno di un gruppo. È possibile definire un profilo di sicurezza gruppo finale e avviare la visualizzazione del gruppo di sicurezza a un ritmo settimana e confrontare hello output finale toohello profilo e creare un report. In questo modo è possibile identificare con facilità tutte le macchine virtuali hello conformi toohello previsto il profilo di sicurezza.

Se non si ha familiarità con i gruppi di sicurezza di rete, visitare [Controllare il flusso del traffico di rete con i gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)

## <a name="before-you-begin"></a>Prima di iniziare

In questo scenario, si confronta un gruppo di sicurezza noti buona base di riferimento toohello visualizzare i risultati restituiti per una macchina virtuale.

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete. scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.

## <a name="scenario"></a>Scenario

scenario di Hello illustrato in questo articolo Ottiene vista gruppo di sicurezza hello per una macchina virtuale.

In questo scenario si apprenderà come:

- Recuperare un set di buone regole noto
- Recuperare una macchina virtuale con l'API REST
- Ottenere la visualizzazione del gruppo di sicurezza per la macchina virtuale
- Valutare la risposta

## <a name="retrieve-rule-set"></a>Recuperare il set di regole

primo passaggio di Hello in questo esempio è toowork con una linea di base esistente. esempio Hello è alcuni json estratto da un gruppo di sicurezza di rete esistente utilizzando hello `Get-AzureRmNetworkSecurityGroup` cmdlet che viene utilizzata come linea di base hello per questo esempio.

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

## <a name="convert-rule-set-toopowershell-objects"></a>Convertire gli oggetti tooPowerShell set di regole

In questo passaggio, venga letto un file json che è stato creato in precedenza con le regole hello toobe previsto su hello il gruppo di sicurezza di rete per questo esempio.

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a>Recuperare Network Watcher

passaggio successivo Hello è istanza di tooretrieve hello Watcher di rete. Hello `$networkWatcher` variabile viene passata toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Ottenere una macchina virtuale

Una macchina virtuale è obbligatorio toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet di base. Hello di esempio seguente ottiene un oggetto macchina virtuale.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a>Recuperare la visualizzazione del gruppo di sicurezza

passaggio successivo Hello è tooretrieve hello sicurezza gruppo Visualizza il risultato. Questo risultato viene confrontato toohello "base" json che è stato illustrato in precedenza.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a>Analisi dei risultati di hello

risposta Hello è raggruppato per interfacce di rete. Hello diversi tipi di regole restituite sono efficaci e regole di sicurezza predefinite. risultato Hello viene ulteriormente suddiviso da come viene applicata, su una subnet o una scheda di rete virtuale.

Hello script PowerShell riportato di seguito vengono confrontati hello risultati di hello output esistente tooan di visualizzazione di gruppo di sicurezza di un gruppo. esempio Hello è un semplice esempio di come è possibile confrontare i risultati di hello con `Compare-Object` cmdlet.

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

Hello di esempio seguente è risultato hello. È possibile visualizzare due delle regole di hello nel primo set di regole hello non erano presenti in confronto hello.

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

## <a name="next-steps"></a>Passaggi successivi

Se sono state modificate le impostazioni, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza che sono in questione.













