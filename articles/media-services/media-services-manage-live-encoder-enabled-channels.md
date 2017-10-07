---
title: "aaaLive streaming mediante flussi più velocità in bit toocreate di servizi multimediali di Azure | Documenti Microsoft"
description: "In questo argomento viene descritto come tooset un canale che riceve una velocità in bit singola live flusso da un codificatore in locale e quindi esegue in tempo reale flusso a velocità in bit tooadaptive codifica con servizi multimediali. Hello flusso può essere quindi recapitato tooclient applicazioni di riproduzione tramite uno o più endpoint Streaming, utilizzando uno dei seguenti protocolli di streaming adattivo hello: HLS, Smooth Streaming, MPEG DASH."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 30ce6556-b0ff-46d8-a15d-5f10e4c360e2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: a8bbdd1570cc9a11bfc2de7bb4ceb9006cc25534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams"></a>Live streaming mediante flussi più velocità in bit toocreate di servizi multimediali di Azure
## <a name="overview"></a>Panoramica
In Servizi multimediali di Azure (AMS) un **canale** rappresenta una pipeline per l'elaborazione dei contenuti in streaming live. Un **canale** riceve i flussi di input live in uno dei due modi seguenti:

* Un codificatore live locale invia un flusso a velocità in bit singola canale toohello tooperform abilitato live codifica con servizi multimediali in uno dei seguenti formati hello: RTP (MPEG-TS), RTMP o Smooth Streaming (MP4 frammentato). Hello canale esegue quindi la codifica live di hello in arrivo velocità in bit singola flusso tooa più velocità in bit (adattivo) flusso video. Quando richiesto, servizi multimediali offre toocustomers flusso hello.
* Un codificatore live locale invia una più velocità in bit **RTMP** o **Smooth Streaming** canale toohello (MP4 frammentato) che non è abilitato in tempo reale di codifica con AMS tooperform. flussi di caricamento Hello passano-through **canale**s senza ulteriore elaborazione. Questo metodo viene chiamato **pass-through**. È possibile utilizzare i seguenti codificatori live Smooth Streaming con più velocità in bit di output di hello: MediaExcel, Ateme, le comunicazioni immaginare, Envivio, Cisco ed elementare. Hello codificatori live seguenti generano output in RTMP: Adobe Flash multimediali Live codificatore (FMLE), Telestream Wirecast, Haivision, Teradek e Tricaster codificatori.  Un codificatore live può inoltre inviare una velocità in bit singola tooa il canale del flusso che non è abilitato per la codifica live, ma che non è consigliata. Quando richiesto, servizi multimediali offre toocustomers flusso hello.
  
  > [!NOTE]
  > Utilizzo di un metodo pass-through è hello più conveniente toodo live streaming.
  > 
  > 

A partire dalla versione di hello 2.10 di servizi multimediali, quando si crea un canale, è possibile specificare in che modo si desidera per il flusso di input del canale tooreceive hello e se si vuole che per hello canale tooperform live codifica del flusso di lavoro. Sono disponibili due opzioni:

* **Nessuna** : specificare questo valore, se si prevede di toouse un codificatore live locale che genera più velocità in bit flusso (flusso di pass-through). In questo caso, il flusso in ingresso di hello passati toohello output senza codifica. Questo è il comportamento di hello di una versione precedente di too2.10 canale.  Per informazioni più dettagliate sull'uso dei canali di questo tipo, vedere [Streaming live con codificatori locali che creano flussi a bitrate multipli](media-services-live-streaming-with-onprem-encoders.md).
* **Standard** -scegliere questo valore, se si prevede di tooencode di servizi multimediali toouse il flusso di velocità in bit toomulti flusso live a velocità in bit singola. Tenere presente che vi sia un impatto sulla fatturazione per la codifica live è opportuno tenere presente che se si lascia un canale di codifica live in stato "Running" hello comporterà ulteriori addebiti nella fatturazione.  È consigliabile arrestare immediatamente i canali in esecuzione dopo l'evento di streaming in tempo reale viene completato tooavoid costi extra orarie.

> [!NOTE]
> In questo argomento vengono descritti gli attributi dei canali abilitati la codifica live tooperform (**Standard** tipo di codifica). Per informazioni sull'utilizzo di canali che non sono abilitati tooperform la codifica live, vedere [Live streaming con codificatori locali che creano flussi più velocità in bit](media-services-live-streaming-with-onprem-encoders.md).
> 
> Verificare che hello tooreview [considerazioni](media-services-manage-live-encoder-enabled-channels.md#Considerations) sezione.
> 
> 

## <a name="billing-implications"></a>Implicazioni relative alla fatturazione
Un canale di codifica live inizia non appena lo stato del passa troppo "Running" tramite hello API di fatturazione.   Inoltre, è possibile visualizzare lo stato di hello in hello portale di Azure o nello strumento Esplora servizi multimediali di Azure hello (http://aka.ms/amse).

Hello nella tabella seguente illustra gli stati dei canali mapping stati toobilling hello API e portale di Azure. Si noti che sono leggermente diversi tra hello API e portale interfaccia hello stati Non appena un canale è nello stato "Running" hello tramite API hello o in stato di "Streaming" nel portale di Azure hello o hello "Pronto", la fatturazione sarà attiva.
Canale di hello toostop dalla fatturazione è ulteriormente, hai tooStop hello canale tramite API hello o nel portale di Azure hello.
È responsabile per l'arresto dei canali al termine con canale codifica live hello.  Errore toostop un canale codifica comporterà la fatturazione continua.

### <a id="states"></a>Gli stati dei canali e modalità di mapping toohello modalità di fatturazione
stato corrente di Hello di un canale. I valori possibili sono:

* **Arrestato**. Si tratta dello stato iniziale di hello di hello canale dopo la sua creazione, (a meno che l'avvio automatico è stato selezionato nel portale di hello.) In questo stato non viene eseguita alcuna attività di fatturazione. In questo stato, le proprietà del canale hello possono essere aggiornate, ma non è consentito lo streaming.
* **Avvio in corso**. Canale Hello viene avviato. In questo stato non viene eseguita alcuna attività di fatturazione. In questo stato non è consentito alcun aggiornamento o streaming. Se si verifica un errore, hello canale restituisce toohello stato arrestato.
* **In esecuzione**. Hello canale è in grado di elaborare flussi live. La fatturazione è ora attiva. È necessario arrestare hello canale tooprevent ulteriormente di fatturazione. 
* **Arresto in corso**. Canale Hello è stata interrotta. In questo stato di transizione non viene eseguita alcuna attività di fatturazione. In questo stato non è consentito alcun aggiornamento o streaming.
* **Eliminazione in corso**. Canale Hello viene eliminata. In questo stato di transizione non viene eseguita alcuna attività di fatturazione. In questo stato non è consentito alcun aggiornamento o streaming.

Hello nella tabella seguente viene illustrato come canale stati modalità di fatturazione toohello mappa. 

| Stato del canale | Indicatori dell'interfaccia utente del portale | Fatturazione? |
| --- | --- | --- |
| Avvio in corso |Avvio in corso |No (stato temporaneo) |
| In esecuzione |Pronto (nessun programma in esecuzione)<br/>oppure<br/>Streaming (almeno un programma in esecuzione) |SÌ |
| Arresto in corso |Arresto in corso |No (stato temporaneo) |
| Arrestato |Arrestato |No |

### <a name="automatic-shut-off-for-unused-channels"></a>Spegnimento automatico per i canali non usati
A partire dal 25 gennaio 2016, Servizi multimediali ha distribuito un aggiornamento che interrompe automaticamente un canale (con la codifica live abilitata) dopo che è rimasto in esecuzione in stato di mancato utilizzo per un lungo periodo. Si applica tooChannels che non dispongono di alcuna i programmi attivi e che non hanno ricevuto un input contributo feed per un lungo periodo di tempo.

soglia di Hello per un periodo inutilizzato è nominalmente 12 ore, ma è soggetto toochange.

## <a name="live-encoding-workflow"></a>Flusso di lavoro della codifica live
il diagramma seguente Hello rappresenta un flusso di lavoro streaming in tempo reale in cui un canale riceve un flusso a velocità in bit singola in uno dei seguenti protocolli hello: RTMP, Smooth Streaming o RTP (MPEG-TS); Consente di codificare quindi hello flusso tooa multi-flusso velocità in bit. 

![Flusso di lavoro live][live-overview]

## <a id="scenario"></a>Scenario comune di streaming live
di seguito Hello sono passaggi generali per la creazione di applicazioni comuni di streaming in tempo reale.

> [!NOTE]
> Attualmente, hello max consigliata la durata di un evento in tempo reale è 8 ore. Se è necessario un canale toorun per lunghi periodi di tempo, contattare amslived all'indirizzo Microsoft.com. Tenere presente che vi sia un impatto sulla fatturazione per la codifica live è opportuno tenere presente che se si lascia un canale di codifica live in stato "Running" hello daranno luogo ad addebiti fatturazione orari.  È consigliabile arrestare immediatamente i canali in esecuzione dopo l'evento di streaming in tempo reale viene completato tooavoid costi extra orarie. 
> 
> 

1. Connettere un computer tooa videocamera. Avviare e configurare un codificatore live locale che può restituire un **singolo** flusso a velocità in bit in uno dei seguenti protocolli hello: RTP (MPEG-TS), Smooth Streaming o RTMP. 
   
    Questa operazione può essere eseguita anche dopo la creazione del canale.
2. Creare e avviare un canale. 
3. URL di inserimento recuperare hello del canale. 
   
    URL di inserimento Hello viene utilizzato dal codificatore live di hello toosend hello flusso toohello canale.
4. Recuperare l'URL di anteprima del canale hello. 
   
    Utilizzare questo tooverify URL che il canale riceve correttamente flusso live hello.
5. Creare un programma. 
   
    Quando tramite hello portale di Azure, la creazione di un programma crea inoltre un asset. 
   
    Quando si utilizza il SDK per .NET o REST è necessario toocreate un asset e specificare toouse questo asset durante la creazione di un programma. 
6. Pubblicare hello asset associato al programma hello.   
   
    >[!NOTE]
    >Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. endpoint da cui si desidera toostream contenuto di streaming Hello è toobe in hello **esecuzione** stato. 
    
7. Avviare il programma di hello quando sei pronto toostart streaming e l'archiviazione.
8. Facoltativamente, codificatore live hello può essere segnalato toostart un annuncio. annuncio Hello viene inserito nel flusso di output di hello.
9. Arrestare il programma hello ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello.
10. Eliminare programma hello (e facoltativamente elimina hello asset).   

> [!NOTE]
> È molto importante non tooforget tooStop un canale di codifica Live. Tenere presente che è oraria fatturazione impatto per la codifica in tempo reale e occorre tenere presente che se si lascia un canale di codifica live in stato "Running" hello comporterà ulteriori addebiti nella fatturazione.  È consigliabile arrestare immediatamente i canali in esecuzione dopo l'evento di streaming in tempo reale viene completato tooavoid costi extra orarie. 
> 
> 

## <a id="channel"></a>Configurazioni di input (inserimento) del canale
### <a id="Ingest_Protocols"></a>Protocollo di streaming di inserimento
Se hello **tipo di codificatore** è troppo**Standard**, le opzioni valide sono:

* **RTP** (MPEG-TS): MPEG-2 Transport Stream su RTP.  
* **RTMP**
* **MP4 frammentato** (Smooth Streaming) a velocità in bit singola

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP (MPEG-TS): MPEG-2 Transport Stream su RTP.
Caso di utilizzo tipico: 

Professional emittenti in genere utilizzano codificatori di fascia alta in locale da fornitori di tecnologie elementare, Ericsson, Ateme, Imagine o Envivio toosend un flusso. Usato spesso insieme a reti di reparti IT e private.

Considerazioni:

* si consiglia di utilizzare Hello di un flusso di trasporto unico programma (SPTS) di input. 
* È possibile immettere i flussi audio di too8 utilizzando MPEG-2 TS su RTP. 
* flusso video Hello deve avere una velocità in bit media inferiore a 15 Mbps
* Hello aggregazione velocità in bit media dei flussi audio hello deve essere inferiore a 1 Mbps
* Seguenti sono hello codec supportati:
  
  * MPEG-2/H.262 Video 
    
    * Main Profile (4:2:0)
    * High Profile (4:2:0, 4:2:2)
    * 422 Profile (4:2:0, 4:2:2)
  * MPEG-4 AVC/H.264 Video  
    
    * Baseline, Main, High Profile (4:2:0 a 8 bit)
    * High 10 Profile (4:2:0 a 10 bit)
    * High 422 Profile (4:2:2 a 10 bit)
  * MPEG-2 AAC-LC Audio 
    
    * Mono, Stereo, Surround (5.1, 7.1)
    * Stile MPEG-2, pacchetto ADTS
  * Dolby Digital (AC-3) Audio 
    
    * Mono, Stereo, Surround (5.1, 7.1)
  * MPEG Audio (Layer II e III) 
    
    * Mono, Stereo
* I codificatori di trasmissione consigliati includono:
  
  * Imagine Communications Selenio ENC 1
  * Imagine Communications Selenio ENC 2
  * Elemental Live

#### <a id="single_bitrate_RTMP"></a>RTMP a velocità in bit singola
Considerazioni:

* flusso in ingresso Hello non può contenere più velocità in bit video
* flusso video Hello deve avere una velocità in bit media inferiore a 15 Mbps
* flusso audio Hello deve avere una velocità in bit media di sotto di 1 Mbps
* Seguenti sono hello codec supportati:
* MPEG-4 AVC/H.264 Video
* Baseline, Main, High Profile (4:2:0 a 8 bit)
* High 10 Profile (4:2:0 a 10 bit)
* High 422 Profile (4:2:2 a 10 bit)
* MPEG-2 AAC-LC Audio
* Mono, Stereo, Surround (5.1, 7.1)
* Frequenza di campionamento a 44.1 kHz
* Stile MPEG-2, pacchetto ADTS
* I codec consigliati includono:
* Telestream Wirecast
* Flash Media Live Encoder

#### <a name="single-bitrate-fragmented-mp4-smooth-streaming"></a>MP4 frammentato (Smooth Streaming) a velocità in bit singola
Caso di utilizzo tipico:

Usare i codificatori live locale da fornitori di tecnologie elementare, Ericsson, Ateme, Envivio toosend hello flusso di input su hello aprire internet tooa nelle vicinanze data center di Azure.

Considerazioni:

Come per [RTMP a velocità in bit singola](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP).

#### <a name="other-considerations"></a>Altre considerazioni
* È possibile modificare hello protocollo input durante hello canale o relativi programmi sono in esecuzione. Se sono necessari protocolli diversi, è consigliabile creare canali separati per ciascun protocollo di input.
* Risoluzione massima per il flusso video in ingresso hello è diverse da 1920x1080 e al massimo 60 campi al secondo se interlacciata o 30 frame al secondo se progressivo.

### <a name="ingest-urls-endpoints"></a>URL di inserimento (endpoint)
Un canale, fornisce un endpoint di input (URL di inserimento) specificare nel codificatore live hello, in modo da propagare codificatore hello flussi tooyour canali.

È possibile ottenere hello URL di inserimento dopo aver creato un canale. tooget questi URL, hello canale non presenti toobe hello **esecuzione** stato. Quando si è pronti toostart push dei dati in hello canale, deve essere hello **esecuzione** stato. Una volta hello canale inizia l'inserimento di dati, puoi visualizzare in anteprima il flusso tramite hello anteprima URL.

È possibile inserire un flusso live MP4 frammentato (Smooth Streaming) tramite una connessione SSL. tooingest su SSL, verificare che hello tooupdate tooHTTPS URL di inserimento. Si noti che attualmente AMS non supporta SSL con domini personalizzati.  

### <a name="allowed-ip-addresses"></a>Indirizzi IP consentiti
È possibile definire gli indirizzi IP hello consentiti toopublish toothis video channel. Gli indirizzi IP consentiti possono essere specificati come un singolo indirizzo IP, ad esempio '10.0.0.1', come un intervallo IP usando un indirizzo IP e una subnet mask CIDR, ad esempio '10.0.0.1/22' o come un intervallo di indirizzi IP usando un indirizzo IP e una subnet mask decimale puntata, ad esempio '10.0.0.1(255.255.252.0)'.

Se non viene specificato alcun indirizzo IP e non è presente una definizione della regola, non sarà consentito alcun indirizzo IP. tooallow qualsiasi indirizzo IP, creare una regola e impostare 0.0.0.0/0.

## <a name="channel-preview"></a>Anteprima del canale
### <a name="preview-urls"></a>URL di anteprima
I canali forniscono un endpoint di anteprima (URL di anteprima) di utilizzare toopreview e convalidare il flusso prima di elaborarlo ulteriormente e di recapito.

È possibile ottenere l'URL di anteprima di hello quando si crea il canale hello. URL hello tooget, canale hello non presenti toobe hello **esecuzione** stato.

Una volta hello canale inizia l'inserimento di dati, è possibile visualizzare in anteprima il flusso.

> [!NOTE]
> Attualmente il flusso di anteprima hello può solo essere recapitato in MP4 frammentato (Smooth Streaming) formato indipendentemente dalla hello specificato il tipo di input. È possibile utilizzare hello [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) player tootest hello Smooth Streaming. È anche possibile usare un lettore ospitato in Azure tooview portale hello del flusso.
> 
> 

### <a name="allowed-ip-addresses"></a>Indirizzi IP consentiti
È possibile definire gli indirizzi IP hello consentiti tooconnect toohello endpoint di anteprima. Se non viene specificato alcun indirizzo IP, sarà consentito qualsiasi indirizzo IP. Gli indirizzi IP consentiti possono essere specificati come un singolo indirizzo IP, ad esempio '10.0.0.1', come un intervallo di indirizzi IP usando un indirizzo IP e una subnet mask CIDR, ad esempio '10.0.0.1/22' o come un intervallo di indirizzi IP usando un indirizzo IP e una subnet mask decimale puntata, ad esempio '10.0.0.1(255.255.252.0)').

## <a name="live-encoding-settings"></a>Impostazioni per la codifica live
In questa sezione viene descritto come le impostazioni di hello per codificatore live di hello all'interno di hello canale è possono essere modificata, quando hello **tipo di codifica** di un canale è stato impostato troppo**Standard**.

> [!NOTE]
> Quando si immettono più tracce di lingua e si esegue la codifica live con Azure, per l'input multilingua è supportato solo RTP. È possibile definire i flussi audio di too8 utilizzando MPEG-2 TS su RTP. Non è invece supportato l'inserimento di più tracce audio con RTMP o Smooth Streaming. Quando esegue la codifica live con [locale live codifica](media-services-live-streaming-with-onprem-encoders.md), non si verifica questa limitazione poiché qualsiasi viene inviato tooAMS passa attraverso un canale senza ulteriore elaborazione.
> 
> 

### <a name="ad-marker-source"></a>Origine del marcatore di annunci
È possibile specificare l'origine di hello per segnali dei marcatori di Active Directory. Valore predefinito è **Api**, che indica il codificatore live di hello all'interno di hello canale deve essere in ascolto tooan asincrona **API marcatore Ad**.

Hello valido è **Scte35** (consentito solo se l'inserimento di hello protocollo di streaming è impostato tooRTP (MPEG-TS). Quando viene specificato Scte35, codificatore live hello analizza i segnali i segnali SCTE-35 hello flusso di input RTP (MPEG-TS).

### <a name="cea-708-closed-captions"></a>Sottotitoli codificati CEA-708
Flag facoltativo che indica hello codificatore live tooignore dati CEA 708 sottotitoli incorporati nel video in ingresso hello. Quando il flag di hello è impostato toofalse (impostazione predefinita), il codificatore hello rileverà e reinserire i dati CEA 708 nei flussi video di output hello.

### <a name="video-stream"></a>Flusso video
Facoltativo. Descrive flusso video input hello. Se questo campo non viene specificato, viene utilizzato il valore di predefinito hello. Questa impostazione è consentita solo se hello tooRTP (MPEG-TS) si imposta il protocollo di flusso di input.

#### <a name="index"></a>Indice
Indice in base zero che specifica quale flusso video di input deve essere elaborata dal codificatore live di hello all'interno di hello del canale. Questa impostazione si applica solo se il protocollo di streaming di inserimento è RTP (MPEG-TS).

Il valore predefinito è zero. È consigliabile toosend in un flusso di trasporto unico programma (SPTS). Se il flusso di input hello contiene più programmi, codificatore live hello analizza hello tabella mappa programmi (PMT) nell'input hello identifica gli input hello che hanno un nome tipo flusso MPEG-2 Video o h. 264 e li dispone in ordine di hello specificato in hello pag. Indice in base zero di Hello viene quindi utilizzato toopick voce n-esimo hello in tale disposizione.

### <a name="audio-stream"></a>Flusso audio
Facoltativo. Descrive i flussi audio di hello input. Se questo campo non viene specificato, vengono applicati i valori predefiniti di hello specificati. Questa impostazione è consentita solo se hello tooRTP (MPEG-TS) si imposta il protocollo di flusso di input.

#### <a name="index"></a>Indice
È consigliabile toosend in un flusso di trasporto unico programma (SPTS). Se il flusso di input hello contiene più programmi, hello codificatore live all'interno di hello canale analizza hello tabella mappa programmi (PMT) nell'input hello, identifica gli input hello che dispone di un nome di tipo flusso di MPEG-2 AAC ADTS o AC-3 System-A, AC-3 System-B o MPEG-2 Private File PE o MPEG-1 Audio o MPEG-2 Audio e li dispone in ordine di hello specificato in hello pag. Indice in base zero di Hello viene quindi utilizzato toopick voce n-esimo hello in tale disposizione.

#### <a name="language"></a>Lingua
Identificatore della lingua del flusso audio hello, conformi tooISO 639-2, ad esempio jolly Hello Se non è presente, il valore predefinito di hello è UND (undefined).

Possono essere presenti backup too8 flusso audio specificare set se l'input hello toohello canale è MPEG-2 TS su RTP. Tuttavia, può essere presenti due voci con hello dello stesso valore di indice.

### <a id="preset"></a>Set di impostazioni del sistema
Specifica hello preimpostato toobe utilizzato dal codificatore live di hello all'interno di questo canale. Attualmente, hello consentiti è solo **Default720p** (impostazione predefinita).

Si noti che se sono necessari set di impostazioni personalizzati, si deve contattare amslived in Microsoft.com.

**Default720p** verrà codificare video hello in hello 7 livelli seguenti.

#### <a name="output-video-stream"></a>Flusso video di output
| Velocità in bit | Larghezza | Altezza: | MaxFPS | Profilo | Nome del flusso di output |
| --- | --- | --- | --- | --- | --- |
| 3500 |1280 |720 |30 |Alto |Video_1280x720_3500kbps |
| 2200 |960 |540 |30 |Principale |Video_960x540_2200kbps |
| 1350 |704 |396 |30 |Principale |Video_704x396_1350kbps |
| 850 |512 |288 |30 |Principale |Video_512x288_850kbps |
| 550 |384 |216 |30 |Principale |Video_384x216_550kbps |
| 350 |340 |192 |30 |Di base |Video_340x192_350kbps |
| 200 |340 |192 |30 |Di base |Video_340x192_200kbps |

#### <a name="output-audio-stream"></a>Flusso audio di output
L'audio viene codificato toostereo AAC-LC a 64 kbps, frequenza di campionamento di 44,1 kHz di campionamento.

## <a name="signaling-advertisements"></a>Segnalazione di annunci
Quando nel canale è abilitata la codifica live, nella pipeline è presente un componente che elabora il flusso video ed è in grado di modificarlo. È possibile segnalare per hello canale tooinsert Slate e/o gli annunci in flusso a velocità in bit adattiva in uscita hello. Slate sono comunque le immagini che è possibile utilizzare toocover dei feed live input hello in alcuni casi (ad esempio durante un'interruzione pubblicitaria). Invia annunci segnali, sono ora sincronizzata segnali che si incorpora in hello in uscita flusso tootell hello lettore video tootake azione speciale, ad esempio tooswitch tooan annuncio al momento appropriato hello. Vedere questo [blog](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/) per una panoramica del meccanismo di segnalazione hello i segnali SCTE-35 usato a questo scopo. Di seguito è illustrato uno scenario tipico che è possibile implementare in un evento live.

1. Disporre i visualizzatori di ottenere un'immagine di pre-evento prima dell'avvio evento hello.
2. Disporre i visualizzatori di ottenere un'immagine di post-evento al termine dell'evento hello.
3. Disporre i visualizzatori di ottenere un'immagine di evento di errore se si verifica un problema durante l'evento hello (ad esempio, interruzione dell'alimentazione in stadio hello).
4. Invio di un'interruzione Pubblicitaria immagine toohide hello in tempo reale di eventi durante un'interruzione pubblicitaria.

di seguito Hello sono proprietà hello che è possibile impostare quando segnali degli annunci. 

### <a name="duration"></a>Duration
durata Hello, in secondi, di un'interruzione pubblicitaria hello. Questo è un valore positivo diverso da zero toobe in un'interruzione pubblicitaria ordine toostart hello. Quando un'interruzione pubblicitaria in corso e durata hello è toozero set con hello battuta corrispondente interruzione pubblicitaria in corso di hello, quindi l'interruzione viene annullata.

### <a name="cueid"></a>ID battuta
Un ID univoco per l'interruzione pubblicitaria hello, toobe utilizzato dall'applicazione downstream tootake le operazioni necessarie. È necessario toobe un numero intero positivo. È possibile impostare questo valore tooany casuale numero intero positivo o usare un hello tootrack sistema upstream ID battuta. Apportare alcune toonormalize qualsiasi integer toopositive ID prima dell'invio tramite hello API.

### <a name="show-slate"></a>Visualizza slate
Facoltativo. Segnala hello codificatore live tooswitch toohello [predefinito slate](media-services-manage-live-encoder-enabled-channels.md#default_slate) immagine durante un'interruzione pubblicitaria e nascondere feed video in ingresso hello. Durante la visualizzazione dello slate viene disattivato anche l'audio. Il valore predefinito è **false**. 

immagine di Hello usata sarà hello quella specificata tramite l'asset dello slate predefinito hello proprietà Id in fase di creazione del canale hello di hello. lo slate Hello sarà adattata dimensioni dell'immagine toofit hello visualizzato. 

## <a name="insert-slate--images"></a>Inserire immagini dello slate
codificatore live di Hello all'interno di hello canale può essere l'immagine dello slate tooa tooswitch segnalato. Può anche essere segnalato tooend un slate in corso. 

codificatore live Hello può essere configurato tooswitch tooa ardesia immagine e nascondere hello segnale video in ingresso in determinate situazioni, ad esempio durante un'interruzione pubblicitaria. Se non è configurato uno slate, il video di input non viene mascherato durante l'interruzione pubblicitaria.

### <a name="duration"></a>Duration
Hello durata dello slate hello in secondi. Questo è un valore positivo diverso da zero toobe in slate hello toostart di ordine. Se è in corso uno slate e viene specificata una durata pari a zero, lo slate in corso verrà terminato.

### <a name="insert-slate-on-ad-marker"></a>Inserisci slate su marcatore di annuncio
Quando set tootrue, questa impostazione configura hello codificatore live tooinsert un'immagine dello slate durante un'interruzione pubblicitaria. valore predefinito di Hello è true. 

### <a id="default_slate"></a>ID asset dello slate predefinito

Facoltativo. Specifica l'Id dell'Asset di servizi multimediali che contiene l'immagine dello slate hello hello hello. Il valore predefinito è Null. 


>[!NOTE] 
>Prima di creare il canale hello hello immagine dello slate con hello seguenti vincoli deve essere caricato come asset dedicato (devono essere presenti altri file in questo asset). Questa immagine viene utilizzata solo quando l'inserimento di uno slate causa l'interruzione pubblicitaria tooan codificatore live hello oppure è stata in modo esplicito segnalato tooinsert uno slate. codificatore live Hello possono essere inoltre inserite in una modalità dello slate durante determinate condizioni di errore: ad esempio se segnale di input hello viene perso. Quando non viene attualmente non toouse opzione un'immagine personalizzata codificatore live hello entra in uno stato 'perdita di segnale di input'. È possibile votare per l'aggiunta di questa funzionalità [qui](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel).


* Risoluzione massima: 1920x1080.
* Dimensione massima: 3 MB.
* nome del file Hello deve avere un'estensione *. jpg.
* immagine di Hello deve essere caricati in un Asset come hello che assetfile solo in tale Asset e questo AssetFile deve essere contrassegnato come file primario hello. Hello Asset non può essere crittografato di archiviazione.

Se hello **predefinito slate Id Asset** non viene specificato, e **Inserisci slate su marcatore di annuncio** è troppo**true**, un'immagine di servizi multimediali di Azure predefinita verrà utilizzato toohide hello di input flusso video. Durante la visualizzazione dello slate viene disattivato anche l'audio. 

## <a name="channels-programs"></a>Programmi del canale
Un canale è associato a programmi che consentono la pubblicazione di hello toocontrol e l'archiviazione di segmenti in un flusso in tempo reale. I programmi sono gestiti dai canali. Hello relazione canale e il programma è molto simile tootraditional media, in cui un canale è un flusso costante di contenuto e l'evento con ambito toosome timeout su tale canale è un programma.

È possibile specificare hello numero di ore che si vuole tooretain hello registrato contenuto per il programma hello, impostazione hello **finestra archivio** lunghezza. Questo valore può essere impostato da un minimo di 25 ore massimo tooa 5 minuti. Lunghezza dell'intervallo di archiviazione determina anche l'intervallo di tempo i client possono cercare indietro nel tempo dalla posizione live corrente hello massimo hello. I programmi eseguibili sul periodo di tempo specificato hello, ma il contenuto che non è sincronizzato con la lunghezza della finestra hello viene scartato in modo continuo. Questo valore di questa proprietà determina anche per quanto tempo hello client possono raggiungere i manifesti.

Ogni programma è associato a un Asset che archivia il contenuto di hello inviati nel flusso. Un asset è mappato tooa blocco contenitore blob di account di archiviazione Azure hello e file hello in asset hello vengono archiviati come BLOB nel contenitore. il programma hello toopublish in modo che i clienti possono visualizzare il flusso di hello è necessario creare un localizzatore OnDemand per hello associati asset. Con questo localizzatore sarà si toobuild un URL di streaming che è possibile fornire tooyour client.

Un canale supporta fino toothree programmi in esecuzione contemporaneamente in modo è possibile creare più archivi di hello stesso flusso in ingresso. In questo modo toopublish e archiviare parti diverse di un evento in base alle esigenze. Ad esempio, il requisito di business è tooarchive 6 ore di un programma, ma toobroadcast solo ultimi 10 minuti. tooaccomplish, è necessario toocreate due programmi in esecuzione simultanea. Un programma è impostato tooarchive 6 ore dell'evento hello ma hello non viene pubblicato. Hello altro programma è tooarchive insieme per 10 minuti e questo programma viene pubblicato.

Non riutilizzare i programmi esistenti per nuovi eventi. In alternativa, creare e avviare un nuovo programma per ogni evento, come descritto nella sezione di programmazione di applicazioni di Streaming Live hello.

Avviare il programma di hello quando sei pronto toostart streaming e l'archiviazione. Arrestare il programma hello ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello. 

contenuto toodelete archiviato, interrompere ed eliminare hello programma, quindi eliminare asset associato hello. Non è possibile eliminare un asset se è utilizzato da un programma. programma Hello deve prima essere eliminato. 

Anche dopo aver arrestato ed eliminato il programma hello, hello gli utenti sarebbero in grado di toostream il contenuto archiviato come video on demand, per fino a quando non si elimina asset hello.

Se si desidera hello tooretain archiviato il contenuto, ma non è disponibile per lo streaming, eliminare hello localizzatore di streaming.

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>Ottenere un'anteprima di un feed live
Se la codifica Live è abilitata, è ora possibile ottenere un'anteprima del feed in tempo reale hello come raggiunge hello canale. Può trattarsi di un toocheck strumento estremamente utile se il feed in tempo reale stia effettivamente raggiungendo il canale hello. 

## <a id="states"></a>Gli stati dei canali e il mapping tra stati toohello modalità di fatturazione
stato corrente di Hello di un canale. I valori possibili sono:

* **Arrestato**. Si tratta dello stato iniziale di hello di hello canale dopo la sua creazione. In questo stato, le proprietà del canale hello possono essere aggiornate, ma non è consentito lo streaming.
* **Avvio in corso**. Canale Hello viene avviato. In questo stato non è consentito alcun aggiornamento o streaming. Se si verifica un errore, hello canale restituisce toohello stato arrestato.
* **In esecuzione**. Hello canale è in grado di elaborare flussi live.
* **Arresto in corso**. Canale Hello è stata interrotta. In questo stato non è consentito alcun aggiornamento o streaming.
* **Eliminazione in corso**. Canale Hello viene eliminata. In questo stato non è consentito alcun aggiornamento o streaming.

Hello nella tabella seguente viene illustrato come canale stati modalità di fatturazione toohello mappa. 

| Stato del canale | Indicatori dell'interfaccia utente del portale | Fatturato? |
| --- | --- | --- |
| Avvio in corso |Avvio in corso |No (stato temporaneo) |
| In esecuzione |Pronto (nessun programma in esecuzione)<br/>oppure<br/>Streaming (almeno un programma in esecuzione) |SÌ |
| Arresto in corso |Arresto in corso |No (stato temporaneo) |
| Arrestato |Arrestato |No |

> [!NOTE]
> Attualmente, Media iniziale di canale hello è circa 2 minuti, ma in alcuni casi potrebbe richiedere too20 + minuti. Reimpostazioni di canale possono richiedere too5 minuti.
> 
> 

## <a id="Considerations"></a>Considerazioni
* Quando un canale di **Standard** tipo di codifica si verifica una perdita di feed di origine di input/contributo, compensa sostituendo hello origine video o audio con un slate di errore e di inattività. Hello canale continuerà tooemit uno slate fino a quando l'input hello/contributo feed riprende. Si consiglia di non lasciare un canale live in tale stato per più di 2 ore. Oltre tale punto, non è garantito il comportamento di hello di hello canale di input dopo la riconnessione, non è il comportamento in risposta tooa comando di ripristino. Sarà disponibile toostop hello canale, eliminarlo e crearne uno nuovo.
* È possibile modificare hello protocollo input durante hello canale o relativi programmi sono in esecuzione. Se sono necessari protocolli diversi, è consigliabile creare canali separati per ciascun protocollo di input.
* Ogni volta che si riconfigura il codificatore live di hello, chiamare hello **reimpostare** metodo sul canale hello. Prima reimpostare il canale di hello, è necessario programma hello toostop. Dopo aver reimpostato il canale di hello, riavviare il programma di hello.
* Un canale può essere arrestato solo quando è in stato di esecuzione hello e tutti i programmi sul canale hello sono stati arrestati.
* Per impostazione predefinita è possibile aggiungere solo 5 canali tooyour account di servizi multimediali. Si tratta di una quota flessibile per tutti i nuovi account. Per altre informazioni, vedere [Quote e limitazioni](media-services-quotas-and-limitations.md).
* È possibile modificare hello protocollo input durante hello canale o relativi programmi sono in esecuzione. Se sono necessari protocolli diversi, è consigliabile creare canali separati per ciascun protocollo di input.
* Verrà addebitato solo quando il canale è in hello **esecuzione** stato. Per ulteriori informazioni, vedere troppo[questo](media-services-manage-live-encoder-enabled-channels.md#states) sezione.
* Attualmente, hello max consigliata la durata di un evento in tempo reale è 8 ore. Se è necessario un canale toorun per lunghi periodi di tempo, contattare amslived all'indirizzo Microsoft.com.
* Assicurarsi che toohave hello endpoint di streaming da cui si desidera toostream contenuto hello **esecuzione** stato.
* Quando si immettono più tracce di lingua e si esegue la codifica live con Azure, per l'input multilingua è supportato solo RTP. È possibile definire i flussi audio di too8 utilizzando MPEG-2 TS su RTP. Non è invece supportato l'inserimento di più tracce audio con RTMP o Smooth Streaming. Quando esegue la codifica live con [locale live codifica](media-services-live-streaming-with-onprem-encoders.md), non si verifica questa limitazione poiché qualsiasi viene inviato tooAMS passa attraverso un canale senza ulteriore elaborazione.
* codifica utilizza set di impostazioni di Hello hello nozione di "frequenza dei fotogrammi max" di 30 fps. Pertanto se hello input 60fps, 59.97i / frame input hello vengono eliminati/deserializzare-interlaced too30/29.97 fps. Se l'input di hello è 50fps/50i, frame input hello sono too25 eliminati/deserializzare-interlaced fps. Se l'input di hello è 25 fps, l'output rimane 25 fps.
* Non dimenticare tooSTOP YOUR canali al termine. per evitare il proseguimento della fatturazione.

## <a name="known-issues"></a>Problemi noti
* Tempo di avvio del canale è stato migliorato tooan Media di 2 minuti, ma in alcuni casi di aumento della domanda potrebbe richiedere ancora too20 + minuti.
* Alle emittenti professionali viene fornito il supporto RTP. Vedere le note di hello su RTP in [questo](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/) blog.
* Immagini dello Slate devono essere conforme toorestrictions descritto [qui](media-services-manage-live-encoder-enabled-channels.md#default_slate). Se si tenta di creare un canale con un errore slate predefinita che è maggiore di 1920x1080, hello verrà richiesta.
* Ancora una volta... non dimenticare tooSTOP YOUR canali al termine streaming. per evitare il proseguimento della fatturazione.

## <a name="next-step"></a>Passaggio successivo
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Argomenti correlati
[Distribuzione di eventi Live Streaming con Servizi multimediali di Azure](media-services-overview.md)

[Creare canali che eseguono la codifica live da un flusso di velocità in bit singola tooadaptive velocità in bit con il portale](media-services-portal-creating-live-encoder-enabled-channel.md)

[Creare canali che eseguono la codifica live da un flusso di velocità in bit singola velocità in bit tooadaptive con .NET SDK](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[Gestire i canali con l'API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[Concetti su Servizi multimediali di Azure](media-services-concepts.md)

[Specifica per l'inserimento live di un flusso MP4 frammentato con Servizi multimediali di Azure](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

