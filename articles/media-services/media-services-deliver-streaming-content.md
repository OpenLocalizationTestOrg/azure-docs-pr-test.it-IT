---
title: Pubblicare contenuti di Servizi multimediali di Azure mediante .NET | Microsoft Docs
description: Informazioni su come creare un localizzatore da usare per un URL di streaming. Negli esempi di codice, scritti in C#, viene usato Media Services SDK per .NET.
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 2bcb012eef84faa7c1e13ed22e88e45e4300ed54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="1e081-104">Pubblicare contenuti di Servizi multimediali di Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="1e081-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e081-105">REST</span><span class="sxs-lookup"><span data-stu-id="1e081-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="1e081-106">.NET</span><span class="sxs-lookup"><span data-stu-id="1e081-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="1e081-107">Portale</span><span class="sxs-lookup"><span data-stu-id="1e081-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="1e081-108">Overview</span><span class="sxs-lookup"><span data-stu-id="1e081-108">Overview</span></span>
<span data-ttu-id="1e081-109">È possibile trasmettere in streaming un set MP4 a velocità in bit adattiva creando un localizzatore di streaming OnDemand e un URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="1e081-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="1e081-110">L'argomento relativo alla [codifica di un asset](media-services-encode-asset.md) illustra come codificare un asset in un set MP4 a bitrate adattivo.</span><span class="sxs-lookup"><span data-stu-id="1e081-110">The [encoding an asset](media-services-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="1e081-111">Se il contenuto è crittografato, configurare i criteri di distribuzione degli asset (come descritto in [questo](media-services-dotnet-configure-asset-delivery-policy.md) argomento) prima di creare un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="1e081-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="1e081-112">È inoltre possibile usare un localizzatore di streaming OnDemand per creare URL che puntano a file MP4 scaricabili in modo progressivo.</span><span class="sxs-lookup"><span data-stu-id="1e081-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="1e081-113">Questo argomento illustra come creare un localizzatore di streaming OnDemand, per pubblicare l'asset e creare URL di streaming Smooth, MPEG DASH e HLS,</span><span class="sxs-lookup"><span data-stu-id="1e081-113">This topic shows how to create an OnDemand streaming locator to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="1e081-114">e come creare URL di download progressivo.</span><span class="sxs-lookup"><span data-stu-id="1e081-114">It also shows hot to build progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="1e081-115">Creare un localizzatore di streaming OnDemand</span><span class="sxs-lookup"><span data-stu-id="1e081-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="1e081-116">Per creare un localizzatore di streaming OnDemand e ottenere gli URL, è necessario effettuare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1e081-116">To create the OnDemand streaming locator and get URLs, you need to do the following things:</span></span>

1. <span data-ttu-id="1e081-117">Se il contenuto viene crittografato, definire i criteri di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e081-117">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="1e081-118">Creare un localizzatore di streaming OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1e081-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="1e081-119">Se si pianifica lo streaming, ottenere il file manifesto di streaming (.ism) nell'asset.</span><span class="sxs-lookup"><span data-stu-id="1e081-119">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="1e081-120">Se si pianifica il download progressivo, ottenere i nomi dei file MP4 nell'asset.</span><span class="sxs-lookup"><span data-stu-id="1e081-120">If you plan to progressively download, get the names of MP4 files in the asset.</span></span>  
4. <span data-ttu-id="1e081-121">Creare URL che puntano al file manifesto o ai file MP4.</span><span class="sxs-lookup"><span data-stu-id="1e081-121">Build URLs to the manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="1e081-122">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="1e081-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="1e081-123">Se si usano sempre gli stessi giorni/autorizzazioni di accesso, usare lo stesso ID criterio.</span><span class="sxs-lookup"><span data-stu-id="1e081-123">Use the same policy ID if you are always using the same days / access permissions.</span></span> <span data-ttu-id="1e081-124">Ad esempio, i criteri dei localizzatori che devono rimanere sul posto per molto tempo (criteri di non-caricamento).</span><span class="sxs-lookup"><span data-stu-id="1e081-124">For example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="1e081-125">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="1e081-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="1e081-126">Usare l'SDK di Servizi multimediali per .NET</span><span class="sxs-lookup"><span data-stu-id="1e081-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="1e081-127">Creare URL di streaming</span><span class="sxs-lookup"><span data-stu-id="1e081-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator to the streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference to the streaming manifest file from the  
        // collection of files in the asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL to the manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL to manifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL to manifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL to manifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="1e081-128">Gli output:</span><span class="sxs-lookup"><span data-stu-id="1e081-128">The outputs:</span></span>

    URL to manifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL to manifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL to manifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="1e081-129">Lo streaming dei contenuti può essere eseguito anche tramite una connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="1e081-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="1e081-130">A questo scopo, verificare che gli URL di streaming inizino con HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1e081-130">To do this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="1e081-131">Attualmente AMS non supporta SSL con domini personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1e081-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="1e081-132">Creare URL di download progressivo</span><span class="sxs-lookup"><span data-stu-id="1e081-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator to the asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL to the MP4 files. Use this to progressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="1e081-133">Gli output:</span><span class="sxs-lookup"><span data-stu-id="1e081-133">The outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="1e081-134">Usare le estensioni dell'SDK di Servizi multimediali per .NET</span><span class="sxs-lookup"><span data-stu-id="1e081-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="1e081-135">Il codice seguente chiama i metodi delle estensioni dell'SDK per .NET che creano un localizzatore e generano URL Smooth Streaming, HLS e MPEG-DASH per lo streaming adattivo.</span><span class="sxs-lookup"><span data-stu-id="1e081-135">The following code calls .NET SDK extensions methods that create a locator and generate the Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get the streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="1e081-136">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1e081-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1e081-137">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1e081-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1e081-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e081-138">Next steps</span></span>
* [<span data-ttu-id="1e081-139">Scaricare gli asset</span><span class="sxs-lookup"><span data-stu-id="1e081-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="1e081-140">Configurare i criteri di distribuzione dell'asset</span><span class="sxs-lookup"><span data-stu-id="1e081-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

