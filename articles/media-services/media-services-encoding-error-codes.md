---
title: Servizi multimediali aaaAzure codici di errore di codifica | Documenti Microsoft
description: "In questo argomento elenca i codici di errore che possono essere restituiti nel caso in cui si è verificato un errore durante l'esecuzione dell'attività di codifica hello..."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="98c7f-103">Codici di errore di codifica</span><span class="sxs-lookup"><span data-stu-id="98c7f-103">Encoding error codes</span></span>

<span data-ttu-id="98c7f-104">Hello nella tabella seguente sono elencati i codici di errore che possono essere restituiti nel caso in cui si è verificato un errore durante l'esecuzione dell'attività di codifica hello.</span><span class="sxs-lookup"><span data-stu-id="98c7f-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="98c7f-105">i dettagli dell'errore tooget nel codice .NET, usare hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="98c7f-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="98c7f-106">i dettagli dell'errore tooget nel codice REST, usare hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) API REST.</span><span class="sxs-lookup"><span data-stu-id="98c7f-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="98c7f-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="98c7f-107">ErrorDetail.Code</span></span> | <span data-ttu-id="98c7f-108">Le possibili cause dell'errore</span><span class="sxs-lookup"><span data-stu-id="98c7f-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="98c7f-109">Sconosciuto</span><span class="sxs-lookup"><span data-stu-id="98c7f-109">Unknown</span></span> |<span data-ttu-id="98c7f-110">Errore sconosciuto durante l'esecuzione di attività hello</span><span class="sxs-lookup"><span data-stu-id="98c7f-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="98c7f-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="98c7f-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="98c7f-112">Categoria di errori relativa agli errori durante il download di asset di input, ad esempio nomi di file non validi, file di lunghezza zero, formati errati e così via.</span><span class="sxs-lookup"><span data-stu-id="98c7f-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="98c7f-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="98c7f-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="98c7f-114">Categoria di errori che verranno descritti i problemi sul lato servizio hello - errori di rete o archiviazione di esempio durante il download.</span><span class="sxs-lookup"><span data-stu-id="98c7f-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="98c7f-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="98c7f-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="98c7f-116">Categoria di errori in cui attività <see cref="MediaTask.PrivateData"/> (configurazione) non è valido, ad esempio configurazione hello non predefinito di un sistema valido o contiene codice XML non valido.</span><span class="sxs-lookup"><span data-stu-id="98c7f-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="98c7f-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="98c7f-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="98c7f-118">Categoria di errori durante l'esecuzione di hello dell'attività hello in cui i problemi all'interno di hello input file multimediali provocare un errore.</span><span class="sxs-lookup"><span data-stu-id="98c7f-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="98c7f-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="98c7f-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="98c7f-120">Categoria di errori in cui il processore di contenuti multimediali hello non è in grado di elaborare il file hello forniti: formato di file multimediale non supportato o non corrisponde a hello configurazione.</span><span class="sxs-lookup"><span data-stu-id="98c7f-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="98c7f-121">Ad esempio, il tentativo tooproduce un output di solo audio da un'attività che ha il solo video</span><span class="sxs-lookup"><span data-stu-id="98c7f-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="98c7f-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="98c7f-122">ErrorProcessingTask</span></span> |<span data-ttu-id="98c7f-123">Categoria di altri errori hello processore di contenuti multimediali rilevata durante l'elaborazione di hello dell'attività hello che sono toocontent non correlati.</span><span class="sxs-lookup"><span data-stu-id="98c7f-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="98c7f-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="98c7f-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="98c7f-125">Categoria di errori durante il caricamento di asset di output di hello</span><span class="sxs-lookup"><span data-stu-id="98c7f-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="98c7f-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="98c7f-126">ErrorCancelingTask</span></span> |<span data-ttu-id="98c7f-127">Categoria di errori di toocover errori durante il tentativo di hello toocancel attività</span><span class="sxs-lookup"><span data-stu-id="98c7f-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="98c7f-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="98c7f-128">TransientError</span></span> |<span data-ttu-id="98c7f-129">Categoria di errori toocover temporanei i problemi (ad es.</span><span class="sxs-lookup"><span data-stu-id="98c7f-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="98c7f-130">problemi di rete temporanei con Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="98c7f-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="98c7f-131">Guida tooget da hello **servizi multimediali** team, aprire un [ticket di supporto](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="98c7f-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="98c7f-132">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="98c7f-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="98c7f-133">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="98c7f-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="98c7f-134">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="98c7f-134">Related articles</span></span>
* [<span data-ttu-id="98c7f-135">Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="98c7f-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="98c7f-136">Quote e limitazioni</span><span class="sxs-lookup"><span data-stu-id="98c7f-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
