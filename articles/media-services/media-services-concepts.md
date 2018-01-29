---
title: Concetti relativi a Servizi multimediali di Azure | Microsoft Docs
description: Questo argomento fornisce una panoramica dei concetti relativi ai Servizi multimediali di Azure
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: dcefc8bc-e2ea-4b38-a643-9010f4436fb5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: juliako
ms.openlocfilehash: bb02aaf541d2d2f4b1206136847af2b46621501d
ms.sourcegitcommit: 234c397676d8d7ba3b5ab9fe4cb6724b60cb7d25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2017
---
# <a name="azure-media-services-concepts"></a>Concetti relativi ai Servizi multimediali di Azure
Questo argomento fornisce una panoramica dei concetti più importanti su Servizi multimediali.

## <a name="a-idassetsassets-and-storage"></a><a id="assets"/>Asset e archiviazione
### <a name="assets"></a>Asset
Un'entità [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) contiene file digitali, tra cui video, audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli codificati, con i relativi metadati. Una volta caricati in un asset, i file digitali possono essere usati nei flussi di lavoro di codifica e trasmissione di Servizi multimediali.

Un asset viene mappato a un contenitore BLOB nell'account di archiviazione di Azure e i file contenuti nell'asset vengono archiviati come BLOB in blocchi in tale contenitore. I BLOB di pagine non sono supportati da Servizi multimediali di Azure.

Per decidere quale contenuto multimediale caricare e archiviare in un asset, tenere presenti le seguenti considerazioni:

* Un asset deve contenere una sola istanza univoca di contenuto multimediale, ad esempio una singola modifica di un episodio televisivo, di un film o di un annuncio pubblicitario.
* Un asset non deve contenere più rendering o modifiche di un file audiovisivo. Il tentativo di archiviare più episodi televisivi, annunci pubblicitari o angolazioni di una singola produzione all'interno di un asset è un esempio di uso non corretto di un'entità Asset. L'archiviazione di più rendering o modifiche di un file audiovisivo in un asset può comportare difficoltà durante l'invio di processi di codifica, la trasmissione in flusso o la protezione della distribuzione dell'asset in una fase successiva del flusso di lavoro.  

### <a name="asset-file"></a>File di asset
Un'entità [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) rappresenta un file video o audio effettivo archiviato in un contenitore BLOB. Un file di asset è sempre associato a un asset e un asset può contenere uno o più file. Se un oggetto di file di asset non è associato a un file digitale in un contenitore BLOB, l'attività del codificatore di Servizi multimediali restituisce un errore.

L'istanza di **AssetFile** e il file multimediale effettivo sono due oggetti distinti. L'istanza di AssetFile contiene metadati relativi al file multimediale, mentre quest'ultimo contiene l'effettivo contenuto multimediale.

È sconsigliabile tentare di modificare i contenuti dei contenitori BLOB generati da Servizi multimediali senza usare le API di Servizi multimediali.

### <a name="asset-encryption-options"></a>Opzioni di crittografia di asset
A seconda del tipo di contenuto che si vuole caricare, archiviare e distribuire, in Servizi multimediali è possibile scegliere tra varie opzioni di crittografia.

>[!NOTE]
>Non viene usata alcuna crittografia. Si tratta del valore predefinito. Quando si usa questa opzione il contenuto non è protetto durante il transito, né nell'archiviazione locale.

Se si prevede di distribuire un file MP4 tramite download progressivo, usare questa opzione per caricare il contenuto.

**StorageEncrypted**: usare questa opzione per crittografare localmente il contenuto non crittografato applicando la crittografia AES a 256 bit e quindi caricarlo in Archiviazione di Azure, dove viene archiviato in forma crittografata. Gli asset protetti con la crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file system crittografato prima della codifica. Se necessario, inoltre, possono essere ricrittografati prima del successivo caricamento come nuovo asset di output. La crittografia di archiviazione viene usata principalmente per proteggere file multimediali di input di alta qualità archiviati su disco applicando una crittografia avanzata. 

Per poter trasmettere l'asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset in modo da informare Servizi multimediali della modalità di distribuzione del contenuto. Per potere permettere lo streaming dell'asset, il server di streaming rimuove la crittografia di archiviazione ed esegue lo streaming dei contenuti usando i criteri di recapito specificati (ad esempio, AES, PlayReady o nessuna crittografia). 

**CommonEncryptionProtected** : usare questa opzione se si vuole crittografare o caricare contenuto già crittografato e protetto con la crittografia comune o con DRM PlayReady, ad esempio Smooth Streaming protetto con DRM PlayReady.

**EnvelopeEncryptionProtected** : usare questa opzione se si vuole proteggere o caricare contenuto HLS (HTTP Live Streaming) già protetto, crittografato con AES. Se si sta caricando contenuto HLS già crittografato con AES, la crittografia deve essere stata eseguita con Transform Manager.

### <a name="access-policy"></a>Criterio di accesso
Un'entità [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy) definisce le autorizzazioni, ad esempio di lettura, scrittura ed elenco, nonché la durata dell'accesso a un asset. In genere, si passa un oggetto AccessPolicy a un localizzatore, che viene quindi usato per l'accesso ai file contenuti in un asset.

>[!NOTE]
>È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy). Usare lo stesso ID criterio se si usano sempre gli stessi giorni/autorizzazioni di accesso, come nel cado di criteri per i localizzatori che devono rimanere attivi per molto tempo (criteri di non caricamento). Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.

### <a name="blob-container"></a>Contenitore BLOB
Un contenitore BLOB consente di raggruppare un insieme di BLOB. I contenitori BLOB vengono usati in Servizi multimediali come delimitazione per il controllo di accesso e per i localizzatori di firma di accesso condiviso negli asset. Un account di archiviazione di Azure può includere un numero illimitato di contenitori BLOB, In un contenitore può essere archiviato un numero illimitato di BLOB.

>[!NOTE]
> È sconsigliabile tentare di modificare i contenuti dei contenitori BLOB generati da Servizi multimediali senza usare le API di Servizi multimediali.
> 
> 

### <a name="a-idlocatorslocators"></a><a id="locators"/>Localizzatori
I [localizzatori](https://docs.microsoft.com/rest/api/media/operations/locator) forniscono un punto di ingresso per accedere ai file contenuti in un asset. Per definire le autorizzazioni e il periodo di tempo durante il quale un client ha accesso a un determinato asset viene usato un criterio di accesso. I localizzatori possono disporre di una relazione uno-a-molti con un criterio di accesso. In tal modo, localizzatori diversi possono fornire date/ore di inizio e tipi di connessione diversi a client diversi usando tutti le stesse impostazioni per le autorizzazioni e la durata. Tuttavia, a causa di una restrizione sul criterio di accesso condiviso impostata dai servizi di archiviazione di Azure, a un determinato asset non possono essere associati più di cinque localizzatori univoci alla volta. 

Servizi multimediali supporta due tipi di localizzatori: localizzatori OnDemandOrigin usati per trasmettere in streaming file multimediali (ad esempio, MPEG DASH, HLS o Smooth Streaming) o scaricare progressivamente file multimediali e localizzatori URL di firma di accesso condiviso, usati per caricare o scaricare file multimediali a/da Archiviazione di Azure. 

>[!NOTE]
>L'autorizzazione di elenco (AccessPermissions.List) non deve essere usata durante la creazione di un localizzatore OnDemandOrigin. 

### <a name="storage-account"></a>Account di archiviazione
l'accesso ad Archiviazione di Azure viene eseguito esclusivamente tramite un account di archiviazione. Un account di Servizi multimediali può essere associato a uno o più account di archiviazione. Un account può contenere un numero illimitato di contenitori, purché la dimensione totale di questi sia inferiore a 500TB per ogni account di archiviazione.  In Servizi multimediali sono disponibili strumenti di SDK che consentono di gestire più account di archiviazione e di bilanciare il carico della distribuzione degli asset durante il caricamento negli account in base a metriche specifiche oppure secondo una distribuzione casuale. Per altre informazioni, vedere Uso di [Archiviazione di Azure](https://msdn.microsoft.com/library/azure/dn767951.aspx). 

## <a name="jobs-and-tasks"></a>Processi e attività
Un'entità [Job](https://docs.microsoft.com/rest/api/media/operations/job) viene in genere usata per elaborare (ad esempio, indicizzare o codificare) una presentazione audio/video. Se si stanno elaborando più video, è necessario creare un processo per ciascun video codificato.

Un processo contiene i metadati relativi all'elaborazione da eseguire. Ogni processo contiene una o più entità [task](https://docs.microsoft.com/rest/api/media/operations/task)che specificano un'attività di elaborazione atomica, i relativi asset di input e output, un processore di contenuti multimediali e le impostazioni associate. Le attività contenute in un processo possono essere concatenate, in modo che l'asset di output di un'attività sia indicato come asset di input dell'attività successiva. In questo modo un processo può contenere tutte le operazioni di elaborazione necessarie per una presentazione multimediale.

## <a id="encoding"></a>Codifica
Servizi multimediali di Azure offre diverse opzioni per la codifica di servizi multimediali nel cloud.

Quando si iniziano ad utilizzare i servizi multimediali, è importante comprendere la differenza tra codec e formati di file.
I codec sono costituiti da software che implementa gli algoritmi di compressione/decompressione, mentre i formati di file sono contenitori che includono il video compresso.

Servizi multimediali include la funzionalità per la creazione dinamica dei pacchetti, che consente di distribuire contenuto con codifica Smooth Streaming o MP4 a bitrate adattivo nei formati supportati da Servizi multimediali, ovvero MPEG-DASH, HLS, Smooth Streaming, senza dover ricreare i pacchetti in questi formati di streaming.

Per sfruttare i vantaggi della [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md), è necessario codificare il file mezzanine (di origine) in un set di file MP4 con bitrate adattivo o di file Smooth Streaming a bitrate adattivo e disporre di almeno un endpoint di streaming Standard o Premium con stato avviato.

Servizi multimediali supporta i seguenti codificatori su richiesta descritti in questo articolo:

* [Codificatore multimediale standard](media-services-encode-asset.md#media-encoder-standard)
* [Flusso di lavoro Premium del codificatore multimediale](media-services-encode-asset.md#media-encoder-premium-workflow)

Per informazioni sui codificatori supportati, vedere [Codificatori](media-services-encode-asset.md).

## <a name="live-streaming"></a>Streaming live
In Servizi multimediali di Azure un canale rappresenta una pipeline per l'elaborazione di contenuto in streaming live. Un canale riceve i flussi di input live in uno dei due modi seguenti:

* Un codificatore live locale invia al canale un flusso RTMP o Smooth Streaming (MP4 frammentato) a più velocità in bit. È possibile usare i codificatori live seguenti che generano output in formato Smooth Streaming a bitrate multipli: MediaExcel, Ateme, Imagine Communications, Envivio, Cisco ed Elemental. I codificatori live seguenti generano output in formato RTMP: Adobe Flash Live Encoder, Telestream Wirecast, Teradek, Haivision e codificatori Tricaster. I flussi inseriti attraversano i canali senza ulteriori operazioni di transcodifica e codifica. Quando richiesto, Servizi multimediali invia il flusso ai clienti.
* Un flusso a velocità in bit singola (in uno dei formati seguenti: RTP (MPEG-TS), RTMP o Smooth Streaming (MP4 frammentato)) viene inviato al canale abilitato per l'esecuzione della codifica live con Servizi multimediali. Il canale esegue quindi la codifica live del flusso in ingresso a velocità in bit singola in un flusso video a più velocità in bit (adattivo). Quando richiesto, Servizi multimediali invia il flusso ai clienti.

### <a name="channel"></a>Canale
In Servizi multimediali le entità [Channel](https://docs.microsoft.com/rest/api/media/operations/channel)sono responsabili dell'elaborazione dei contenuti in streaming live. Un'entità Channel, o canale, fornisce un endpoint di input (URL di inserimento) che può essere a sua volta fornito al transcodificatore live. Un'entità Channel riceve flussi di input live dal trascodificatore live e li rende disponibili per lo streaming mediante uno o più StreamingEndpoints. I canali forniscono anche un endpoint di anteprima(URL di anteprima) che consente di visualizzare in anteprima e convalidare il flusso prima dell'ulteriore elaborazione e del recapito.

È possibile ottenere l'URL di inserimento e l'URL di anteprima quando si crea il canale. Per ottenere questi URL, non è necessario che il canale sia nello stato avviato. Quando si è pronti per avviare l'inserimento di dati da un transcodificatore live nel canale, il canale deve essere avviato. Una volta che il transcodificatore live inizia a inserire i dati, è possibile visualizzare in anteprima il flusso.

Ogni account di Servizi multimediali può contenere più entità Channel, Program e StreamingEndpoint. In base alle esigenze di sicurezza e alla larghezza di banda, i servizi di StreamingEndpoint possono essere dedicati a uno o più canali. Qualsiasi StreamingEndpoint può effettuare il pull da qualsiasi canale.

### <a name="program-event"></a>Programma (evento)
Un [programma (evento)](https://docs.microsoft.com/rest/api/media/operations/program) consente di controllare la pubblicazione e l'archiviazione di segmenti in un flusso live. I programmi (eventi) sono gestiti dai canali. La relazione tra queste due entità è simile a quella che intercorre tra di essi nei media tradizionali, in cui un canale è costituito da un flusso costante di contenuti, mentre un programma ha come ambito una serie di eventi programmati sul canale.
È possibile specificare il numero di ore per cui si vuole mantenere il contenuto registrato per il programma impostando la proprietà **ArchiveWindowLength** . Il valore impostato può essere compreso tra 5 minuti e 25 ore.

La proprietà ArchiveWindowLength determina anche il limite di tempo per cui i client possono eseguire ricerche a ritroso nel tempo dalla posizione live corrente. I programmi possono essere eseguiti per la quantità di tempo specificata, ma il contenuto che va oltre la durata prevista viene scartato in modo continuo. Il valore della proprietà determina anche il tempo per cui i manifesti client possono crescere.

Ogni programma (evento) è associato a un asset. Per pubblicare il programma, è necessario creare un localizzatore per l'asset associato. Con questo localizzatore sarà possibile creare un URL di streaming da fornire ai client.

Un canale supporta fino a tre programmi in esecuzione simultanea, in modo da poter creare più archivi dello stesso flusso in ingresso. Questo consente di pubblicare e archiviare parti diverse di un evento a seconda delle necessità. Si consideri ad esempio uno scenario in cui un'azienda richiede l'archiviazione di 6 ore di un programma e la trasmissione solo degli ultimi 10 minuti. A tale scopo, è necessario creare due programmi in esecuzione contemporaneamente. Un programma è impostato per l'archiviazione di 6 ore dell'evento, ma non viene pubblicato. L'altro programma è impostato per l'archiviazione di 10 minuti e viene pubblicato.

Per altre informazioni, vedere:

* [Uso di canali abilitati per l'esecuzione della codifica live con Servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md)
* [Uso di canali che ricevono il flusso live a più velocità in bit da codificatori locali](media-services-live-streaming-with-onprem-encoders.md)
* [Quote e limitazioni](media-services-quotas-and-limitations.md).

## <a name="protecting-content"></a>Protezione del contenuto
### <a name="dynamic-encryption"></a>Crittografia dinamica
Servizi multimediali di Azure consente di proteggere i file multimediali dal momento in cui escono dal computer fino alle fasi di archiviazione, elaborazione e recapito. Servizi multimediali consente di distribuire contenuti crittografati dinamicamente con AES (Advanced Encryption Standard), mediante chiavi di crittografia a 128 bit, e con la crittografia comune (CENC), mediante PlayReady e/o Widevine DRM. Servizi multimediali fornisce inoltre un servizio per la distribuzione di chiavi AES e licenze PlayReady ai client autorizzati.

Attualmente è possibile crittografare i formati di streaming seguenti: HLS, MPEG DASH e Smooth Streaming. Non è possibile crittografare i download progressivi.

Per consentire a Servizi multimediali di crittografare un asset, è necessario associare una chiave di crittografia (CommonEncryption o EnvelopeEncryption) all'asset e configurare anche i criteri di autorizzazione per la chiave.

Se si vuole trasmettere l'asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset in modo da specificare la modalità di distribuzione dell'asset.

Quando un flusso viene richiesto da un lettore, Servizi multimediali usa la chiave specificata per crittografare dinamicamente i contenuti mediante la crittografia envelope (con AES) o la crittografia common (con PlayReady o Widevine). Per decrittografare il flusso, il lettore richiederà la chiave dal servizio di distribuzione delle chiavi. Per decidere se l'utente è autorizzato a ottenere la chiave, il servizio valuta i criteri di autorizzazione specificati.

### <a name="token-restriction"></a>Restrizione Token
I criteri di autorizzazione delle chiavi simmetriche possono avere una o più restrizioni di tipo Open, Token o IP. I criteri con restrizione Token devono essere accompagnati da un token rilasciato da un servizio STS (Secure Token Service, servizio token di sicurezza). Servizi multimediali supporta i token nei formati Simple Web Tokens (SWT) e JSON Web Token (JWT). Servizi multimediali non fornisce servizi token di sicurezza. Per il rilascio di token è possibile creare un servizio token di sicurezza personalizzato oppure usare il Servizio di controllo di accesso di Microsoft Azure. Il servizio token di sicurezza deve essere configurato in modo da creare un token firmato con la chiave specificata e rilasciare le attestazioni specificate nella configurazione della restrizione token. Il servizio di distribuzione di chiavi di Servizi multimediali restituirà al client la chiave o la licenza richiesta se il token è valido e le attestazioni del token corrispondono a quelle configurate per la chiave o la licenza.

Quando si configurano i criteri di restrizione Token, è necessario specificare i parametri primary verification key, issuer e audience. Il parametro primary verification key include la chiave usata per firmare il token. Il parametro issuer è il servizio token di sicurezza che emette il token. Il parametro audience (talvolta denominato scope) descrive l'ambito del token o la risorsa a cui il token autorizza l'accesso. Il servizio di distribuzione delle chiavi di Servizi multimediali verifica che i valori nel token corrispondano ai valori nel modello.

Per altre informazioni, vedere gli articoli seguenti:
- [Informazioni generali sulla protezione dei contenuti](media-services-content-protection-overview.md)
- [Protezione con AES-128](media-services-protect-with-aes128.md)
- [Protezione con PlayReady/Widevine](media-services-protect-with-playready-widevine.md)

## <a name="delivering"></a>Recapito
### <a name="a-iddynamicpackagingdynamic-packaging"></a><a id="dynamic_packaging"/>Creazione dinamica dei pacchetti
Quando si usa Servizi multimediali, è consigliabile codificare i file in formato intermedio con un set MP4 a bitrate adattivo e quindi convertire il set nel formato desiderato mediante la [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md).

### <a name="streaming-endpoint"></a>endpoint di streaming
Un'entità StreamingEndpoint rappresenta un servizio di streaming in grado di trasmettere contenuti direttamente a un lettore client o a una rete per la distribuzione di contenuti (CDN) per una successiva ridistribuzione (Servizi multimediali di Azure ora fornisce l'integrazione della rete CDN di Azure). Il flusso in uscita da un servizio endpoint di streaming può essere costituito da un flusso live o da una risorsa video on demand associata all'account di Servizi multimediali. I clienti di Servizi multimediali scelgono un endpoint di streaming **Standard** oppure uno o più endpoint di streaming **Premium**, in base alle esigenze. L'endpoint di streaming Standard è adatto per la maggior parte dei carichi di lavoro di streaming. 

L'endpoint di streaming Standard è adatto per la maggior parte dei carichi di lavoro di streaming. Gli endpoint di streaming Standard offrono la flessibilità necessaria per distribuire il contenuto praticamente a tutti i dispositivi grazie alla creazione dinamica dei pacchetti in HLS, MPEG-DASH e Smooth Streaming, nonché alla crittografia dinamica per Microsoft PlayReady, Google Widevine, Apple Fairplay e AES128.  Tali endpoint sono anche scalabili per destinatari di dimensioni diverse con migliaia di visualizzatori simultanei tramite l'integrazione della rete CDN di Azure. Se il carico di lavoro è avanzato o i requisiti della capacità di streaming non rispondono alle destinazioni con la velocità effettiva degli endpoint di streaming Standard o se si vuole controllare la capacità del servizio StreamingEndpoint per gestire esigenze di crescita in termini di larghezza di banda, è consigliabile allocare unità di scala (note anche come unità di streaming Premium).

È opportuno anche usare la creazione dinamica dei pacchetti e/o la crittografia dinamica.

>[!NOTE]
>Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**. Per avviare lo streaming del contenuto e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming da cui si vuole trasmettere il contenuto deve essere nello stato **In esecuzione**. 

Per altre informazioni, vedere [questo](media-services-portal-manage-streaming-endpoints.md) argomento.

Per impostazione predefinita, è possibile avere fino a due endpoint di streaming nell'account di Servizi multimediali. Per richiedere un limite più elevato, vedere [Quote e limitazioni](media-services-quotas-and-limitations.md).

Il costo verrà addebitato solo quando StreamingEndpoint è in stato di esecuzione.

### <a name="asset-delivery-policy"></a>Criteri di distribuzione degli asset
Uno dei passaggi del flusso di lavoro di distribuzione dei contenuti in Servizi multimediali consiste nella configurazione dei [criteri di distribuzione degli asset ](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy)che si desidera trasmettere in streaming. Questi criteri indicano a Servizi multimediali la modalità di distribuzione di un asset, ovvero il protocollo di streaming da usare per la creazione dinamica dei pacchetti (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), se l'asset deve essere crittografato dinamicamente e l'eventuale modalità di crittografia (envelope o common).

Nel caso di un asset crittografato di archiviazione, prima di trasmettere in streaming l'asset in base ai criteri specificati, il server rimuove la crittografia di archiviazione. Ad esempio, per distribuire l'asset crittografato con una chiave di crittografia AES, impostare il tipo di criteri su DynamicEnvelopeEncryption. Per rimuovere la crittografia di archiviazione e trasmettere l'asset in chiaro, impostare il tipo di criteri su NoDynamicEncryption.

### <a name="progressive-download"></a>Download progressivo
Il download progressivo è una tecnologia che consente di avviare la riproduzione di file multimediali prima che il download dell'intero file sia stato completato. È possibile scaricare in modo progressivo solo file MP4.

>[!NOTE]
>Se si vuole rendere disponibili le risorese crittografate per il download progressivo, sarà necessario decrittografarle.

Per fornire agli utenti gli URL di download progressivo, è necessario prima creare un localizzatore OnDemandOrigin. La creazione del localizzatore produce il valore Path di base dell'asset. È quindi necessario aggiungere il nome del file MP4. Ad esempio: 

http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>URL di streaming
Streaming dei contenuti ai client. Per poter fornire agli utenti URL di streaming, è prima necessario creare un localizzatore OnDemandOrigin. Creando il localizzatore è possibile ottenere il valore Path di base dell'asset che include i contenuti da trasmettere in streaming. Tuttavia, per trasmettere in streaming questi contenuti, è necessario modificare ulteriormente il percorso. Per creare un URL completo per il file manifesto di streaming, si deve concatenare il valore Path del localizzatore e il nome del file manifesto (nomefile.ism), quindi aggiungere /Manifest e un formato appropriato (se necessario) al percorso di origine del localizzatore.

Lo streaming dei contenuti può essere eseguito anche tramite una connessione SSL. A questo scopo, verificare che gli URL di streaming inizino con HTTPS. Attualmente AMS non supporta SSL con domini personalizzati.  

>[!NOTE]
>Lo streaming tramite SSL è possibile solo se l'endpoint di streaming da cui si inviano i contenuti è stato creato dopo il 10 settembre 2014. Se gli URL di streaming si basano sugli endpoint di streaming creati dopo il 10 settembre, l'URL contiene "streaming.mediaservices.windows.net" (nuovo formato). Gli URL di streaming contenenti "origin.mediaservices.windows.net" (vecchio formato) non supportano SSL. Se l'URL è nel vecchio formato e si desidera poter eseguire lo streaming tramite SSL, creare un nuovo endpoint di streaming. Usare gli URL creati con il nuovo endpoint di streaming per lo streaming dei contenuti tramite SSL.

Il seguente elenco include la descrizione dei vari formati di streaming e alcuni esempi:

* Smooth Streaming

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

* MPEG DASH

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

* Apple HTTP Live Streaming (HLS) V4

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

* Apple HTTP Live Streaming (HLS) V3

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

