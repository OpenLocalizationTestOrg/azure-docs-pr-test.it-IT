---
title: aaaProtect i contenuti con servizi multimediali di Azure | Documenti Microsoft
description: Questi articoli forniscono informazioni generali sulla protezione dei contenuti con Servizi multimediali.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>Informazioni generali sulla protezione dei contenuti
Servizi multimediali di Microsoft Azure consente di toosecure gli elementi multimediali dal tempo hello che lascia computer tramite l'archiviazione, elaborazione e il recapito. Servizi multimediali consente toodeliver contenuti in tempo reale e su richiesta crittografati in modo dinamico con Advanced Encryption Standard (AES) (utilizzando le chiavi di crittografia a 128 bit) o una qualsiasi delle hello DRMs principali: Microsoft PlayReady e Google Widevine FairPlay Apple. Servizi multimediali fornisce anche un servizio per il recapito di chiavi AES e le licenze client tooauthorized DRM (PlayReady, Widevine e FairPlay). 

Hello seguente immagine illustra hello protezione del contenuto dei flussi di lavoro che supporta AMS. 

![Protezione con PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 

In questo argomento viene [concetti e terminologia](media-services-content-protection-overview.md) protezione del contenuto con AMS toounderstanding pertinente. Hello comprende anche [collegamenti](media-services-content-protection-overview.md#common-scenarios) tootopics che mostrano come tooachieve contenuto attività di protezione. 

## <a name="dynamic-encryption"></a>Crittografia dinamica
Servizi multimediali di Microsoft Azure consente il contenuto crittografato in modo dinamico con chiave non crittografata AES o la crittografia DRM toodeliver: Microsoft PlayReady e Google Widevine FairPlay Apple.

Attualmente, è possibile crittografare hello seguenti formati di streaming: HLS, MPEG DASH e Smooth Streaming. Non è possibile crittografare i download progressivi.

Se si desidera per servizi multimediali tooencrypt un asset, è necessario tooassociate una chiave di crittografia (CommonEncryption o EnvelopeEncryption) con l'asset e inoltre configurare criteri di autorizzazione per la chiave di hello.

È inoltre necessario criteri di distribuzione dell'asset di tooconfigure hello. Se si desidera toostream asset crittografato di archiviazione, assicurarsi che toospecify come si desidera toodeliver per la configurazione dei criteri di recapito di asset.

Quando un flusso è richiesto da un lettore, servizi multimediali Usa hello specificato toodynamically chiave crittografare il contenuto utilizzando una chiave non crittografata AES o la crittografia DRM. flusso di hello toodecrypt, hello lettore richiederà chiave hello dal servizio di distribuzione delle chiavi hello. Se è o meno utente hello toodecide autorizzato chiave hello tooget, servizio hello valuta i criteri di autorizzazione hello specificato per la chiave di hello.


## <a name="storage-encryption"></a>Crittografia di archiviazione
Utilizzare il contenuto non crittografato localmente tramite crittografia AES a 256 bit di tooencrypt di crittografia di archiviazione e quindi caricarla tooAzure archiviazione dove viene archiviato in forma crittografata. Gli asset protetti con crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file crittografato sistema precedente tooencoding e, facoltativamente, crittografare nuovamente toouploading precedente come nuovo asset di output. Hello primario per la crittografia di archiviazione viene usata quando si desidera toosecure file multimediali di input di alta qualità applicando una crittografia avanzata rest su disco.

In ordine toodeliver asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset hello in modo da servizi multimediali come toodeliver il contenuto. Prima che l'asset può essere trasmesso, hello streaming flussi e crittografia di archiviazione hello viene rimosso il server dei contenuti usando hello specificato criterio di recapito (ad esempio, AES, crittografia comune o Nessuna crittografia).

## <a name="common-encryption-cenc"></a>Crittografia comune (CENC)
La crittografia comune viene usata per crittografare il contenuto con PlayReady e/o Widewine.

## <a name="using-cbcs-aapl-encryption"></a>Uso della crittografia cbcs-aapl
La crittografia cbcs-aapl viene usata per crittografare il contenuto con FairPlay.

## <a name="envelope-encryption"></a>Crittografia envelope
Utilizzare questa opzione se si desidera tooprotect il contenuto con chiave non crittografata AES-128. Se si desidera un'opzione più sicura, scegliere uno dei DRMs hello elencate in questo argomento. 

## <a name="licenses-and-keys-delivery-service"></a>Servizio di distribuzione di licenze e chiavi
Servizi multimediali fornisce un servizio per la distribuzione di licenze DRM (PlayReady, Widevine, FairPlay) e i client tooauthorized chiavi non crittografata AES. È possibile utilizzare [hello Azure portal](media-services-portal-protect-content.md), API REST, o Media Services SDK per .NET tooconfigure autenticazione criteri di autorizzazione e per le licenze e le chiavi.

## <a name="token-restriction"></a>Restrizione Token
Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: apertura o la limitazione del token. criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza). Servizi multimediali supporta i token in formato JSON Web Token (JWT) e i token SWT (Simple Web token) hello. Servizi multimediali non fornisce servizi token di sicurezza. È possibile creare un servizio token di sicurezza personalizzato o utilizzare i token tooissue ACS di Microsoft Azure. Hello servizio token di sicurezza deve essere configurato toocreate un token firmato con hello specificato chiave e rilasciare le attestazioni specificate nella configurazione della restrizione token hello. attestazioni di servizi multimediali Hello servizio di distribuzione chiavi restituirà hello richiesto hello e chiave (o licenza) client toohello se hello token è valido in hello token corrispondono a quelle configurate per la chiave di hello (o licenza).

Quando si configurano i criteri con restrizione token hello, è necessario specificare la chiave di verifica primaria hello, autorità di certificazione e i parametri di destinatari. chiave di verifica primaria Hello contiene hello chiave che hello token è stato firmato con, autorità emittente è hello servizio token di sicurezza che rilascia token hello. destinatari Hello (talvolta denominato ambito) descrive finalità hello del token hello o hello risorse hello token autorizza l'accesso. Hello servizio di distribuzione delle chiavi di servizi multimediali verifica che i valori nel token hello corrispondano valori hello hello modello.

## <a name="streaming-urls"></a>URL di streaming
Se l'asset è stata crittografata con più DRM, è necessario utilizzare un tag di crittografia nell'URL di streaming hello: (formato = 'm3u8-aapl', crittografia = 'xxx').

si applica Hello seguenti considerazioni:

* Può essere specificato solo un tipo di crittografia oppure nessuno.
* Tipo di crittografia non dispone di toobe specificata nell'url di hello se solo uno di crittografia è stata applicata toohello asset.
* Il tipo di crittografia non fa distinzione tra maiuscole e minuscole.
* è possibile specificare i seguenti tipi di crittografia Hello:  
  * **cenc**: crittografia comune (Playready o Widevine)
  * **cbcs-aapl**: Fairplay
  * **cbc**: crittografia AES envelope.

## <a name="common-scenarios"></a>Scenari comuni
Hello argomenti seguenti illustrano come tooprotect contenuto nel servizio di archiviazione, fornire in modo dinamico crittografati flussi multimediali, utilizzare il servizio di recapito di AMS chiave licenza

* [Proteggere i contenuti con AES](media-services-protect-with-aes128.md) 
* [Proteggere i contenuti con PlayReady e/o Widevine ](media-services-protect-with-drm.md)
* [Trasmettere i contenuti HLS in modo protetto con Apple FairPlay e/o PlayReady](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>Scenari aggiuntivi
* [La modalità di servizio toointegrate licenze PlayReady di Azure con il proprio server di crittografia/streaming](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).
* [Utilizzando castLabs toodeliver DRM licenze tooAzure servizi multimediali](media-services-castlabs-integration.md)

>[!NOTE]
>Uno scenario in cui si usa un server DRM esterno (tecnologia) e un flusso da AMS non è attualmente supportato.


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Collegamenti correlati
[Annuncio di PlayReady come servizio e della crittografia dinamica AES con Servizi multimediali di Azure](http://mingfeiy.com/playready)

[Prezzi della distribuzione della licenza PlayReady di Servizi multimediali di Azure](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[La modalità di crittografia di flusso in servizi multimediali di Azure toodebug per AES](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[Autenticazione dei token JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Integrare l'app basata su OWIN MVC di Servizi multimediali di Azure con Azure Active Directory e limitare la distribuzione di chiavi simmetriche in base ad attestazioni JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Utilizzare i token ACS di Azure tooissue](http://mingfeiy.com/acs-with-key-services).

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
