---
title: Codici di errore di codifica di Servizi multimediali di Azure | Documentazione Microsoft
description: "Questo argomento riporta un elenco dei possibili codici di errore restituiti in caso di errore durante l'esecuzione di attività di codifica."
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
ms.openlocfilehash: f4fd2212d19f89148dde08c75c5a48cdd322d029
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="9de50-103">Codici di errore di codifica</span><span class="sxs-lookup"><span data-stu-id="9de50-103">Encoding error codes</span></span>

<span data-ttu-id="9de50-104">Nella tabella seguente sono elencati i codici di errore che potrebbero essere restituiti quando si verifica un errore durante l'esecuzione di attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="9de50-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span></span>  <span data-ttu-id="9de50-105">Per ottenere i dettagli dell'errore nel codice .NET, usare la classe [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9de50-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="9de50-106">Per ottenere i dettagli dell'errore nel codice REST, usare l'API REST [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9de50-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="9de50-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="9de50-107">ErrorDetail.Code</span></span> | <span data-ttu-id="9de50-108">Le possibili cause dell'errore</span><span class="sxs-lookup"><span data-stu-id="9de50-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="9de50-109">Sconosciuto</span><span class="sxs-lookup"><span data-stu-id="9de50-109">Unknown</span></span> |<span data-ttu-id="9de50-110">Errore sconosciuto durante l'esecuzione dell'attività</span><span class="sxs-lookup"><span data-stu-id="9de50-110">Unknown error while executing the task</span></span> |
| <span data-ttu-id="9de50-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="9de50-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="9de50-112">Categoria di errori relativa agli errori durante il download di asset di input, ad esempio nomi di file non validi, file di lunghezza zero, formati errati e così via.</span><span class="sxs-lookup"><span data-stu-id="9de50-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="9de50-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="9de50-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="9de50-114">Categoria di errori relativa a problemi sul lato del servizio, ad esempio errori di rete o archiviazione durante il download.</span><span class="sxs-lookup"><span data-stu-id="9de50-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="9de50-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="9de50-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="9de50-116">Categoria di errori in cui l'attività <see cref="MediaTask.PrivateData"/> (configurazione) non è valida, ad esempio la configurazione non è un set di impostazioni di sistema valido o contiene XML non valido.</span><span class="sxs-lookup"><span data-stu-id="9de50-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="9de50-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="9de50-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="9de50-118">Categoria di errori durante l'esecuzione dell'attività in cui i problemi nei file multimediali di input causano un errore.</span><span class="sxs-lookup"><span data-stu-id="9de50-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span></span> |
| <span data-ttu-id="9de50-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="9de50-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="9de50-120">Categoria di errori in cui il processore di contenuti multimediali non è in grado di elaborare i file forniti: formato di file multimediale non supportato o non corrispondente alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="9de50-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span></span> <span data-ttu-id="9de50-121">Ad esempio, si tenta di produrre un output solo audio da un asset che ha il solo video</span><span class="sxs-lookup"><span data-stu-id="9de50-121">For example, trying to produce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="9de50-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="9de50-122">ErrorProcessingTask</span></span> |<span data-ttu-id="9de50-123">Categoria di altri errori che il processore di contenuti multimediali rileva durante l'elaborazione dell'attività non correlati al contenuto.</span><span class="sxs-lookup"><span data-stu-id="9de50-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span></span> |
| <span data-ttu-id="9de50-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="9de50-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="9de50-125">Categoria di errori durante il caricamento di asset di output</span><span class="sxs-lookup"><span data-stu-id="9de50-125">Category of errors when uploading the output asset</span></span> |
| <span data-ttu-id="9de50-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="9de50-126">ErrorCancelingTask</span></span> |<span data-ttu-id="9de50-127">Categoria di errori per coprire gli errori durante il tentativo di annullare l'attività</span><span class="sxs-lookup"><span data-stu-id="9de50-127">Category of errors to cover failures when attempting to cancel the Task</span></span> |
| <span data-ttu-id="9de50-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="9de50-128">TransientError</span></span> |<span data-ttu-id="9de50-129">Categoria di errori sui problemi transitori (es.</span><span class="sxs-lookup"><span data-stu-id="9de50-129">Category of errors to cover transient issues (eg.</span></span> <span data-ttu-id="9de50-130">problemi di rete temporanei con Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="9de50-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="9de50-131">Per ottenere assistenza dal team di **Servizi multimediali** , aprire un [ticket di supporto](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="9de50-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9de50-132">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="9de50-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9de50-133">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="9de50-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="9de50-134">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="9de50-134">Related articles</span></span>
* [<span data-ttu-id="9de50-135">Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="9de50-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="9de50-136">Quote e limitazioni</span><span class="sxs-lookup"><span data-stu-id="9de50-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
