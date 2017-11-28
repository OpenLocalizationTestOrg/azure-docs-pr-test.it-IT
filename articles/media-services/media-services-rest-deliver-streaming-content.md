---
title: contenuto di servizi multimediali di Azure aaaPublish tramite REST
description: Informazioni su come toocreate un indicatore di posizione toobuild usato un URL di streaming. codice Hello viene utilizzata l'API REST.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: f849e21b3103b9b33bc652e886b2016ea495b19a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="b01b4-104">Pubblicare contenuti di Servizi multimediali di Azure mediante REST</span><span class="sxs-lookup"><span data-stu-id="b01b4-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b01b4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b01b4-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="b01b4-106">REST</span><span class="sxs-lookup"><span data-stu-id="b01b4-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="b01b4-107">Portale</span><span class="sxs-lookup"><span data-stu-id="b01b4-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="b01b4-108">Overview</span><span class="sxs-lookup"><span data-stu-id="b01b4-108">Overview</span></span>
<span data-ttu-id="b01b4-109">È possibile trasmettere in streaming un set MP4 a velocità in bit adattiva creando un localizzatore di streaming OnDemand e un URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="b01b4-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="b01b4-110">Hello [codifica un asset](media-services-rest-encode-asset.md) argomento viene illustrato come imposta di tooencode in un file MP4 a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="b01b4-110">hello [encoding an asset](media-services-rest-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="b01b4-111">Se il contenuto è crittografato, configurare i criteri di distribuzione degli asset (come descritto in [questo](media-services-rest-configure-asset-delivery-policy.md) argomento) prima di creare un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="b01b4-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="b01b4-112">È possibile utilizzare anche un OnDemand localizzatore toobuild URL tooMP4 punto che i file che possono essere scaricati progressivamente di streaming.</span><span class="sxs-lookup"><span data-stu-id="b01b4-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="b01b4-113">In questo argomento viene illustrato toocreate un localizzatore di streaming OnDemand in ordine toopublish l'asset e creare un formato Smooth Streaming, MPEG DASH e HLS gli URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="b01b4-113">This topic shows how toocreate an OnDemand streaming locator in order toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="b01b4-114">Viene inoltre gli URL di download progressivo toobuild a caldo.</span><span class="sxs-lookup"><span data-stu-id="b01b4-114">It also shows hot toobuild progressive download URLs.</span></span>

<span data-ttu-id="b01b4-115">Hello [seguente](#types) sezione Mostra hello tipi enum i cui valori vengono utilizzati nelle chiamate REST hello.</span><span class="sxs-lookup"><span data-stu-id="b01b4-115">hello [following](#types) section shows hello enum types whose values are used in hello REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="b01b4-116">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="b01b4-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="b01b4-117">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b01b4-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="b01b4-118">Connessione dei servizi tooMedia</span><span class="sxs-lookup"><span data-stu-id="b01b4-118">Connect tooMedia Services</span></span>

<span data-ttu-id="b01b4-119">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b01b4-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="b01b4-120">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b01b4-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="b01b4-121">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="b01b4-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="b01b4-122">Creare un localizzatore di streaming OnDemand</span><span class="sxs-lookup"><span data-stu-id="b01b4-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="b01b4-123">toocreate hello localizzatore di streaming OnDemand e ottenere l'URL è necessario hello toodo seguenti:</span><span class="sxs-lookup"><span data-stu-id="b01b4-123">toocreate hello OnDemand streaming locator and get URLs you need toodo hello following:</span></span>

1. <span data-ttu-id="b01b4-124">Hello contenuto crittografato, è possibile definire un criterio di accesso.</span><span class="sxs-lookup"><span data-stu-id="b01b4-124">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="b01b4-125">Creare un localizzatore di streaming OnDemand.</span><span class="sxs-lookup"><span data-stu-id="b01b4-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="b01b4-126">Se si prevede di toostream, ottenere il flusso di file manifesto (ISM) nel asset hello hello.</span><span class="sxs-lookup"><span data-stu-id="b01b4-126">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="b01b4-127">Se si prevede di download tooprogressively, ottenere i nomi di hello di file MP4 in asset hello.</span><span class="sxs-lookup"><span data-stu-id="b01b4-127">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span> 
4. <span data-ttu-id="b01b4-128">Compilare i file MP4 o file di manifesto toohello URL.</span><span class="sxs-lookup"><span data-stu-id="b01b4-128">Build URLs toohello manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="b01b4-129">Si noti che non è possibile creare un localizzatore di streaming utilizzando un criterio di accesso che include autorizzazioni alla scrittura o all’eliminazione.</span><span class="sxs-lookup"><span data-stu-id="b01b4-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="b01b4-130">Creare i criteri di accesso</span><span class="sxs-lookup"><span data-stu-id="b01b4-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="b01b4-131">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="b01b4-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="b01b4-132">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="b01b4-132">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="b01b4-133">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="b01b4-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="b01b4-134">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b01b4-134">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="b01b4-135">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b01b4-135">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="b01b4-136">Creare un localizzatore di streaming OnDemand</span><span class="sxs-lookup"><span data-stu-id="b01b4-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="b01b4-137">Creazione localizzatore hello per asset specificato hello e criteri di asset.</span><span class="sxs-lookup"><span data-stu-id="b01b4-137">Create hello locator for hello specified asset and asset policy.</span></span>

<span data-ttu-id="b01b4-138">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b01b4-138">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="b01b4-139">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b01b4-139">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="b01b4-140">Creare URL di streaming</span><span class="sxs-lookup"><span data-stu-id="b01b4-140">Build streaming URLs</span></span>
<span data-ttu-id="b01b4-141">Hello utilizzare **percorso** valore restituito dopo la creazione di hello di hello toobuild di hello localizzatore URL di MPEG DASH, HLS e Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="b01b4-141">Use hello **Path** value returned after hello creation of hello locator toobuild hello Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="b01b4-142">Smooth Streaming: **Path** + nome file manifesto + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="b01b4-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="b01b4-143">esempio:</span><span class="sxs-lookup"><span data-stu-id="b01b4-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="b01b4-144">HLS: **Path** + nome file manifesto + "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="b01b4-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="b01b4-145">esempio:</span><span class="sxs-lookup"><span data-stu-id="b01b4-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="b01b4-146">DASH: **Path** + nome file manifesto + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="b01b4-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="b01b4-147">esempio:</span><span class="sxs-lookup"><span data-stu-id="b01b4-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="b01b4-148">Creare URL di download progressivo</span><span class="sxs-lookup"><span data-stu-id="b01b4-148">Build progressive download URLs</span></span>
<span data-ttu-id="b01b4-149">Hello utilizzare **percorso** valore restituito dopo la creazione di hello dell'URL di download progressivo hello toobuild locator hello.</span><span class="sxs-lookup"><span data-stu-id="b01b4-149">Use hello **Path** value returned after hello creation of hello locator toobuild hello progressive download URL.</span></span>   

<span data-ttu-id="b01b4-150">URL: **Path** + nome file mp4 asset</span><span class="sxs-lookup"><span data-stu-id="b01b4-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="b01b4-151">esempio:</span><span class="sxs-lookup"><span data-stu-id="b01b4-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="b01b4-152"><a id="types"></a>Tipi enum</span><span class="sxs-lookup"><span data-stu-id="b01b4-152"><a id="types"></a>Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="b01b4-153">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b01b4-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b01b4-154">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b01b4-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="b01b4-155">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b01b4-155">See also</span></span>
[<span data-ttu-id="b01b4-156">Informazioni generali sull'API REST di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b01b4-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="b01b4-157">Configurare i criteri di distribuzione dell'asset</span><span class="sxs-lookup"><span data-stu-id="b01b4-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

