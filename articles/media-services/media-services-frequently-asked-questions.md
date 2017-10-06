---
title: Servizi multimediali di domande frequenti aaaAzure | Documenti Microsoft
description: Domande frequenti (FAQ)
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>Domande frequenti

Questo articolo illustra domande più frequenti generati da una comunità di utenti di servizi multimediali di Azure (AMS) hello.

## <a name="general-ams-faqs"></a>Domande frequenti generali su AMS
D: Come scalare l'indicizzazione?

R: unità hello riservato sono hello stesso per la codifica e l'indicizzazione delle attività. Seguire le istruzioni [come unità riservate di codifica tooScale](media-services-scale-media-processing-overview.md). **Tenere presente** che le prestazioni dell'indicizzatore non vengono influenzate dal tipo di unità riservata.

D: Ho caricato, codificato e pubblicato un video. Che verrebbero video di hello hello motivo non viene riprodotto quando si tenta di toostream è?

R: una delle più comuni motivi è hello da cui si sta tentando di tooplayback in hello endpoint di streaming non si dispone di hello **esecuzione** stato.  

D: È possibile eseguire la composizione in un flusso live?

R: composizione dei flussi in tempo reale attualmente non è disponibile in servizi multimediali di Azure, pertanto sarà necessario toopre-comporre nel computer in uso.

D: È possibile usare la rete CDN di Azure con Live Streaming?

R: Media Services supporta l'integrazione con rete CDN di Azure (per ulteriori informazioni, vedere [come endpoint di Streaming tooManage in un Account di servizi multimediali](media-services-portal-manage-streaming-endpoints.md)).  È quindi possibile usare Live streaming con la rete CDN. Servizi multimediali di Azure fornisce output in formato Smooth Streaming, HLS e MPEG-DASH. Tutti questi formati usano il protocollo HTTP per trasferire dati e ottenere i vantaggi derivanti dalla cache HTTP. In dati video o audio effettivi in streaming in tempo reale è diviso toofragments e memorizzazione nella cache di questo singoli frammenti nella rete CDN. Solo i toobe di esigenze dati aggiornati è dati hello del manifesto. e viene effettuato periodicamente dalla rete CDN.

D: Servizi multimediali di Azure supporta anche l'archiviazione di immagini?

R: se si vuole semplicemente toostore JPEG o immagini PNG, è consigliabile mantenere quelle nell'archiviazione Blob di Azure. Non è tooputting alcun vantaggio in servizi multimediali account a meno che non si desidera tookeep che li associate a un Video o Audio asset. O se è necessario un toouse necessità hello immagini come sovrapposizioni di codificatore video hello. Media Encoder Standard supporta la sovrapposizione delle immagini su video, e che vengono elencati JPEG e PNG come supportati i formati di input. Per altre informazioni, vedere [Creazione di sovrimpressioni](media-services-advanced-encoding-with-mes.md#overlay).

D: come è possibile copiare le risorse da un tooanother di account di servizi multimediali.

R: toocopy asset da uno tooanother di account di servizi multimediali usando .NET, usare [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) metodo di estensione disponibile in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository. Per altre informazioni, vedere [questo](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) thread del forum.

D: quali sono hello caratteri supportati per la denominazione dei file quando si lavora con AMS?

R: Media Services utilizza il valore di hello di hello IAssetFile.Name proprietà durante la creazione di URL per hello streaming del contenuto (ad esempio, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Per questo motivo, la codifica percentuale non è consentita. valore di hello Hello **nome** proprietà non può avere uno dei seguenti hello [% riservati per la codifica caratteri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Può essere presente solo un carattere '.' per l'estensione di file hello.

D: come tooconnect usando REST?

R: per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali. È necessario effettuare le chiamate successive toohello nuovo URI. 

D: come è possibile ruotare un video durante il processo di codifica hello.

R: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supporta rotazione dagli angoli di 90/180 o 270. comportamento predefinito di Hello è "Auto", in cui tenta di metadati di rotazione toodetect hello in file MP4/MOV di hello in arrivo e compensare relativo. Sono inclusi i seguenti hello **origini** tooone elemento delle impostazioni predefinite di json hello definito [qui](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
