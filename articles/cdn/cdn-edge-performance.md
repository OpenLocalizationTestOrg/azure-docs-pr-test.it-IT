---
title: le prestazioni del nodo perimetrale aaaAnalyze nella rete CDN di Azure | Documenti Microsoft
description: Analizzare le prestazioni del nodo perimetrale nella rete CDN di Microsoft Azure. Bordo prestazioni Analitica fornisce informazioni granulare di utilizzo di larghezza di banda e il traffico per hello CDN.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 8cc596a7-3e01-4f76-af7b-a05a1421517e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 35361d1c5e27fc6b8536c29e33c2ed217ee4d17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-edge-node-performance-in-microsoft-azure-cdn"></a>Analizzare le prestazioni del nodo perimetrale nella rete CDN di Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Panoramica
Analitica prestazioni Edge fornisce informazioni granulare di utilizzo di larghezza di banda e il traffico per hello CDN. Queste informazioni possono quindi essere statistiche sulle tendenze toogenerate usato, che consentono di toogain informazioni dettagliate su come gli asset vengono memorizzate nella cache e recapitati tooyour client. A sua volta, in questo modo si tooform una strategia per il recapito di hello toooptimize del contenuto e toodetermine problemi che deve essere affrontati toobetter hello di utilizzo della rete CDN. Di conseguenza, non solo sarà in grado di tooimprove le prestazioni di distribuzione dati, ma sarà inoltre essere in grado di tooreduce i costi di rete CDN.

> [!NOTE]
> Tutti i report usano la notazione UTC/GMT quando specificano una data/ora.
> 
> 

## <a name="reports-and-log-collection"></a>Report e raccolta di log
Dati di attività della rete CDN devono essere raccolti dal modulo Edge prestazioni Analitica hello prima che è possibile generare rapporti su di esso. Questo processo di raccolta si verifica una volta al giorno e spiega attività hello avvenute hello giorno precedente. Ciò significa che le statistiche di un report rappresentano un campione di statistiche del giorno hello in fase di hello è stata elaborata e non necessariamente contenere set di dati per hello completo hello giorno corrente. funzione principale di Hello di questi rapporti è tooassess prestazioni. Non devono essere usati per finalità relative alla fatturazione o per estrarre statistiche numeriche.

> [!NOTE]
> dati non elaborati di Hello da cui vengono generati report analitici di prestazioni Edge sono disponibili per almeno 90 giorni.
> 
> 

## <a name="dashboard"></a>Dashboard
dashboard Edge prestazioni Analitica Hello tiene traccia del traffico di rete CDN attuali e cronologico tramite un grafico e le statistiche. Usare questo dashboard toodetect recente e a lungo termine le tendenze sulle prestazioni di hello del traffico di rete CDN per l'account.

Il dashboard è costituito da:

* Un grafico interattivo che consente la visualizzazione hello di metriche chiave e le tendenze.
* Una sequenza temporale che fornisce indicazioni relative ai modelli a lungo termine per le metriche chiave e le tendenze.
* Metriche chiave e informazioni statistiche sul modo in cui la rete CDN migliora il traffico del sito, sulla base dei dati complessivi relativi a prestazioni, utilizzo ed efficienza.

### <a name="accessing-hello-edge-performance-dashboard"></a>L'accesso ai dashboard di prestazioni edge hello
1. Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    viene visualizzato il portale di gestione della rete CDN Hello.
2. Passare il mouse su hello **Analitica** scheda, quindi passare il mouse su hello **bordo prestazioni Analitica** riquadro a comparsa.  Fare clic su **Dashboard**.
   
    Hello edge nodo analitica dashboard viene visualizzato.

### <a name="chart"></a>Grafico
dashboard Hello contiene un grafico che tiene traccia di una metrica su hello periodo di tempo selezionato nella sequenza temporale hello visualizzato direttamente inferiore.  Una sequenza temporale in un grafico di toohello ultimi due anni di attività della rete CDN viene visualizzata direttamente sotto il grafico hello.

#### <a name="using-hello-chart"></a>Utilizzo di hello grafico
* Per impostazione predefinita, verrà rappresentato i tasso l'efficienza della cache di hello per hello ultimi 30 giorni.
* Questo grafico viene generato dai dati raccolti su base giornaliera.
* Passaggio del mouse su un giorno nel grafico a linee hello indicherà un valore di data e hello della metrica hello in tale data.
* Fare clic su fine settimana evidenziare tootoggle una sovrapposizione di colore grigio chiare barre verticali che rappresentano i fine settimana nel grafico hello. Questo tipo di overlay è utile per identificare i modelli di traffico nei fine settimana.
* Fare clic su Visualizza un anno fa tootoggle una sovrapposizione di hello precedente di attività anno su hello stesso periodo, nel grafico hello. Questo tipo di confronto fornisce approfondimenti relativi ai modelli di utilizzo a lungo termine della rete CDN. Nell'angolo superiore destro di Hello del grafico hello contiene una legenda che indica il codice colore hello per ogni grafico a linee.

#### <a name="updating-hello-chart"></a>Aggiornamento di hello grafico
* Intervallo di tempo: Eseguire uno dei seguenti hello:
  * Selezionare la regione desiderata hello nella sequenza temporale hello. Hello grafico verrà aggiornato con i dati che corrisponde a toohello periodo di tempo selezionato.
  * Fare doppio clic su hello grafico toodisplay tutti i dati cronologici disponibili backup tooa massimo di due anni.
* Metrica: Fare clic su hello grafico visualizzata al successivo metrica toohello desiderato. grafico Hello e sequenza temporale hello verranno aggiornati con dati di metrica corrispondente hello.

### <a name="key-metrics-and-statistics"></a>Metriche chiave e statistiche
#### <a name="efficiency-metrics"></a>Metriche relative all'efficienza
scopo di Hello di queste metriche è toosee se è possibile migliorare l'efficienza della cache. vantaggi principali di Hello derivati dall'efficienza della cache sono:

* Riduzione del carico dei server di origine hello ciò potrebbe portare a:
  * Migliori prestazioni del server Web.
  * Costi operativi ridotti.
* Migliorata l'accelerazione di recapito di dati poiché saranno servite più richieste direttamente da hello CDN.

| Campo | Descrizione |
| --- | --- |
| Efficienza della cache |Indica una percentuale di hello di dati trasferiti in cui è stato fornito dalla cache. Questa metrica misure quando una versione memorizzata nella cache di hello richiesto è stato fornito il contenuto direttamente dal hello toorequesters (server edge) della rete CDN (ad esempio, il browser web) |
| Percentuale riscontri |Indica la percentuale hello di richieste che sono state soddisfatte dalla cache. Questa metrica misure quando una versione memorizzata nella cache di hello richiesto è stato fornito il contenuto direttamente dal hello toorequesters (server edge) della rete CDN (ad esempio, il browser web). |
| % di byte remoti - Nessuna cache configurata |Indica la percentuale hello di traffico di cui è stata gestita dal server di origine toohello CDN (server edge) che non verranno memorizzate in seguito a funzionalità di ignorare la Cache di hello (motore di regole HTTP). |
| % di byte remoti - Cache scaduta |Indica la percentuale di hello di traffico di cui è stata gestita dal server di origine toohello CDN (server edge) come risultato la riconvalida del contenuto non aggiornata. |

#### <a name="usage-metrics"></a>Metriche di utilizzo
scopo di Hello di queste metriche è tooprovide approfondite hello riduzione dei costi misure seguenti:

* Riduzione dei costi operativi tramite hello CDN.
* Riduzione delle spese della rete CDN tramite l'efficienza e la compressione della cache.

> [!NOTE]
> Numeri di volume di traffico rappresentano il traffico che è stato utilizzato nel calcolo dei rapporti e percentuali e potrebbe visualizzare una parte del traffico totale hello solo per i clienti con volumi elevati.
> 
> 

| Campo | Descrizione |
| --- | --- |
| Media byte in uscita |Indica hello numero medio di byte trasferiti per ogni richiesta servita dal richiedente di toohello hello CDN (server edge) (ad esempio, il browser web). |
| Velocità in byte senza cache configurata |Indica la percentuale hello del traffico servito da hello CDN (server edge) toohello richiedente (ad esempio, il browser web) che non verrà memorizzate a causa di funzionalità di ignorare la Cache toohello. |
| Velocità in byte con compressione |Indica la percentuale hello del traffico inviato da hello toorequesters (server edge) della rete CDN (ad esempio, il browser web) in un formato compresso. |
| Byte in uscita |Indica la quantità hello dei dati, in byte, che sono stati recapitati dal richiedente di toohello hello CDN (server edge) (ad esempio, il browser web). |
| Byte in entrata |Indica la quantità hello dei dati, in byte, inviati dal toohello richiedenti (ad esempio, il browser web) della rete CDN (server edge). |
| Byte remoti |Indica la quantità hello dei dati, in byte inviati dalla rete CDN e cliente toohello di server di origine della rete CDN (server edge). |

#### <a name="performance-metrics"></a>Metriche delle prestazioni
scopo di Hello di queste metriche è tootrack complessivo delle prestazioni della rete CDN per il traffico.

| Campo | Descrizione |
| --- | --- |
| Velocità di trasferimento |Indica in corrispondenza del quale è stato trasferito il contenuto dal richiedente di hello CDN tooa la frequenza media hello. |
| Duration |Indica il tempo medio di hello, in millisecondi, impiegato toodeliver un richiedente tooa asset (ad esempio, il browser web). |
| Velocità richieste con compressione |Indica la percentuale hello di accessi che sono stati recapitati dal richiedente di toohello hello CDN (server edge) (ad esempio, il browser web) in un formato compresso. |
| Frequenza degli errori 4xx |Indica la percentuale hello di accessi che ha generato un codice di stato 4xx. |
| Frequenza degli errori 5xx |Indica la percentuale hello di accessi che ha generato un codice di stato 5xx. |
| Riscontri |Indica il numero di hello di richieste di contenuto della rete CDN. |

#### <a name="secure-traffic-metrics"></a>Metriche relative al traffico sicuro
scopo di Hello di queste metriche è tootrack delle prestazioni di rete CDN per il traffico HTTPS.

| Campo | Descrizione |
| --- | --- |
| Efficienza della cache sicura |Indica la percentuale hello di dati trasferiti per le richieste HTTPS che sono state soddisfatte dalla cache. Questa metrica misura quando è richiesta una versione memorizzata nella cache di hello contenuto è stato fornito direttamente dalla rete CDN (server edge) toorequesters (ad esempio, il browser web) hello tramite HTTPS. |
| Velocità di trasferimento sicuro |Indica il tasso di medio hello in corrispondenza del quale è stato trasferito il contenuto da hello toorequesters (server edge) della rete CDN (ad esempio, il server web) tramite HTTPS. |
| Durata media sicura |Indica il tempo medio di hello, in millisecondi, impiegato toodeliver un richiedente tooa asset (ad esempio, il browser web) tramite HTTPS. |
| Riscontri sicuri |Indica il numero di hello di richieste HTTPS per il contenuto della rete CDN. |
| Byte sicuri in uscita |Indica la quantità hello del traffico HTTPS, in byte, che sono stati recapitati dal richiedente di toohello hello CDN (server edge) (ad esempio, il browser web). |

## <a name="reports"></a>Report
Ogni report in questo modulo contiene un grafico e statistiche relative a larghezza di banda e utilizzo del traffico per diversi tipi di metriche, ad esempio codici di stato HTTP, codici di stato della cache, URL di richiesta e così via. Queste informazioni potrebbero essere utilizzati toodelve ulteriormente il contenuto viene servito tooyour client e le prestazioni di distribuzione dati toofine ottimizzazione della rete CDN comportamento tooimprove.

### <a name="accessing-hello-edge-performance-reports"></a>Accesso ai report di prestazioni edge hello
1. Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    viene visualizzato il portale di gestione della rete CDN Hello.
2. Passare il mouse su hello **Analitica** scheda, quindi passare il mouse su hello **bordo prestazioni Analitica** riquadro a comparsa.  Fare clic su **Oggetto di grandi dimensioni HTTP**.
   
    viene visualizzata la schermata report Hello edge nodo analitica.

| Report | Descrizione |
| --- | --- |
| Riepilogo giornaliero |Consente le tendenze di traffico giornaliero tooview in un periodo di tempo specificato. Ogni barra di questo grafico rappresenta una data specifica. dimensioni Hello della barra di hello indica hello Totale riscontri per cui si è verificato in tale data. |
| Riepilogo orario |Consente le tendenze di traffico oraria tooview in un periodo di tempo specificato. Ogni barra di questo grafico rappresenta una singola ora in una data specifica. dimensioni Hello della barra di hello indica hello Totale riscontri per cui si è verificato durante quell'ora. |
| Protocolli |Visualizza suddivisione hello del traffico tra hello HTTP e protocolli HTTPS. Grafico ad anello indica la percentuale hello di riscontri per cui si è verificato per ogni tipo di protocollo. |
| Metodi HTTP |Consente di tooget senso rapido di metodi HTTP sono da toorequest utilizzati i dati. In genere, metodi di richiesta HTTP più comuni hello sono GET, HEAD e POST. Grafico ad anello indica la percentuale hello di riscontri per cui si è verificato per ogni tipo di metodo di richiesta HTTP. |
| URL |Contiene un grafico che consente di visualizzare hello top 10 richiesta URL. Viene visualizzata una barra per ogni URL. altezza di Hello di hello barra indica il numero di risultati che ha generato un URL specifico tramite hello intervallo di tempo coperto dal report hello. Le statistiche per primi hello 100 richieste che URL vengono visualizzati direttamente sotto il grafico. |
| CNAME |Contiene un grafico che mostra i primi 10 asset di toorequest CNAME utilizzati hello arco di tempo hello di un report. Le statistiche per primi hello 100 richiesto che CNAME vengono visualizzati direttamente sotto il grafico. |
| Origini |Contiene un grafico che consente di visualizzare hello primi 10 clienti o rete CDN server di origine da cui sono stati richiesti asset in un periodo di tempo specificato. Le statistiche per primi hello 100 richieste direttamente di sotto di questo grafico vengono visualizzati i server di origine della rete CDN o cliente. Server di origine cliente sono identificate dal nome hello definito in hello opzione nome di Directory. |
| POP geografici |Mostra la quantità di traffico che viene indirizzata attraverso un Point of Presence (POP) specifico. abbreviazione di tre lettere Hello rappresenta un POP nella rete CDN. |
| Client |Contiene un grafico che consente di visualizzare hello top 10 client che ha richiesto di asset in un periodo di tempo specificato. Ai fini di hello di questo report, tutte le richieste che provengono da hello stesso indirizzo IP vengono considerati toobe da hello client stesso. Le statistiche per 100 client hello superiore vengono visualizzate direttamente sotto il grafico. Questo report è utile per determinare i modelli di attività di download per i client principali. |
| Stati della cache |Fornisce una descrizione dettagliata del funzionamento della cache, che potrà rivelare approcci per migliorare hello complessiva dell'utente finale. Poiché le prestazioni più veloci hello provengono da riscontri nella cache, è possibile ottimizzare le velocità di recapito dei dati dalla riduzione dei mancati riscontri nella cache e di ricerche riuscite nella cache scaduti. |
| Dettagli NONE |Contiene un grafico che consente di visualizzare hello superiore 10 URL per le risorse per cui aggiornamento del contenuto della cache non è stata selezionata in un periodo di tempo specificato. Statistiche per gli 100 URL superiore hello per questi tipi di attività vengono visualizzate direttamente sotto il grafico. |
| Dettagli CONFIG_NOCACHE |Contiene un grafico che vengono visualizzati gli URL delle prime 10 hello per le risorse che non sono state memorizzate nella cache a causa di configurazione della rete CDN toohello del cliente. Questi tipi di attività sono state soddisfatte direttamente dal server di origine hello. Statistiche per gli 100 URL superiore hello per questi tipi di attività vengono visualizzate direttamente sotto il grafico. |
| Dettagli UNCACHEABLE |Contiene un grafico che consente di visualizzare hello superiore 10 URL per le risorse che non può essere memorizzato nella cache a causa di dati di intestazione toorequest. Statistiche per gli 100 URL superiore hello per questi tipi di attività vengono visualizzate direttamente sotto il grafico. |
| Dettagli TCP_HIT |Contiene un grafico che consente di visualizzare hello superiore 10 URL per le risorse che vengono immediatamente dalla cache. Statistiche per gli 100 URL superiore hello per questi tipi di attività vengono visualizzate direttamente sotto il grafico. |
| Dettagli TCP_MISS |Contiene un grafico che consente di visualizzare hello superiore 10 URL per le risorse che lo stato della cache del TCP_MISS. Statistiche per gli 100 URL superiore hello per questi tipi di attività vengono visualizzate direttamente sotto il grafico. |
| Dettagli TCP_EXPIRED_HIT |Contiene un grafico che consente di visualizzare hello superiore 10 URL per le risorse non aggiornati che sono state soddisfatte direttamente dalla hello POP. Statistiche per gli 100 URL superiore hello per questi tipi di attività vengono visualizzate direttamente sotto il grafico. |
| Dettagli TCP_EXPIRED_MISS |Contiene un grafico che consente di visualizzare hello superiore 10 URL per le risorse non aggiornati per il quale una nuova versione era toobe recuperati dal server di origine hello. Statistiche per gli 100 URL superiore hello per questi tipi di attività vengono visualizzate direttamente sotto il grafico. |
| Dettagli TCP_CLIENT_REFRESH_MISS |Contiene un grafico a barre che visualizza hello superiore 10 URL per gli asset sono stati recuperati da un server di origine di scadenza richiesta no-cache tooa da client hello. Statistiche per gli 100 URL superiore hello per questi tipi di richieste vengono visualizzate direttamente sotto il grafico. |
| Tipi di richiesta client |Indica il tipo di hello di richieste effettuate dai client HTTP (ad esempio, i browser). Questo report include un grafico ad anello che fornisce un certo senso come toohow vengono gestite le richieste. Larghezza di banda e il traffico di informazioni per ogni tipo di richiesta viene visualizzate sotto il grafico hello. |
| Agente utente |Contiene un grafico a barre visualizzazione hello top 10 utente agenti toorequest contenuti attraverso la rete CDN. In genere un agente utente è un Web browser, un lettore multimediale o un browser di un telefono cellulare. Le statistiche per gli agenti utente 100 superiore hello vengono visualizzate direttamente sotto il grafico. |
| Referrer |Contiene un grafico a barre visualizzazione hello principali riferimenti 10 toocontent che si accede tramite la rete CDN. In genere, un riferimento è hello URL della pagina web hello o risorse che si collega tooyour contenuto. Per 100 riferimenti principali hello, sotto il grafico di hello sono disponibili informazioni dettagliate. |
| Tipi di compressione |Contiene un grafico ad anello che suddivide gli asset richiesti in base alla compressione o meno da parte dei server perimetrali. percentuale di Hello degli asset compresso è suddivisi per tipo di hello di compressione utilizzato. Informazioni dettagliate vengono fornite sotto il grafico hello per ogni tipo di compressione e lo stato. |
| Tipi di file |Contiene un grafico a barre che visualizza i tipi di file 10 superiore hello che sono state richieste attraverso la rete CDN per l'account. Ai fini di hello di questo report, è definito un tipo di file dall'estensione del nome di file dell'asset hello e tipo di supporto di Internet (ad esempio HTML \[text/html\], con estensione htm \[text/html\], aspx \[text/html\], ecc.). Sotto il grafico hello sono fornite informazioni dettagliate per primi tipi di 100 file hello. |
| File univoci |Contiene un grafico a cui viene tracciata hello totale cespiti univoci che sono stati richiesti in un determinato giorno in un periodo di tempo specificato. |
| Riepilogo autenticazione con token |Contiene un grafico a torta che fornisce una rapida panoramica relativa alla protezione tramite autenticazione con token degli asset richiesti. Elementi protetti vengono visualizzati nel grafico hello in base toohello risultati i tentativi. |
| Dettagli di autenticazione con token rifiutata |Contiene un grafico a barre che consente di tooview hello top 10 richieste che sono state negate a causa dell'autenticazione basata su tooToken. |
| Codici di risposta HTTP |Fornisce un riepilogo dei codici di stato HTTP hello (ad esempio 200 OK, 403 non consentito, 404 non trovato, e così via) che sono stati recapitati ai client HTTP tooyour nostri server edge. Un grafico a torta consente tooquickly valutare la modalità in cui sono state soddisfatte le risorse. Dati statistici dettagliati viene forniti per ogni codice di risposta sotto il grafico hello. |
| Errori 404 |Contiene un grafico a barre che consente di tooview hello top 10 richieste che hanno restituito un codice di risposta 404 non trovato. |
| Errori 403 |Contiene un grafico a barre che consente di tooview hello top 10 richieste che hanno restituito un codice di risposta 403 accesso negato. Un codice di risposta di tipo 403 Accesso negato viene restituito quando una richiesta viene rifiutata da un server di origine del cliente o da un server perimetrale sul POP. |
| Errori 4xx |Contiene un grafico a barre che consente di tooview hello top 10 richieste che hanno restituito un codice di risposta nell'intervallo di 400 hello. I codici di risposta di tipo 403 Accesso negato e 404 Non trovato sono esclusi da questo report. In genere, un codice di risposta di tipo 4xx viene restituito quando una richiesta viene rifiutata a causa di un errore del client. |
| Errori 504 |Contiene un grafico a barre che consente di tooview hello top 10 richieste che hanno restituito un codice di risposta 504 Timeout del Gateway. Un codice di risposta 504 Timeout del Gateway si verifica quando si verifica un timeout quando un proxy HTTP tenta toocommunicate con un altro server. In caso di hello della rete CDN, un codice di risposta 504 Timeout del Gateway in genere si verifica quando un server perimetrale tooestablish non è possibile la comunicazione con un server di origine del cliente. |
| Errori 502 |Contiene un grafico a barre che consente di tooview hello top 10 richieste che hanno restituito un codice di risposta 502 Gateway non valido. Un codice di risposta di tipo 502 - Gateway non valido viene restituito in caso di errore del protocollo HTTP tra un server e un proxy HTTP. In caso di hello della rete CDN, un codice di risposta 502 Gateway non valido si verifica in genere quando un server di origine cliente restituisce un server perimetrale tooan di risposta non valida. Una risposta non è valida se non può essere analizzata o se è incompleta. |
| Errori 5xx |Contiene un grafico a barre che consente di tooview hello top 10 richieste che hanno restituito un codice di risposta nell'intervallo di 500 hello.  I codici di risposta di tipo 502 - Gateway non valido e 504 - Timeout gateway sono esclusi da questo report. |

## <a name="see-also"></a>Vedere anche
* [Panoramica della rete CDN di Azure](cdn-overview.md)
* [Statistiche in tempo reale nella rete CDN di Microsoft Azure](cdn-real-time-stats.md)
* [Override del comportamento HTTP predefinito utilizzando il motore regole di hello](cdn-rules-engine.md)
* [Report HTTP avanzati](cdn-advanced-http-reports.md)

