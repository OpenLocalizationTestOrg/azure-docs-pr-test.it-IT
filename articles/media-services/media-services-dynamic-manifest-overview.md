---
title: aaaFilters e dinamici manifesti | Documenti Microsoft
description: "In questo argomento viene descritto come toocreate filtra il client può utilizzarli toostream sezioni specifiche di un flusso. Servizi multimediali crea manifesti dinamica tooarchive questo flusso selettiva."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a>Filtri e manifesti dinamici
A partire dalla versione 2.11, servizi multimediali consente toodefine filtri per le risorse. Questi filtri sono regole lato server che consentono ai clienti toochoose toodo elementi quali: la riproduzione solo una sezione di un video (anziché la riproduzione di hello video interi), oppure specificare solo un subset di rendering audio e video che (è possono gestire i dispositivi del cliente invece di tutte le copie trasformate hello associati asset hello). Questo filtro delle risorse di archiviazione tramite **manifesto dinamica**che vengono creati al momento di toostream di richiesta del cliente, un video in base a filtri specificati.

Questo argomento vengono descritti scenari comuni in cui utilizzando filtri sarebbe tootopics tooyour molto utili ai clienti e i collegamenti che illustrano come toocreate filtri a livello di codice (attualmente, è possibile creare filtri con le API REST solo).

## <a name="overview"></a>Panoramica
Per il recapito del contenuto toocustomers (flusso di eventi in tempo reale o video on Demand) l'obiettivo è toodeliver un toovarious video di qualità elevata per i dispositivi in condizioni di rete diverso. tooachieve hello questo obiettivo seguente:

* codificare il flusso toomulti velocità in bit ([velocità in bit adattiva](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) flusso video (questo si occuperà di condizioni di qualità e la rete) e 
* usare servizi multimediali [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md) toodynamically comprimere nuovamente il flusso in diversi protocolli (questo si occuperà di streaming su dispositivi diversi). Servizi multimediali supporta il recapito di hello velocità in bit adattive tecnologie seguenti: MPEG DASH, Smooth Streaming e HTTP Live Streaming (HLS). 

### <a name="manifest-files"></a>File manifesto
Quando si codifica un asset per lo streaming a velocità in bit adattiva, un **manifesto** viene creato il file (playlist) (file hello è basato su XML o testo). Hello **manifesto** file include il flusso di metadati, ad esempio: tenere traccia di tipo (audio, video o testo), tenere traccia di nome, ora di inizio e fine, velocità in bit (qualità), i linguaggi di traccia, la finestra di presentazione (finestra temporale scorrevole di durata fissa), video codec (FourCC). Indica inoltre hello player tooretrieve hello successivo frammento fornendo informazioni sull'hello Avanti riproducibile frammenti video disponibili e la relativa posizione. Frammenti o segmenti sono hello effettivo "blocchi" di contenuto video.

Di seguito è riportato un esempio di file manifesto: 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a>Manifesti dinamici
Esistono [scenari](media-services-dynamic-manifest-overview.md#scenarios) quando il client richiede una maggiore flessibilità rispetto a quanto descritto nel file manifesto dell'asset di hello predefinito. ad esempio:

* Dispositivo specifico: recapitare solo hello specificato e/o trasformate specificato tracce lingue supportate dal dispositivo hello tooplayback utilizzati hello contenuto ("Copia filtro"). 
* Ridurre hello manifesto tooshow un clip secondario di un evento in tempo reale ("clip secondario filtro").
* Inizio hello taglio di un video ("l'eliminazione di un video").
* Modificare la finestra di presentazione (DVR) in ordine tooprovide una lunghezza limitata della finestra DVR hello nel lettore hello ("finestra presentazione modifica").

tooachieve questa flessibilità, offerte di servizi multimediali **manifesti dinamica** basato su via predefiniti [filtri](media-services-dynamic-manifest-overview.md#filters).  Dopo aver definito i filtri di hello, i client potrebbero utilizzate toostream una copia trasformata specifica o clip secondari del video. Specificano i filtri in hello URL di streaming. I filtri potrebbe essere applicato tooadaptive Usa velocità in bit protocolli supportati da [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md): HLS, MPEG-DASH e Smooth Streaming. ad esempio:

URL MPEG DASH con filtro

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

URL Smooth Streaming con filtro

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


Per ulteriori informazioni su come toodeliver il contenuto e la compilazione di streaming URL, vedere [recapito Panoramica contenuto](media-services-deliver-content-overview.md).

> [!NOTE]
> Si noti che i manifesti dinamica non modificare asset hello e hello manifesto predefinito per tale asset. Il client può scegliere toorequest un flusso con o senza filtri. 
> 
> 

### <a id="filters"></a>Filtri
Sono disponibili due tipi di filtri di asset: 

* Filtri globali (possono essere applicati tooany asset in hello account servizi multimediali di Azure, hanno una durata del conto hello) e 
* Filtri locali (può solo essere applicate tooan asset con cui hello filtro è associato al momento della creazione, avere una durata di asset hello). 

Tipi di filtri globali e locali sono esattamente hello stesse proprietà. Hello differenza principale tra hello due è per scenari di quale tipo di un filtro non è più adatto. Filtri globali vengono in genere adatti per i profili di dispositivo (filtro di rendering) in cui i filtri locali possano essere tootrim usato un asset specifico.

## <a id="scenarios"></a>Scenari comuni
Come accennato in precedenza, quando il recapito del contenuto toocustomers (flusso di eventi in tempo reale o video on Demand) l'obiettivo è toodeliver un video di alta qualità toovarious dispositivi in diversi le condizioni della rete. Possono tuttavia verificarsi anche altre situazioni in cui è opportuno applicare filtri agli asset e usare **manifesti dinamici**. Hello le sezioni seguenti offre una breve panoramica dei diversi scenari di filtro.

* Specificare solo un subset di audio e video trasformate in grado di gestire alcuni dispositivi (anziché tutte le copie trasformate hello associati asset hello). 
* Consente di riprodurre solo una sezione di un video (anziché riprodurre video interi hello).
* Regolazione della finestra di presentazione DVR

## <a name="rendition-filtering"></a>Filtro di rendering
È possibile scegliere tooencode l'asset toomultiple profili di codifica (linea di base h. 264, h. 264 alta, AACL, AACH, Dolby Digital Plus) e più velocità in bit qualità. Non tutti i dispositivi, tuttavia, supportano tutti i profili e le velocità in bit dell'asset. Solo i dispositivi Android di precedente generazione, ad esempio, supportano il profilo H.264 Baseline+AACL. Invio dispositivo tooa di velocità superiore che non è possibile ottenere vantaggi hello, costituisce uno spreco di calcolo della larghezza di banda e dispositivo. Tale dispositivo necessario decodificare tutti hello specificato informazioni solo tooscale, verso il basso per la visualizzazione.

Con un manifesto dinamica, è possibile creare profili di dispositivo, ad esempio dispositivi mobili, console, HD/SD e così via e includere tracce hello e qualità di cui si desidera toobe una parte di ciascun profilo.

![Esempio di filtro di rendering][renditions2]

Hello l'esempio seguente, un codificatore è stato utilizzato tooencode un asset in formato intermedio in sette trasformate video di ISO MP4s (da too1080p p 180). Hello asset codificato possono essere dinamicamente assemblati in uno dei seguenti protocolli di streaming hello: MPEG DASH, HLS e Smooth Streaming.  Nella parte superiore di hello del diagramma di hello, viene visualizzato hello HLS manifesto per asset hello senza filtri (contiene tutte le copie sette trasformate).  In basso a sinistra hello hello che HLS manifesto toowhich è stato applicato un filtro denominato "ott" viene visualizzato. filtro "ott" Hello specifica tooremove tutte le velocità in bit di sotto di 1 Mbps, che hanno comportato hello inferiore due livelli di qualità in risposta hello viene eliminati.  In hello in basso a destra, hello HLS toowhich manifesto è stato applicato un filtro denominato "mobile" viene visualizzato. filtro "mobile" Hello specifica tooremove trasformate in hello risoluzione è più grande 720p, che hanno comportato trasformate 1080p due hello viene rimosse.

![Filtro di rendering][renditions1]

## <a name="removing-language-tracks"></a>Rimozione delle tracce di lingua
Gli asset possono includere più lingue audio, ad esempio inglese, spagnolo, francese e così via. In genere, i responsabili di SDK di Windows Media Player hello selezione traccia audio e predefiniti tracce audio disponibile per selezione dell'utente. È difficile toodevelop tale SDK di Windows Media Player, è necessario che diverse implementazioni in player-Framework specifico del dispositivo. Inoltre, in alcune piattaforme, le API di Windows Media Player sono limitate e non includono funzionalità di selezione audio in cui gli utenti non è possibile selezionare o modificare una traccia audio predefinita hello. Con i filtri di asset, è possibile controllare il comportamento di hello creando filtri che includono solo le lingue audio desiderate.

![Filtro delle tracce di lingua][language_filter]

## <a name="trimming-start-of-an-asset"></a>Trimming della parte iniziale di un asset
Nella maggior parte degli eventi live streaming, operatori vengono eseguiti alcuni test prima dell'evento effettivo hello. Ad esempio, potrebbero includere uno slate simile al seguente prima di inizio dell'evento hello hello: "Programma avrà inizio momentaneamente". Se il programma hello è l'archiviazione, test di hello e dello slate dati vengono archiviati anche e verranno inclusi nella presentazione hello. Tuttavia, queste informazioni non devono essere visualizzate toohello client. Con un manifesto dinamica, è possibile creare un filtro di ora di inizio e rimuovere dati hello indesiderato dal manifesto hello.

![Trimming della parte iniziale][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a>Creazione di sottoclip (visualizzazioni) da un archivio live
Molti eventi live hanno una durata molto lunga ed è possibile quindi che un archivio live includa più eventi. Dopo aver hello evento live termina emittenti opportuno toobreak backup hello live archivio nella logica di programma e arrestare le sequenze. Quindi, pubblicare separatamente, tali programmi virtuali senza registra l'elaborazione di archivio in tempo reale hello e non la creazione di asset separati (che non sarà possibile ricevere vantaggio di frammenti memorizzati nella cache di hello esistente in hello CDN). Esempi di tali programmi virtuale (ritagliano secondari) sono hello trimestri di football o gioco basket, punti di hello nel baseball o singoli eventi di un pomeriggio del programma Olimpiadi.

Con un manifesto dinamica, è possibile creare filtri utilizzando l'ora di inizio e fine e creare visualizzazioni virtuali sopra hello dell'archivio in tempo reale. 

![Filtro di sottoclip][subclip_filter]

Asset filtrato:

![Sci][skiing]

## <a name="adjusting-presentation-window-dvr"></a>Regolazione della finestra di presentazione (DVR)
Attualmente servizi multimediali di Azure offre archiviazione circolare dove è possibile configurare la durata di hello tra 5 minuti: 25 ore. Manifesto dell'applicazione di filtri può essere utilizzato toocreate una sequenza finestra DVR sopra hello dell'archivio di hello, senza eliminare i supporti. Esistono molti scenari in cui emittenti tooprovide una finestra DVR limitata che consente di spostare con hello live edge e in hello contemporaneamente mantenere una finestra di archiviazione più grande. Un emittente possibile toouse hello dati fuori clip toohighlight di hello DVR finestra oppure he\she richiedere che tooprovide diversi DVR per dispositivi diversi. Ad esempio, la maggior parte dei dispositivi mobili hello non gestiscono big windows DVR (si può avere una finestra DVR 2 minuti per i dispositivi mobili e di 1 ora per i client desktop).

![Finestra DVR][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a>Regolazione LiveBackoff (posizione live)
Manifesto dell'applicazione di filtri può essere utilizzato tooremove alcuni secondi dal bordo in tempo reale di hello di un programma in tempo reale. In questo modo emittenti presentazione hello toowatch pubblicazione anteprima hello punto e creare punti di inserimento dell'annuncio visualizzatori hello ricevere flusso hello (in genere eseguito-off da 30 secondi). Emittenti possono quindi push questi framework client tootheir di annunci nel tempo per le informazioni di hello tooreceived e il processo prima opportunità di annuncio hello.

Supportano inoltre annuncio toohello, LiveBackoff può essere utilizzato per la regolazione posizione in tempo reale di download nel client in modo che quando i client dello sfasamento e hit edge in tempo reale hello possono comunque ottenere frammenti dal server anziché gli errori HTTP 404 o 412.

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a>Combinazione di più regole in un unico filtro
È possibile combinare più regole di filtro in un unico filtro. Ad esempio, è possibile definire uno slate tooremove regola di intervallo da un archivio in tempo reale e anche filtrare velocità in bit disponibili. Per più end di hello regole filtro risultato è la composizione hello (solo intersezione) di queste regole.

![multiple-rules][multiple-rules]

## <a name="create-filters-programmatically"></a>Creare filtri a livello di codice
Hello seguente argomento vengono illustrate le entità di servizi multimediali che sono correlati toofilters. argomento Hello viene inoltre illustrato come tooprogrammatically creare filtri.  

[Creare filtri con le API REST](media-services-rest-dynamic-manifest.md).

## <a name="combining-multiple-filters-filter-composition"></a>Combinazione di più filtri (filtro composizione)
È inoltre possibile combinare più filtri in un singolo URL. 

Hello scenario seguente viene illustrato perché potrebbe essere necessario toocombine filtri:

1. È necessario toofilter la qualità video per i dispositivi mobili, ad esempio Android o iPAD (in qualità di video toolimit ordine). tooremove hello qualità indesiderata, è necessario creare un filtro globale che è adatto per i profili di dispositivo. Come indicato in precedenza, è possibile utilizzare filtri globali per tutti gli asset in hello account senza qualsiasi ulteriore associazione di servizi multimediali stesso. 
2. Inoltre si desidera avviare hello tootrim e di fine di un asset. tooachieve, si potrebbe creare un filtro locale e impostare l'ora di inizio e fine hello. 
3. Si desidera toocombine entrambi di questi filtri (senza combinazione sarebbe necessario tooadd filtro toohello rimozione filtro qualità che renderà difficile l'utilizzo del filtro).

toocombine filtri, è necessario tooset hello filtro nomi toohello manifesto/playlist URL con delimitato. Si supponga che si dispone di un filtro denominato *MyMobileDevice* che filtra le qualità e si dispone di un altro denominato *MyStartTime* tooset una determinata ora di inizio. È possibile combinarli nel seguente modo:

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

È possibile combinare i filtri too3. 

Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.

## <a name="know-issues-and-limitations"></a>Problemi noti e limitazioni
* Il manifesto dinamico opera nei limiti dell'intervallo GOP (fotogrammi chiave) e, pertanto, il trimming eredita la precisione del GOP. 
* È possibile usare lo stesso nome di filtro per i filtri globali e locali. I filtri locali, tuttavia, hanno la precedenza e sovrascrivono quindi i filtri globali.
* Se si aggiorna un filtro, può richiedere too2 minuti per le regole di hello toorefresh endpoint di streaming. Se contenuto hello è stato gestito l'utilizzo di alcuni filtri e memorizzati nella cache in proxy e della rete CDN memorizza nella cache, l'aggiornamento di questi filtri possa causare errori di Windows Media player. È consigliabile cache di hello tooclear dopo l'aggiornamento del filtro hello. Se questa operazione non è consentita, prendere in considerazione la possibilità di usare un filtro diverso.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Distribuzione di contenuto tooCustomers Panoramica](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
