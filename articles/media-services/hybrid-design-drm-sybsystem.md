---
title: aaaHybrid progettazione di servizi multimediali di Azure usando i sottosistemi DRM | Documenti Microsoft
description: Questo articolo spiega come usare Servizi multimediali di Azure per la progettazione ibrida di sottosistemi DRM.
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a>Progettazione ibrida di sottosistemi DRM

Questo articolo spiega come usare Servizi multimediali di Azure per la progettazione ibrida di sottosistemi DRM.

## <a name="overview"></a>Panoramica

Servizi multimediali di Azure fornisce il supporto per i seguenti tre sistema DRM hello:

* PlayReady
* Widevine (modulare)
* FairPlay

supporto DRM Hello include crittografia DRM (crittografia dinamica) e il recapito di licenza, con Azure Media Player, che supporta tutti i 3 DRMs come un lettore di browser SDK.

Per una trattazione dettagliata di DRM/CENC sottosistema progettazione e implementazione, vedere il documento hello intitolato [CENC con Multi-DRM e controllo di accesso](media-services-cenc-with-multidrm-access-control.md).

Anche se è offrono supporto completo per i tre sistemi DRM, in alcuni casi i clienti devono toouse varie parti dell'infrastruttura/i propri sottosistemi toobuild di servizi multimediali tooAzure inoltre un sottosistema DRM ibrido.

Di seguito sono riportate alcune delle domande comuni poste dai clienti:

* "Posso usare i miei server licenze DRM?" (in questo caso, i clienti hanno investito in un farm di licenze server DRM con logica di business incorporata)
* "Posso usare solo la funzionalità di distribuzione della licenza DRM di Servizi multimediali di Azure senza ospitare contenuti in AMS?"

## <a name="modularity-of-hello-ams-drm-platform"></a>Modularità di hello piattaforma AMS DRM

In quanto parte di una piattaforma video cloud completa, DRM di Servizi multimediali di Azure è stato progettato all'insegna della flessibilità e modularità. È possibile utilizzare servizi multimediali di Azure con una delle seguenti combinazioni diverse, descritte nella seguente tabella hello (segue una spiegazione della notazione hello utilizzata nella tabella hello) hello. 

|**Hosting e origine del contenuto**|**Crittografia del contenuto**|**Distribuzione di licenze DRM**|
|---|---|---|
|AMS|AMS|AMS|
|AMS|AMS|Terze parti|
|AMS|Terze parti|AMS|
|AMS|Terze parti|Terze parti|
|Terze parti|Terze parti|AMS|

### <a name="content-hosting--origin"></a>Hosting e origine del contenuto

* AMS: l'asset video è ospitato in AMS mentre lo streaming viene eseguito tramite gli endpoint di streaming (ma non necessariamente tramite la creazione dinamica dei pacchetti).
* Terze parti: il video è ospitato e distribuito su una piattaforma di streaming di terze parti, esterna ad AMS.

### <a name="content-encryption"></a>Crittografia del contenuto

* AMS: la crittografia del contenuto viene eseguita dinamicamente/on demand dalla crittografia dinamica di AMS.
* Terze parti: la crittografia del contenuto viene eseguita all'esterno di AMS usando un flusso di lavoro di pre-elaborazione.

### <a name="drm-license-delivery"></a>Distribuzione di licenze DRM

* AMS: la licenza di DRM viene distribuita dal servizio di distribuzione della licenza di AMS.
* Terze parti: la licenza di DRM viene distribuita da un server licenze DRM di terze parti esterno ad AMS.

## <a name="configure-based-on-your-hybrid-scenario"></a>Configurare in base allo scenario ibrido

### <a name="content-key"></a>Chiave simmetrica

La configurazione di una chiave simmetrica, è possibile controllare hello gli attributi di crittografia dinamica AMS sia il servizio di recapito licenza AMS seguenti:

* chiave simmetrica Hello utilizzato per la crittografia dinamica DRM.
* DRM licenza contenuto toobe recapitati da servizi multimediali di licenza: diritti, chiave simmetrica e le restrizioni.
* Tipo di **limitazione dei criteri di autorizzazione della chiave simmetrica**: aperta, IP o limitazione del token.
* Se **token** tipo **restrizione dei criteri di autorizzazione chiave del contenuto viene utilizzato**, hello **contenuto restrizione dei criteri di autorizzazione della chiave** devono essere soddisfatti prima del rilascio di una licenza.

### <a name="asset-delivery-policy"></a>Criteri di distribuzione degli asset

Tramite la configurazione di un criterio di recapito di asset, è possibile controllare hello gli attributi utilizzati da creazione dinamica dei pacchetti AMS e la crittografia dinamica di un sistema AMS di endpoint di streaming seguenti:

* Combinazione di protocollo di streaming e crittografia DRM, come DASH in CENC (PlayReady e Widevine), Smooth Streaming in PlayReady, HLS in Widevine o PlayReady.
* Hello predefinito/incorporati licenza recapito URL per ogni hello coinvolti DRMs.
* Presenza o meno di una stringa query per l'ID chiave (KID) di Widevine e Fairplay negli URL di acquisizione della licenza (LA_URL) nell'elenco di riproduzione DASH MPD o HLS.

## <a name="scenarios-and-samples"></a>Scenari ed esempi

In base a una spiegazione hello nella sezione precedente di hello, hello seguenti cinque scenari ibridi utilizza rispettivi **chiave simmetrica**-**criteri di distribuzione Asset** (Buongiorno combinazioni di configurazioni gli esempi indicati nell'ultima colonna hello seguono tabella hello):

|**Hosting e origine del contenuto**|**Crittografia DRM**|**Distribuzione di licenze DRM**|**Configurare la chiave simmetrica**|**Configurare i criteri di distribuzione dell'asset**|**Esempio**|
|---|---|---|---|---|---|
|AMS|AMS|AMS|Sì|Sì|Esempio 1|
|AMS|AMS|Terze parti|Sì|Sì|Esempio 2|
|AMS|Terze parti|AMS|Sì|No|Esempio 3|
|AMS|Terze parti|Esterno|No|No|Esempio 4|
|Terze parti|Terze parti|AMS|Sì|No|    

Negli esempi di hello, PlayReady protection funziona per DASH e smooth streaming. URL video Hello seguenti sono smooth streaming URL. tooget hello URL DASH corrispondenti, aggiungere solo "(formato = mpd-tempo-csf)". È possibile utilizzare hello [test di azure media player](http://aka.ms/amtest) tootest in un browser. Consente di tooconfigure cui streaming toouse di protocollo, in cui tecnico. IE11 e MS Edge in Windows 10 supportano PlayReady tramite EME. Per ulteriori informazioni, vedere [informazioni dettagliate su hello testare strumento](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).

### <a name="sample-1"></a>Esempio 1

* URL di origine (di base): https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest 
* LA_URL di PlayReady (DASH e smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 
* LA_URL di Widevine (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4 
* LA_URL di FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8 

### <a name="sample-2"></a>Esempio 2

* URL di origine (di base): http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest 
* LA_URL di PlayReady (DASH e smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx 

### <a name="sample-3"></a>Esempio 3

* URL di origine: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest 
* LA_URL di PlayReady (DASH e smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 

### <a name="sample-4"></a>Esempio 4

* URL di origine: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest 
* LA_URL di PlayReady (DASH e smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx 

## <a name="summary"></a>Riepilogo

In sintesi, i componenti DRM di Servizi multimediali di Azure sono flessibili ed è possibile usarli in uno scenario ibrido configurando correttamente la chiave simmetrica e i criteri di distribuzione della licenza, come descritto in questo articolo.

## <a name="next-steps"></a>Passaggi successivi
Visualizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

