---
title: il contenuto di servizi multimediali di Azure aaaPublish usando .NET | Documenti Microsoft
description: Informazioni su come toocreate un indicatore di posizione toobuild usato un URL di streaming. Esempi di codice sono scritti in c# e utilizzano hello Media Services SDK per .NET.
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
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="a79f9-104">Pubblicare contenuti di Servizi multimediali di Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="a79f9-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a79f9-105">REST</span><span class="sxs-lookup"><span data-stu-id="a79f9-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="a79f9-106">.NET</span><span class="sxs-lookup"><span data-stu-id="a79f9-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="a79f9-107">Portale</span><span class="sxs-lookup"><span data-stu-id="a79f9-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a79f9-108">Overview</span><span class="sxs-lookup"><span data-stu-id="a79f9-108">Overview</span></span>
<span data-ttu-id="a79f9-109">È possibile trasmettere in streaming un set MP4 a velocità in bit adattiva creando un localizzatore di streaming OnDemand e un URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="a79f9-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="a79f9-110">Hello [codifica un asset](media-services-encode-asset.md) argomento viene illustrato come imposta di tooencode in un file MP4 a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="a79f9-110">hello [encoding an asset](media-services-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="a79f9-111">Se il contenuto è crittografato, configurare i criteri di distribuzione degli asset (come descritto in [questo](media-services-dotnet-configure-asset-delivery-policy.md) argomento) prima di creare un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="a79f9-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="a79f9-112">È possibile utilizzare anche un OnDemand localizzatore toobuild URL tooMP4 punto che i file che possono essere scaricati progressivamente di streaming.</span><span class="sxs-lookup"><span data-stu-id="a79f9-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="a79f9-113">Questo argomento viene illustrato come toocreate un OnDemand toopublish localizzatore di streaming, l'asset e compilare un formato Smooth Streaming, MPEG DASH e HLS gli URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="a79f9-113">This topic shows how toocreate an OnDemand streaming locator toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="a79f9-114">Viene inoltre gli URL di download progressivo toobuild a caldo.</span><span class="sxs-lookup"><span data-stu-id="a79f9-114">It also shows hot toobuild progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="a79f9-115">Creare un localizzatore di streaming OnDemand</span><span class="sxs-lookup"><span data-stu-id="a79f9-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="a79f9-116">toocreate hello localizzatore di streaming OnDemand e ottenere l'URL, è necessario hello toodo seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="a79f9-116">toocreate hello OnDemand streaming locator and get URLs, you need toodo hello following things:</span></span>

1. <span data-ttu-id="a79f9-117">Hello contenuto crittografato, è possibile definire un criterio di accesso.</span><span class="sxs-lookup"><span data-stu-id="a79f9-117">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="a79f9-118">Creare un localizzatore di streaming OnDemand.</span><span class="sxs-lookup"><span data-stu-id="a79f9-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="a79f9-119">Se si prevede di toostream, ottenere il flusso di file manifesto (ISM) nel asset hello hello.</span><span class="sxs-lookup"><span data-stu-id="a79f9-119">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="a79f9-120">Se si prevede di download tooprogressively, ottenere i nomi di hello di file MP4 in asset hello.</span><span class="sxs-lookup"><span data-stu-id="a79f9-120">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span>  
4. <span data-ttu-id="a79f9-121">Compilare i file MP4 o file di manifesto toohello URL.</span><span class="sxs-lookup"><span data-stu-id="a79f9-121">Build URLs toohello manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="a79f9-122">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a79f9-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a79f9-123">Utilizzare hello stesso ID criteri se si utilizza sempre hello stesso giorni / le autorizzazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="a79f9-123">Use hello same policy ID if you are always using hello same days / access permissions.</span></span> <span data-ttu-id="a79f9-124">Ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="a79f9-124">For example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a79f9-125">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="a79f9-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="a79f9-126">Usare l'SDK di Servizi multimediali per .NET</span><span class="sxs-lookup"><span data-stu-id="a79f9-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="a79f9-127">Creare URL di streaming</span><span class="sxs-lookup"><span data-stu-id="a79f9-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="a79f9-128">output di Hello:</span><span class="sxs-lookup"><span data-stu-id="a79f9-128">hello outputs:</span></span>

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="a79f9-129">Lo streaming dei contenuti può essere eseguito anche tramite una connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="a79f9-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="a79f9-130">toodo questo approccio, assicurarsi che l'URL di streaming inizino con HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a79f9-130">toodo this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="a79f9-131">Attualmente AMS non supporta SSL con domini personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a79f9-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="a79f9-132">Creare URL di download progressivo</span><span class="sxs-lookup"><span data-stu-id="a79f9-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="a79f9-133">output di Hello:</span><span class="sxs-lookup"><span data-stu-id="a79f9-133">hello outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="a79f9-134">Usare le estensioni dell'SDK di Servizi multimediali per .NET</span><span class="sxs-lookup"><span data-stu-id="a79f9-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="a79f9-135">Hello codice seguente viene chiamato i metodi di estensione .NET SDK che creano un localizzatore e generano l'URL di MPEG-DASH, HLS e Smooth Streaming hello per streaming adattivo.</span><span class="sxs-lookup"><span data-stu-id="a79f9-135">hello following code calls .NET SDK extensions methods that create a locator and generate hello Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="a79f9-136">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a79f9-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a79f9-137">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="a79f9-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a79f9-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a79f9-138">Next steps</span></span>
* [<span data-ttu-id="a79f9-139">Scaricare gli asset</span><span class="sxs-lookup"><span data-stu-id="a79f9-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="a79f9-140">Configurare i criteri di distribuzione dell'asset</span><span class="sxs-lookup"><span data-stu-id="a79f9-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

