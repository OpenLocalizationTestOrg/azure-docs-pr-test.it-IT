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
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>Individuare il tipo dell'hop successivo hello sta utilizzando funzionalità Hop successivo hello in Watcher di rete di Azure tramite PowerShell

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST di Azure](network-watcher-check-next-hop-rest.md)

Hop successivo è una funzionalità di controllo di rete che consente di hello ottenere il tipo dell'hop successivo di hello e l'indirizzo IP in base a una macchina virtuale specificata. Questa funzionalità è utile per determinare se il traffico da una macchina virtuale consente di scorrere un gateway, internet o reti virtuali tooget tooits destinazione.

## <a name="before-you-begin"></a>Prima di iniziare

In questo scenario, si utilizzerà il tipo dell'hop successivo di toofind portale Azure hello hello e l'indirizzo IP.

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete. scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.

## <a name="scenario"></a>Scenario

scenario di Hello illustrato in questo articolo Usa Hop successivo, una funzionalità del controllo di rete che consente di trovare il tipo dell'hop successivo hello e indirizzo IP per una risorsa. toolearn su più Hop successivo, visitare [panoramica dell'Hop successivo](network-watcher-next-hop-overview.md).

## <a name="retrieve-network-watcher"></a>Recuperare Network Watcher

innanzitutto Hello è l'istanza di tooretrieve hello Watcher di rete. Hello `$networkWatcher` variabile viene passata l'hop successivo toohello verificare cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>Ottenere una macchina virtuale

Hop successivo restituisce hop successivo hello e hello l'indirizzo IP dell'hop successivo hello da una macchina virtuale. Un Id di una macchina virtuale è obbligatorio per i cmdlet di hello. Se si conosce già ID hello di hello toouse di macchina virtuale, è possibile ignorare questo passaggio.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> Hop successivo è necessario che risorsa macchina virtuale hello è allocato toorun.

## <a name="get-hello-network-interfaces"></a>Ottenere le interfacce di rete hello

è necessario l'indirizzo IP Hello di una scheda di rete nella macchina virtuale hello, in questo esempio vengono recuperate le schede NIC hello in una macchina virtuale. Se si conosce già hello IP indirizzo che si desidera tootest sulla macchina virtuale hello, è possibile ignorare questo passaggio.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>Ottenere l'hop successivo

Ora è chiamare hello `Get-AzureRmNetworkWatcherNextHop` cmdlet. Abbiamo passare hello cmdlet hello Watcher di rete, la macchina virtuale Id, origine, indirizzo IP e indirizzo IP di destinazione. In questo esempio, indirizzo IP di destinazione hello è tooa macchina virtuale in un'altra rete virtuale. È un gateway di rete virtuale tra due reti virtuali hello.

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>Esaminare i risultati

Al termine, vengono forniti i risultati di hello. indirizzo IP dell'hop successivo Hello viene restituito nonché il tipo di hello della risorsa che è. In questo scenario, è l'indirizzo IP pubblico di hello del gateway di rete virtuale hello.

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

Hello seguito sono elencati i valori NextHopType hello attualmente disponibili:

**Tipo di hop successivo**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooreview le impostazioni di gruppo di sicurezza di rete a livello di codice, visitare il sito [NSG il controllo con Watcher di rete](network-watcher-nsg-auditing-powershell.md)

















