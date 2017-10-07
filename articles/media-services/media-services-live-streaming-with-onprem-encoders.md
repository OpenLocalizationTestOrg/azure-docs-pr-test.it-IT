---
title: "aaaStream live con codificatori locali che creano flussi di più velocità in bit - Azure | Documenti Microsoft"
description: "In questo argomento viene descritto come tooset un canale che riceve un più velocità in bit live flusso da un codificatore in locale. Hello flusso può essere quindi recapitato tooclient applicazioni di riproduzione tramite uno o più endpoint di streaming, utilizzando uno dei seguenti protocolli di streaming adattivo hello: HLS, Smooth Streaming, DASH."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: d9f0912d-39ec-4c9c-817b-e5d9fcf1f7ea
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 04/12/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 00709cecfc3b5b5dcfaa8f1e4b25bcf9d470d50b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-with-on-premises-encoders-that-create-multi-bitrate-streams"></a>Streaming live con codificatori locali che creano flussi a bitrate multipli
## <a name="overview"></a>Panoramica
In Servizi multimediali di Azure un *canale* rappresenta una pipeline per l'elaborazione di contenuto in streaming live. Un canale riceve i flussi di input live in uno dei due modi seguenti:

* Un codificatore live locale invia una RTMP asset MP4 o Smooth Streaming (MP4 frammentato) toohello il canale del flusso che non è abilitato tooperform live codifica con servizi multimediali. Hello caricamento flussi pass-through canali senza altre elaborazioni. Questo metodo viene chiamato *pass-through*. È possibile utilizzare i seguenti codificatori live con più velocità in bit Smooth Streaming come output di hello: supporto di Excel, Ateme, immaginare le comunicazioni, Envivio, Cisco ed elementare. dispone di Hello seguenti codificatori live RTMP come output: Adobe Flash codificatore multimediale di Live, Telestream Wirecast, Haivision, Teradek e TriCaster. Un codificatore live può inoltre inviare un canale tooa flusso a velocità in bit singola che non è abilitato per la codifica live, ma non consigliabile. Servizi multimediali offre toocustomers flusso hello che lo richiedono.

  > [!NOTE]
  > Utilizzo di un metodo pass-through è hello più conveniente toodo live streaming.


* Un codificatore live locale invia un canale toohello flusso a velocità in bit singola che è abilitato in tempo reale di codifica con servizi multimediali in uno dei seguenti formati hello tooperform: RTP (MPEG-TS), RTMP o Smooth Streaming (MP4 frammentato). canale Hello esegue quindi la codifica live di hello in arrivo velocità in bit singola flusso tooa più velocità in bit (adattivo) flusso video. Servizi multimediali offre toocustomers flusso hello che lo richiedono.

A partire dalla versione di hello 2.10 di servizi multimediali, quando si crea un canale, è possibile specificare come si desidera che il flusso di input del canale tooreceive hello. È inoltre possibile specificare se si desidera hello canale tooperform codifica del flusso in tempo reale. Sono disponibili due opzioni:

* **Pass-Through**: specificare questo valore se si prevede di toouse un codificatore live locale che disporrà di un flusso a più velocità in bit (un flusso di tipo pass-through) come output. In questo caso, il flusso in ingresso di hello attraversa toohello output senza codifica. Questo è il comportamento di hello di un canale prima della versione 2.10 hello. Questo argomento fornisce informazioni dettagliate sull'uso dei canali di questo tipo.
* **Codifica Live**: selezionare questo valore se si prevede di tooencode di servizi multimediali toouse il flusso di asset MP4 velocità in bit singola tooa flusso live. Si noti che se si lascia un canale di codifica live nello stato **In esecuzione**, verranno applicati addebiti. Si consiglia di arrestare immediatamente i canali in esecuzione dopo l'evento live streaming è completo tooavoid costi extra orarie. Servizi multimediali offre toocustomers flusso hello che lo richiedono.

> [!NOTE]
> In questo argomento vengono descritti gli attributi di canali che non sono abilitati la codifica live tooperform. Per informazioni sull'utilizzo di canali abilitata tooperform la codifica live, vedere [Live streaming con flussi di servizi multimediali di Azure toocreate più velocità in bit](media-services-manage-live-encoder-enabled-channels.md).
>
>

Hello seguente diagramma rappresenta un flusso di lavoro con live streaming che utilizza un flussi di on-premise codificatore live toohave più velocità in bit RTMP o MP4 frammentato (Smooth Streaming) come output.

![Flusso di lavoro live][live-overview]

## <a id="scenario"></a>Scenario comune di streaming live
Hello passaggi seguenti descrivono le attività coinvolte nella creazione di applicazioni live streaming comuni.

1. Connettere un computer tooa videocamera. Avviare e configurare un codificatore live locale che genera un flusso in formato RTMP o MP4 frammentato (Smooth Streaming) a bitrate multipli come output. Per altre informazioni, vedere l'argomento relativo a [codificatori live e supporto RTMP di Servizi multimediali di Azure](http://go.microsoft.com/fwlink/?LinkId=532824).

    È anche possibile eseguire questo passaggio dopo la creazione del canale.
2. Creare e avviare un canale.

3. URL di inserimento del canale di hello recuperare.

    Hello codificatore live utilizza hello inserimento URL toosend hello toohello il canale del flusso.
4. Recuperare l'URL di anteprima del canale hello.

    Utilizzare questo tooverify URL che il canale riceve correttamente flusso live hello.
5. Creare un programma.

    Quando si usa hello portale di Azure, la creazione di un programma crea inoltre un asset.

    Quando si utilizza hello SDK .NET o REST, è necessario toocreate un asset e specificare toouse questo asset durante la creazione di un programma.
6. Pubblicare l'asset hello associata programma hello.   

    >[!NOTE]
    >Quando viene creato l'account di servizi multimediali di Azure, un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. endpoint da cui si desidera toostream contenuto di streaming Hello è toobe in hello **esecuzione** stato.

7. Avviare il programma di hello quando sarai pronto toostart streaming e l'archiviazione.

8. Facoltativamente, codificatore live hello può essere segnalato toostart un annuncio. annuncio Hello viene inserito nel flusso di output di hello.

9. Arrestare il programma hello ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello.

10. Eliminare il programma hello (e facoltativamente elimina hello asset).     

## <a id="channel"></a>Descrizione di un canale e dei relativi componenti
### <a id="channel_input"></a>Configurazioni di input (inserimento) del canale
#### <a id="ingest_protocols"></a>Protocollo di streaming di inserimento
Servizi multimediali supporta l'inserimento di feed live usando MP4 frammentato a bitrate multipli e RTMP a bitrate multipli come protocolli di streaming. Quando di inserimento RTMP hello protocollo di streaming è selezionata, due inserimento (inpui) gli endpoint vengono creati per il canale hello:

* **URL principale**: hello specifica un URL completo di RTMP primario del canale hello endpoint di inserimento.
* **URL secondario** (facoltativo): hello specifica un URL completo di RTMP secondario del canale hello endpoint di inserimento.

Utilizzare URL secondario hello se si desidera tooimprove hello durabilità e la tolleranza dell'inserimento flusso (nonché codificatore failover e tolleranza di errore), in particolare per hello seguenti scenari:

- Singolo codificatore doppia-inserendo gli URL primario e secondario tooboth:

    Hello scopo principale di questo scenario è tooprovide ulteriori fluttuazioni toonetwork resilienza e tremolio nella. Alcuni codificatori RTMP non gestiscono correttamente le disconnessioni dalla rete. Quando si verifica una disconnessione della rete, un codificatore potrebbe interrompere la codifica e non inviare dati hello memorizzato nel buffer quando si verifica una riconnessione. causando discontinuità e perdita di dati. Disconnessioni di rete possono essere eseguiti a causa di una rete non valida o manutenzione su hello lato Azure. URL primario o secondario ridurre i problemi di rete hello e fornire un processo di aggiornamento controllata. Ogni volta che si verifica una disconnessione programmata di rete, servizi multimediali gestisce hello primario e secondario si disconnette e fornisce un ritardata disconnettere tra due hello. Codificatori tookeep ora l'invio dei dati sono quindi eseguire nuovamente la connessione. ordine di Hello di hello disconnette può essere casuale, ma sarà sempre presente un ritardo tra l'URL secondario o principale o primario o secondario. In questo scenario, il codificatore hello è ancora punto debole hello.

- Più codificatori, con ogni codificatore push tooa dedicato punto:

    Questo scenario fornisce sia la ridondanza di inserimento che del codificatore. In questo scenario, encoder1 inserisce URL principale toohello ed encoder2 inserisce URL secondario toohello. Quando un codificatore non riesce, hello altri codificatore può mantenere l'invio dei dati. È possibile mantenere la ridondanza dei dati poiché servizi multimediali non disconnettere gli URL primari e secondari in hello contemporaneamente. Questo scenario si presuppone che i codificatori sono sincronizzati e forniscono esattamente hello stessi dati.  

- Più codificatori doppia-inserendo gli URL primario e secondario tooboth:

    In questo scenario, entrambi i codificatori push URL primario e secondario tooboth di dati. In questo modo l'affidabilità migliore hello e tolleranza di errore, nonché la ridondanza dei dati. Questo scenario può tollerare i guasti di entrambi i codificatori e si disconnette se un solo codificatore smette di funzionare. Si presuppone che i codificatori sono sincronizzati e forniscono esattamente hello stessi dati.  

Per informazioni sui codificatori RTMP live, vedere [Codificatori live e supporto RTMP di Servizi multimediali di Azure](http://go.microsoft.com/fwlink/?LinkId=532824).

#### <a name="ingest-urls-endpoints"></a>URL di inserimento (endpoint)
Un canale, fornisce un endpoint di input (URL di inserimento) specificare nel codificatore live hello, in modo da propagare codificatore hello flussi tooyour canali.   

È possibile ottenere hello URL di inserimento quando si crea il canale hello. Per è tooget questi URL, il canale di hello non deve toobe in hello **esecuzione** stato. Quando sarai pronto toostart push canale toohello dati, deve essere canale hello hello **esecuzione** stato. Dopo che il canale hello inizia l'inserimento di dati, puoi visualizzare in anteprima il flusso tramite hello anteprima URL.

È possibile inserire un flusso live MP4 frammentato (Smooth Streaming) tramite una connessione SSL. tooingest su SSL, verificare che hello tooupdate tooHTTPS URL di inserimento. Attualmente, non è possibile inserire flussi RTMP tramite SSL.

#### <a id="keyframe_interval"></a>Intervallo tra fotogrammi chiave
Quando si utilizza un flusso di più velocità in bit toogenerate codificatore live locale, intervallo di fotogrammi chiave hello specifica durata hello di hello GOP group of pictures () utilizzato da tale codificatore esterno. Dopo che il canale hello riceve questo flusso in ingresso, è possibile distribuire il flusso live tooclient applicazioni di riproduzione in uno dei seguenti formati hello: Smooth Streaming, il flusso adattivo dinamica su HTTP (trattino) e HTTP Live Streaming (HLS). Quando si esegue lo streaming live, la creazione di pacchetti in HLS avviene sempre in modo dinamico. Per impostazione predefinita, servizi multimediali calcola automaticamente hello imballaggio rapporto dei segmenti HLS (frammenti per segmento) in base a intervallo di fotogrammi chiave hello ricevuto dal codificatore live hello.

Hello nella tabella seguente viene illustrata la modalità di calcolo durata segmento hello:

| Intervallo tra fotogrammi chiave | Rapporto per la creazione di pacchetti dei segmenti HLS (FragmentsPerSegment) | Esempio |
| --- | --- | --- |
| Minore o uguale a too3 secondi |3:1 |Se durata di KeyFrameInterval (o GOP) è 2 secondi, il rapporto di compressione segmento HLS predefinito hello è too1 3. Viene creato un segmento HLS di 6 secondi. |
| too5 3 secondi |2:1 |Se durata di KeyFrameInterval (o GOP) è 4 secondi, il rapporto di compressione segmento HLS predefinito hello è too1 2. Viene creato un segmento HLS di 8 secondi. |
| Maggiore di 5 secondi |1:1 |Se durata di KeyFrameInterval (o GOP) è di 6 secondi, il rapporto di compressione segmento HLS di hello predefinito è 1 too1. Viene creato un segmento HLS di 6 secondi. |

È possibile modificare il rapporto frammenti ogni segmento hello output e l'impostazione FragmentsPerSegment su ChannelOutputHls configurazione canale hello.

È inoltre possibile modificare valore dell'intervallo dei fotogrammi chiave hello impostando la proprietà di durata di KeyFrameInterval hello in ChanneInput. Se si imposta in modo esplicito di durata di KeyFrameInterval, hello rapporto di compressione segmento HLS che fragmentspersegment viene calcolato tramite hello regole descritte in precedenza.  

Se si imposta in modo esplicito sia la durata di KeyFrameInterval FragmentsPerSegment, servizi multimediali utilizzerà i valori hello impostati.

#### <a name="allowed-ip-addresses"></a>Indirizzi IP consentiti
È possibile definire gli indirizzi IP hello consentiti toopublish toothis video channel. In una delle seguenti hello, è possibile specificare un indirizzo IP:

* Un singolo indirizzo IP, ad esempio, 10.0.0.1
* Un intervallo di indirizzi IP che usa un indirizzo IP e una subnet mask CIDR, ad esempio, 10.0.0.1/22
* Un intervallo di indirizzi IP che usa un indirizzo IP e una subnet mask decimale puntata, ad esempio, 10.0.0.1(255.255.252.0)

Se non viene specificato alcun indirizzo IP e non è presente una definizione della regola, non sarà consentito alcun indirizzo IP. tooallow qualsiasi indirizzo IP, creare una regola e impostare 0.0.0.0/0.

### <a name="channel-preview"></a>Anteprima del canale
#### <a name="preview-urls"></a>URL di anteprima
I canali forniscono un endpoint di anteprima (URL di anteprima) di utilizzare toopreview e convalidare il flusso prima di elaborarlo ulteriormente e di recapito.

È possibile ottenere l'URL di anteprima di hello quando si crea il canale hello. Per è tooget hello URL, canale hello non hanno toobe hello **esecuzione** stato. Dopo che il canale hello inizia l'inserimento di dati, puoi visualizzare in anteprima il flusso.

Attualmente, il flusso di anteprima hello può essere recapitato solo in formato MP4 frammentato (Smooth Streaming) formato, indipendentemente dal hello specificato il tipo di input. È possibile utilizzare hello [Smooth Streaming Health Monitor](http://smf.cloudapp.net/healthmonitor) smooth streaming hello tootest player. È anche possibile usare un lettore che è ospitato in hello tooview portale Azure il flusso.

#### <a name="allowed-ip-addresses"></a>Indirizzi IP consentiti
È possibile definire gli indirizzi IP hello consentiti tooconnect toohello endpoint di anteprima. Se non viene specificato alcun indirizzo IP, sarà consentito qualsiasi indirizzo IP. In una delle seguenti hello, è possibile specificare un indirizzo IP:

* Un singolo indirizzo IP, ad esempio, 10.0.0.1
* Un intervallo di indirizzi IP che usa un indirizzo IP e una subnet mask CIDR, ad esempio, 10.0.0.1/22
* Un intervallo di indirizzi IP che usa un indirizzo IP e una subnet mask decimale puntata, ad esempio, 10.0.0.1(255.255.252.0)

### <a name="channel-output"></a>Output del canale
Per informazioni sull'output di canale, vedere hello [intervallo di fotogrammi chiave](#keyframe_interval) sezione.

### <a name="channel-managed-programs"></a>Programmi gestiti dal canale
Un canale è associato a programmi che è possibile utilizzare toocontrol hello pubblicazione e l'archiviazione di segmenti in un flusso in tempo reale. I programmi sono gestiti dai canali. Hello relazione canale e il programma è molto simile tootraditional media, in cui un canale è un flusso costante di contenuto e l'evento con ambito toosome timeout su tale canale è un programma.

È possibile specificare hello numero di ore che si vuole tooretain hello registrato contenuto per il programma hello, impostazione hello **finestra archivio** lunghezza. Questo valore può essere impostato da un minimo di 25 ore massimo tooa 5 minuti. Lunghezza dell'intervallo di archiviazione determina anche l'intervallo di tempo i client possono cercare indietro nel tempo dalla posizione live corrente hello massimo hello. I programmi eseguibili sul periodo di tempo specificato hello, ma il contenuto che non è sincronizzato con la lunghezza della finestra hello viene scartato in modo continuo. Questo valore di questa proprietà determina anche per quanto tempo hello client possono raggiungere i manifesti.

Ogni programma è associato a un asset che archivia il contenuto di hello inviati nel flusso. Un asset è mappato tooa blocco blob contenitore nell'account di archiviazione Azure hello e file hello in asset hello vengono archiviati come BLOB nel contenitore. toopublish hello in modo che i clienti possono visualizzare flusso hello, è necessario creare un localizzatore OnDemand per asset hello associata. Utilizzare un URL di streaming che è possibile fornire ai client tooyour toobuild questo indicatore di posizione.

Un canale supporta fino toothree contemporaneamente programmi in esecuzione, pertanto è possibile creare più archivi di hello stesso flusso in ingresso. È possibile pubblicare e archiviare parti diverse di un evento a seconda delle necessità. Ad esempio, si supponga che il requisito di business sia tooarchive 6 ore di un programma, ma toobroadcast solo hello ultimi 10 minuti. tooaccomplish, è necessario toocreate due programmi in esecuzione simultanea. Un programma è impostato tooarchive 6 ore dell'evento hello, ma non è pubblicato programma hello. Hello altro programma è tooarchive insieme per 10 minuti e il programma viene pubblicato.

Non riutilizzare i programmi esistenti per nuovi eventi. Al contrario, creare un nuovo programma per ogni evento. Avviare il programma di hello quando sarai pronto toostart streaming e l'archiviazione. Arrestare il programma hello ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello.

contenuto toodelete archiviato, interrompere eliminare hello programma e quindi eliminare l'asset associato hello. Un asset non può essere eliminato se viene usato da un programma. programma Hello deve prima essere eliminato.

Anche dopo aver arrestato ed eliminato il programma hello, gli utenti possono trasmettere il contenuto archiviato come video on demand, fino a quando non si elimina l'asset hello. Se si desidera che il contenuto archiviato hello tooretain ma non è disponibile per lo streaming, eliminare hello localizzatore di streaming.

## <a id="states"></a>Stati del canale e fatturazione
I valori possibili per lo stato corrente di hello di un canale includono:

* **Arrestato**: si tratta dello stato iniziale di hello del canale hello dopo la sua creazione. In questo stato, le proprietà del canale hello possono essere aggiornate, ma non è consentito lo streaming.
* **Avvio**: canale hello viene avviato. In questo stato non è consentito alcun aggiornamento o streaming. Se si verifica un errore, il canale hello restituisce toohello **arrestato** stato.
* **Esecuzione**: canale hello può elaborare flussi live.
* **Arresto**: canale hello è stato arrestato. In questo stato non è consentito alcun aggiornamento o streaming.
* **L'eliminazione di**: canale hello è stato eliminato. In questo stato non è consentito alcun aggiornamento o streaming.

Hello nella tabella seguente viene illustrato come canale stati modalità di fatturazione toohello mappa.

| Stato del canale | Indicatori dell'interfaccia utente del portale | Fatturato? |
| --- | --- | --- | --- |
| **Avvio** |**Avvio** |No (stato temporaneo) |
| **Running** |**Pronto** (nessun programma in esecuzione)<p><p>oppure<p>**Streaming** (almeno un programma in esecuzione) |Sì |
| **Arresto** |**Arresto** |No (stato temporaneo) |
| **Stopped** |**Stopped** |No |

## <a id="cc_and_ads"></a>Sottotitoli codificati e inserimento di annunci
Hello nella tabella seguente illustra gli standard supportati per i sottotitoli codificati e inserimento di annunci.

| Standard | Note |
| --- | --- |
| CEA-708 e EIA-608 (708/608) |CEA-708 ed EIA-608 sono sottotitoli standard per hello Uniti e Canada.<p><p>Attualmente, i sottotitoli sono supportati solo se trasportati nel flusso di input codificata hello. È necessario un codificatore multimediale live che può inserire 608 o 708 sottotitoli nel flusso codificato hello che ha inviato servizi tooMedia toouse. Servizi multimediali invia il contenuto di hello con visualizzatori tooyour sottotitoli inseriti. |
| TTML all'interno di file ismt (tracce di testo Smooth Streaming) |Creazione dinamica dei pacchetti di servizi multimediali consente il contenuto di toostream client in uno dei seguenti formati hello: DASH, HLS o Smooth Streaming. Tuttavia, se inserimento MP4 frammentato (Smooth Streaming) con sottotitoli all'interno dei file ismt (tracce di testo Smooth Streaming), è possibile recapitare tooonly flusso hello client Smooth Streaming. |
| SCTE-35 |I segnali SCTE-35 è un sistema di segnalazione digitale che ha utilizzato l'inserimento di annunci pubblicitari toocue. Ricevitori a valle usano pubblicità toosplice di segnale hello in flusso hello per hello tempo assegnato. I segnali SCTE-35 devono essere inviati come una traccia di tipo sparse nel flusso di input hello.<p><p>Attualmente, formato flusso di input hello solo supportato che trasporta i segnali di Active Directory è frammentato MP4 (Smooth Streaming). Hello è supportato solo il formato di output è inoltre Smooth Streaming. |

## <a id="considerations"></a>Considerazioni
Quando si utilizza un toosend codificatore live locale un canale di tooa flusso più velocità in bit, hello seguenti vincoli:

* Assicurarsi di avere sufficiente dati toohello gratuito per Internet connettività toosend punti di inserimento.
* Per usare un URL di inserimento secondario, è necessaria larghezza di banda aggiuntiva.
* flusso più velocità in bit in ingresso Hello può avere un massimo di 10 livelli di qualità video (livelli) e un massimo di 5 tracce audio.
* Hello più alta velocità in bit media per uno qualsiasi dei livelli di qualità video hello deve essere inferiore a 10 Mbps.
* aggregazione di hello velocità in bit media per tutti i flussi audio e video di hello Hello deve essere inferiore a 25 Mbps.
* È possibile modificare hello protocollo input durante il canale hello o relativi programmi sono in esecuzione. Se sono necessari protocolli diversi, è consigliabile creare canali separati per ciascun protocollo di input.
* È possibile inserire un bitrate singolo nel canale, Ma poiché canale hello non elabora il flusso di hello, le applicazioni client hello verranno visualizzato anche un flusso a velocità in bit singola. Questa opzione non è consigliata.

Ecco altri tooworking correlati considerazioni con i canali e i componenti correlati:

* Ogni volta che si riconfigura il codificatore live di hello, chiamare hello **reimpostare** metodo sul canale hello. Prima reimpostare il canale di hello, è necessario programma hello toostop. Dopo aver reimpostato il canale di hello, riavviare il programma di hello.
* Un canale può essere arrestato solo quando è presente nel hello **esecuzione** lo stato e tutti i programmi sul canale hello sono stati arrestati.
* Per impostazione predefinita, è possibile aggiungere l'account di servizi multimediali tooyour solo 5 canali. Per altre informazioni, vedere [Quote e limitazioni](media-services-quotas-and-limitations.md).
* Verrà addebitato solo quando il canale è in hello **esecuzione** stato. Per ulteriori informazioni, vedere toohello [Channel stati e fatturazione](media-services-live-streaming-with-onprem-encoders.md#states) sezione.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="feedback"></a>Commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Argomenti correlati
[Specifica per l'inserimento live di un flusso MP4 frammentato con Servizi multimediali di Azure](media-services-fmp4-live-ingest-overview.md)

[Panoramica e scenari comuni di Servizi multimediali di Azure](media-services-overview.md)

[Concetti relativi ai Servizi multimediali](media-services-concepts.md)

[live-overview]: ./media/media-services-manage-channels-overview/media-services-live-streaming-current.png
