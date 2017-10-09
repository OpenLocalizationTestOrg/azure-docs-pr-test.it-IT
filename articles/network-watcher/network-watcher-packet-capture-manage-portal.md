---
title: acquisizioni di pacchetti aaaManage con Watcher di rete di Azure - portale di Azure | Documenti Microsoft
description: "Questa pagina viene illustrato come toomanage hello funzionalità di acquisizione di pacchetti di controllo di rete tramite il portale di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a>Gestire le acquisizioni di pacchetti con Watcher di rete di Azure tramite il portale di hello

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API REST di Azure](network-watcher-packet-capture-manage-rest.md)

Acquisizione di pacchetti di rete Watcher consente tooand toocreate acquisizione sessioni tootrack traffico da una macchina virtuale. I filtri vengono forniti per hello acquisizione sessione tooensure che si acquisisce solo il traffico hello desiderato. Acquisizione di pacchetti consente toodiagnose anomalie di rete in modo proattivo e reattivo. Altri usi includono la raccolta di statistiche di rete, ottenere informazioni su intrusioni di rete, client-server toodebug le comunicazioni e molto altro ancora. Essendo in grado di tooremotely trigger pacchetto acquisizioni, questa funzionalità semplifica il carico di hello dell'esecuzione di acquisizione pacchetto eseguita manualmente e nel computer desiderato hello, che consente di risparmiare tempo prezioso.

In questo articolo illustra hello diverse operazioni di gestione che sono attualmente disponibili per l'acquisizione di pacchetti.

- [**Avviare un'acquisizione di pacchetti**](#start-a-packet-capture)
- [**Interrompere un'acquisizione di pacchetti**](#stop-a-packet-capture)
- [**Eliminare un'acquisizione di pacchetti**](#delete-a-packet-capture)
- [**Scaricare un'acquisizione di pacchetti**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Prima di iniziare

Questo articolo si presuppone di aver hello seguenti risorse:

- Un'istanza del controllo di rete nell'area di hello desiderato toocreate un'acquisizione pacchetti
- Una macchina virtuale con i pacchetti hello acquisire estensione abilitata.

> [!IMPORTANT]
> L'acquisizione di pacchetti richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`. Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-hello-portal"></a>Estensione tramite il portale di hello agente acquisizione pacchetti

acquisizione di pacchetti hello tooinstall agente della macchina virtuale tramite il portale di hello, passare una macchina virtuale tooyour, fare clic su **estensioni** > **Aggiungi** e cercare **rete Watcher agente per Windows**

![Visualizzazione agente][agent]

## <a name="packet-capture-overview"></a>Panoramica dell'acquisizione di pacchetti

Passare toohello [portale di Azure](https://portal.azure.com) e fare clic su **rete** > **Watcher di rete** > **acquisizione pacchetti**

pagina di panoramica Hello mostra che un elenco di tutti i pacchetti acquisisce che esistono indipendentemente dal stato hello.

> [!NOTE]
> Acquisizione pacchetto richiede account di archiviazione di connettività toohello sulla porta 443.

![Schermata della panoramica di acquisizione di pacchetti][1]

## <a name="start-a-packet-capture"></a>Avviare un'acquisizione di pacchetti

Fare clic su **Aggiungi** toocreate un'acquisizione di pacchetti.

sono proprietà Hello che può essere definita in un'acquisizione di pacchetti.

**Impostazioni principali**

- **Sottoscrizione** -questo valore è una sottoscrizione di hello utilizzato, è necessaria un'istanza del controllo di rete in ogni sottoscrizione.
- **Gruppo di risorse** -gruppo di risorse hello della macchina virtuale hello cui si fa riferimento.
- **Macchina virtuale di destinazione** -macchina virtuale hello che esegue l'acquisizione di pacchetti hello
- **Nome dell'acquisizione pacchetto** -questo valore è il nome di hello dell'acquisizione di pacchetti hello.

**Acquisisci configurazione**

- **Account di archiviazione**: determina se l'acquisizione di pacchetti viene salvata in un'account di archiviazione.
- **File** -determina se un'acquisizione pacchetto viene salvata in locale nella macchina virtuale hello.
- **Gli account di archiviazione** -hello selezionato acquisizione pacchetto nell'archiviazione account toosave hello. Il percorso predefinito è https://{nome account di archiviazione}.blob.core.windows.net/network-watcher-logs/subscriptions/{ID sottoscrizione}/resourcegroups/{nome gruppo di risorse}/providers/microsoft.compute/virtualmachines/{nome macchina virtuale}/{AA}/{MM}/{GG}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap. È abilitato solo se viene selezionato **Archiviazione**.
- **Percorso del file locale** -percorso locale di hello su un'acquisizione di pacchetti hello toosave macchina virtuale. È abilitato solo se viene selezionato **File**. È necessario specificare un percorso valido
- **Numero massimo di byte per ogni pacchetto** -hello numero di byte da ogni pacchetto che vengono acquisiti, vengono acquisiti tutti i byte se lasciato vuoto.
- **Numero massimo di byte per ogni sessione** - totale numero di byte che vengono acquisiti, una volta raggiunto il valore di hello arresta acquisizione di pacchetti hello.
- **Il limite di tempo (secondi)** -imposta un limite di tempo per toostop di acquisizione di pacchetti hello. Il valore predefinito è 18000 secondi.

> [!NOTE]
> Gli account di archiviazione Premium non sono attualmente supportati per l'archiviazione delle acquisizioni di pacchetti.

**Filtro (facoltativo)**

- **Protocollo** -hello toofilter di protocollo per l'acquisizione di pacchetti hello. i valori disponibili Hello sono TCP, UDP e qualsiasi.
- **L'indirizzo IP locale** -questo valore consente di filtrare toopackets acquisizione di pacchetti hello in cui l'indirizzo IP locale hello corrisponde a questo valore di filtro.
- **Porta locale** -questo valore consente di filtrare toopackets acquisizione di pacchetti hello in cui la porta locale hello corrisponde a questo valore di filtro.
- **Indirizzo IP remoto** -questo valore consente di filtrare toopackets acquisizione di pacchetti hello in IP remoti hello corrisponde a questo valore di filtro.
- **Porta remota** -questo valore consente di filtrare toopackets acquisizione di pacchetti hello in cui la porta remota hello corrisponde a questo valore di filtro.

> [!NOTE]
> I valori di indirizzo IP e porta possono essere un valore singolo, un intervallo di valori o un set, ovvero 80-1024 per la porta. È possibile definire tutti i filtri desiderati.

Una volta che vengono compilati i valori hello, fare clic su **OK** toocreate acquisizione di pacchetti hello.

![Creare un'acquisizione di pacchetti][2]

Dopo aver impostato il limite di tempo hello in acquisizione pacchetti hello è scaduto, acquisizione pacchetti hello verrà interrotta e può essere esaminati. È possibile arrestare manualmente sessioni di acquisizioni di pacchetti hello.

## <a name="delete-a-packet-capture"></a>Eliminare un'acquisizione di pacchetti

Nel pacchetto di hello acquisizione visualizzazione, fare clic su hello **menu di scelta rapida** (...) o fare clic destro e fare clic su **eliminare** acquisizione di pacchetti hello toostop

![Eliminare un'acquisizione di pacchetti][3]

> [!NOTE]
> L'eliminazione di un'acquisizione di pacchetti non elimina il file hello nell'account di archiviazione hello.

Verrà chiesto tooconfirm desiderato di acquisizione di pacchetti hello toodelete, fare clic su **Sì**

![Conferma][4]

## <a name="stop-a-packet-capture"></a>Interrompere un'acquisizione di pacchetti

Nel pacchetto di hello acquisizione visualizzazione, fare clic su hello **menu di scelta rapida** (...) o fare clic destro e fare clic su **arrestare** acquisizione di pacchetti hello toostop

## <a name="download-a-packet-capture"></a>Scaricare un'acquisizione di pacchetti

Una volta completata la sessione di acquisizione di pacchetti, file di acquisizione hello è caricato tooblob tooa o archiviazione locale file hello macchina virtuale. percorso di archiviazione Hello dell'acquisizione di pacchetti hello è definito al momento della creazione della sessione hello. Tooaccess un utile strumento questi file di acquisizione di account di archiviazione tooa salvato è Microsoft Azure Storage Explorer, che può essere scaricata qui: http://storageexplorer.com/

Se viene specificato un account di archiviazione, i file di acquisizione dei pacchetti vengono salvati tooa account di archiviazione in hello seguente posizione:
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)

Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













