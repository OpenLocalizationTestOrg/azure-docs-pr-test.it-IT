---
title: Come creare un processore di contenuti multimediali usando Azure Media Services SDK per .NET| Microsoft Docs
description: Informazioni su come creare un componente del processore di contenuti multimediali per codificare, decodificare, convertire il formato, crittografare o decrittografare contenuti multimediali per Servizi multimediali di Azure. Negli esempi di codice, scritti in C#, viene usato Media Services SDK per .NET.
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
ms.openlocfilehash: c2cbe41b71afa8acc184f9d7f4cfe94686de783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="25ba1-104">Procedura: Ottenere un'istanza del processore di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="25ba1-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="25ba1-105">.NET</span><span class="sxs-lookup"><span data-stu-id="25ba1-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="25ba1-106">REST</span><span class="sxs-lookup"><span data-stu-id="25ba1-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="25ba1-107">Overview</span><span class="sxs-lookup"><span data-stu-id="25ba1-107">Overview</span></span>
<span data-ttu-id="25ba1-108">In Servizi multimediali un processore di contenuti multimediali è un componente che gestisce un'attività di elaborazione specifica, ad esempio la codifica, la conversione del formato, la crittografia o la decrittografia di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="25ba1-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="25ba1-109">Un processore multimediale viene generalmente creato durante la creazione di un'attività per la codifica, la crittografia o la conversione di formato di contenuto multimediale.</span><span class="sxs-lookup"><span data-stu-id="25ba1-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="25ba1-110">Processori di contenuti multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="25ba1-110">Azure media processors</span></span> 

<span data-ttu-id="25ba1-111">L'argomento seguente fornisce elenchi di processori di contenuti multimediali:</span><span class="sxs-lookup"><span data-stu-id="25ba1-111">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="25ba1-112">Processori di contenuti multimediali di codifica</span><span class="sxs-lookup"><span data-stu-id="25ba1-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="25ba1-113">Processori di contenuti multimediali di analisi</span><span class="sxs-lookup"><span data-stu-id="25ba1-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="25ba1-114">Ottenere un processore di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="25ba1-114">Get Media Processor</span></span>

<span data-ttu-id="25ba1-115">Il seguente metodo illustra come ottenere un'istanza del processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="25ba1-115">The following method shows how to get a media processor instance.</span></span> <span data-ttu-id="25ba1-116">Nell'esempio si suppone che si usi una variabile a livello di modulo denominata **_context** per fare riferimento al contesto del server descritto nella sezione [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md) (Procedura: Connettersi a Servizi multimediali a livello di codice).</span><span class="sxs-lookup"><span data-stu-id="25ba1-116">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="25ba1-117">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="25ba1-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="25ba1-118">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="25ba1-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="25ba1-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25ba1-119">Next Steps</span></span>
<span data-ttu-id="25ba1-120">Dopo avere ottenuto un'istanza del processore di contenuti multimediali, passare all'argomento [Come codificare un asset](media-services-dotnet-encode-with-media-encoder-standard.md) che illustra come usare Media Encoder Standard per codificare un asset.</span><span class="sxs-lookup"><span data-stu-id="25ba1-120">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

