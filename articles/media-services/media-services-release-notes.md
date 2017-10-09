---
title: note sulla versione di servizi aaaMedia | Documenti Microsoft
description: Note sulla versione di Servizi multimediali
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Note sulla versione di Servizi multimediali di Azure
Nelle presenti note sulla versione vengono riepilogati le modifiche rispetto alle versioni precedenti e i problemi noti.

> [!NOTE]
> È necessario toohear dai clienti e concentrarsi sulla risoluzione dei problemi che interessano è. tooreport un problema o porre domande, pubblicare un post nel hello [Forum MSDN di Azure Media Services].
> 
> 

## <a id="issues"></a>Problemi noti correnti
### <a id="general_issues"></a>Problemi generali di Servizi multimediali
| Problema | Descrizione |
| --- | --- |
| Numerose intestazioni HTTP comuni non sono incluse nei hello API REST. |Se si sviluppano applicazioni di servizi multimediali usando hello API REST, si stabilisce che alcuni campi di intestazione HTTP comuni (inclusi CLIENT-REQUEST-ID REQUEST-ID e RETURN-CLIENT-REQUEST-ID) non sono supportati. Hello intestazioni verranno aggiunte in un aggiornamento futuro. |
| La codifica percentuale non è consentita. |Servizi multimediali Usa valore hello hello IAssetFile.Name proprietà durante la creazione di URL per hello streaming del contenuto (ad esempio, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Per questo motivo, la codifica percentuale non è consentita. valore di hello Hello **nome** proprietà non può avere uno dei seguenti hello [% riservati per la codifica caratteri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Può essere presente solo un carattere '.' per l'estensione di file hello. |
| metodo ListBlobs che fa parte di Hello Azure Storage SDK versione di hello 3 ha esito negativo. |Servizi multimediali genera URL di firma di accesso condiviso in base alle hello [2012-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12) versione. Se si desidera BLOB di toolist toouse Azure Storage SDK in un contenitore blob, utilizzare hello [cloudblobcontainer. Listblobs](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx) metodo che fa parte di Azure Storage SDK versione 2. x. metodo ListBlobs che fa parte di Hello Azure Storage SDK versione di hello 3. x avranno esito negativo. |
| Meccanismo di limitazione di servizi multimediali limita l'utilizzo delle risorse di hello per le applicazioni che esegue un numero eccessivo di richieste al servizio toohello. servizio di Hello potrebbe restituire il codice di stato HTTP di servizio non disponibile (503) hello. |Per ulteriori informazioni, vedere la descrizione di hello del codice di stato HTTP 503 hello in hello [codici di errore di Azure Media Services](media-services-encoding-error-codes.md) argomento. |
| Quando una query sulle entità, è previsto un limite di 1000 entità restituito in una sola volta perché v2 REST pubblici limita risultati too1000 risultati della query. |È necessario toouse **Skip** e **richiedere** (.NET) / **top** (REST) come descritto in [in questo esempio .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) e [questa API REST esempio](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). |
| Alcuni client possono provenire tra un problema di ripetizione tag nel manifesto Smooth Streaming hello. |Per altre informazioni, vedere [questa](media-services-deliver-content-overview.md#known-issues) sezione. |
| Gli oggetti nel modulo .NET SDK di Servizi multimediali di Azure non possono essere serializzati e di conseguenza non funzionano con Caching di Azure. |Se si tenta di tooadd oggetto assetcollection del modulo SDK di tooserialize hello è tooAzure la memorizzazione nella cache, un'eccezione viene generata. |
| I processi di codifica hanno esito negativo e viene mostrata la stringa messaggio "Stage: DownloadFile. Code: System.NullReferenceException". |Hello codifica flusso di lavoro tipico è tooupload input file video tooan Asset di input, nonché inviare uno o più processi di codifica per tale input Asset, senza modificare altri Asset di input. Tuttavia, se si modifica hello input Asset (ad esempio mediante l'aggiunta, eliminazione o ridenominazione di file all'interno di hello Asset), quindi i processi successivi potrebbero non riuscire con un errore DownloadFile. soluzione alternativa Hello è toodelete hello Asset di input e caricare nuovamente input tooa file nuovo Asset. |

## <a id="rest_version_history"></a>Cronologia delle versioni dell'API REST
Per informazioni sulla cronologia delle versioni API REST di servizi multimediali di hello, vedere [riferimento all'API REST di Azure Media Services].

## <a name="june-2017-release"></a>Versione di giugno 2017

Servizi multimediali supporta ora l'[autenticazione basata su Azure Active Directory (Azure AD)](media-services-use-aad-auth-to-access-ams-api.md).

> [!IMPORTANT]
> Attualmente servizi multimediali supporta modello di autenticazione hello Azure Access Control service. L'autorizzazione di Controllo di accesso, tuttavia, verrà dichiarata deprecata il 1° giugno 2018. Si consiglia di migrare il modello di autenticazione di Azure AD toohello appena possibile.

## <a name="march-2017-release"></a>Versione di marzo 2017

È ora possibile usare Azure Media Standard troppo[genera automaticamente una scala di velocità in bit](media-services-autogen-bitrate-ladder-with-mes.md) specificando l'opzione "Il flusso adattivo" hello preimpostato stringa durante la creazione di un'attività di codifica. "Streaming adattivo" è hello consigliato predefinito se si desidera tooencode un video per lo streaming con servizi multimediali. Se è necessario toocustomize una codifica predefinita per lo scenario specifico, è possibile iniziare con [questi](media-services-mes-presets-overview.md) predefiniti.

È ora possibile usare Azure Media Standard o flusso di lavoro Premium del codificatore multimediale troppo[creare un'attività di codifica che genera l'errore blocchi fMP4](media-services-generate-fmp4-chunks.md). 


## <a name="febuary-2017-release"></a>Versione di febbraio 2017

A partire dal 1 aprile 2017, qualsiasi record di processo più vecchi di 90 giorni account vengono eliminate automaticamente, insieme ai relativi record di attività associato, anche se il numero di record hello sotto la quota massima di hello. Se sono necessarie informazioni di processi/attività hello tooarchive, è possibile utilizzare codice hello descritto [qui](media-services-dotnet-manage-entities.md).

## <a name="january-2017-release"></a>Versione di gennaio 2017

In Microsoft Azure Media Services (AMS), un **Endpoint di Streaming** rappresenta un servizio di streaming in grado di fornire contenuto direttamente applicazione di lettore client tooa o tooa rete di contenuti (CDN) per ulteriore distribuzione. Servizi multimediali fornisce inoltre un'integrazione completa della rete CDN di Azure. flusso in uscita di Hello da un servizio StreamingEndpoint può essere un flusso in tempo reale, un video su richiesta o il download progressivo dell'asset nell'account di servizi multimediali. Ogni account di Servizi multimediali di Azure include un servizio StreamingEndpoint predefinito. È possibile creare le entità Streamingendpoint ulteriori account hello. Esistono due versioni di servizi StreamingEndpoint, ovvero 1.0 e 2.0. A partire dal 10 gennaio 2017, ogni account di AMS appena creato includerà lo StreamingEndpoint **predefinito** della versione 2.0. Aggiungere account toothis endpoint di streaming aggiuntive saranno anche versione 2.0. Questa modifica non avrà impatto sulle account esistenti hello; le entità Streamingendpoint esistente sarà la versione 1.0 e può essere aggiornato tooversion 2.0. Tale modifica comporta cambiamenti nel comportamento, nella fatturazione e nelle funzionalità (per altre informazioni, vedere [questo](media-services-streaming-endpoints-overview.md) argomento).

Inoltre, a partire dalla versione di hello 2.15, servizi multimediali di Azure aggiunta hello seguenti entità Endpoint di Streaming di proprietà toohello: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Per una panoramica dettagliata di queste proprietà, vedere [questo articolo](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

## <a name="december-2016-release"></a>Versione di dicembre 2016

Servizi multimediali di Azure consente ora i dati di telemetria/metrica tooaccess per i propri servizi. versione corrente di Hello del sistema AMS consente di raccogliere dati di telemetria per il canale live, StreamingEndpoint, e in tempo reale le entità di archiviazione. Per altre informazioni, vedere [questo](media-services-telemetry-overview.md) argomento.

## <a id="july_changes16"></a>Versione di luglio 2016
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>Il file degli aggiornamenti toomanifest (*. ISM) generati dall'attività di codifica
Quando un'attività di codifica è inviato tooMedia codificatore Standard o Azure Media Encoder, attività di codifica hello genera un [file manifesto di streaming](media-services-deliver-content-overview.md) (*. ISM) file in hello Asset di output. Con l'ultima versione del servizio di hello, sintassi hello del file manifesto di streaming è stata aggiornata.

> [!NOTE]
> sintassi di Hello di hello streaming file manifesto (ISM) è riservata per uso interno e sia soggetto toochange nelle versioni future. Non modificare o modificare contenuto hello di questo file.
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>Un nuovo manifesto client (*. File ISMC) viene generato in hello Asset di output quando un'attività di codifica restituisce uno o più file MP4
A partire da hello ultima versione, dopo il completamento di un'attività di codifica che genera uno più file MP4, hello hello output che asset conterrà anche un file manifesto (*.ismc) client streaming. file ismc Hello consente di migliorare le prestazioni di hello di lo streaming dinamico. 

> [!NOTE]
> sintassi di Hello del file manifesto (ismc) di hello client è riservata per uso interno e sia soggetto toochange nelle versioni future. Non modificare o modificare contenuto hello di questo file.
> 
> 

Per altre informazioni, vedere [questo](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) blog.

### <a name="known-issues"></a>Problemi noti
Alcuni client possono provenire tra un problema di ripetizione tag nel manifesto Smooth Streaming hello. Per altre informazioni, vedere [questa](media-services-deliver-content-overview.md#known-issues) sezione.

## <a id="apr_changes16"></a>Versione di aprile 2016
### <a name="azure-media-analytics"></a>Analisi Servizi multimediali di Azure
Servizi multimediali di Azure presenta la funzionalità di Analisi Servizi multimediali di Azure per una straordinaria esperienza di video intelligence. Per altre informazioni, vedere [Panoramica di Analisi Servizi multimediali di Azure](media-services-analytics-overview.md).

### <a name="apple-fairplay-preview"></a>FairPlay di Apple (anteprima)
Ora si toodynamically crittografare l'HTTP Live Streaming (HLS) consente di contenuto con Apple FairPlay, servizi multimediali di Azure. È inoltre possibile utilizzare AMS licenza recapito servizio toodeliver FairPlay licenze tooclients. Per ulteriori informazioni, vedere [tooStream di servizi multimediali di Azure Usa il contenuto HLS protetto con Apple FairPlay ](media-services-protect-hls-with-fairplay.md).

## <a id="feb_changes16"></a>Versione di febbraio 2016
versione più recente di Hello di Azure Media Services SDK per .NET (3.5.3) contiene una correzione di bug Widevine correlata. è stato problema Hello: AssetDeliveryPolicy non può essere riutilizzato per più asset crittografato con Widevine. Come parte di questa correzione di bug di hello seguenti proprietà è stata aggiunta toohello SDK: **WidevineBaseLicenseAcquisitionUrl**.

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>Versione di gennaio 2016
Unità riservate di codifica rinominato tooreduce confusione con i nomi di codificatore.

Hello Basic, Standard e Premium unità riservate di codifica tooS1 rinominato, S2, e S3 riservare unità, rispettivamente.  I clienti che utilizzano unità riservate di codifica Basic oggi verranno visualizzato S1 come etichetta di hello nel portale di Azure (e nella fattura hello), mentre Standard e Premium verrà visualizzato rispettivamente a etichette hello S2 e S3. 

## <a id="dec_changes_15"></a>Versione di dicembre 2015

### <a name="azure-media-encoder-deprecation-announcement"></a>Avviso di dichiarazione obsolescenza per Azure Media Encoder

Azure Media Encoder verrà deprecata a partire da circa 12 mesi dalla versione di hello di Media Encoder Standard.

### <a name="azure-sdk-for-php"></a>Azure SDK per PHP
il team di Azure SDK Hello pubblicato una nuova versione di hello [Azure SDK per PHP](http://github.com/Azure/azure-sdk-for-php) pacchetto che contiene aggiornamenti e nuove funzionalità per servizi multimediali di Microsoft Azure. In particolare, hello Azure Media Services SDK per PHP ora supporta la versione più recente è hello [protezione del contenuto](media-services-content-protection-overview.md) funzionalità: crittografia dinamica AES con DRM (PlayReady e Widevine) con e senza alcuna restrizione Token. Supporta inoltre la scalabilità delle [unità di codifica](media-services-dotnet-encoding-units.md).

Per altre informazioni, vedere:

* Hello [Microsoft Azure Media Services SDK per PHP](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/) blog.
* esempio Hello [esempi di codice](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices) toohelp iniziare rapidamente:
  * **vodworkflow_aes.PHP**: si tratta di un file PHP che mostra come toouse crittografia dinamica AES-128 e il servizio di recapito di chiave. È basato su .NET: esempio hello illustrato in [questo](media-services-protect-with-aes128.md) articolo.
  * **vodworkflow_aes.PHP**: si tratta di un file PHP che mostra come toouse crittografia dinamica PlayReady e il servizio di recapito di licenza. È basato su .NET: esempio hello illustrato in [questo](media-services-protect-with-drm.md) articolo.
  * **scale_encoding_units.PHP**: si tratta di un file PHP che mostra come codifica tooscale prenotati unità.

## <a id="nov_changes_15"></a>Versione di novembre 2015
Servizi multimediali di Azure offre ora servizio di distribuzione di licenze Google Widevine nel cloud hello. Per ulteriori informazioni, vedere troppo[questo blog di annuncio](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/). Vedere anche [questa esercitazione](media-services-protect-with-drm.md) e il [repository GitHub](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm). 

Si noti che i servizi di distribuzione delle licenze Widevine forniti da Servizi multimediali di Azure sono in anteprima. Per altre informazioni, vedere [questo blog](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/).

## <a id="oct_changes_15"></a>Versione di ottobre 2015
Azure Media Services (AMS) è ora disponibile in seguito centri dati hello: Brasile meridionale, India occidentale, India meridionale e India centrale. È ora possibile usare il portale di Azure hello troppo[creare gli account del servizio di supporto](media-services-portal-create-account.md) ed eseguire diverse attività descritta [qui](https://azure.microsoft.com/documentation/services/media-services/). In questi data center la codifica live non è tuttavia abilitata. Inoltre, non sono disponibili tutti i tipi di unità riservate di codifica.

* Brasile meridionale:                                           sono disponibili solo unità riservate di codifica Standard e Basic
* India occidentale, India meridionale e India centrale:             sono disponibili solo unità riservate di codifica Basic

## <a id="september_changes_15"></a>Versione di settembre 2015
* AMS ora offerte hello possibilità tooprotect video on Demand (VOD) sia flussi in tempo reale con la tecnologia DRM modulare Widevine. È possibile utilizzare hello seguente toohelp partner servizi di recapito recapitare licenze Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Per altre informazioni, vedere [questo blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).
  
    È possibile utilizzare [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (a partire dalla versione di hello 3.5.1) o REST API tooconfigure il toouse AssetDeliveryConfiguration Widevine.  
* AMS ha aggiunto il supporto per i video Apple ProRes. È ora possibile caricare i file video di origine QuickTime che utilizzano Apple ProRes o altri codec. Per altre informazioni, vedere [questo blog](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/).
* È ora possibile usare Media Encoder Standard toodo Sub ritaglio e in tempo reale archivio l'estrazione. Per altre informazioni, vedere [questo blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).
* sono stata apportata Hello filtro gli aggiornamenti seguenti: 
  
  * È ora possibile utilizzare il formato Apple HTTP Live Streaming (HLS) con il filtro solo audio. Questo aggiornamento consente di tenere traccia di solo audio tooremove specificando (solo audio = false) nell'URL hello.
  * Quando si definiscono i filtri per le risorse, è ora toocombine possibilità consente di filtrare più (too3 up) in un singolo URL.
    
    Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.
* AMS supporta ora gli I-Frames in HLS v4. Il supporto I-Frame consente di ottimizzare le operazioni di avanzamento veloce e riavvolgimento. Per impostazione predefinita, tutti gli output v4 HLS includono le playlist I-Frame (EXT-X-I-FRAME-STREAM-INF).
  
    Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.

## <a id="august_changes_15"></a>Versione di agosto 2015
* La release Azure Media Services SDK per Java V0.8.0 e nuovi esempi sono ora disponibili. Per altre informazioni, vedere:
  
  * [Post di blog](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Repository di esempi Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* Aggiornamento di Azure Media Player con supporto per flussi multi-audio. Per altre informazioni, vedere:
  * [Post di blog](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>Versione di luglio 2015
* Per annunciare la disponibilità generale di hello di Media Encoder Standard. Per altre informazioni, vedere [questo post di blog](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/).
  
    Il codificatore multimediale standard usa i set di impostazioni descritti in [questa](http://go.microsoft.com/fwlink/?LinkId=618336) sezione. Si noti che quando si utilizza un set di impostazioni di codifica 4 KB, è necessario ottenere hello **Premium** tipo di unità riservate. Per ulteriori informazioni, vedere [come tooScale codifica](media-services-scale-media-processing-overview.md).
* Didascalie live in tempo reale con servizi multimediali e Player di Azure. Per altre informazioni, vedere [questo post di blog](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/)

### <a name="media-services-net-sdk-updates"></a>Aggiornamenti dell'SDK di Servizi multimediali per .NET
Azure Media Services .NET SDK è ora disponibile nella versione 3.4.0.0. in questa versione è stata aggiunta Hello seguenti funzionalità:  

* Implementazione del supporto per l'archivio live. Si noti che non è possibile scaricare un asset che contiene un archivio live.
* Implementazione del supporto per i filtri dinamici.
* Funzionalità implementata che consente a utenti tookeep archiviazione contenitore durante l'eliminazione di asset.
* Correzioni di bug relativi criteri tooretry nei canali.
* **Flusso di lavoro Premium del codificatore multimediale** abilitato.

## <a id="june_changes_15"></a>Versione di giugno 2015
### <a name="media-services-net-sdk-updates"></a>Aggiornamenti dell'SDK di Servizi multimediali per .NET
L'SDK di Servizi multimediali di Azure per .NET è ora disponibile nella versione 3.3.0.0. in questa versione è stata aggiunta Hello seguenti funzionalità:  

* supporto per la specifica di individuazione OpenId Connect
* supporto per la gestione del rollover delle chiavi sul lato del provider di identità. 

Se si utilizza un provider di identità che espone documento di individuazione OpenID Connect (come hello tale provider seguenti: Azure Active Directory, Google, Salesforce), è possibile indicare la firma delle chiavi per la convalida dei token JWT da tooobtain di servizi multimediali di Azure OpenID connect specifiche di individuazione. 

Per ulteriori informazioni, vedere [usando Json Web le chiavi da toowork specifica individuazione OpenID Connect con JWT token di autenticazione in servizi multimediali di Azure](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/).

## <a id="may_changes_15"></a>Versione di maggio 2015
Annuncio hello nuove funzionalità seguenti:

* [Anteprima della codifica live con Servizi multimediali](media-services-manage-live-encoder-enabled-channels.md)
* [Manifesto dinamico](media-services-dynamic-manifest-overview.md)
* [Anteprima del processore di contenuti multimediali Azure Media Hyperlapse](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>Versione di aprile 2015
### <a name="general-media-services-updates"></a>Aggiornamenti generali di Servizi multimediali
* [Annuncio di Azure Media Player](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/).
* A partire da 2.10 REST di servizi multimediali, i canali vengono configurati tooingest un protocollo RTMP, vengono creati con primario e secondario URL di inserimento. Per altre informazioni, vedere [Configurazioni di inserimento del canale](media-services-live-streaming-with-onprem-encoders.md#channel_input)
* Aggiornamenti di Azure Media Indexer
* Supporto per la lingua spagnola
* Nuovo formato xml di configurazione

Per altre informazioni, vedere [questo blog](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

### <a name="media-services-net-sdk-updates"></a>Aggiornamenti dell'SDK di Servizi multimediali per .NET
L'SDK di Servizi multimediali per .NET è ora disponibile nella versione 3.2.0.0.

di seguito Hello sono alcuni dei clienti hello aggiornamenti:

* **Modifica di rilievo**: modificato **TokenRestrictionTemplate.Issuer** e **TokenRestrictionTemplate.Audience** toobe di tipo stringa.
* Gli aggiornamenti correlati toocreating i criteri di tentativi personalizzati.
* Correzioni di bug e il download di toouploading i file relativi.
* Hello **MediaServicesCredentials** classe accetta ora tooauthenticate di endpoint di controllo di accesso primarie e secondarie rispetto.

## <a id="march_changes_15"></a>Versione di marzo 2015
### <a name="general-media-services-updates"></a>Aggiornamenti generali di Servizi multimediali
* Servizi multimediali offre ora l'integrazione con la rete CDN di Azure. toosupport hello integrazione, hello **CdnEnabled** proprietà è stata aggiunta troppo**StreamingEndpoint**.  **CdnEnabled** può essere usata con le API REST a partire dalla versione 2.9 (per altre informazioni, vedere [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)).  La proprietà **CdnEnabled** può essere inoltre usata con SDK .NET a partire dalla versione 3.1.0.2. Per altre informazioni, vedere [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx).
* Annuncio del **flusso di lavoro Premium del codificatore multimediale**. Per altre informazioni, vedere [Introduzione alla codifica Premium in Servizi multimediali di Azure](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/).

## <a id="february_changes_15"></a>Versione di febbraio 2015
### <a name="general-media-services-updates"></a>Aggiornamenti generali di Servizi multimediali
È ora disponibile la versione 2.9 dell'API REST di Servizi multimediali. A partire da questa versione, è possibile abilitare l'integrazione della rete CDN di Azure con gli endpoint di streaming hello. Per altre informazioni, vedere [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx).

## <a id="january_changes_15"></a>Versione di gennaio 2015
### <a name="general-media-services-updates"></a>Aggiornamenti generali di Servizi multimediali
Annuncio della versione GA (General Availability) per la protezione dei contenuti con la crittografia dinamica. Per altre informazioni, vedere la pagina relativa a [Servizi multimediali di Azure per il miglioramento della sicurezza di flusso con la versione GA della tecnologia DRM](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/).

### <a name="media-services-net-sdk-updates"></a>Aggiornamenti dell'SDK di Servizi multimediali per .NET
L'SDK di Servizi multimediali di Azure per .NET è ora disponibile nella versione 3.1.0.1.

Questa versione è contrassegnato come costruttore di Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate hello predefinito come obsoleto. Hello nuovo costruttore accetta TokenType come argomento.

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>Versione di dicembre 2014
### <a name="general-media-services-updates"></a>Aggiornamenti generali di Servizi multimediali
* Alcuni aggiornamenti e nuove funzionalità sono stati aggiunti il processore di contenuti multimediali dell'indicizzatore di Azure di toohello. Per altre informazioni, vedere le [note sulla versione di Azure Media Indexer versione 1.1.6.7](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/).
* Aggiunta una nuova API REST che consente di unità riservate di codifica tooupdate: [EncodingReservedUnitType con REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype).
* È stato aggiunto il supporto CORS per il servizio di distribuzione delle chiavi.
* Sono stati apportati miglioramenti alle prestazioni delle opzioni per i criteri di autorizzazioni delle query.
* Nel centro dati Cina hello [URL di distribuzione chiave](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url) è ora per ogni cliente (proprio come negli altri data center).
* È stata aggiunta una durata con destinazione automatica HLS. Quando si esegue lo streaming live, la creazione di pacchetti in HLS avviene sempre in modo dinamico. Per impostazione predefinita, servizi multimediali calcola automaticamente rapporto di compressione di segmento HLS (FragmentsPerSegment) in base a tooas hello intervallo (durata di KeyFrameInterval), denominato anche dei fotogrammi chiave Group of Pictures GOP, che viene ricevuto dal codificatore Live hello. Per altre informazioni, vedere [Uso di Live Streaming di Servizi multimediali di Azure].

### <a name="media-services-net-sdk-updates"></a>Aggiornamenti dell'SDK di Servizi multimediali per .NET
* [SDK di Servizi multimediali di Azure per .NET](http://www.nuget.org/packages/windowsazure.mediaservices/) è ora disponibile nella versione 3.1.0.0.
* Aggiornamento .net SDK hello dipendenza too.NET 4.5 Framework.
* Aggiungere una nuova API che consente di tooupdate unità riservate di codifica. Per altre informazioni, vedere [Aggiornamento del tipo di unità riservata e aumento delle unità riservate di codifica](media-services-dotnet-encoding-units.md).
* È stato aggiunto il supporto JWT (JSON Web Token) per l'autenticazione dei token. Per altre informazioni, vedere l'articolo relativo all' [autenticazione di token JWT in Servizi multimediali di Azure e alla crittografia dinamica](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).
* Aggiunti offset relativi per BeginDate ed ExpirationDate nel modello di licenza PlayReady hello.

## <a id="november_changes_14"></a>Versione di novembre 2014
* Servizi multimediali consente ora tooingest un live Smooth Streaming (FMP4) contenuto in una connessione SSL. tooingest su SSL, verificare che hello tooupdate tooHTTPS URL di inserimento.  Si noti che attualmente AMS non supporta SSL con domini personalizzati.  Per altre informazioni sullo streaming live, vedere [Uso di Live Streaming di Servizi multimediali di Azure].
* Attualmente non è possibile inserire lo streaming live RTMP tramite una connessione SSL.
* È possibile trasmettere solo tramite SSL, se l'endpoint da cui si distribuisce il contenuto di streaming hello è stato creato dopo il 10 settembre 2014. Se gli URL di streaming sono basati su hello streaming creati dopo il 10 settembre, hello URL contiene "streaming.mediaservices.windows.net" (formato nuovo hello). URL di streaming che contengono "origin.mediaservices.windows.net" (formato precedente hello) non supportano SSL. Se l'URL è nel formato precedente hello e si desidera toostream in grado di toobe su SSL, [creare un nuovo endpoint di streaming](media-services-portal-manage-streaming-endpoints.md). Usare gli URL creati in base a hello streaming nuovi endpoint toostream il contenuto tramite SSL.

## <a id="october_changes_14"></a>Versione di ottobre 2014
### <a id="new_encoder_release"></a>Versione del Codificatore di Servizi multimediali
Annuncio nuova versione di hello del codificatore multimediale di Azure Media Services. Con hello vengono addebitati solo i più recenti Azure Media Encoder output GB, ma in caso contrario hello nuovo codificatore è una funzionalità compatibile con il codificatore precedente hello. Per altre informazioni, vedere [Dettagli prezzi dei servizi multimediali].

### <a id="oct_sdk"></a>SDK di Servizi multimediali per .NET
Media Services .NET SDK Extensions è ora alla versione 2.0.0.3.

L'SDK di Servizi multimediali per .NET è ora disponibile nella versione 3.0.0.8.

sono stata apportata Hello seguenti modifiche:

* Refactoring nelle classi di criteri per l'esecuzione di nuovi tentativi.
* Aggiunta di intestazioni di richiesta toohttp stringa agente utente.
* Aggiunta del passaggio di compilazione nuget.
* Correzione scenario test toouse x509 cert dal repository.
* Convalida delle impostazioni durante l'aggiornamento di un endpoint di canale e di streaming.

### <a name="new-github-repository-toohost-media-services-samples"></a>Nuovi esempi di servizi multimediali toohost del repository GitHub
Gli esempi si trovano nel [repository GitHub degli esempi di Servizi multimediali di Azure](https://github.com/Azure/Azure-Media-Services-Samples).

## <a id="september_changes_14"></a>Versione di settembre 2014
È ora disponibile la versione 2.7 dei metadati di REST di Servizi multimediali. Per ulteriori informazioni sugli ultimi aggiornamenti REST hello, vedere [riferimento all'API REST di Azure Media Services].

Media Services SDK per .NET è ora alla versione 3.0.0.7.

### <a id="sept_14_breaking_changes"></a>Modifiche di rilievo
* **Origine** è stato rinominato troppo[StreamingEndpoint].
* Una modifica nel comportamento predefinito di hello quando si utilizza hello **portale di Azure** tooencode e pubblicare file MP4.

In precedenza, quando si utilizza hello portale di Azure classico toopublish una risorsa di singolo file MP4 video un URL SAS verrebbe creato (URL di firma di accesso condiviso consentono di hello toodownload video da un archivio blob). Attualmente, quando si utilizza tooencode portale di Azure classico hello e quindi pubblica una risorsa video di singolo file MP4, hello generato URL punti tooan servizi multimediali di Azure endpoint di streaming.  Questa modifica non influisce sul video MP4 che vengono caricati direttamente tooMedia servizi e pubblicati senza essere codificati da servizi multimediali di Azure.

Al momento non hai hello seguente hello problema toosolve di due opzioni.

* Abilitare l'unità di streaming e usare asset MP4 di creazione dinamica dei pacchetti toostream hello come presentazione smooth streaming.
* Creare un toodownload url SAS MP4 hello (o progressivamente riprodurre). Per ulteriori informazioni su come toocreate un localizzatore SAS, vedere [recapito contenuto].

### <a id="sept_14_GA_changes"></a>Nuove funzionalità o scenari nella versione di disponibilità generale
* **Processore multimediale di indicizzazione**. Per altre informazioni vedere [Indicizzazione di file multimediali con Azure Media Indexer].
* Hello [StreamingEndpoint] entità consente ora tooadd i nomi di dominio personalizzato (host).
  
    Per toobe un nome di dominio personalizzato utilizzato come nome dell'endpoint di streaming di servizi di supporto hello, è necessario tooyour di nomi host personalizzati tooadd endpoint di streaming. Utilizzare hello le API REST di servizi multimediali o .NET SDK tooadd i nomi host personalizzati.
  
    si applica Hello seguenti considerazioni:
  
  * È necessario disporre di proprietà hello hello personalizzato del nome di dominio.
  * la proprietà Hello hello del nome di dominio deve essere convalidata da servizi multimediali di Azure. dominio hello toovalidate, creare un record CName che esegue il mapping <MediaServicesAccountId>.<parent domain> tooverifydns. < zona-dns-mediaservices >. 
  * È necessario creare un altro record CName che esegue il mapping hello host personalizzato (ad esempio, sports.contoso.com) nome tooyour nome host di Streamingendpoint Services Media (ad esempio, amstest.streaming.mediaservices.windows.net).

    Per ulteriori informazioni, vedere hello **CustomHostNames** proprietà hello [StreamingEndpoint] argomento.

### <a id="sept_14_preview_changes"></a>Nuove funzionalità e scenari che fanno parte della versione di anteprima pubblica di hello
* Live Streaming Preview. Per altre informazioni, vedere [Uso di Live Streaming di Servizi multimediali di Azure].
* Servizio di distribuzione di chiavi. Per altre informazioni, vedere [Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi].
* Crittografia dinamica AES. Per altre informazioni, vedere [Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi].
* Servizio di distribuzione di licenze per PlayReady. Per altre informazioni, vedere [Uso della crittografia dinamica PlayReady e del server di distribuzione di licenze PlayReady].
* Crittografia dinamica PlayReady. Per altre informazioni, vedere [Uso della crittografia dinamica PlayReady e del server di distribuzione di licenze PlayReady].
* Modello di licenza PlayReady di Servizi multimediali. Per altre informazioni, vedere [Panoramica del modello di licenza PlayReady di Servizi multimediali].
* Trasmissione in flusso di asset di archiviazione crittografati. Per altre informazioni, vedere [Streaming di contenuto crittografato di archiviazione].

## <a id="august_changes_14"></a>Versione di agosto 2014
Quando si codifica un asset, viene generato un asset di output al termine del processo di codifica hello. Fino a questa versione, il codificatore di Servizi multimediali di Azure ha restituito metadati relativi ad asset di output. A partire da questo codificatore hello versione genera inoltre i metadati sull'asset di input. Per ulteriori informazioni, vedere hello [Input metadati] e [Output metadati] argomenti.

## <a id="july_changes_14"></a>Versione di luglio 2014
Hello seguenti correzioni di bug sono stati introdotti per hello Azure Media Services Packager e componente di crittografia.

* Solo l'audio viene riprodotto quando un tooHTTP asset di archivio in tempo reale transmux Live Streaming: questo problema è stato risolto e ora vengono riprodotti sia audio e video.
* Quando il pacchetto di un tooHTTP asset crittografia envelope Live Streaming e AES a 128 bit, flussi hello incluso nel pacchetto non vengono riprodotti in dispositivi Android: è stato corretto il bug e flusso di pacchetti hello riprodotti in dispositivi Android che supportano HTTP Live Streaming.

## <a id="may_changes_14"></a>Versione di maggio 2014
### <a id="may_14_changes"></a>Aggiornamenti generali di Servizi multimediali
È ora possibile usare [creazione dinamica dei pacchetti] toostream HTTP Live Streaming (HLS) v3. toostream HLS v3, aggiungere hello percorso localizzatore di origine toohello formato seguenti: * .ism/manifest(format=m3u8-aapl-v3). Per altre informazioni, vedere il [blog di Nick Drouin].

La funzionalità Dynamic Packaging supporta attualmente la distribuzione di HTTP Live Streaming (v3 e v4) con crittografia PlayReady basata sulla funzionalità Smooth Streaming crittografata staticamente con PlayReady. Per informazioni su come tooencrypt Smooth Streaming con PlayReady, vedere [protezione Smooth Streaming con PlayReady].

### <a name="may_14_donnet_changes"></a>Aggiornamenti dell'SDK di Servizi multimediali per .NET
in hello versione Media Services .NET SDK 3.0.0.5 è incluse Hello seguenti miglioramenti:

* Velocità e resilienza maggiori per il caricamento e il download di asset di file multimediali.
* Miglioramenti nella gestione della logica di retry e delle eccezioni temporanee: 
  
  * Il rilevamento degli errori temporanei e la gestione della logica di retry sono stati migliorati per le eccezioni provocate dall'esecuzione di query, dal salvataggio delle modifiche, dal caricamento o dal download di file. 
  * Quando vengono generate eccezioni Web (ad esempio durante una richiesta di token ACS), si nota che ora gli errori irreversibili vengono gestiti più rapidamente.

Per ulteriori informazioni, vedere [logica di tentativi in Media Services SDK per .NET hello].

## <a id="april_changes_14"></a>Versione del codificatore di aprile 2014
### <a name="april_14_enocer_changes"></a>Aggiornamenti del Codificatore di Servizi multimediali
* Supporto aggiunto per gestire i file AVI creati mediante l'editor non lineare Grass Valley EDIUS hello, in cui hello video viene leggermente compresso tramite codec di annunci di Grass Valley HQ/HQX. Per ulteriori informazioni, vedere [hello annunci di Grass Valley annuncia EDIUS 7 Streaming tramite Cloud].
* Aggiunta del supporto per la specifica di convenzione di denominazione per i file hello prodotta da Media Encoder hello hello. Per altre informazioni, vedere [Controllo dei nomi file di output del codificatore di Servizi multimediali].
* Supporto aggiunto per sovrimpressioni video e/o audio. Per altre informazioni, vedere [Creazione di sovrimpressioni].
* Supporto aggiunto per collegare tra loro più segmenti video. Per altre informazioni, vedere [Unione dei segmenti video].
* Bug correlato tootranscoding di MP4s dove audio hello è stato codificato con MPEG-1 Audio layer 3 (noto anche come formato MP3 risolto).

## <a id="jan_feb_changes_14"></a>Versioni di gennaio/febbraio 2014
### <a name="jan_fab_14_donnet_changes"></a>SDK di Servizi multimediali di Azure per .NET versioni 3.0.0.1, 3.0.0.2 e 3.0.0.3
le modifiche alla Hello versioni 3.0.0.1 e 3.0.0.2 includono:

* Risoluzione dei problemi correlati toousage di query LINQ con istruzioni OrderBy.
* Soluzioni di test in [GitHub] divise in test basati su unità e test basati su scenario.

Per ulteriori informazioni sulle modifiche di hello, vedere: [rilascia Azure Media Services .NET SDK versioni 3.0.0.1 e 3.0.0.2].

Hello dopo le modifiche sono stata apportata alla versione 3.0.0.3:

* Versione toouse dipendenze di archiviazione di Azure aggiornato 3.0.3.0. 
* Problema relativo alla compatibilità con le versioni precedenti per le versioni 3.0.*.* risolto. 

## <a id="december_changes_13"></a>Versione di dicembre 2013
### <a name="dec_13_donnet_changes"></a>SDK di Servizi multimediali di Azure per .NET versione 3.0.0.0
> [!NOTE]
> Le versioni 3.0.x.x non sono compatibili con le versioni precedenti 2.4.x.x.
> 
> 

versione più recente di Hello di hello Media Services SDK è ora 3.0.0.0. È possibile scaricare il pacchetto più recente di hello da Nuget o ottenere bit hello da [GitHub].

A partire da Media Services SDK versione 3.0.0.0 hello, è possibile riutilizzare hello [Azure Active Directory servizio Access Control (ACS)] token. Per ulteriori informazioni, vedere hello "riutilizzo di controllo del servizio token di accesso" sezione hello [tooMedia servizi di connessione con hello Media Services SDK per .NET] argomento.

### <a name="dec_13_donnet_ext_changes"></a>Estensioni dell'SDK di Servizi multimediali di Azure per .NET versione 2.0.0.0
Hello Azure Media Services .NET SDK Extensions è un set di metodi di estensione e funzioni di supporto che semplificano il codice e rendere più semplice toodevelop con servizi multimediali di Azure. È possibile ottenere i bit più recenti di hello da [Azure Media Services .NET SDK Extensions].

## <a id="november_changes_13"></a>Versione di novembre 2013
### <a name="nov_13_donnet_changes"></a>Modifiche apportate all'SDK di Servizi multimediali di Azure per .NET
A partire da questa versione, hello Media Services SDK per .NET gestisce gli errori temporanei che possono verificarsi quando si apportano livello API REST di servizi multimediali toohello di chiamate.

## <a id="august_changes_13"></a>Versione di agosto 2013
### <a name="aug_13_powershell_changes"></a>Cmdlet di PowerShell per Servizi multimediali inclusi negli strumenti SDK di Azure
Hello seguendo i cmdlet PowerShell di servizi multimediali è ora inclusi in [azure-sdk-tools].

* Get-AzureMediaServices 
  
    ad esempio `Get-AzureMediaServicesAccount`.
* New-AzureMediaServicesAccount 
  
    ad esempio `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`.
* New-AzureMediaServicesKey 
  
    ad esempio `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`.
* Remove-AzureMediaServicesAccount 
  
    ad esempio `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`.

## <a id="june_changes_13"></a>Versione di giugno 2013
### <a name="june_13_general_changes"></a>Modifiche di Servizi multimediali di Azure
modifiche di Hello citate in questa sezione sono aggiornamenti inclusi in servizi multimediali di giugno 2013 rilascia hello.

* Account di archiviazione più possibilità toolink tooa account di servizi multimediali. 
  
    StorageAccount
  
    Asset.StorageAccountName e Asset.StorageAccount
* Possibilità tooupdate Priority. 
* Entità e proprietà correlate alle notifiche: 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    Processo
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Modifiche apportate all'SDK di Servizi multimediali di Azure per .NET
salve le modifiche seguenti sono incluse nel giugno 2013 rilascia Media Services SDK. Hello più recente di Media Services SDK è disponibile su GitHub.

* A partire dalla versione di hello 2.3.0.0, hello Media Services SDK supporta il collegamento tooa gli account di archiviazione più account di servizi multimediali. Hello seguenti API supportano questa funzionalità:
  
    tipo IStorageAccount Hello.
  
    proprietà Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts Hello.
  
    Hello proprietà StorageAccount.
  
    proprietà StorageAccountName Hello.
  
    Per altre informazioni, vedere [Gestione di asset di Servizi multimediali su più account di archiviazione].
* API correlate alle notifiche. A partire dalla versione di hello 2.2.0.0 ricevere le notifiche di archiviazione di hello possibilità toolisten tooAzure coda. Per altre informazioni vedere [Gestione delle notifiche dei processi di Media Services].
  
    proprietà Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions Hello.
  
    tipo Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint Hello.
  
    tipo Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription Hello.
  
    tipo Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection Hello.
  
    tipo Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType Hello.
  
    tipo Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState Hello.
* Dipendenza hello Azure Storage Client SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll).
* Dipendenza da OData 5.5 (Microsoft.Data.OData.dll).

## <a id="december_changes_12"></a>Versione di dicembre 2012
### <a name="dec_12_dotnet_changes"></a>Modifiche apportate all'SDK di Servizi multimediali di Azure per .NET
* Intellisense: è stata aggiunta documentazione di Intellisense mancante per molti tipi.
* Microsoft.Practices.TransientFaultHandling.Core: Risolto un problema in cui hello SDK era ancora presente una versione precedente di tooan dipendenza di questo assembly. Hello SDK ora fa riferimento alla versione 5.1.1209.1 dell'assembly.

Consente di risolvere i problemi riscontrati in hello novembre 2012 SDK:

* IAsset.Locators.Count: questo valore è ora riportato in modo corretto nelle nuove interfacce IAsset dopo l'eliminazione di tutti i localizzatori.
* IAssetFile.ContentFileSize: questo valore viene ora impostato correttamente dopo un caricamento da IAssetFile.Upload(filepath).
* IAssetFile.ContentFileSize: questa proprietà ora può essere impostata quando si crea un file di asset, mentre in precedenza era di sola lettura.
* Iassetfile: Risolto un problema in cui questo metodo di caricamento sincrono è stato generando un'eccezione di errore seguente durante il caricamento di più asset di toohello file hello. Errore di Hello: "richiesta hello tooauthenticate Server non riuscita. Verificare che il valore di hello dell'intestazione di autorizzazione è del formato corretto, inclusa la firma hello."
* IAssetFile.UploadAsync: è stato risolto un problema quando non era possibile caricare più di 5 file contemporaneamente.
* Iassetfile. UploadProgressChanged: Questo evento viene attualmente fornito dall'hello SDK.
* IAssetFile.DownloadAsync(string, BlobTransferClient, ILocator, CancellationToken): questo overload del metodo è ora disponibile.
* IAssetFile.DownloadAsync: è stato risolto un problema quando non era possibile scaricare più di 5 file contemporaneamente.
* IAssetFile.Delete(): Risolto un problema in cui la chiamata di delete può generare un'eccezione se è stato caricato alcun file per hello IAssetFile.
* Processi: Risolto un problema in cui il concatenamento di una "MP4 tooSmooth flussi attività" con un "attività di protezione PlayReady" utilizzo di un modello di processo non crea tutte le attività affatto.
* EncryptionUtils.GetCertificateFromStore(): Questo metodo non genera più un'eccezione di riferimento null a causa di errori nella tooa ricerca certificato hello basato sui problemi di configurazione di certificati.

## <a id="november_changes_12"></a>Versione di novembre 2012
le modifiche citate in questa sezione Hello sono aggiornamenti inclusi nel hello novembre 2012 (versione 2.0.0.0) SDK. Tali modifiche possono richiedere un codice scritto per hello giugno 2012 anteprima SDK versione toobe riscrittura o la modifica.

* Asset
  
    IAsset è una funzione di creazione degli asset solo hello. IAsset non carica più file come parte della chiamata al metodo hello. Usare IAssetFile per il caricamento.
  
    metodo IAsset Hello e il valore di enumerazione Assetstate hello sono stati rimossi da hello Services SDK. Qualsiasi codice che si basa su questo valore deve essere riscritto.
* FileInfo
  
    Questa classe è stata rimossa e sostituita da IAssetFile.
  
    IAssetFiles
  
    IAssetFile sostituisce FileInfo e ha un comportamento diverso. toouse, creare un'istanza di oggetto IAssetFiles hello, seguito da un caricamento di file tramite hello Media Services SDK o hello Azure Storage SDK. è possibile utilizzare Hello overload iassetfile. upload seguenti:
  
  * Iassetfile: Un metodo sincrono che blocca il thread di hello ed è consigliato solo durante il caricamento di un singolo file.
  * IAssetFile.UploadAsync(filePath, blobTransferClient, locator, cancellationToken): un metodo asincrono. Questo è il meccanismo di caricamento hello preferito. 
    
    Bug noto: utilizzando hello cancellationToken determina l'annullamento caricamento hello; Tuttavia, lo stato di annullamento hello delle attività hello può essere qualsiasi di un numero di stati. È necessario rilevare e gestire le eccezioni in modo appropriato.
* Localizzatori
  
    versioni di specifiche dell'origine Hello sono stati rimossi. contesto Hello SAS specifiche. Locators.CreateSasLocator (asset, accessPolicy) verrà contrassegnato deprecate o rimosse dalla fase GA. Vedere hello localizzatori nella sezione nuove funzionalità per il comportamento aggiornato.

## <a id="june_changes_12"></a>Versione di anteprima di giugno 2012
Hello funzionalità seguente è una caratteristica introdotta nella versione di novembre hello di hello SDK.

* Eliminazione di entità
  
    IAsset, IAssetFile, ILocator, IAccessPolicy, IContentKey oggetti vengono attualmente eliminati a livello di oggetto hello, ad esempio Usa, anziché richiedere un'eliminazione in hello insieme, Delete (objinstance).
* Localizzatori
  
    I localizzatori devono ora essere creati utilizzando il metodo CreateLocator hello e utilizzare i valori di enumerazione LocatorType.SAS o Locatortype hello come argomento di tipo di localizzatore specifico hello desiderato toocreate.
  
    Nuove proprietà sono state aggiunte tooLocators toomake è più facile tooobtain URI utilizzabile per il contenuto. Questa riprogettazione dei localizzatori è stata destinata tooprovide una maggiore flessibilità futura estensibilità di terze parti e di aumentare la facilità di utilizzo per applicazioni client multimediali.
* Supporto di metodi asincroni
  
    Metodi tooall è stato aggiunto il supporto asincrono.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[Forum MSDN di Azure Media Services]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[riferimento all'API REST di Azure Media Services]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[Dettagli prezzi dei servizi multimediali]: http://azure.microsoft.com/pricing/details/media-services/
[Input metadati]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[Output metadati]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[recapito contenuto]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[Indicizzazione di file multimediali con Azure Media Indexer]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[StreamingEndpoint]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[Uso di Live Streaming di Servizi multimediali di Azure]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[Uso della crittografia dinamica PlayReady e del server di distribuzione di licenze PlayReady]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[Panoramica del modello di licenza PlayReady di Servizi multimediali]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[Streaming di contenuto crittografato di archiviazione]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[creazione dinamica dei pacchetti]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[blog di Nick Drouin]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[protezione Smooth Streaming con PlayReady]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[logica di tentativi in Media Services SDK per .NET hello]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[hello annunci di Grass Valley annuncia EDIUS 7 Streaming tramite Cloud]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[Controllo dei nomi file di output del codificatore di Servizi multimediali]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[Creazione di sovrimpressioni]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[Unione dei segmenti video]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[rilascia Azure Media Services .NET SDK versioni 3.0.0.1 e 3.0.0.2]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory servizio Access Control (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[tooMedia servizi di connessione con hello Media Services SDK per .NET]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[Azure Media Services .NET SDK Extensions]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure-sdk-tools]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[Gestione di asset di Servizi multimediali su più account di archiviazione]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[Gestione delle notifiche dei processi di Media Services]: http://msdn.microsoft.com/library/azure/dn261241.aspx

