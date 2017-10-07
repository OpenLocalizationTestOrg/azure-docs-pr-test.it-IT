---
title: ispezione aaaPacket con Watcher di rete di Azure | Documenti Microsoft
description: In questo articolo viene descritto come toouse analisi approfondita dei pacchetti di rete Watcher tooperform raccolti da una macchina virtuale
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a>Ispezione dei pacchetti con Azure Network Watcher

Utilizza la funzionalità di acquisizione pacchetti hello del controllo di rete, è possibile avviare e gestire le sessioni di acquisizioni su macchine virtuali di Azure dal portale di hello, PowerShell CLI e a livello di programmazione tramite hello SDK e API REST. Acquisizione di pacchetti consente tooaddress scenari che richiedono dati a livello di pacchetto, fornendo informazioni hello in un formato facilmente utilizzabile. Sfruttando i dati di hello tooinspect strumenti liberamente disponibili, è possibile esaminare le comunicazioni inviate tooand dalle macchine virtuali e ottenere informazioni approfondite del traffico di rete. Alcuni esempi di uso dei dati di acquisizione di pacchetti includono: esame dei problemi della rete o delle applicazioni, rilevamento dell'uso improprio della rete e dei tentativi di intrusione o gestione della conformità alle normative. In questo articolo viene illustrata come tooopen un file di acquisizione di pacchetti forniti dal controllo di rete utilizzando uno strumento open source comuni. Inoltre, Microsoft fornisce esempi che mostrano come toocalculate una latenza della connessione, identificare il traffico anomalo ed esaminare le statistiche di rete.

## <a name="before-you-begin"></a>Prima di iniziare

Questo articolo descrive alcuni scenari preconfigurati in un'acquisizione di pacchetti eseguita prima. Gli scenari esaminano un'acquisizione di pacchetti per illustrare le funzionalità accessibili. Questo scenario Usa [WireShark](https://www.wireshark.org/) tooinspect acquisizione di pacchetti hello.

Questo scenario presume che sia già stata eseguita un'acquisizione di pacchetti in una macchina virtuale. modalità di acquisizione pacchetto eseguita toocreate visitare toolearn [acquisizioni di pacchetti di gestione con il portale di hello](network-watcher-packet-capture-manage-portal.md) o con REST visitando [acquisizioni di pacchetti di gestione con l'API REST](network-watcher-packet-capture-manage-rest.md).

## <a name="scenario"></a>Scenario

In questo scenario:

* Si esamina un'acquisizione di pacchetti

## <a name="calculate-network-latency"></a>Calcolare la latenza di rete

In questo scenario viene illustrata la modalità tooview hello iniziale Round Trip Time (RTT) di una conversazione di protocollo TCP (Transmission Control) che si verificano tra due endpoint.

Quando viene stabilita una connessione TCP, hello primi tre pacchetti inviati nella connessione hello seguono un handshake a tre vie hello tooas modello conosciuta. Esaminando i pacchetti hello primi due inviati questo handshake, una richiesta iniziale dal client hello e una risposta dal server hello, è possibile calcolare la latenza di hello quando è stata stabilita la connessione. Tale latenza è tooas cui hello Round Trip Time (RTT). Per ulteriori informazioni sul protocollo TCP hello e handshake a tre vie hello consultare toohello seguente risorsa. https://support.microsoft.com/it-it/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip

### <a name="step-1"></a>Passaggio 1

Avviare WireShark

### <a name="step-2"></a>Passaggio 2

Hello carico **CAP** file di acquisizione del pacchetto. Questo file è reperibile nel blob hello è stato salvato nella macchina virtuale di hello localmente nel, a seconda di come è stato configurato.

### <a name="step-3"></a>Passaggio 3

tooview hello iniziale Round Trip Time (RTT) nelle conversazioni TCP, verrà letto solo in pacchetti primi due hello coinvolti nell'handshake TCP hello. Si utilizzerà innanzitutto due i pacchetti hello in handshake a tre vie hello, che sono hello [SYN], [SYN, ACK] pacchetti. Hanno un nome per i flag impostati nell'intestazione TCP hello. non Hello ultimo pacchetto handshake hello, pacchetti hello [ACK], verrà utilizzato in questo scenario. Hello [SYN] pacchetto viene inviato dal client hello. Dopo che viene ricevuto server hello invia pacchetti hello [ACK] come una conferma di ricezione hello SYN dal client hello. Utilizzo delle tabelle dei fatti hello che risposta hello del server richiede un overhead minimo, è calcolare hello RTT sottraendo tempo hello pacchetti hello [SYN, ACK] è stato ricevuto da client hello dal pacchetto di tempo [SYN] hello inviato dal client hello.

Usando WireShark questo valore viene calcolato automaticamente.

toomore visualizzare facilmente i primi due pacchetti hello in handshake a tre vie TCP hello, verrà utilizzato il filtro delle funzionalità fornite da WireShark hello.

filtro hello tooapply WireShark, espandere hello "Transmission Control Protocol" segmento di un pacchetto [SYN] nell'acquisizione ed esaminare i flag di hello impostati nell'intestazione TCP hello.

Poiché in esame toofilter in tutti i [SYN] e [SYN, ACK] pacchetti, con flag cofirm che hello Syn bit impostato too1, quindi fare clic destro sul bit Syn hello -> Applica come filtro -> selezionati.

![Figura 7][7]

### <a name="step-4"></a>Passaggio 4

Ora che sono stati filtrati finestra tooonly vedere i pacchetti hello con hello [SYN] bit impostato, è possibile selezionare le conversazioni si è interessati a tooview hello RTT iniziale. Hello di tooview un modo semplice RTT in WireShark fare clic su elenco a discesa hello contrassegnato analysis "SEQ/ACK". Verrà quindi visualizzato hello che RTT visualizzato. In questo caso, hello RTT era 0.0022114 secondi o 2.211 ms.

![Figura 8][8]

## <a name="unwanted-protocols"></a>Protocolli indesiderati

In un'istanza di una macchina virtuale distribuita in Azure potrebbero essere in esecuzione più applicazioni. Molte di queste applicazioni di comunicare in rete hello, probabilmente senza alcuna autorizzazione esplicita. L'uso della comunicazione di rete toostore acquisizione pacchetto, è possibile esaminare come applicazione comunichino sulla rete hello e cercare eventuali problemi.

In questo esempio viene esaminata un'acquisizione di pacchetti già eseguita per trovare protocolli indesiderati che potrebbero indicare una comunicazione non autorizzata da un'applicazione in esecuzione nel computer.

### <a name="step-1"></a>Passaggio 1

Utilizzo di hello stessa acquisizione in hello precedente scenario, scegliere **statistiche** > **protocollo gerarchia**

![Menu Protocol Hierarchy (Gerarchia protocolli)][2]

verrà visualizzata la finestra gerarchia di protocollo Hello. Questa visualizzazione fornisce un elenco di tutti i protocolli di hello che erano in uso durante la sessione di acquisizione hello e numero di hello di pacchetti trasmessi e ricevuti tramite protocolli hello. Si tratta di una visualizzazione utile per trovare il traffico di rete indesiderato nelle macchine virtuali o in rete.

![Gerarchia dei protocolli aperta][3]

Come si può notare in hello dopo l'acquisizione dello schermo, si è verificato il traffico tramite il protocollo BitTorrent hello, che viene utilizzato per la condivisione di file toopeer peer. Un amministratore non si prevede toosee BitTorrent traffico specifico le macchine virtuali. Ora è consapevoli del traffico, è possibile rimuovere hello peer toopeer software installato in questa macchina virtuale o hello blocco del traffico tramite un Firewall o i gruppi di sicurezza di rete. Inoltre, è possibile scegliere toorun acquisizioni di pacchetti in una pianificazione, pertanto è possibile esaminare regolarmente hello protocollo utilizzo nelle macchine virtuali. Per un esempio sulle modalità di attività di rete tooautomate in azure visita [monitoraggio delle risorse di rete con automazione di azure](network-watcher-monitor-with-azure-automation.md)

## <a name="finding-top-destinations-and-ports"></a>Ricerca di porte e destinazioni principali

Informazioni sui tipi di hello del traffico, hello endpoint e porte hello comunicate tramite è un importante durante il monitoraggio e risoluzione dei problemi delle applicazioni e risorse di rete. Utilizzo di un file di acquisizione dei pacchetti precedente, è possibile apprendere rapidamente hello prime destinazioni la macchina virtuale sta comunicando e hello porte in uso.

### <a name="step-1"></a>Passaggio 1

Utilizzando hello stessa acquisizione in hello precedente scenario, scegliere **statistiche** > **statistiche IPv4** > **destinazioni e le porte**

![Finestra di acquisizione di pacchetti][4]

### <a name="step-2"></a>Passaggio 2

Come esaminare i risultati di hello distingue una riga, si sono verificati più connessioni sulla porta 111. porta Hello più utilizzato è 3389, ovvero desktop remoto e hello rimanenti sono porte dinamiche RPC.

Questo traffico può significare nothing, ma è una porta che veniva utilizzata per un numero di connessioni e amministratore toohello sconosciuto.

![Figura 5][5]

### <a name="step-3"></a>Passaggio 3

Ora che è stato rilevato un timeout della porta sul posto che è possibile filtrare l'acquisizione in base a una porta di hello.

filtro Hello in questo scenario sarà:

```
tcp.port == 111
```

Testo del filtro hello sopra è immettere nella casella di testo hello filtro e premere INVIO.

![Figura 6][6]

Dai risultati di hello, possiamo vedere tutto il traffico hello proviene da una macchina virtuale locale hello stessa subnet. Se ancora non comprendere perché è in corso il traffico, è possibile controllare ulteriormente toodetermine pacchetti hello motivo per cui esegue queste chiamate sulla porta 111. Con queste informazioni è possibile effettuare l'azione appropriata hello.

## <a name="next-steps"></a>Passaggi successivi

Informazioni circa hello altre funzionalità di diagnostica di rete Watcher visitando [Panoramica di monitoraggio della rete di Azure](network-watcher-monitoring-overview.md)

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













