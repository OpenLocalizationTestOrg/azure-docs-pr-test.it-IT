---
title: Scaricare asset di Servizi multimediali nel computer - Azure | Documentazione Microsoft
description: Informazioni su come scaricare asset nel computer. Negli esempi di codice, scritti in C#, viene usato Media Services SDK per .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d8e740e969f68c85842f42c109328423da1b4414
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="6e7b2-104">Procedura: Distribuire un asset mediante download</span><span class="sxs-lookup"><span data-stu-id="6e7b2-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="6e7b2-105">Questo argomento illustra le opzioni per la distribuzione di asset di file multimediali caricati in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="6e7b2-105">This topic discusses options for delivering media assets uploaded to Media Services.</span></span> <span data-ttu-id="6e7b2-106">È possibile distribuire contenuti di Servizi multimediali in numerosi scenari di applicazione.</span><span class="sxs-lookup"><span data-stu-id="6e7b2-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="6e7b2-107">È possibile scaricare asset di file multimediali oppure accedervi mediante un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="6e7b2-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="6e7b2-108">I contenuti multimediali possono essere inviati a un'altra applicazione o un altro provider di contenuti.</span><span class="sxs-lookup"><span data-stu-id="6e7b2-108">You can send media content to another application or to another content provider.</span></span> <span data-ttu-id="6e7b2-109">Per ottenere livelli più elevati di prestazioni e scalabilità, è anche possibile distribuire contenuti usando una rete per la distribuzione di contenuti (CDN).</span><span class="sxs-lookup"><span data-stu-id="6e7b2-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="6e7b2-110">Questo esempio illustra come scaricare asset di file multimediali da Servizi multimediali nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="6e7b2-110">This example shows how to download media assets from Media Services to your local computer.</span></span> <span data-ttu-id="6e7b2-111">Il codice esegue query sui processi associati all'account di Servizi multimediali mediante l'ID processo e accede alla relativa raccolta **OutputMediaAssets** , ovvero il set con uno o più asset di file multimediali di output risultante dall'esecuzione di un processo.</span><span class="sxs-lookup"><span data-stu-id="6e7b2-111">The code queries the jobs associated with the Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is the set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="6e7b2-112">In questo esempio di codice viene illustrato come scaricare asset di file multimediali di output da un processo, ma lo stesso approccio può essere usato anche per scaricare altri asset.</span><span class="sxs-lookup"><span data-stu-id="6e7b2-112">This  example shows how to download output media assets from a job, but you can apply the same approach to download other assets.</span></span>

>[!NOTE]
><span data-ttu-id="6e7b2-113">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="6e7b2-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="6e7b2-114">Usare lo stesso ID criterio se si usano sempre gli stessi giorni/autorizzazioni di accesso, come nel cado di criteri per i localizzatori che devono rimanere attivi per molto tempo (criteri di non caricamento).</span><span class="sxs-lookup"><span data-stu-id="6e7b2-114">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="6e7b2-115">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="6e7b2-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download the output asset of the specified job to a local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how to download a single asset. 
        // However, you can iterate through the OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference to the job. 
        IJob job = GetJob(jobId);

        // Get a reference to the first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator to download the asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use the following event handler to check download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="6e7b2-116">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="6e7b2-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6e7b2-117">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="6e7b2-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6e7b2-118">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6e7b2-118">See Also</span></span>
[<span data-ttu-id="6e7b2-119">Distribuire contenuti in streaming</span><span class="sxs-lookup"><span data-stu-id="6e7b2-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

