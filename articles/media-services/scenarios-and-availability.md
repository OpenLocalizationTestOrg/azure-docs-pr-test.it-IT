---
title: "Servizi multimediali di Azure aaaMicrosoft scenari e la disponibilità di funzionalità tra più Data Center | Documenti Microsoft"
description: "Questo argomento offre una panoramica degli scenari e della disponibilità delle funzionalità e dei servizi di Servizi multimediali di Microsoft Azure nei data center."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>Scenari e disponibilità delle funzionalità di Servizi multimediali nei data center

Microsoft Azure Media Services (AMS) consente il caricamento di toosecurely, archiviare, codificare e creare il pacchetto di contenuto video o audio per su richiesta e live streaming toovarious client di recapito (ad esempio, TV, PC e dispositivi mobili).

AMS opera in più data center in tutto il mondo hello. Questi data center sono raggruppati in aree toogeographic, offrendo maggiore flessibilità nella scelta where toobuild delle applicazioni. È possibile esaminare hello [elenco di aree e le relative posizioni](https://azure.microsoft.com/regions/). 

Questo argomento illustra scenari comuni per la distribuzione di contenuti [live](#live_scenarios) o [on demand](#vod_scenarios) Hello inoltre fornite informazioni dettagliate sulla disponibilità delle funzionalità di supporto e servizi nei data center.

## <a name="overview"></a>Panoramica

### <a name="prerequisites"></a>Prerequisiti

toostart tramite servizi multimediali di Azure, è necessario seguente hello:

* Un account Azure. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com).
* Un account di Servizi multimediali di Azure. Per altre informazioni, vedere [Creare un account](media-services-portal-create-account.md).
* endpoint da cui si desidera toostream contenuto di streaming Hello è toobe in hello **esecuzione** stato.

    Quando viene creato l'account di sistema AMS, un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. toostart streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, hello endpoint di streaming è toobe in hello **esecuzione** stato.

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a>Gli oggetti comunemente utilizzati durante lo sviluppo in hello modello AMS OData

Hello immagine seguente mostra alcuni degli oggetti hello più comunemente utilizzato quando si sviluppa in base a modello di Media Services OData hello.

Fare clic su tooview immagine hello le dimensioni massime.  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

È possibile visualizzare l'intero modello hello [qui](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a>Proteggere il contenuto nel servizio di archiviazione e recapito di flussi multimediali in hello deselezionare (non crittografata)

![Flusso di lavoro VoD](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. Caricare un file multimediale di alta qualità in un asset.

    È consigliabile asset tooapply archiviazione crittografia opzione tooyour in ordine tooprotect il contenuto durante il caricamento e mentre inattivi presenti nell'archivio.
2. Codificare tooa set di file MP4 a velocità in bit adattiva.

    È consigliabile tooapply archiviazione crittografia opzione toohello output asset in ordine tooprotect il contenuto inattivo.
3. Configurare i criteri di distribuzione degli asset (usati per la creazione dinamica dei pacchetti).

    Se l'asset è protetto con crittografia di archiviazione, è **necessario** configurare i criteri di distribuzione degli asset.
4. Pubblicare l'asset hello creando un localizzatore OnDemand.
5. Trasmettere in streaming i contenuti pubblicati.

Per informazioni sulla disponibilità in Data Center, vedere hello [disponibilità](#availability) sezione.

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>Proteggere i contenuti nella risorsa di archiviazione e distribuire dinamicamente i flussi multimediali crittografati

![Protezione con PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. Caricare un file multimediale di alta qualità in un asset. Applicare asset toohello opzione crittografia di archiviazione.
2. Codificare tooa set di file MP4 a velocità in bit adattiva. Applicare l'asset di output toohello opzione crittografia archiviazione.
3. Creare una chiave simmetrica di crittografia per hello bene toobe crittografati in modo dinamico durante la riproduzione.
4. Configurare i criteri di autorizzazione della chiave simmetrica.
5. Configurare i criteri di distribuzione degli asset (usati per la creazione dinamica dei pacchetti e la crittografia dinamica).
6. Pubblicare l'asset hello creando un localizzatore OnDemand.
7. Trasmettere in streaming i contenuti pubblicati.

Per informazioni sulla disponibilità in Data Center, vedere hello [disponibilità](#availability) sezione.

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a>Usare Media Analitica tooderive ricavare informazioni utili da video

Supporto Analitica è una raccolta di componenti di riconoscimento vocale e visione che rendono più semplice per aziende e organizzazioni tooderive ricavare informazioni utili dai propri file video. Per altre informazioni, vedere [Panoramica di Analisi Servizi multimediali di Azure](media-services-analytics-overview.md).

1. Caricare un file multimediale di alta qualità in un asset.
2. Elaborare i video con uno dei servizi di supporto Analitica hello descritti in hello [Panoramica supporto Analitica](media-services-analytics-overview.md) sezione.
3. I processori di contenuti multimediali di Analisi Servizi multimediali producono file MP4 o JSON. Se un processore di contenuti multimediali ha prodotto un file MP4, è possibile scaricare progressivamente file hello. Se un processore di contenuti multimediali ha prodotto un file JSON, è possibile scaricare file hello da hello archiviazione blob di Azure.

Per informazioni sulla disponibilità in Data Center, vedere hello [disponibilità](#availability) sezione.

## <a name="deliver-progressive-download"></a>Definizione del download progressivo

1. Caricare un file multimediale di alta qualità in un asset.
2. Codificare tooa singolo file MP4.
3. Pubblicare l'asset hello creando un localizzatore OnDemand o SAS.

    Se si utilizza il localizzatore di firma di accesso condiviso, è possibile che il contenuto di hello viene scaricato da hello archiviazione blob di Azure. In questo caso, non è necessario toohave streaming endpoint in stato avviato.
4. Eseguire il download progressivo.

## <a id="live_scenarios"></a>Distribuzione di eventi di streaming live 

1. Inserire contenuti live usando vari protocolli di streaming live (ad esempio, RTMP o Smooth Streaming).
2. Facoltativamente, codificare il flusso in flusso a bitrate adattivo.
3. Visualizzare in anteprima il flusso live.
4. distribuire il contenuto di hello tramite protocolli di streaming comuni (ad esempio, MPEG DASH, Smooth, HLS) direttamente ai clienti di tooyour o tooa rete di contenuti (CDN) per ulteriore distribuzione.

    -oppure-

    Record e l'archivio contenuto hello caricamento in ordine toobe streaming successive (video on Demand).

Quando si esegue lo streaming in tempo reale, è possibile scegliere uno dei seguenti hello instrada:

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Uso di canali che ricevono un flusso live a bitrate multipli da codificatori locali (pass-through)

Hello diagramma seguente mostra hello parti principali della piattaforma hello AMS coinvolti nel hello **pass-through** flusso di lavoro.

![Flusso di lavoro live](./media/scenarios-and-availability/media-services-live-streaming-current.png)

Per altre informazioni, vedere l'articolo relativo all' [uso di canali che ricevono il flusso live a velocità in bit multipla da codificatori locali](media-services-live-streaming-with-onprem-encoders.md).

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Utilizzo di canali che sono abilitati tooperform in tempo reale di codifica con servizi multimediali di Azure

Hello diagramma seguente viene illustrato hello principale parti della piattaforma AMS hello coinvolti in Streaming Live del flusso di lavoro in cui un canale è abilitato tooperform in tempo reale di codifica con servizi multimediali.

![Flusso di lavoro live](./media/scenarios-and-availability/media-services-live-streaming-new.png)

Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).

Per informazioni sulla disponibilità in Data Center, vedere hello [disponibilità](#availability) sezione.

## <a name="consuming-content"></a>Utilizzo di contenuto

Servizi multimediali di Azure fornisce gli strumenti hello necessario toocreate completi, applicazioni di lettore client dinamiche per la maggior parte delle piattaforme, tra cui: iOS, dispositivi, i dispositivi Android, Windows, Windows Phone, Xbox e Set-top caselle. Hello argomento fornisce collegamenti tooSDKs e Player Framework che è possibile utilizzare toodevelop proprie applicazioni client che utilizzano i flussi multimediali da servizi multimediali. Per altre informazioni, vedere [Sviluppo di applicazioni di lettore video](media-services-develop-video-players.md).

## <a name="enabling-azure-cdn"></a>Abilitazione della rete CDN di Azure

Servizi multimediali supporta l'integrazione con la rete CDN di Azure. Per informazioni su come tooenable rete CDN di Azure, vedere [come endpoint di Streaming tooManage in un Account di servizi multimediali](media-services-portal-manage-streaming-endpoints.md).

## <a id="scaling"></a>Ridimensionamento di un account di Servizi multimediali

I clienti di AMS possono ridimensionare gli endpoint di streaming, l'elaborazione di contenuti multimediali e lo spazio di archiviazione nei propri account AMS.

* I clienti di Servizi multimediali possono scegliere un endpoint di streaming **Standard** o **Premium**. Un endpoint di streaming **Standard** è adatto per la maggior parte dei carichi di lavoro di streaming. Include hello stesse caratteristiche disponibili come un **Premium** streaming automaticamente gli endpoint e scale di larghezza di banda in uscita. 

    Gli endpoint di streaming **Premium** sono ideali per i carichi di lavoro avanzati, in quanto offrono una capacità di larghezza di banda dedicata e scalabile. Per impostazione predefinita, i clienti con un endpoint di streaming **Premium** ottengono un'unità di streaming. è possibile scalare aggiungendo SUs Hello endpoint di streaming. Ogni SU fornisce applicazione toohello capacità di larghezza di banda aggiuntiva. Per ulteriori informazioni sulla scalabilità **Premium** gli endpoint di streaming, vedere hello [scalabilità gli endpoint di streaming](media-services-portal-scale-streaming-endpoints.md) argomento.

* Un account di servizi multimediali è associato a un tipo di unità riservate, che determina la velocità di hello con cui vengono elaborati i file multimediali l'elaborazione delle attività. È possibile scegliere tra segue hello i tipi di unità riservata: **S1**, **S2**, o **S3**. Ad esempio, hello stesso processo di codifica viene eseguito più velocemente quando si utilizza hello **S2** toohello di confronto del tipo di unità riservata **S1** tipo.

    Inoltre toospecifying hello riservati di tipo di unità, è possibile specificare l'account con tooprovision **unità riservate** (RUs). numero di Hello di provisioning RUs determina il numero di hello delle attività multimediali che possono essere elaborate contemporaneamente in un determinato account.

    >[!NOTE]
    >UR di lavoro per la parallelizzazione di tutta l'elaborazione di supporti di memorizzazione, tra cui l'indicizzazione di processi tramite Azure Media Indexer. Tuttavia, a differenza della codifica, l'indicizzazione di processi non viene elaborata più velocemente con unità riservate più veloci.

    Per altre informazioni, vedere l'argomento relativo al [ridimensionamento dell'elaborazione di contenuti multimediali](media-services-portal-scale-media-processing.md).
* È anche possibile ridimensionare l'account di servizi multimediali aggiungendo tooit gli account di archiviazione. Ogni account di archiviazione è limitato too500 TB. tooexpand lo spazio di archiviazione oltre i limiti di hello predefinite, è possibile scegliere tooattach più storage account tooa singolo account di servizi multimediali. Per altre informazioni, vedere l'argomento relativo alla [gestione degli account di archiviazione](meda-services-managing-multiple-storage-accounts.md).

##<a id="availability"></a>Disponibilità delle funzionalità di Servizi multimediali nei data center

Questa sezione offre informazioni dettagliate sulla disponibilità delle funzionalità di Servizi multimediali nei data center.

### <a name="ams-accounts"></a>Account AMS

#### <a name="availability"></a>Disponibilità

È possibile creare gli account di servizi multimediali in hello seguenti aree: Europa settentrionale, Europa occidentale, Stati Uniti occidentali, Stati Uniti orientali, Asia sudorientale, Asia orientale, Giappone orientale, Giappone orientale, Brasile meridionale, India occidentale, India meridionale e India centrale. 

### <a name="streaming-endpoints"></a>Endpoint di streaming 

I clienti di Servizi multimediali possono scegliere un endpoint di streaming **Standard** o **Premium**. Per ulteriori informazioni, vedere hello [scalabilità](#scaling) sezione.

#### <a name="availability"></a>Disponibilità

|Nome|Stato|Data center
|---|---|---|
|Standard|GA|Tutti|
|Premium|GA|Tutti|

### <a name="live-encoding"></a>Codifica live

#### <a name="availability"></a>Disponibilità

È disponibile in tutti i data center tranne Germania, Brasile meridionale, India occidentale, India meridionale e India centrale. 

### <a name="encoding-media-processors"></a>Processori di contenuti multimediali di codifica

AMS offre due codificatori su richiesta: **Media Encoder Standard** e **Flusso di lavoro Premium del codificatore multimediale**. Per altre informazioni, vedere [Panoramica e confronto dei codificatori multimediali su richiesta di Azure](media-services-encode-asset.md). 

#### <a name="availability"></a>Disponibilità

|Nome processore di contenuti multimediali|Stato|Data center
|---|---|---|
|Codificatore multimediale standard|GA|Tutti|
|Flusso di lavoro Premium del codificatore multimediale|GA|Tutti tranne Cina|

### <a name="analytics-media-processors"></a>Processori di contenuti multimediali di analisi

Supporto Analitica è una raccolta di componenti di riconoscimento vocale e visione che rende più semplice per aziende e organizzazioni tooderive ricavare informazioni utili dai propri file video. Per altre informazioni, vedere [Panoramica di Analisi Servizi multimediali di Azure](media-services-analytics-overview.md).

#### <a name="availability"></a>Disponibilità

|Nome processore di contenuti multimediali|Stato|Data center
|---|---|---|
|Rilevamento multimediale volti di Azure|Preview|Tutti|
|Azure Media Hyperlapse|Preview|Tutti|
|Azure Media Indexer|GA|Tutti|
|Rilevatore multimediale di movimento Azure|Preview|Tutti|
|Riconoscimento ottico dei caratteri multimediale di Azure|Preview|Tutti|
|Azure Media Redactor|Preview|Tutti|
|Azure Media Stabilizer|Preview|Tutti|
|Anteprime video multimediali di Azure|Preview|Tutti|
|Azure Media Indexer 2|Preview|Tutti tranne Cina e area Governo federale|

### <a name="protection"></a>Protezione

Servizi multimediali di Microsoft Azure consente di toosecure gli elementi multimediali dal tempo hello che lascia computer tramite l'archiviazione, elaborazione e il recapito. Per altre informazioni, vedere l'argomento relativo alla [protezione dei contenuti di AMS](media-services-content-protection-overview.md).

#### <a name="availability"></a>Disponibilità

|Crittografia|Stato|Data center|
|---|---|---| 
|Archiviazione|GA|Tutti|
|Chiavi AES-128|GA|Tutti|
|Fairplay|GA|Tutti|
|PlayReady|GA|Tutti|
|Widevine|GA|Tutti tranne Germania, Governo federale e Cina.

### <a name="reserved-units-rus"></a>Unità riservate

numero di Hello di unità riservate sottoposte a provisioning determina il numero di hello delle attività multimediali che possono essere elaborate contemporaneamente in un determinato account. 

Per ulteriori informazioni, vedere hello [scalabilità](#scaling) sezione.

#### <a name="availability"></a>Disponibilità

Sono disponibili in tutti i data center.

### <a name="reserved-unit-ru-type"></a>Tipo di unità riservata

Un account di servizi multimediali è associato a un tipo di unità riservate, che determina la velocità di hello con cui vengono elaborati i file multimediali l'elaborazione delle attività. È possibile scegliere tra segue hello i tipi di unità riservata: S1, S2 o S3.

Per ulteriori informazioni, vedere hello [scalabilità](#scaling) sezione.

#### <a name="availability"></a>Disponibilità

|Nome tipo di unità riservata|Stato|Data center
|---|---|---|
|S1|GA|Tutti|
|S2|GA|Tutti tranne Brasile meridionale e India occidentale|
|S3|GA|Tutti tranne India occidentale|

## <a name="next-steps"></a>Passaggi successivi

Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

