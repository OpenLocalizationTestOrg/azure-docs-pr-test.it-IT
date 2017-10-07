---
title: aaaFind hop successivo con rete Azure Watcher Hop successivo - portale di Azure | Documenti Microsoft
description: "In questo articolo descrive come è possibile trovare quale hello tipo dell'hop successivo è e indirizzo ip utilizzando di Hop successivo hello portale di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>Individuare il tipo dell'hop successivo hello sta utilizzando funzionalità Hop successivo hello in Watcher di rete di Azure tramite il portale di hello

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST di Azure](network-watcher-check-next-hop-rest.md)

Hop successivo è una funzionalità di controllo di rete che consente di hello ottenere il tipo dell'hop successivo di hello e l'indirizzo IP in base a una macchina virtuale specificata. Questa funzionalità è utile per determinare se il traffico da una macchina virtuale consente di scorrere un gateway, internet o reti virtuali tooget tooits destinazione.

## <a name="before-you-begin"></a>Prima di iniziare

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete. scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.

## <a name="scenario"></a>Scenario

scenario di Hello illustrato in questo articolo Usa toofind hop successivo tipo dell'hop successivo hello e indirizzo IP per una risorsa. toolearn su più Hop successivo, visitare [panoramica dell'Hop successivo](network-watcher-next-hop-overview.md).

In questo scenario si apprenderà come:

* Recuperare l'hop successivo hello da una macchina virtuale.

## <a name="get-next-hop"></a>Ottenere l'hop successivo

### <a name="step-1"></a>Passaggio 1

Passare risorsa Watcher di rete tooyour hello portale di Azure.

### <a name="step-2"></a>Passaggio 2

Fare clic su **hop successivo** nel riquadro di spostamento hello, macchina virtuale selezionare hello e interfaccia di rete, compilare hello IP di origine e di destinazione e fare clic su hello **hop successivo** pulsante.

> [!NOTE]
> Hop successivo è necessario che risorsa macchina virtuale hello è allocato toorun.

![Panoramica di come ottenere l'hop successivo][1]

### <a name="step-3"></a>Passaggio 3

Una volta completata l'attività hello, vengono forniti i risultati di hello. Hello indirizzo IP e il tipo dell'hop successivo hello di dispositivo, viene visualizzata. Hello nella tabella seguente mostra i valori restituiti di hello disponibili nel portale di hello.

**Tipo di hop successivo**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Nessuno

Se una route personalizzata è stata utilizzata tooroute il traffico, route definite dall'utente hello (UDR) viene visualizzato anche con risultati hello.

![Risultati dell'ottenimento dell'hop successivo][2]

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooreview le impostazioni di gruppo di sicurezza di rete a livello di codice, visitare il sito [NSG il controllo con Watcher di rete](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














