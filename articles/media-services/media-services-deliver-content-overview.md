---
title: toocustomers contenuto aaaDelivering | Documenti Microsoft
description: Questo argomento fornisce informazioni generali su tutti gli aspetti inerenti la distribuzione di contenuti con Servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>Recapitare contenuto toocustomers
Quando si sta offrendo il toocustomers contenuto streaming o video on Demand, l'obiettivo è dispositivi di alta qualità video toovarious toodeliver in condizioni di rete diverso.

tooachieve questo obiettivo, è possibile:

* Codificare il flusso video di flusso tooa più velocità in bit (velocità in bit adattiva). In questo modo la qualità e le condizioni di rete saranno gestite adeguatamente.
* Utilizzare Microsoft Azure Media Services [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md) toodynamically comprimere nuovamente il flusso in diversi protocolli. In questo modo si garantisce la trasmissione a diversi tipi di dispositivi. Servizi multimediali supporta il recapito di hello velocità in bit adattive tecnologie seguenti: MPEG-DASH, Smooth Streaming e HTTP Live Streaming (HLS).

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 

In questo articolo viene fornita una panoramica di importanti concetti di consegna dei contenuti.

toocheck problemi noti, vedere [problemi noti](media-services-deliver-content-overview.md#known-issues).

## <a name="dynamic-packaging"></a>creazione dinamica dei pacchetti
Con creazione dinamica dei pacchetti hello che servizi multimediali sono disponibili, che è possibile distribuire il contenuto di velocità in bit adattiva MP4 o Smooth Streaming con codifica in streaming formati supportati da servizi multimediali (MPEG-DASH, HLS, Smooth Streaming) senza toore-package in Questi formati di streaming. Si consiglia di distribuzione il contenuto con la creazione dinamica dei pacchetti.

Il vantaggio di tootake creazione dinamica dei pacchetti, è necessario tooencode il file mezzanine (origine) in un set di file MP4 a velocità in bit adattiva o file Smooth Streaming a velocità in bit adattiva.

Con creazione dinamica dei pacchetti, archiviare e pagare file hello in unico formato di archiviazione. Servizi multimediali creerà e fornirà una risposta di hello appropriata in base alle richieste.

La creazione dinamica dei pacchetti è disponibile per endpoint di streaming Standard e Premium. 

Per altre informazioni, vedere [Creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md).

## <a name="filters-and-dynamic-manifests"></a>Filtri e manifesti dinamici
Con Servizi multimediali è possibile definire filtri per i propri asset. Questi filtri sono regole lato server che consentono ai clienti di eseguire operazioni come riprodurre una sezione specifica di un video o specificare un subset di audio e video trasformate in grado di gestire i dispositivi del cliente (invece di tutte le copie trasformate hello associati asset hello ). Questo filtro viene ottenuto tramite *manifesti dinamici* che vengono creati quando il cliente richiede toostream un video in base a uno o più filtri specificati.

Per altre informazioni, vedere [Filtri e manifesti dinamici](media-services-dynamic-manifest-overview.md).

## <a name="locators"></a>Localizzatori
tooprovide l'utente con un URL che possa essere utilizzati toostream o scaricare il contenuto, è necessario innanzitutto toopublish l'asset creando un localizzatore. Un indicatore di posizione vengono forniti un hello tooaccess punto di ingresso i file contenuti in un asset. Servizi multimediali supporta due tipi di localizzatori:

* Localizzatori OnDemandOrigin. Si tratta di media toostream utilizzato (ad esempio, MPEG-DASH, HLS o Smooth Streaming) o scaricare file in modo progressivo.
* localizzatori URL di firma di accesso condiviso. Si tratta di computer locale tooyour toodownload usato supporti i file.

Un *criterio di accesso* è usato toodefine autorizzazioni hello (ad esempio lettura, scrittura ed elenco) e la durata per cui un client ha accesso per una particolare attività. Si noti che autorizzazione elenco hello (AccessPermissions.List) non deve essere utilizzato per la creazione di un indicatore di posizione OrDemandOrigin.

Per i localizzatori vengono definite date di scadenza. portale di Azure Hello imposta 100 anni la data di scadenza in hello futuri per i localizzatori.

> [!NOTE]
> Se si utilizza i localizzatori toocreate portale Azure hello prima marzo 2015, i localizzatori sono stati impostati tooexpire dopo due anni.
> 
> 

tooupdate data di scadenza su un indicatore di posizione, utilizzare [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API. Si noti che quando si aggiorna la data di scadenza hello di un localizzatore SAS, hello URL viene modificato.

I localizzatori non sono progettati toomanage controllo di accesso per utente. È possibile assegnare gli utenti tooindividual diritti accesso diverso mediante le soluzioni di Digital Rights Management (DRM). Per altre informazioni, vedere [Protezione dei file multimediali](http://msdn.microsoft.com/library/azure/dn282272.aspx).

Quando si crea un localizzatore, potrebbe esserci un ritardo di 30 secondi a causa di toorequired i processi di archiviazione e propagazione in archiviazione di Azure.

## <a name="adaptive-streaming"></a>Streaming adattivo
Le tecnologie a velocità in bit adattive consentono alle applicazioni di lettore video toodetermine le condizioni della rete e selezionare più velocità in bit. Quando si riducono le comunicazioni di rete, client hello possibile selezionare una velocità in bit inferiore possibile continuare la riproduzione con una qualità video inferiore. Come migliorare le condizioni della rete, il client di hello può passare tooa velocità in bit maggiore con miglioramento della qualità video. Servizi multimediali di Azure supporta hello seguenti tecnologie a velocità in bit adattiva: MPEG-DASH, Smooth Streaming e HTTP Live Streaming (HLS).

gli utenti tooprovide con URL di streaming, è innanzitutto necessario creare un localizzatore OnDemandOrigin. Creazione di hello offre localizzatore hello asset toohello percorso di base che include contenuto hello desiderato toostream. Tuttavia, toobe toostream in grado di questo contenuto, è necessario toomodify ulteriormente il percorso. tooconstruct un toohello URL completo il flusso di file manifesto, è necessario concatenare il percorso del localizzatore hello valore e hello manifesto (nomefile.ISM) nome del file. Aggiungere quindi **/manifesto** e percorso del localizzatore toohello un formato appropriato (se necessario).

> [!NOTE]
> Lo streaming dei contenuti può essere eseguito anche tramite una connessione SSL. toodo, assicurarsi che l'URL di streaming inizino con HTTPS. Si noti che attualmente AMS non supporta SSL con domini personalizzati.  
> 


È possibile trasmettere solo tramite SSL, se l'endpoint da cui si distribuisce il contenuto di streaming hello è stato creato dopo il 10 settembre 2014. Se gli URL di streaming sono basati su hello streaming creati dopo il 10 settembre 2014 hello URL contiene "streaming.mediaservices.windows.net". URL di streaming che contengono "origin.mediaservices.windows.net" (formato precedente hello) non supportano SSL. Se l'URL è nel formato precedente hello e si desidera toostream in grado di toobe su SSL, è possibile creare un nuovo endpoint di streaming. Usare gli URL basati su hello streaming nuovi endpoint toostream il contenuto tramite SSL.

## <a name="streaming-url-formats"></a>Formati degli URL di streaming URL:
### <a name="mpeg-dash-format"></a>Formato MPEG-DASH
{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Formato Apple HTTP Live Streaming (HLS) V4
{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Formato Apple HTTP Live Streaming (HLS) V3
{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>Formato Apple HTTP Live Streaming (HLS) con il filtro solo audio
Per impostazione predefinita, le tracce di solo audio presenti nel manifesto HLS hello. È necessario per la certificazione di Apple store per reti cellulari. In questo caso, se un client non dispone di larghezza di banda sufficiente o è connesso tramite una connessione 2G, la riproduzione passa solo tooaudio. In questo modo il contenuto di tookeep streaming senza memorizzarlo nel buffer, ma senza video. In alcuni scenari si potrebbe preferire il buffer del lettore di Windows solamente per l'audio. Se si desidera tenere traccia di solo audio hello tooremove, aggiungere **solo audio = false** toohello URL.

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)

Per altre informazioni, vedere l'articolo sul [supporto della composizione di Dynamic Manifest e sulle funzioni aggiuntive di HLS](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/).

### <a name="smooth-streaming-format"></a>Formato Smooth Streaming
{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest

Esempio:

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

### <a id="fmp4_v20"></a>Manifesto Smooth Streaming 2.0 (manifesto legacy)
Per impostazione predefinita, il formato del manifesto Smooth Streaming contiene tag hello di ripetizione (r-tag). Tuttavia, alcuni lettori non supportano hello r-tag. I client con i lettori possono usare un formato che disabilita hello r-tag:

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=fmp4-v20)

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>Download progressivo
È possibile avviare il download progressivo, riproduzione di file multimediali prima di aver scaricato l'intero file hello. Non è possibile eseguire il download progressivo di file .ism* (ismv, isma, ismt o ismc).

tooprogressively scaricare il contenuto, utilizzare hello OnDemandOrigin tipo di localizzatore. Hello riportato di seguito hello URL basato su hello OnDemandOrigin tipo di localizzatore:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

È necessario decrittografare qualsiasi asset crittografato di archiviazione che si desidera toostream dal servizio di origine hello per il download progressivo.

## <a name="download"></a>Scaricare
toodownload tooa contenuto dispositivo client, è necessario creare un localizzatore SAS. Hello che consenta per accedere al contenitore di archiviazione di Azure toohello in cui si trova il file. URL di download hello toobuild, si dispone di nome di file hello tooembed tra host hello e la firma.

Hello riportato di seguito hello URL basato sul localizzatore SAS hello:

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

si applica Hello seguenti considerazioni:

* È necessario decrittografare qualsiasi asset crittografato di archiviazione che si desidera toostream dal servizio di origine hello per il download progressivo.
* Un download ha esito negativo se non viene completato entro 12 ore.

## <a name="streaming-endpoints"></a>Endpoint di streaming

Un endpoint di streaming rappresenta un servizio di streaming in grado di fornire contenuto direttamente tooa client player applicazione o tooa contenuto rete (CDN per) ulteriore distribuzione. flusso in uscita di Hello da un servizio di endpoint di streaming può essere un flusso in tempo reale o un asset video on Demand nell'account di servizi multimediali. Sono disponibili due tipi di endpoint di streaming, **Standard** e **Premium**. Per altre informazioni, vedere [Streaming endpoints overview](media-services-streaming-endpoints-overview.md) (Panoramica degli endpoint di streaming).

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 

## <a name="known-issues"></a>Problemi noti
### <a name="changes-toosmooth-streaming-manifest-version"></a>Versione del manifesto Streaming tooSmooth modifiche
Prima versione del servizio di luglio 2016 - quando il manifesto generato da Media Encoder Standard, flusso di lavoro Premium del codificatore multimediale o hello Azure Media Encoder precedenti sono stati trasmessi tramite la creazione dinamica dei pacchetti: hello Smooth Streaming asset hello restituito risulterebbero conformi tooversion 2.0. Nella versione 2.0, durate frammento hello non utilizzano tag di hello cosiddetti ripetizione ("r"). ad esempio:

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

Nella versione di luglio 2016 servizio hello, manifesto Smooth Streaming hello generato è conforme tooversion 2.2, con la relativa durata frammento con il tag di ripetizione. ad esempio:

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

Alcuni dei client Smooth Streaming legacy hello potrebbe non supportare i tag di ripetizione hello e manifesto hello tooload non riuscirà. toomitigate questo problema, è possibile utilizzare il parametro di formato di manifesto legacy hello **(formato = fmp4-v20)** o aggiornare la versione più recente di toohello client, che supporta i tag di ripetizione. Per altre informazioni, vedere [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Argomenti correlati
[Aggiornamento di Servizi multimediali dopo il rollover delle chiavi di accesso alle risorse di archiviazione](media-services-roll-storage-access-keys.md)

