---
title: traffico aaaVerify con Azure rete Watcher IP flusso verificare - CLI di Azure | Documenti Microsoft
description: "Questo articolo viene descritto come toocheck se tooor il traffico da una macchina virtuale è consentito o negato tramite l'interfaccia CLI di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Verifica se il traffico non è consentito o negato tooor da una macchina virtuale con IP flusso verificare un componente del controllo di rete di Azure

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST di Azure](network-watcher-check-ip-flow-verify-rest.md)


Flusso di IP verificare è una funzionalità di controllo di rete che consente tooverify se il traffico consentito tooor da una macchina virtuale. Questo scenario è utile tooget uno stato corrente di fatto una macchina virtuale possono comunicare con la risorsa esterna tooan o back-end. Verificare di flusso IP può essere utilizzato tooverify se le regole di sicurezza gruppo (rete) sono configurate correttamente e risolvere i problemi di flussi che sono bloccati dalle regole di gruppo. Un altro motivo per l'uso di IP flusso verificare tooensure che si desidera bloccare il traffico viene bloccato correttamente dal gruppo hello.

Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.

## <a name="before-you-begin"></a>Prima di iniziare

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete o dispone di un'istanza esistente del controllo di rete. scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.

## <a name="scenario"></a>Scenario

Questo scenario Usa tooverify IP flusso verificare se una macchina virtuale possono comunicare con tooa noti indirizzo IP di Bing. Regola di sicurezza hello che nega il traffico viene restituito se il traffico hello viene negato. toolearn ulteriori informazioni su IP flusso verificare, visitare [IP Flow verificare Overview](network-watcher-ip-flow-verify-overview.md)


## <a name="get-a-vm"></a>Ottenere una macchina virtuale

Flusso IP verificare tooor il traffico di test da un indirizzo IP su tooor una macchina virtuale da una destinazione remota. Un Id di una macchina virtuale è obbligatorio per i cmdlet di hello. Se si conosce già ID hello di hello toouse di macchina virtuale, è possibile ignorare questo passaggio.

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a>Ottenere hello NIC

è necessario l'indirizzo IP Hello di una scheda di rete nella macchina virtuale hello, in questo esempio vengono recuperate le schede NIC hello in una macchina virtuale. Se si conosce già hello IP indirizzo che si desidera tootest sulla macchina virtuale hello, è possibile ignorare questo passaggio.

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a>Eseguire la verifica del flusso IP

Ora che si dispone di informazioni hello necessari toorun hello cmdlet, eseguiamo hello `network watcher ip-flow-verify` traffico hello tootest di cmdlet. In questo esempio, utilizziamo primo indirizzo IP di hello in hello prima scheda di rete.

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> Flusso di IP verificare richiede che risorsa macchina virtuale hello è allocato toorun.

## <a name="review-results"></a>Esaminare i risultati

Dopo aver eseguito `network watcher ip-flow-verify` hello risultati vengono restituiti, esempio hello è risultato hello restituito da hello passaggio precedente.

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a>Passaggi successivi

Se il traffico viene bloccato e non può essere, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza definiti.

Informazioni su impostazioni gruppo tooaudit visitando [il controllo di sicurezza gruppi (rete) con Watcher di rete](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
