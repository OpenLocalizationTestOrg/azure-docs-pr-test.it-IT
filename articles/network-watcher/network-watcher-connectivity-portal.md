---
title: "connettività aaaCheck con Watcher di rete di Azure - portale di Azure | Documenti Microsoft"
description: "Questa pagina viene illustrato come toouse connettività verificare con il Watcher di rete utilizzando hello portale di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a>Verificare la connettività con Watcher di rete di Azure utilizzando hello portale di Azure

> [!div class="op_single_selector"]
> - [Portale](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-connectivity-cli.md)
> - [API REST di Azure](network-watcher-connectivity-rest.md)

Informazioni su come è possibile stabilire toouse connettività tooverify se una connessione TCP diretta da una macchina virtuale di tooa dato endpoint.

## <a name="before-you-begin"></a>Prima di iniziare

Questo articolo si presuppone di che aver hello seguenti risorse:

* Un'istanza del controllo di rete nell'area di hello desiderato toocheck connettività.

* Connettività toocheck di macchine virtuali con.

> [!IMPORTANT]
> Il controllo della connettività richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`. Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-tooa-virtual-machine"></a>Verificare la connettività tooa virtual machine

Questo esempio viene verificata la connettività tooa macchina virtuale di destinazione sulla porta 80.

Passare tooyour Watcher di rete e fare clic su **verifica della connettività (anteprima)**. Selezionare la connettività di hello macchina virtuale toocheck da. In hello **destinazione** sezione scegliere **selezionare una macchina virtuale** e scegliere porta tootest e la macchina virtuale corretta hello.

Quando si fa clic su **controllare**, vengono controllati connettività hello tra le macchine virtuali hello sulla porta hello specificato. Nell'esempio hello hello destinazione macchina virtuale non è raggiungibile, vengono visualizzati un elenco di hop.

![Verificare i risultati di connettività per una macchina virtuale][1]

## <a name="check-remote-endpoint-connectivity"></a>Verificare la connettività dell'endpoint remoto

connettività hello toocheck e l'endpoint remoto tooa di latenza, scegliere hello **specificare manualmente** pulsante di opzione nella hello **destinazione** sezione input hello url e la porta hello e fare clic su **controllare** .  Questa procedura può essere usata per endpoint remoti come siti Web ed endpoint di archiviazione.

![Verificare i risultati di connettività per un sito Web][2]

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)

Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
