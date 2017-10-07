---
title: aaaFind hop successivo con rete Azure Watcher Hop successivo - CLI di Azure 1.0 | Documenti Microsoft
description: "In questo articolo viene descritto come è possibile trovare quale hello tipo dell'hop successivo è e tramite indirizzo ip dell'Hop successivo utilizzando l'interfaccia CLI di Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a>Individuare il tipo dell'hop successivo hello sta utilizzando funzionalità Hop successivo hello in Watcher di rete di Azure mediante Azure CLI 1.0

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST di Azure](network-watcher-check-next-hop-rest.md)

Hop successivo è una funzionalità di controllo di rete che consente di hello ottenere il tipo dell'hop successivo di hello e l'indirizzo IP in base a una macchina virtuale specificata. Questa funzionalità è utile per determinare se il traffico da una macchina virtuale consente di scorrere un gateway, internet o reti virtuali tooget tooits destinazione.

Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.

## <a name="before-you-begin"></a>Prima di iniziare

In questo scenario, si utilizzerà il tipo dell'hop successivo di CLI di Azure toofind hello hello e l'indirizzo IP.

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete. scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.

## <a name="scenario"></a>Scenario

scenario di Hello illustrato in questo articolo Usa Hop successivo, una funzionalità del controllo di rete che consente di trovare il tipo dell'hop successivo hello e indirizzo IP per una risorsa. toolearn su più Hop successivo, visitare [panoramica dell'Hop successivo](network-watcher-next-hop-overview.md).


## <a name="get-next-hop"></a>Ottenere l'hop successivo

tooget hello dell'hop successivo è chiamare hello `azure netowrk watcher next-hop` cmdlet. Passiamo hello NetworkWatcher, gruppo di risorse di hello cmdlet hello Watcher di rete, la macchina virtuale Id, indirizzo IP di origine e indirizzo IP di destinazione. In questo esempio, indirizzo IP di destinazione hello è tooa macchina virtuale in un'altra rete virtuale. È un gateway di rete virtuale tra due reti virtuali hello. 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
Se è abilitato l'inoltro IP in una delle schede di rete hello hello VM ha più schede di rete, quindi hello parametro NIC (-i nic-id) deve essere specificato. In caso contrario, è facoltativo.

## <a name="review-results"></a>Esaminare i risultati

Al termine, vengono forniti i risultati di hello. indirizzo IP dell'hop successivo Hello viene restituito nonché il tipo di hello della risorsa che è.

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
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
