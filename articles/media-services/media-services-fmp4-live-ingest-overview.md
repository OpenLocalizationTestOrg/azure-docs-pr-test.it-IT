---
title: Specifica di inserimento aaaAzure Media Services live MP4 frammentato | Documenti Microsoft
description: "Questa specifica viene descritto il protocollo hello e il formato per frammentato basato su MP4 live streaming inserimento per servizi multimediali di Azure. È possibile utilizzare gli eventi in tempo reale di servizi multimediali di Azure toostream e trasmettere i contenuti in tempo reale mediante Azure come piattaforma di cloud hello. Questo documento contiene anche le procedure consigliate per creare meccanismi di inserimento live solidi e altamente ridondanti."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 43fac263-a5ea-44af-8dd5-cc88e423b4de
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 0c191f8d6c5a595621feaba0e571fb984b666f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-fragmented-mp4-live-ingest-specification"></a>Specifica per l'inserimento live di un flusso MP4 frammentato con Servizi multimediali di Azure
Questa specifica viene descritto il protocollo hello e il formato per frammentato basato su MP4 live streaming inserimento per servizi multimediali di Azure. Servizi multimediali fornisce un servizio di streaming in tempo reale che i clienti possono utilizzare gli eventi in tempo reale toostream e trasmettere i contenuti in tempo reale mediante Azure come piattaforma di cloud hello. Questo documento contiene anche le procedure consigliate per creare meccanismi di inserimento live solidi e altamente ridondanti.

## <a name="1-conformance-notation"></a>1. Nota di conformità
Hello parole chiave "deve", "non deve," "Obbligatorio", "SHALL", "non dovrà," "Opportuno", "Non dovrebbe," "Consigliati", "Potrebbe" e "Facoltativo" in questo documento vengono interpretati come se fossero descritti in RFC2119 toobe.

## <a name="2-service-diagram"></a>2. Diagramma del servizio
Hello seguente diagramma illustra architettura di alto livello hello di hello servizio in servizi multimediali di streaming in tempo reale:

1. Un codificatore live inserisce toochannels feed in tempo reale che vengono creati e il provisioning tramite hello Azure Media Services SDK.
2. Cloud di canali, programmi e gli endpoint di streaming handle di servizi multimediali hello tutti live streaming di funzionalità, tra cui inserimento, formattazione, DVR, sicurezza, scalabilità e ridondanza.
3. Facoltativamente, i clienti possono scegliere toodeploy un livello di rete CDN Azure tra endpoint e l'endpoint client hello flusso hello.
4. Flusso di endpoint client da hello endpoint di streaming con protocolli di Streaming adattivo HTTP. Alcuni esempi includono Microsoft Smooth Streaming, flusso adattivo dinamico su HTTP (DASH o MPEG-DASH) e Apple HTTP Live Streaming (HLS).

![Flusso di inserimento][image1]

## <a name="3-bitstream-format--iso-14496-12-fragmented-mp4"></a>3. Formato del flusso di bit: MP4 frammentato ISO 14496-12
Hello formato wire per lo streaming live inserimento descritti in questo documento è basato su [ISO-14496-12]. Per una spiegazione dettagliata del formato MP4 frammentato e delle estensioni disponibili per i file video on demand e l'inserimento di streaming live, vedere [[MS-SSTR]](http://msdn.microsoft.com/library/ff469518.aspx).

### <a name="live-ingest-format-definitions"></a>Definizioni del formato di inserimento live
Hello elenco seguente descrive il formato speciale definizioni che si applicano toolive di inserimento in servizi multimediali di Azure:

1. Hello **ftyp**, **Live Server manifesto casella**, e **moov** caselle devono essere inviate con ogni richiesta (HTTP POST). Queste finestre devono essere inviate all'inizio di hello del flusso di hello e ogni volta che il codificatore hello deve riconnettersi tooresume flusso di inserimento. Per altre informazioni, vedere la sezione 6 di [1].
2. La sezione 3.3.2 di [1] definisce una casella facoltativa chiamata **StreamManifestBox** per l'inserimento live. A causa di logica di routing toohello di bilanciamento del carico di Azure hello, tramite questa casella è deprecata. casella Hello non devono essere presente durante l'inserimento in servizi multimediali. Se la casella è presente, Servizi multimediali la ignora automaticamente.
3. Hello **TrackFragmentExtendedHeaderBox** casella definito in 3.2.3.2 [1] deve essere presente per ogni frammento.
4. La versione 2 di hello **TrackFragmentExtendedHeaderBox** casella deve essere utilizzato toogenerate i segmenti che dispongono di un URL identico in più Data Center. campo indice di frammento Hello è obbligatorio per il failover tra Data Center di formati di streaming basata sull'indice, ad esempio Apple HLS e MPEG-DASH basata sull'indice. il failover tra Data Center tooenable, indice frammento hello deve essere sincronizzati tra più codificatori e incrementato di 1 per ogni frammento di supporti successivo, anche attraverso il riavvio di codificatore o errori.
5. Sezione 3.3.6 [1] definisce una casella denominata **MovieFragmentRandomAccessBox** (**mfra**) che possono essere inviati alla fine di hello del canale di toohello (fine del flusso) di fine del flusso di inserimento in tempo reale tooindicate. Scadenza toohello inserimento della logica di servizi multimediali, usando un sovraccarico di tensione è deprecato e hello **mfra** casella per l'inserimento in tempo reale non deve essere inviata. Se viene inviata, Servizi multimediali la ignora automaticamente. punto di inserimento stato hello tooreset di hello, si consiglia di utilizzare [canale reimpostato](https://docs.microsoft.com/rest/api/media/operations/channel#reset_channels). È inoltre consigliabile utilizzare [programma](https://msdn.microsoft.com/library/azure/dn783463.aspx#stop_programs) tooend una presentazione e il flusso.
6. durata frammento MP4 Hello deve essere costante, pari a hello tooreduce hello client manifesti. Una costante durata frammento MP4 migliora anche l'euristica di download di client tramite l'utilizzo di hello del tag di ripetizione. durata Hello fluttuazione toocompensate per le frequenze di frame non integer.
7. durata frammento MP4 Hello deve essere compreso tra circa 2 e 6 secondi.
8. I timestamp e gli indici (**TrackFragmentExtendedHeaderBox** `fragment_ absolute_ time` e `fragment_index`) del frammento MP4 dovrebbero (SHOULD) arrivare in ordine crescente. Anche se Servizi multimediali è frammenti tooduplicate resilienti, frammenti tooreorder possibilità in base della sequenza temporale supporti toohello è limitata.

## <a name="4-protocol-format--http"></a>4. Formato del protocollo: HTTP
ISO frammentato basato su file MP4 in tempo reale di inserimento per servizi multimediali Usa un lunga HTTP POST richiesta tootransmit con codificata supporti dati standard che viene creato un pacchetto nel servizio di toohello formato MP4 frammentato. Ogni POST HTTP invia completa frammentato bitstream MP4 ("stream"), a partire dall'inizio di hello con caselle di intestazione (**ftyp**, **Live Server manifesto casella**, e **moov** caselle) e continuare con una sequenza di frammenti (**moof** e **mdat** caselle). Per la sintassi dell'URL per una richiesta HTTP POST hello, vedere la sezione in 9.2 [1]. Un esempio di hello URL POST è: 

    http://customer.channel.mediaservices.windows.net/ingest.isml/streams(720p)

### <a name="requirements"></a>Requisiti
Di seguito sono hello informazioni dettagliate sui requisiti:

1. Hello codificatore deve iniziare hello broadcast inviando una richiesta HTTP POST con un oggetto vuoto "body" (lunghezza zero contenuto) utilizzando hello stesso URL di inserimento. Questo può aiutare codificatore hello rilevare rapidamente se l'endpoint di inserimento in tempo reale hello sia valido e se non esiste alcuna autenticazione o altre condizioni necessarie. Per ogni protocollo HTTP, server hello non può restituire una risposta HTTP fino a quando non hello intera richiesta, incluso il corpo POST hello, viene ricevuto. Natura lunga hello di un evento in tempo reale, senza questo passaggio, il codificatore hello potrebbe non essere toodetect in grado di qualsiasi errore finché non viene completata l'invio di tutti i dati di hello.
2. codificatore Hello deve gestire eventuali errori o richieste di autenticazione a causa di (1). Se in (1) è stata restituita una risposta 200, continua.
3. codificatore Hello deve iniziare una nuova richiesta HTTP POST con il flusso di file MP4 frammentato hello. payload Hello deve iniziare con caselle dell'intestazione hello, seguite da frammenti. Si noti che hello **ftyp**, **Live Server manifesto casella**, e **moov** caselle (nell'ordine indicato) devono essere inviate con ogni richiesta, anche se è necessario riconnettere codificatore hello perché hello richiesta precedente è stata interrotta fine toohello precedente del flusso di hello. 
4. codificatore Hello deve utilizzare la codifica per il caricamento di trasferimento chunked, perché è Impossibile toopredict hello intera lunghezza del contenuto di hello in tempo reale di eventi.
5. Quando l'evento hello è stata completata, dopo l'ultimo frammento hello, invio codificatore hello deve terminare correttamente la sequenza dei messaggi (la maggior parte degli stack di client HTTP gestirla automaticamente) di codifica di trasferimento chunked hello. codificatore Hello deve attendere per il codice di risposta finale di hello servizio tooreturn hello e quindi terminare la connessione hello. 
6. codificatore Hello non deve utilizzare hello `Events()` sostantivo come descritto in 9.2 in [1] per l'inserimento in tempo reale in servizi multimediali.
7. Se una richiesta HTTP POST hello termina o volte out con un elemento end toohello precedente errore TCP di flusso hello, hello codificatore deve rilasciare una nuova richiesta POST con una nuova connessione e seguire hello requisiti precedenti. Inoltre, hello codificatore deve rinviare hello due frammenti MP4 precedenti per ogni traccia nel flusso hello e riprendere senza introdurre una discontinuità nella sequenza temporale dei supporti hello. Inviare di nuovo i frammenti MP4 ultime due per ogni traccia hello non assicura che sia presente alcuna perdita di dati. In altre parole, se un flusso contiene una audio sia una traccia video e hello corrente POST richiesta ha esito negativo, è necessario riconnettere codificatore hello e reinvia hello ultime due frammenti per traccia audio hello, che in precedenza sono stati inviati correttamente, e hello ultime due frammenti per Hello traccia video, che sono stati precedentemente inviato correttamente, tooensure che non vi è alcuna perdita di dati. codificatore Hello mantenga un buffer di frammenti di supporti, inviare nuovamente quando si riconnette "Avanti".

## <a name="5-timescale"></a>5. Scala cronologica
[[MS-SSTR] ](https://msdn.microsoft.com/library/ff469518.aspx) descrive l'uso di hello della scala cronologica per **SmoothStreamingMedia** (sezione 2.2.2.1), **StreamElement** (sezione 2.2.2.3), **StreamFragmentElement**(Sezione 2.2.2.6) e **LiveSMIL** (sezione 2.2.7.3.1). Se il valore di scala cronologica hello non è presente, il valore predefinito hello utilizzato è 10.000.000 (10 MHz). Sebbene hello specifica del formato Smooth Streaming non blocca l'utilizzo di altri valori della scala cronologica, la maggior parte delle implementazioni del codificatore predefinito questo valore (10 MHz) toogenerate Smooth Streaming di inserimento dati. Scadenza toohello [Azure Media creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md) funzionalità, è consigliabile utilizzare una scala cronologica 90 KHz per flussi video e 44,1 KHz o KHz 48.1 per i flussi audio. Se vengono utilizzati valori di scala cronologica diversi per i flussi diversi, della scala cronologica di hello a livello di flusso deve essere inviata. Per altre informazioni, vedere [[MS-SSTR]](https://msdn.microsoft.com/library/ff469518.aspx).     

## <a name="6-definition-of-stream"></a>6. Definizione di "flusso"
Flusso è hello unità di base dell'operazione di inserimento in tempo reale per la composizione di presentazioni in tempo reale, la gestione di scenari di ridondanza e failover del flusso. Il flusso è definito come un flusso di bit MP4 frammentato univoco che può contenere una singola traccia o più tracce. Una presentazione live completo può contenere uno o più flussi, a seconda della configurazione di hello di codificatori di hello. Hello seguenti esempi illustrano varie opzioni di utilizzo di flussi toocompose una presentazione completa in tempo reale.

**Esempio:** 

Un cliente desidera toocreate una presentazione di streaming in tempo reale che include hello velocità in bit audio/video seguente:

Video: 3000 kbps, 1500 kbps, 750 kbps

Audio: 128 kbps

### <a name="option-1-all-tracks-in-one-stream"></a>Opzione 1: tutte le tracce in un flusso
In questo caso, un unico codificatore genera tutte le tracce audio/video e le aggrega in un flusso di bit MP4 frammentato. Hello fmp4 bitstream viene quindi inviato tramite una singola connessione HTTP POST. In questo esempio è presente un solo flusso per la presentazione live.

![Flussi - Una traccia][image2]

### <a name="option-2-each-track-in-a-separate-stream"></a>Opzione 2: ogni traccia in un flusso separato
In questo caso, hello codificatore inserisce una traccia in bitstream ogni frammento MP4 e successivamente invia tutti i flussi di hello tramite connessioni HTTP separate. Questa operazione può essere eseguita con uno o più codificatori. inserimento in tempo reale Hello vede la presentazione in tempo reale come composto da quattro flussi.

![Flussi - Tracce separate][image3]

### <a name="option-3-bundle-audio-track-with-hello-lowest-bitrate-video-track-into-one-stream"></a>Opzione 3: Aggregare traccia audio con traccia hello più bassa velocità in bit video in un flusso
In questo caso, il cliente di hello sceglie di tenere traccia audio hello toobundle con traccia video di hello più bassa velocità in bit in un frammento MP4 bitstream e lasciare hello altre due tracce video come flussi separati. 

![Flussi - Tracce audio e video][image4]

### <a name="summary"></a>Riepilogo
Questo non è un elenco completo di tutte le possibili opzioni di inserimento applicabili all'esempio. In realtà, qualsiasi forma di raggruppamento di tracce in flussi è supportata dal processo di inserimento live. Clienti e fornitori di codificatori possono scegliere le proprie implementazioni in base alla complessità di progettazione, alla capacità del codificatore e a considerazioni sui livelli di ridondanza e failover. Tuttavia, nella maggior parte dei casi, è solo una traccia audio per la presentazione live intera hello. In tal caso, è importante tooensure hello healthiness di hello inserimento flusso che contiene la traccia audio hello. Questa considerazione spesso comporta l'inserimento di traccia audio hello nel flusso (ad esempio l'opzione 2) o viene aggiunta con traccia video di hello più bassa velocità in bit (come opzione 3). Inoltre, per una migliore ridondanza e tolleranza di errore, l'invio di hello stessa traccia audio in due diversi flussi (opzione 2 con tracce audio ridondanti) o aggregazione traccia audio di hello con almeno due delle tracce di hello più bassa velocità in bit video (opzione 3 con l'audio nell'inclusi in almeno due flussi video) è fortemente consigliato in tempo reale per acquisire in servizi multimediali.

## <a name="7-service-failover"></a>7. Failover del servizio
Specificato natura hello di streaming in tempo reale, supporto del failover buona è fondamentale per garantire la disponibilità del servizio hello hello. Servizi multimediali è progettato toohandle vari tipi di errori, inclusi errori di rete, errori del server e problemi di archiviazione. Quando utilizzato in combinazione con la logica di failover appropriata dal lato codificatore live hello, i clienti possono ottenere un servizio di streaming in tempo reale altamente affidabile dal cloud hello.

Questa sezione descrive gli scenari di failover del servizio. In questo caso, l'errore hello avviene in un punto qualsiasi all'interno del servizio di hello e manifesta un errore di rete. Ecco alcune indicazioni per l'implementazione del codificatore hello per il failover del servizio di gestione:

1. Utilizzare un timeout di 10 secondi per stabilire una connessione TCP hello. Se una connessione di hello tooestablish tentativo richiede più di 10 secondi, interrompere l'operazione di hello e riprovare. 
2. Utilizzare un timeout breve per l'invio di blocchi di messaggio di richiesta HTTP hello. Se la durata frammento MP4 di hello destinazione N secondi, utilizzare un timeout di invio tra N e 2 N secondi. ad esempio, se la durata di frammento MP4 hello è di 6 secondi, utilizzare un timeout di 6 secondi too12. Se si verifica un timeout, la reimpostazione della connessione di hello, aprire una nuova connessione e resume flusso inserimento sulla nuova connessione hello. 
3. Mantenere un buffer in sequenza con hello ultime due frammenti per ogni traccia sono stati inviati correttamente e completamente toohello servizio.  Se la richiesta HTTP POST hello per un flusso viene terminata o si verifica il timeout fine toohello precedente del flusso di hello, aprire una nuova connessione e iniziare un'altra richiesta HTTP POST, inviare nuovamente le intestazioni di flusso hello, inviare nuovamente hello ultime due frammenti per ogni traccia e riprendere il flusso di hello senza Consente di introdurre una discontinuità nella sequenza temporale dei supporti hello. Ciò riduce hello possibilità di perdita di dati.
4. È consigliabile tale codificatore hello non limitare il numero di hello di tentativi tooestablish una connessione o riprendere il flusso dopo che si verifica un errore TCP.
5. Dopo un errore TCP:
  
    a. la connessione corrente Hello deve essere chiusi e deve essere creata una nuova connessione per una nuova richiesta HTTP POST.

    b. nuovo HTTP POST URL deve essere Hello hello stesso hello URL POST iniziale.
  
    c. Hello nuovo HTTP POST deve includere le intestazioni di flusso (**ftyp**, **Live Server manifesto casella**, e **moov** caselle) che sono identiche toohello intestazioni flusso hello iniziale POST.
  
    d. ultimi due frammenti di hello inviati per ogni traccia devono essere reinviati e streaming deve riprendere senza introdurre una discontinuità nella sequenza temporale dei supporti hello. timestamp frammento MP4 Hello deve aumentare in modo continuo, anche tra le richieste HTTP POST.
6. codificatore Hello deve terminare una richiesta HTTP POST hello se dati non viene inviati a una velocità in relazione alla durata di frammento MP4 hello.  Una richiesta POST HTTP che non inviano i dati può impedire servizi multimediali di rapidamente la disconnessione dal codificatore hello nell'evento hello di un aggiornamento del servizio. Per questo motivo, hello HTTP POST per sparse tracce (segnale dell'annuncio) devono essere breve durate, chiusura come frammento di tipo sparse hello viene inviato.

## <a name="8-encoder-failover"></a>8. Failover del codificatore
Failover del codificatore è hello secondo scenario di failover che deve toobe indirizzato per il recapito di streaming in tempo reale end-to-end. In questo scenario, la condizione di errore hello viene eseguita sul lato di codificatore hello. 

![Failover del codificatore][image5]

Quando si verifica il failover del codificatore, si applica Hello seguendo le aspettative dei clienti dall'endpoint di inserimento in tempo reale hello:

1. Una nuova istanza del codificatore deve essere creata toocontinue streaming, come illustrato nel diagramma hello (flusso di 3000k video, con linea tratteggiata).
2. nuovo codificatore Hello deve utilizzare hello stesso richiede l'URL per HTTP POST come hello Impossibile istanza.
3. Hello richiesta POST del nuovo codificatore deve includere hello stesso frammentata caselle dell'intestazione MP4 come hello istanza non riuscita.
4. nuovo codificatore Hello deve essere sincronizzati correttamente con tutti gli altri codificatori in esecuzione per stessa presentazione live toogenerate hello sincronizzati gli esempi di audio e video con i limiti di frammento allineati.
5. nuovo flusso di Hello devono essere semanticamente equivalente con flusso precedente hello e intercambiabili a livello di intestazione e di frammento hello.
6. nuovo codificatore Hello deve provare toominimize perdita di dati. Hello `fragment_absolute_time` e `fragment_index` del supporto necessario aumentare i frammenti dal punto di hello punto in cui è stato interrotto il codificatore hello. Hello `fragment_absolute_time` e `fragment_index` devono aumentare in modo continuo, ma è ammessa toointroduce discontinuità, se necessario. Servizi multimediali Ignora frammenti che ha già ricevuto ed elaborato, pertanto è migliore tooerr sul lato di hello di inviare di nuovo i frammenti di toointroduce discontinuità nella sequenza temporale dei supporti hello. 

## <a name="9-encoder-redundancy"></a>9. Ridondanza del codificatore
Per alcuni eventi live critici per che anche una maggiore disponibilità e qualità di esperienza, è consigliabile usare codificatori ridondanti attivo-attivo tooachieve di failover senza perdita di dati.

![Ridondanza del codificatore][image6]

Come illustrato nella figura seguente, due gruppi di codificatori push contemporaneamente due copie di ogni flusso nel servizio di hello in tempo reale. Questa configurazione è supportata perché Servizi multimediali è in grado di escludere i frammenti duplicati in base all'ID flusso e al timestamp del frammento. Hello risulta flusso in tempo reale e archiviazione è una singola copia di tutti i flussi di hello è hello aggregazione possibili migliore da due origini hello. Ad esempio, in un ipotetico caso estremo, purché vi sia un codificatore (hello toobe identico a quello non deve) in esecuzione in qualsiasi punto nel tempo per ogni flusso, hello risultante flusso live dal servizio hello è continua senza perdita di dati. 

requisiti di Hello per questo scenario sono quasi uguali hello come requisiti hello in caso di "Failover codificatore" hello, con l'eccezione hello secondo set di codificatori di hello in esecuzione in hello stesso tempo come hello codificatori primari.

## <a name="10-service-redundancy"></a>10. Ridondanza del servizio
Per la distribuzione globale altamente ridondante, talvolta è necessario disporre di calamità toohandle backup tra più aree. Espansione sulla topologia "Ridondanza codificatore" hello, clienti possono scegliere toohave distribuzione di un servizio ridondante in un'area diversa è connesso con secondo set di hello dei codificatori. Possono funzionare anche i clienti con un toodeploy provider Content Delivery Network una gestione traffico globale davanti traffico del servizio distribuzioni tooseamlessly route client hello due. requisiti Hello codificatori hello sono uguali a quelli hello case "Ridondanza codificatore" hello. Hello solo eccezione è che secondo set di hello di codificatori esigenze toobe puntata tooa diversa in tempo reale endpoint di inserimento. Hello diagramma seguente viene illustrato il programma di installazione:

![Ridondanza del servizio][image7]

## <a name="11-special-types-of-ingestion-formats"></a>11. Tipi speciali di formati di inserimento
In questa sezione vengono illustrati tipi speciali di formati di inserimento in tempo reale toohandle progettato di scenari specifici.

### <a name="sparse-track"></a>Traccia di tipo sparse
Quando una presentazione live streaming con un'esperienza rich client, spesso è necessario tootransmit sincronizzati ora eventi o segnala in banda con i dati di supporto principale hello. Un esempio di questo scenario è l'inserimento dinamico di annunci live. La segnalazione per questo tipo di eventi è diversa dal normale streaming di flussi audio/video a causa della particolare natura di tipo sparse. In altre parole, hello segnalazione dei dati in genere non si verifica in modo continuo e intervallo hello può essere toopredict disco rigido. il concetto di Hello di tracce di tipo sparse è stato progettato tooingest e dati di segnalazione di trasmissione in banda.

Hello passaggi seguenti sono un'implementazione consigliata per l'inserimento di tracce di tipo sparse:

1. Creare un flusso di bit MP4 frammentato separato contenente solo le tracce di tipo sparse, senza tracce audio/video.
2. In hello **Live Server manifesto casella** come definito nella sezione 6 [1], utilizzare hello *parentTrackName* nome del parametro toospecify hello della traccia di hello padre. Per altre informazioni, vedere la sezione 4.2.1.2.1.2 di [1].
3. In hello **Live Server manifesto casella**, **manifestOutput** deve essere impostato troppo**true**.
4. Natura hello sparse di hello segnalazione dell'evento, è consigliabile seguente hello:
   
    a. Inizio hello dell'evento in tempo reale di hello, finestre di intestazione iniziali hello codificatore hello invia toohello servizio, che consente di tenere traccia di tipo sparse hello servizio tooregister hello nel manifesto client hello.
   
    b. codificatore Hello deve terminare una richiesta HTTP POST hello quando i dati non inviati. Un POST HTTP con esecuzione prolungata che non inviano i dati può impedire il rapidamente la disconnessione dal codificatore hello nell'evento hello di un riavvio del servizio, update o da server di servizi multimediali. In questi casi, server dei contenuti multimediali hello è temporaneamente bloccato in un'operazione di ricezione sul socket hello.
   
    c. Durante la fase di hello quando la segnalazione di dati non è disponibile, il codificatore hello deve chiudere una richiesta HTTP POST hello. Quando richiesta POST hello è attivo, il codificatore hello deve inviare dati.

    d. Quando si inviano i frammenti di tipo sparse, il codificatore hello possibile impostare un'intestazione content-length esplicita, se disponibile.

    e. Quando si inviano i frammenti di tipo sparse con una nuova connessione, il codificatore hello dovrebbe iniziare l'invio dalle finestre di intestazione hello aggiungendo nuovi frammenti di hello. Questo è per i casi in cui failover avviene intermedio e connessione di tipo sparse nuovo hello viene stabilita tooa nuovo server non rilevati tracce di tipo sparse hello prima.

    f. frammento di tracce di tipo sparse Hello diventa disponibile toohello client quando hello corrispondente padre traccia frammento che ha un valore uguale o maggiore di timestamp viene effettuata client toohello disponibili. Ad esempio, se il frammento di tipo sparse hello ha un timestamp di t = 1000, è previsto che dopo client hello vede timestamp 1000 di frammento "video" (presupponendo che il nome di tenere traccia del padre hello è "video") o versioni successive, è possibile scaricare hello frammento sparse t = 1000. Si noti che segnale effettivo hello può essere utilizzate per un'altra posizione nella sequenza temporale di presentazione hello per lo scopo designato. In questo esempio di possibili che hello frammento di tipo sparse di t = 1000 ha un payload XML, che è possibile inserire un annuncio in una posizione che è di pochi secondi in un secondo momento.

    g. payload Hello di frammenti di tracce di tipo sparse possono essere in formati diversi (ad esempio XML, testo o binario), a seconda dello scenario di hello.

### <a name="redundant-audio-track"></a>Traccia audio ridondante
HTTP adattivo streaming uno scenario tipico (ad esempio, Smooth Streaming o trattino), è spesso solo una traccia audio nell'intera presentazione hello. A differenza delle tracce video, che dispongono di più livelli di qualità per hello toochoose di client da in condizioni di errore, la traccia audio hello può essere un singolo punto di errore se hello inserimento del flusso di hello che contiene la traccia audio hello viene interrotta. 

Questo problema, servizi multimediali supporta toosolve live inserimento delle tracce audio ridondanti. l'idea Hello è tale hello stessa traccia audio può essere inviato più volte in diversi flussi. Sebbene hello servizio solo registri traccia audio hello una volta nel manifesto client hello, è possibile utilizzare ridondanti tracce audio come backup per il recupero dei frammenti audio se traccia audio principale hello presenta problemi. tracce audio tooingest ridondante, il codificatore hello deve:

1. Creare più frammento MP4 bitstreams hello traccia audio stesso. tracce audio ridondanti Hello devono essere semanticamente equivalenti, con hello stesso frammento timestamp e intercambiabile al livello di frammento e intestazione hello.
2. Verificare la voce "audio" hello in hello Live Server manifesto (sezione 6 [1]) è hello stesso per le tracce audio tutti ridondanti.

Hello dopo l'implementazione è consigliata per le tracce audio ridondanti:

1. Inviare ogni singola traccia audio in un flusso separato. È inoltre possibile inviare un flusso ridondante per ciascuno di questi flussi di traccia audio, in cui secondo flusso hello differisce da hello prima solo per identificatore hello in hello URL POST HTTP: {protocollo} :// {indirizzo del server} / {path}/Streams({identifier}) punto di pubblicazione.
2. Utilizzare flussi distinti toosend hello due più basso video velocità in bit. Ciascuno di questi flussi dovrebbe (SHOULD) inoltre contenere una copia di ogni singola traccia audio. Se, ad esempio, sono supportate più lingue, i flussi dovrebbero (SHOULD) contenere tracce audio per ogni lingua.
3. Utilizzare tooencode istanze server distinti (codificatore) e invia i flussi di ridondanza hello indicati (1) e (2). 

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
