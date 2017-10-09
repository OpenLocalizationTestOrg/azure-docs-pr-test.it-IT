---
title: tooCreate aaaHow un processore di supporto tramite hello Azure Media Services SDK per .NET | Documenti Microsoft
description: Informazioni su come toocreate tooencode di componente processore una media, convertire il formato, crittografare o decrittografare il contenuto multimediale per servizi multimediali di Azure. Esempi di codice sono scritti in c# e utilizzano hello Media Services SDK per .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a>Procedura: Ottenere un'istanza del processore di contenuti multimediali
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Overview
In Servizi multimediali un processore di contenuti multimediali è un componente che gestisce un'attività di elaborazione specifica, ad esempio la codifica, la conversione del formato, la crittografia o la decrittografia di contenuti multimediali. In genere creare un processore di contenuti multimediali quando si crea un'attività tooencode, crittografare o convertire il formato del contenuto multimediale hello.

## <a name="azure-media-processors"></a>Processori di contenuti multimediali di Azure 

Hello argomento fornisce elenchi di processori di contenuti multimediali:

* [Processori di contenuti multimediali di codifica](scenarios-and-availability.md#encoding-media-processors)
* [Processori di contenuti multimediali di analisi](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a>Ottenere un processore di contenuti multimediali

Hello seguente metodo mostra come tooget un'istanza di processore di contenuti multimediali. Hello di codice seguente presuppone l'utilizzo di hello di una variabile a livello di modulo denominata **contesto** il contesto server hello tooreference come descritto nella sezione hello [procedura: connettersi tooMedia servizi a livello di codice](media-services-use-aad-auth-to-access-ams-api.md).

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato appreso come tooget un'istanza di processore di contenuti multimediali, andare toohello [come tooEncode un Asset](media-services-dotnet-encode-with-media-encoder-standard.md) argomento in cui è visualizzate come toouse hello Media Encoder Standard tooencode un asset.

