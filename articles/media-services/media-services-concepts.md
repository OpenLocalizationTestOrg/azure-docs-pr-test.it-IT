---
title: concetti relativi a servizi multimediali aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 0a45deff32336dfcf778552f720c1ea21927951b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-concepts"></a>Concetti relativi ai Servizi multimediali di Azure
In questo argomento fornisce una panoramica dei concetti di servizi multimediali più importanti hello.

## <a id="assets"></a>Asset e archiviazione
### <a name="assets"></a>Asset
Un [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) contiene file digitali (tra cui video, audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli) e i metadati relativi a questi file hello. Una volta caricati i file digitali hello in un asset, potrebbero essere utilizzati in servizi multimediali di hello di codifica e trasmissione di flussi di lavoro.

Un asset è mappato tooa contenitore di blob nell'account di archiviazione di Azure hello e file hello in asset hello vengono archiviati come BLOB in blocchi nel contenitore. I BLOB di pagine non sono supportati da Servizi multimediali di Azure.

Quando si decide quali tooupload contenuto multimediale e l'archivio in un asset, applica hello seguenti considerazioni:

* Un asset deve contenere una sola istanza univoca di contenuto multimediale, ad esempio una singola modifica di un episodio televisivo, di un film o di un annuncio pubblicitario.
* Un asset non deve contenere più rendering o modifiche di un file audiovisivo. Un esempio di uso non corretto di un cespite tentano toostore più episodi Televisivi, annunci pubblicitari o angolazioni di una singola produzione all'interno di un asset. L'archiviazione di più rendering o modifiche di un file audiovisivo in un asset può comportare difficoltà durante l'invio di processi di codifica, streaming e recapito hello del cespite hello in un secondo momento nel flusso di lavoro hello di protezione.  

### <a name="asset-file"></a>File di asset
Un'entità [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) rappresenta un file video o audio effettivo archiviato in un contenitore BLOB. Un file di asset è sempre associato a un asset e un asset può contenere uno o più file. attività di Media Services Encoder Hello non riesce se un oggetto di file di asset non è associato a un file digitale in un contenitore blob.

Hello **AssetFile** istanza e hello effettivo file multimediale sono due oggetti distinti. istanza di AssetFile Hello contiene i metadati relativi a file di supporto hello, mentre i file di supporto hello contiene hello effettivo contenuto multimediale.

Non è consigliabile tentare contenuto hello toochange dei contenitori di blob che sono stati generati da servizi multimediali senza usare le API di servizi multimediali.

### <a name="asset-encryption-options"></a>Opzioni di crittografia di asset
In base al tipo di contenuto di hello desiderate tooupload, archivio e recapito, servizi multimediali offre varie opzioni di crittografia che è possibile scegliere.

>[!NOTE]
>Non viene usata alcuna crittografia. Questo è il valore di predefinito hello. Quando si usa questa opzione il contenuto non è protetto durante il transito, né nell'archiviazione locale.

Se si prevede di toodeliver un file MP4 tramite download progressivo, usare il contenuto tooupload questa opzione.

**StorageEncrypted** : utilizzare questa opzione tooencrypt il contenuto non crittografato in locale utilizzando la crittografia AES a 256 bit e quindi caricarla tooAzure archiviazione dove viene archiviato in forma crittografata. Gli asset protetti con crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file crittografato sistema precedente tooencoding e, facoltativamente, crittografare nuovamente toouploading precedente come nuovo asset di output. Hello primario per la crittografia di archiviazione viene usata quando si desidera toosecure file multimediali di input di alta qualità applicando una crittografia avanzata rest su disco. 

In ordine toodeliver asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset hello in modo da servizi multimediali come toodeliver il contenuto. Prima che l'asset può essere trasmesso, hello streaming flussi e crittografia di archiviazione hello viene rimosso il server dei contenuti usando hello specificato criterio di recapito (ad esempio, AES, PlayReady o Nessuna crittografia). 

**CommonEncryptionProtected** -utilizzare questa opzione se si desidera tooencrypt (o caricamento già crittografato) contenuto con la crittografia comune o PlayReady DRM (ad esempio, Smooth Streaming protetto con PlayReady DRM).

**EnvelopeEncryptionProtected** : utilizzare questa opzione se si desidera tooprotect (o caricamento già protetto) HTTP Live Streaming (HLS) crittografato con Advanced Encryption Standard (AES). Se si sta caricando contenuto HLS già crittografato con AES, la crittografia deve essere stata eseguita con Transform Manager.

### <a name="access-policy"></a>Criterio di accesso
Un [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy) definisce le autorizzazioni (ad esempio lettura, scrittura ed elenco) e la durata dell'asset tooan di accesso. In genere, è necessario passare un localizzatore di tooa oggetto AccessPolicy che sarebbe quindi file hello tooaccess utilizzati contenuti in un asset.

>[!NOTE]
>È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy). È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri). Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.

### <a name="blob-container"></a>Contenitore BLOB
Un contenitore BLOB consente di raggruppare un insieme di BLOB. I contenitori BLOB vengono usati in Servizi multimediali come delimitazione per il controllo di accesso e per i localizzatori di firma di accesso condiviso negli asset. Un account di archiviazione di Azure può includere un numero illimitato di contenitori BLOB, In un contenitore può essere archiviato un numero illimitato di BLOB.

>[!NOTE]
> Non è consigliabile tentare contenuto hello toochange dei contenitori di blob che sono stati generati da servizi multimediali senza usare le API di servizi multimediali.
> 
> 

### <a id="locators"></a>Localizzatori
[Localizzatore](https://docs.microsoft.com/rest/api/media/operations/locator)forniscono un hello tooaccess punto di ingresso file contenuti in un asset. Un criterio di accesso è usato toodefine hello autorizzazioni e la durata che un client ha accesso tooa asset specificato. I localizzatori possono avere una relazione tooone con un criterio di accesso, ad esempio che localizzatori diversi possono offrire tempi di inizio diversa e i client toodifferent tipi di connessione utilizzando tutti hello stessa autorizzazione e le impostazioni di durata. a causa di una restrizione di criteri di accesso condiviso impostata dai servizi di archiviazione di Azure, tuttavia, non è più di cinque localizzatori univoci associati a un determinato asset contemporaneamente. 

Servizi multimediali sono supportati due tipi di localizzatori: localizzatori OnDemandOrigin, utilizzato toostream media (ad esempio, MPEG DASH, HLS o Smooth Streaming) o il download progressivo supporti e localizzatori URL di firma di accesso condiviso usati tooupload o to\from i file di download supporti di archiviazione di Azure. 

>[!NOTE]
>autorizzazione di elenco Hello (AccessPermissions.List) da utilizzare non quando si crea un localizzatore OnDemandOrigin. 

### <a name="storage-account"></a>Account di archiviazione
Tutti tooAzure accesso archiviazione viene eseguita tramite un account di archiviazione. Un account di Servizi multimediali può essere associato a uno o più account di archiviazione. Un account può contenere un numero illimitato di contenitori, purché la dimensione totale di questi sia inferiore a 500TB per ogni account di archiviazione.  Servizi multimediali fornisce il livello SDK tooling tooallow si toomanage più account di archiviazione e di carico bilanciare la distribuzione di hello degli asset durante il caricamento toothese account in base alle metriche o distribuzione casuale. Per altre informazioni, vedere Uso di [Archiviazione di Azure](https://msdn.microsoft.com/library/azure/dn767951.aspx). 

## <a name="jobs-and-tasks"></a>Processi e attività
Oggetto [processo](https://https://docs.microsoft.com/rest/api/media/operations/job) viene in genere utilizzate tooprocess (ad esempio, indice o codificare) una presentazione audio/video. Se si stanno elaborando più video, creare un processo per ogni toobe video codificato.

Un processo contiene i metadati relativi a elaborazione hello toobe eseguita. Ogni processo contiene una o più entità [task](https://docs.microsoft.com/rest/api/media/operations/task)che specificano un'attività di elaborazione atomica, i relativi asset di input e output, un processore di contenuti multimediali e le impostazioni associate. Attività all'interno di un processo possono essere concatenate insieme, dove hello asset di output di un'attività è specificato come hello attività successiva toohello di asset di input. In questo modo un processo può contenere tutta l'elaborazione di hello necessaria per una presentazione multimediale.

## <a id="encoding"></a>Codifica
Servizi multimediali di Azure fornisce più opzioni per la codifica dei file multimediali in cloud hello hello.

Quando si avvia con servizi multimediali, è importante toounderstand differenza di hello tra codec e formati di file.
Codec sono costituiti da software hello che implementa gli algoritmi di compressione/decompressione hello, mentre i formati di file sono contenitori che includono il video compresso hello.

Servizi multimediali fornisce creazione dinamica dei pacchetti che consente la velocità in bit adattiva MP4 o Smooth Streaming con codifica contenuto in streaming formati supportati da servizi multimediali (MPEG DASH, HLS, Smooth Streaming) toodeliver senza che sia necessario toore-package in questi formati di streaming.

sfruttare tootake [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md), è necessario tooencode il file mezzanine (origine) in un set di file MP4 o file Smooth Streaming a velocità in bit adattiva e si dispone di almeno un endpoint di streaming di standard o premium in stato avviato.

Servizi multimediali supporta hello seguenti codificatori su richiesta che sono descritte in questo articolo:

* [Codificatore multimediale standard](media-services-encode-asset.md#media-encoder-standard)
* [Flusso di lavoro Premium del codificatore multimediale](media-services-encode-asset.md#media-encoder-premium-workflow)

Per informazioni sui codificatori supportati, vedere [Codificatori](media-services-encode-asset.md).

## <a name="live-streaming"></a>Streaming live
In Servizi multimediali di Azure un canale rappresenta una pipeline per l'elaborazione di contenuto in streaming live. Un canale riceve i flussi di input live in uno dei due modi seguenti:

* Un codificatore live locale invia più velocità in bit RTMP o Smooth Streaming (MP4 frammentato) toohello canale. È possibile utilizzare i seguenti codificatori live Smooth Streaming con più velocità in bit di output di hello: MediaExcel, Ateme, le comunicazioni immaginare, Envivio, Cisco ed elementare. Hello codificatori live seguenti generano output in RTMP: Adobe Flash Live Encoder, Telestream Wirecast, Teradek, Haivision e Tricaster codificatori. Hello flussi inseriti passano attraverso i canali senza altre transcodifica e codifica. Quando richiesto, servizi multimediali offre toocustomers flusso hello.
* Un flusso a velocità in bit singola (in uno dei seguenti formati hello: RTP (MPEG-TS)), RTMP o Smooth Streaming (MP4 frammentato)) viene inviato toohello canale che viene attivato tooperform in tempo reale di codifica con servizi multimediali. Hello canale esegue quindi la codifica live di hello in arrivo velocità in bit singola flusso tooa più velocità in bit (adattivo) flusso video. Quando richiesto, servizi multimediali offre toocustomers flusso hello.

### <a name="channel"></a>Canale
In Servizi multimediali le entità [Channel](https://docs.microsoft.com/rest/api/media/operations/channel)sono responsabili dell'elaborazione dei contenuti in streaming live. Un canale, fornisce un endpoint di input (URL di inserimento) che è quindi fornire transcodificatore live tooa. canale Hello riceve flussi di input live dal transcodificatore live hello e rende disponibili per lo streaming tramite uno o più entità Streamingendpoint. I canali forniscono inoltre un endpoint di anteprima (URL di anteprima) di utilizzare toopreview e convalidare il flusso prima di elaborarlo ulteriormente e di recapito.

È possibile ottenere hello inserimento URL e l'URL di anteprima di hello quando si crea il canale hello. tooget questi URL, il canale di hello non avere toobe nello stato avviato hello. Quando si è pronti toostart push dei dati da un transcodificatore live nel canale hello, canale hello deve essere avviati. Una volta transcodificatore live hello inizia l'inserimento di dati, è possibile visualizzare in anteprima il flusso.

Ogni account di Servizi multimediali può contenere più entità Channel, Program e StreamingEndpoint. A seconda delle esigenze di larghezza di banda e sicurezza hello, servizi StreamingEndpoint possono essere dedicato tooone o altri canali. Qualsiasi StreamingEndpoint può effettuare il pull da qualsiasi canale.

### <a name="program-event"></a>Programma (evento)
Oggetto [programma (evento)](https://docs.microsoft.com/rest/api/media/operations/program) consente toocontrol hello pubblicazione e l'archiviazione di segmenti in un flusso in tempo reale. I programmi (eventi) sono gestiti dai canali. Hello relazione canale e il programma è simile tootraditional media, in cui un canale è un flusso costante di contenuto e l'evento con ambito toosome timeout su tale canale è un programma.
È possibile specificare hello numero di ore che si vuole tooretain hello registrato contenuto per il programma hello, impostazione hello **ArchiveWindowLength** proprietà. Questo valore può essere impostato da un minimo di 25 ore massimo tooa 5 minuti.

ArchiveWindowLength determina anche l'intervallo di tempo i client possono cercare indietro nel tempo dalla posizione live corrente hello massimo hello. I programmi eseguibili sul periodo di tempo specificato hello, ma il contenuto che non è sincronizzato con la lunghezza della finestra hello viene scartato in modo continuo. Questo valore di questa proprietà determina anche per quanto tempo hello client possono raggiungere i manifesti.

Ogni programma (evento) è associato a un asset. il programma di hello toopublish è necessario creare un localizzatore per hello associati asset. Con questo localizzatore sarà si toobuild un URL di streaming che è possibile fornire tooyour client.

Un canale supporta fino toothree programmi in esecuzione contemporaneamente in modo è possibile creare più archivi di hello stesso flusso in ingresso. In questo modo toopublish e archiviare parti diverse di un evento in base alle esigenze. Ad esempio, il requisito di business è tooarchive 6 ore di un programma, ma toobroadcast solo ultimi 10 minuti. tooaccomplish, è necessario toocreate due programmi in esecuzione simultanea. Un programma è impostato tooarchive 6 ore dell'evento hello ma hello non viene pubblicato. Hello altro programma è tooarchive insieme per 10 minuti e questo programma viene pubblicato.

Per altre informazioni, vedere:

* [Utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md)
* [Uso di canali che ricevono il flusso live a più velocità in bit da codificatori locali](media-services-live-streaming-with-onprem-encoders.md)
* [Quote e limitazioni](media-services-quotas-and-limitations.md).

## <a name="protecting-content"></a>Protezione del contenuto
### <a name="dynamic-encryption"></a>Crittografia dinamica
Servizi multimediali di Azure consente di toosecure gli elementi multimediali dal tempo hello che lascia computer tramite l'archiviazione, elaborazione e il recapito. Servizi multimediali consente toodeliver il contenuto crittografato in modo dinamico con Advanced Encryption Standard (AES) (utilizzando le chiavi di crittografia a 128 bit) e la crittografia comune (CENC) utilizzando PlayReady e/o Widevine DRM. Servizi multimediali fornisce anche un servizio per la distribuzione client di tooauthorized di licenze PlayReady e chiavi AES.

Attualmente, è possibile crittografare hello seguenti formati di streaming: HLS, MPEG DASH e Smooth Streaming. Non è possibile crittografare i download progressivi.

Se si desidera per servizi multimediali tooencrypt un asset, è necessario tooassociate una chiave di crittografia (CommonEncryption o EnvelopeEncryption) con l'asset e inoltre configurare criteri di autorizzazione per la chiave di hello.

Se si desidera toostream asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset hello in ordine toospecify come si desidera toodeliver dell'asset.

Quando un flusso è richiesto da un lettore, servizi multimediali Usa hello specificato toodynamically chiave crittografare il contenuto utilizzando una crittografia envelope (con AES) o la crittografia comune (con PlayReady o Widevine). flusso di hello toodecrypt, hello lettore richiederà chiave hello dal servizio di distribuzione delle chiavi hello. Se è o meno utente hello toodecide autorizzato chiave hello tooget, servizio hello valuta i criteri di autorizzazione hello specificato per la chiave di hello.

### <a name="token-restriction"></a>Restrizione Token
Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: aprire, token o restrizioni IP. criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza). Servizi multimediali supporta i token in formato JSON Web Token (JWT) e i token SWT (Simple Web token) hello. Servizi multimediali non fornisce servizi token di sicurezza. È possibile creare un servizio token di sicurezza personalizzato o utilizzare i token tooissue ACS di Microsoft Azure. Hello servizio token di sicurezza deve essere configurato toocreate un token firmato con hello specificato chiave e rilasciare le attestazioni specificate nella configurazione della restrizione token hello. attestazioni di servizi multimediali Hello servizio di distribuzione chiavi restituirà hello richiesto hello e chiave (o licenza) client toohello se hello token è valido in hello token corrispondono a quelle configurate per la chiave di hello (o licenza).

Quando si configurano i criteri con restrizione token hello, è necessario specificare la chiave di verifica primaria hello, autorità di certificazione e i parametri di destinatari. chiave di verifica primaria Hello contiene hello chiave che hello token è stato firmato con, autorità emittente è hello servizio token di sicurezza che rilascia token hello. destinatari Hello (talvolta denominato ambito) descrive finalità hello del token hello o hello risorse hello token autorizza l'accesso. Hello servizio di distribuzione delle chiavi di servizi multimediali verifica che i valori nel token hello corrispondano valori hello hello modello.

Per ulteriori informazioni, vedere hello seguenti articoli:

[Informazioni generali sulla protezione dei contenuti](media-services-content-protection-overview.md)
[Proteggere contenuti con AES-128](media-services-protect-with-aes128.md)
[Proteggere contenuti con DRM](media-services-protect-with-drm.md)

## <a name="delivering"></a>Recapito
### <a id="dynamic_packaging"></a>Creazione dinamica dei pacchetti
Quando si lavora con servizi multimediali, è consigliabile tooencode i file in formato intermedio in un file MP4 a velocità in bit adattiva, impostare e quindi convertono hello imposta toohello formato desiderato utilizzando hello [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md).

### <a name="streaming-endpoint"></a>endpoint di streaming
Un'entità StreamingEndpoint rappresenta un servizio di streaming in grado di fornire contenuto direttamente applicazione di lettore client tooa o tooa rete di contenuti (CDN) per ulteriore distribuzione (servizi multimediali di Azure offre ora il servizio di integrazione di hello rete CDN di Azure.) hello flusso in uscita da un servizio di endpoint di streaming può essere un flusso live, o una risorsa video su richiesta nell'account di servizi multimediali. Scegliere i clienti di servizi multimediali un **Standard** streaming endpoint oppure uno o più **Premium** gli endpoint, in base alle esigenze tootheir di streaming. L'endpoint di streaming Standard è adatto per la maggior parte dei carichi di lavoro di streaming. 

L'endpoint di streaming Standard è adatto per la maggior parte dei carichi di lavoro di streaming. Endpoint standard di Streaming offrono hello flessibilità toodeliver toovirtually il contenuto ogni dispositivo tramite creazione dinamica dei pacchetti in HLS e MPEG-DASH, Smooth Streaming, nonché la crittografia dinamica per Microsoft PlayReady, Google Widevine, Fairplay Apple e AES128.  Anche una scalabilità da vasto toovery molto piccoli con migliaia di visualizzatori simultanei attraverso l'integrazione della rete CDN di Azure. Se si dispone di un carico di lavoro avanzato o i requisiti di capacità di streaming non rientrano toostandard destinazioni di velocità effettiva di endpoint di streaming o si desidera toocontrol hello capacità deve hello StreamingEndpoint servizio toohandle aumento della larghezza di banda, è consigliabile unità di scala tooallocate (noto anche come premium unità di streaming).

È consigliabile toouse creazione dinamica dei pacchetti e/o la crittografia dinamica.

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 

Per altre informazioni, vedere [questo](media-services-portal-manage-streaming-endpoints.md) argomento.

Per impostazione predefinita è possibile avere fino a endpoint di streaming too2 nell'account di servizi multimediali. toorequest un limite superiore, vedere [quote e limitazioni](media-services-quotas-and-limitations.md).

Il costo verrà addebitato solo quando StreamingEndpoint è in stato di esecuzione.

### <a name="asset-delivery-policy"></a>Criteri di distribuzione degli asset
Uno dei hello passaggi in servizi multimediali di flusso di lavoro di distribuzione del contenuto è la configurazione di hello [i criteri di distribuzione per asset ](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy)che si desidera toobe trasmesso. criteri di distribuzione di asset Hello indicano a servizi multimediali la modalità desiderata per l'asset toobe recapitati: in quale protocollo di streaming deve l'asset essere dinamicamente incluso nel pacchetto (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), se si desidera toodynamically o meno crittografare l'asset e come (busta o la crittografia comune).

Se si dispone di un asset crittografato di archiviazione, prima dell'asset può essere trasmesso, hello streaming flussi e crittografia di archiviazione hello viene rimosso il server dei contenuti usando hello specifica criteri di distribuzione. Ad esempio, toodeliver l'asset crittografato con chiave di crittografia Advanced Encryption Standard (AES), set hello criteri tipo tooDynamicEnvelopeEncryption. crittografia di archiviazione tooremove e le risorse hello flusso hello chiara, impostare hello criteri tipo tooNoDynamicEncryption.

### <a name="progressive-download"></a>Download progressivo
Il download progressivo consente toostart riproduzione di file multimediali prima di aver scaricato l'intero file hello. È possibile scaricare in modo progressivo solo file MP4.

>[!NOTE]
>Se si desidera, è necessario decrittografare gli asset crittografati toobe disponibili per il download progressivo.

gli utenti tooprovide con progressivo URL di download, è necessario prima creare un localizzatore OnDemandOrigin. Creazione localizzatore hello, offre hello base asset toohello di percorso. È quindi necessario nome hello tooappend di file MP4. ad esempio:

http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>URL di streaming
Tooclients il contenuto di flusso. gli utenti tooprovide con URL di streaming, è innanzitutto necessario creare un localizzatore OnDemandOrigin. Creazione localizzatore hello, offre hello base asset toohello percorso che contiene il contenuto di hello da toostream. Tuttavia, toobe toostream in grado di questo contenuto è necessario toomodify ulteriormente il percorso. tooconstruct un toohello URL completo il flusso di file manifesto, è necessario concatenare il percorso del localizzatore hello valore e hello manifesto (nomefile.ISM) nome del file. Aggiungere quindi /Manifest e percorso del localizzatore toohello un formato appropriato (se necessario).

Lo streaming dei contenuti può essere eseguito anche tramite una connessione SSL. toodo, assicurarsi che l'URL di streaming inizino con HTTPS. Attualmente AMS non supporta SSL con domini personalizzati.  

>[!NOTE]
>È possibile trasmettere solo tramite SSL, se l'endpoint da cui si distribuisce il contenuto di streaming hello è stato creato dopo il 10 settembre 2014. Se gli URL di streaming sono basati su hello streaming creati dopo il 10 settembre, hello URL contiene "streaming.mediaservices.windows.net" (formato nuovo hello). URL di streaming che contengono "origin.mediaservices.windows.net" (formato precedente hello) non supportano SSL. Se l'URL è nel formato precedente hello e si desidera toostream in grado di toobe su SSL, è possibile creare un nuovo endpoint di streaming. Usare gli URL creati in base a hello streaming nuovi endpoint toostream il contenuto tramite SSL.

Hello seguente elenco descrive i vari formati di streaming e alcuni esempi:

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

