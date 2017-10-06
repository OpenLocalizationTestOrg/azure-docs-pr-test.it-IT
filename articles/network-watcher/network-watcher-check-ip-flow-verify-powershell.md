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
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Verificare se il traffico è consentito o negato tooor da una macchina virtuale con flusso IP verificare un componente del controllo di rete di Azure

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST di Azure](network-watcher-check-ip-flow-verify-rest.md)


Verificare di flusso IP è una funzionalità di controllo di rete che consente tooverify se il traffico consentito tooor da una macchina virtuale. Questo scenario è utile tooget uno stato corrente di fatto una macchina virtuale possono comunicare con la risorsa esterna tooan o back-end. Verificare di flusso IP può essere utilizzato tooverify se le regole di sicurezza gruppo (rete) sono configurate correttamente e risolvere i problemi di flussi che sono bloccati dalle regole di gruppo. Un altro motivo per l'uso di IP flusso verificare tooensure che si desidera bloccare il traffico viene bloccato correttamente dal gruppo hello.

## <a name="before-you-begin"></a>Prima di iniziare

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete o dispone di un'istanza esistente del controllo di rete. scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.

## <a name="scenario"></a>Scenario

Questo flusso di scenario utilizza IP verificare tooverify se una macchina virtuale possono comunicare con tooa noti indirizzo IP di Bing. Regola di sicurezza hello che nega il traffico viene restituito se il traffico hello viene negato. informazioni sul flusso IP verificare, visitare toolearn [flusso IP verificare Panoramica](network-watcher-ip-flow-verify-overview.md)

## <a name="retrieve-network-watcher"></a>Recuperare Network Watcher

innanzitutto Hello è l'istanza di tooretrieve hello Watcher di rete. Hello `$networkWatcher` variabile viene passata toohello IP flusso verificare cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Ottenere una macchina virtuale

Flusso IP verificare tooor il traffico di test da un indirizzo IP su tooor una macchina virtuale da una destinazione remota. Un Id di una macchina virtuale è obbligatorio per i cmdlet di hello. Se si conosce già ID hello di hello toouse di macchina virtuale, è possibile ignorare questo passaggio.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a>Ottenere hello NIC

è necessario l'indirizzo IP Hello di una scheda di rete nella macchina virtuale hello, in questo esempio vengono recuperate le schede NIC hello in una macchina virtuale. Se si conosce già hello IP indirizzo che si desidera tootest sulla macchina virtuale hello, è possibile ignorare questo passaggio.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a>Eseguire la verifica del flusso IP

Ora che si dispone di informazioni hello necessari toorun hello cmdlet, eseguiamo hello `Test-AzureRmNetworkWatcherIPFlow` traffico hello tootest di cmdlet. In questo esempio, utilizziamo primo indirizzo IP di hello in hello prima scheda di rete.

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> Flusso IP verificare richiede che risorsa macchina virtuale hello è allocato toorun.

## <a name="review-results"></a>Esaminare i risultati

Dopo aver eseguito `Test-AzureRmNetworkWatcherIPFlow` hello risultati vengono restituiti, esempio hello è risultato hello restituito da hello passaggio precedente.

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a>Passaggi successivi

Se il traffico viene bloccato e non può essere, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza definiti.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













