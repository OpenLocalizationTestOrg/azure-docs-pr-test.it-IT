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
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="f95a5-104">Procedura: Ottenere un'istanza del processore di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="f95a5-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f95a5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f95a5-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="f95a5-106">REST</span><span class="sxs-lookup"><span data-stu-id="f95a5-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="f95a5-107">Overview</span><span class="sxs-lookup"><span data-stu-id="f95a5-107">Overview</span></span>
<span data-ttu-id="f95a5-108">In Servizi multimediali un processore di contenuti multimediali è un componente che gestisce un'attività di elaborazione specifica, ad esempio la codifica, la conversione del formato, la crittografia o la decrittografia di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="f95a5-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="f95a5-109">In genere creare un processore di contenuti multimediali quando si crea un'attività tooencode, crittografare o convertire il formato del contenuto multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="f95a5-109">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="f95a5-110">Processori di contenuti multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f95a5-110">Azure media processors</span></span> 

<span data-ttu-id="f95a5-111">Hello argomento fornisce elenchi di processori di contenuti multimediali:</span><span class="sxs-lookup"><span data-stu-id="f95a5-111">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="f95a5-112">Processori di contenuti multimediali di codifica</span><span class="sxs-lookup"><span data-stu-id="f95a5-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="f95a5-113">Processori di contenuti multimediali di analisi</span><span class="sxs-lookup"><span data-stu-id="f95a5-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="f95a5-114">Ottenere un processore di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="f95a5-114">Get Media Processor</span></span>

<span data-ttu-id="f95a5-115">Hello seguente metodo mostra come tooget un'istanza di processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="f95a5-115">hello following method shows how tooget a media processor instance.</span></span> <span data-ttu-id="f95a5-116">Hello di codice seguente presuppone l'utilizzo di hello di una variabile a livello di modulo denominata **contesto** il contesto server hello tooreference come descritto nella sezione hello [procedura: connettersi tooMedia servizi a livello di codice](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="f95a5-116">hello code example assumes hello use of a module-level variable named **_context** tooreference hello server context as described in hello section [How to: Connect tooMedia Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="f95a5-117">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f95a5-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f95a5-118">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f95a5-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f95a5-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f95a5-119">Next Steps</span></span>
<span data-ttu-id="f95a5-120">Ora che è stato appreso come tooget un'istanza di processore di contenuti multimediali, andare toohello [come tooEncode un Asset](media-services-dotnet-encode-with-media-encoder-standard.md) argomento in cui è visualizzate come toouse hello Media Encoder Standard tooencode un asset.</span><span class="sxs-lookup"><span data-stu-id="f95a5-120">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

