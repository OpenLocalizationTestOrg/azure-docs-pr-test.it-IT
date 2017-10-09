---
title: prezzi e fatturazione del Bus di aaaService | Documenti Microsoft
description: Panoramica della struttura dei prezzi del Bus di servizio.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a>Informazioni sul prezzo e la fatturazione del Bus di servizio
Il bus di servizio è disponibile nei livelli Basic, Standard e [Premium](service-bus-premium-messaging.md). È possibile scegliere un livello di servizio per ogni spazio dei nomi del bus di servizio creato e questa selezione del livello si applica a tutte le entità create all'interno dello spazio dei nomi.

> [!NOTE]
> Per informazioni dettagliate sui prezzi del Bus di servizio corrente, vedere hello [pagina dei prezzi di Azure Service Bus](https://azure.microsoft.com/pricing/details/service-bus/), hello e [domande frequenti su Bus di servizio](service-bus-faq.md#pricing).
>
>

Bus di servizio Usa hello seguenti due contatori per le code e argomenti/sottoscrizioni:

1. **Operazioni di messaggistica**: definite come chiamate API sugli endpoint di servizio di code o argomenti/sottoscrizioni. Questa modalità di calcolo sostituirà i messaggi inviati o ricevuti come unità principale di hello di utilizzo fatturabile per code e argomenti/sottoscrizioni.
2. **Connessioni negoziate**: definita come numero massimo di hello delle connessioni persistenti aperte su code, argomenti o le sottoscrizioni per un periodo di campionamento di un'ora specificata. Questo calcolo si applica solo nel livello Standard hello, in cui è possibile aprire ulteriori connessioni (in precedenza, le connessioni sono state limitate too100 per ogni coda, argomento o sottoscrizione) di una tariffa nominale per connessione.

Hello **Standard** livello introduce prezzi progressiva per operazioni eseguite con code e argomenti/sottoscrizioni, risultante in sconti basati sui volumi di % too80 a livelli di utilizzo più elevati di hello. È inoltre disponibile un addebito di base di livello Standard di $10 al mese, che consente di tooperform backup too12.5 milione di operazioni al mese senza costi aggiuntivi.

Hello **Premium** livello fornisce l'isolamento di risorse a livello di CPU e memoria hello in modo che ogni carico di lavoro del cliente viene eseguita in isolamento. Questo contenitore di risorse viene chiamato *unità di messaggistica*. Ad ogni spazio dei nomi Premium viene allocata almeno un'unità di messaggistica. È possibile acquistare 1, 2 o 4 unità di messaggistica per ogni spazio dei nomi Premium del bus di servizio. Un singolo carico di lavoro o un'entità può estendersi su più unità di messaggistica e il numero di hello di unità di messaggistica può essere cambiato quando è necessario, anche se la fatturazione è previsto un addebito frequenza di 24 ore oppure ogni giorno. il risultato di Hello è prestazioni prevedibili e ripetibile per la soluzione basata sul Bus di servizio. Non solo le prestazioni sono più prevedibili e disponibili, ma anche più veloci.

Si noti che addebito di base di livello Standard hello viene addebitata una sola volta al mese per ogni sottoscrizione di Azure. Ciò significa che dopo aver creato uno spazio dei nomi Service Bus livello di singolo Standard, sarà in grado di toocreate tante Standard spazi dei nomi aggiuntivi che si desidera nella stessa sottoscrizione Azure, senza incorrere in altri addebiti di base.

Hello [ai prezzi del Bus di servizio](https://azure.microsoft.com/pricing/details/service-bus/) tabella riepiloga hello differenze funzionali tra i livelli Basic, Standard e Premium di hello.

## <a name="messaging-operations"></a>Operazioni di messaggistica
Come parte di hello nuovi prezzi, fatturazione di code e argomenti/sottoscrizioni in fase di modifica. Queste entità sono in fase di transizione dalla fatturazione in base al messaggio toobilling per ogni operazione. "Operazione" fa riferimento tooany API chiamata effettuata da un endpoint del servizio code o argomenti/sottoscrizioni. Sono incluse operazioni di stato della sessione, di invio/ricezione e di gestione.

| Tipo di operazione | Descrizione |
| --- | --- |
| gestione |Creazione, lettura, aggiornamento, eliminazione su code o argomenti/sottoscrizioni. |
| Messaggistica |Invio e ricezione di messaggi con code o argomenti/sottoscrizioni. |
| Stato sessione |Acquisizione o impostazione dello stato della sessione su una coda o un argomento o sottoscrizione. |

Per informazioni dettagliate di costo, vedere i prezzi hello elencati in hello [ai prezzi del Bus di servizio](https://azure.microsoft.com/pricing/details/service-bus/) pagina.

## <a name="brokered-connections"></a>Connessioni negoziate
Le *connessioni negoziate* sono ideali per i modelli d'uso dei clienti che prevedono un numero elevato di mittenti/destinatari "connessi in modo permanente" a code, argomenti o sottoscrizioni. I mittenti/destinatari costantemente connessi sono quelli che si connettono tramite AMQP o HTTP con un timeout di ricezione diverso da zero, ad esempio, HTTP (tempo di polling). Non generano connessioni negoziate HTTP mittenti e destinatari con un timeout immediato.

Per le quote di connessione e altri limiti di servizio, vedere hello [le quote di Service Bus](service-bus-quotas.md) articolo.

livello Standard Hello rimuove limite di connessioni negoziate per ogni spazio dei nomi di hello e conta utilizzo aggregato di connessioni negoziate in hello sottoscrizione di Azure. Per ulteriori informazioni, vedere hello [connessioni negoziate](https://azure.microsoft.com/pricing/details/service-bus/) tabella.

> [!NOTE]
> 1000 connessioni negoziate sono incluse con il livello di messaggistica Standard hello (tramite l'addebito di base hello) e possono essere condivise tra tutte le code, argomenti e sottoscrizioni nella sottoscrizione di Azure hello associata.
>
>

<br />

> [!NOTE]
> La fatturazione si basa sul numero di picco hello di connessioni simultanee e viene ripartita ogni ora in base a 744 ore al mese.
>
>

| Livello Premium |
| --- |
| Connessioni negoziate non vengono addebitate nel livello Premium hello. |

Per ulteriori informazioni sulle connessioni negoziate, vedere hello [domande frequenti su](#faq) sezione più avanti in questo argomento.

## <a name="faq"></a>domande frequenti

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a>Quali sono le connessioni negoziate e come viene effettuato l'addebito?
Una connessione negoziata è definita come uno dei seguenti hello:

1. Connessione AMQP da una coda di Service Bus tooa client o un argomento o sottoscrizione.
2. Una chiamata HTTP è tooreceive un messaggio da un argomento del Bus di servizio o una coda con un valore di timeout di ricezione maggiore di zero.

Bus di servizio per il numero massimo hello delle connessioni negoziate simultanee che superano hello incluse quantità (1.000 nel livello Standard hello). I picchi vengono misurati su base oraria, ripartiti dividendo per 744 ore al mese e sommati per hello periodo di fatturazione mensile. quantità di Hello inclusa (1000 connessioni negoziate al mese) viene applicato alla fine di hello del periodo di fatturazione hello contro somma hello dei picchi orari ripartito hello.

ad esempio:

1. Ognuno dei 10.000 dispositivi si connette tramite una singola connessione AMQP e riceve i comandi da un argomento del bus di servizio. dispositivi di Hello inviano eventi di telemetria tooan Hub eventi. Se tutti i dispositivi connettono per 12 ore ogni giorno, applica hello seguenti addebiti di connessione (in aggiunta tooany altri addebiti di argomento del Bus di servizio): 10.000 connessioni * 12 ore * 31 giorni / 744 ore = 5000 connessioni negoziate. Dopo aver hello limite mensile consentito di 1000 connessioni negoziate, vengono addebitate 4000 connessioni negoziate, pari a hello $0,03 per connessione per un totale di $120.
2. 10.000 dispositivi ricevono messaggi da una coda del Bus di servizio tramite HTTP, specificando un timeout diverso da zero. Se tutti i dispositivi connettono per 12 ore ogni giorno, verrà visualizzato hello seguenti addebiti di connessione (in aggiunta tooany altri costi del Bus di servizio): 10.000 connessioni di ricezione HTTP * 12 ore al giorno * 31 giorni / 744 ore = 5000 connessioni negoziate.

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a>Si applicano costi di connessione negoziata tooqueues e argomenti/sottoscrizioni?
Sì. Non sono previsti costi di connessione per l'invio di eventi tramite HTTP, indipendentemente dal numero di hello di invio dei sistemi o dispositivi. La ricezione di eventi con HTTP utilizzando un timeout maggiore di zero, talvolta denominato "polling prolungato" genera costi di connessione negoziata. Le connessioni AMQP generano addebiti di connessione negoziata indipendentemente dal fatto connessioni hello vengono utilizzati toosend o di ricezione. Si noti che sono consentite 100 connessioni negoziate gratuitamente in uno spazio dei nomi Basic. Questo è numero massimo di hello di connessioni negoziate consentite per hello sottoscrizione di Azure. Hello prime 1000 connessioni negoziate in tutti gli spazi dei nomi Standard in una sottoscrizione di Azure sono incluse senza alcun costo aggiuntivo (oltre addebito di base hello). Poiché le quantità consentite sono sufficienti toocover molti service to service scenari di messaggistica, addebiti di connessione negoziata in genere diventano consistenti se si prevede di toouse AMQP o HTTP polling prolungato con un numero elevato di client. ad esempio, tooachieve più efficiente evento streaming o abilitare la comunicazione bidirezionale con più dispositivi o le istanze dell'applicazione.

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni dettagliate sui prezzi del Bus di servizio, vedere hello [Bus di servizio di pagina dei prezzi](https://azure.microsoft.com/pricing/details/service-bus/).
* Vedere hello [domande frequenti su Bus di servizio](service-bus-faq.md#pricing) per alcuni comuni domande frequenti sui prezzi e fatturazione il bus di servizio.

[Azure portal]: https://portal.azure.com
