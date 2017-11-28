---
title: aaaGet avviato con la distribuzione di contenuti su richiesta tramite REST | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello dell'implementazione di un'applicazione di recapito del contenuto su richiesta con servizi multimediali di Azure tramite l'API REST.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="48814-103">Introduzione alla distribuzione di contenuti su richiesta usando REST</span><span class="sxs-lookup"><span data-stu-id="48814-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="48814-104">Questa Guida rapida illustra hello passaggi di implementazione di un'applicazione di distribuzione di contenuti video on Demand (VoD) tramite le API REST di servizi multimediali di Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="48814-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="48814-105">esercitazione Hello introduce hello base servizi multimediali del flusso di lavoro e gli oggetti di programmazione più comuni di hello e attività necessarie per lo sviluppo di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="48814-106">Al termine di hello di esercitazione hello, si verrà toostream in grado o un file multimediale di esempio che caricati, con codifica e scaricato il download progressivo.</span><span class="sxs-lookup"><span data-stu-id="48814-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="48814-107">Hello immagine seguente mostra alcuni degli oggetti hello più comunemente utilizzato quando si sviluppano applicazioni VoD sul modello di Media Services OData hello.</span><span class="sxs-lookup"><span data-stu-id="48814-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="48814-108">Fare clic su tooview immagine hello le dimensioni massime.</span><span class="sxs-lookup"><span data-stu-id="48814-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="48814-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="48814-109">Prerequisites</span></span>
<span data-ttu-id="48814-110">Hello prerequisiti seguenti sono necessari toostart allo sviluppo con servizi multimediali con le API REST.</span><span class="sxs-lookup"><span data-stu-id="48814-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="48814-111">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="48814-111">An Azure account.</span></span> <span data-ttu-id="48814-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48814-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="48814-113">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-113">A Media Services account.</span></span> <span data-ttu-id="48814-114">toocreate un account di servizi multimediali, vedere [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="48814-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="48814-115">Comprensione del concetto toodevelop con API REST di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="48814-116">Per altre informazioni, vedere [Informazioni generali sull'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="48814-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="48814-117">Un'applicazione di propria scelta per l'invio di richieste e risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="48814-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="48814-118">In questa esercitazione viene usato [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="48814-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="48814-119">Hello seguenti attività viene visualizzato in questa Guida rapida.</span><span class="sxs-lookup"><span data-stu-id="48814-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="48814-120">Avviare lo streaming di endpoint (tramite hello portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="48814-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="48814-121">Connettere l'account di servizi multimediali di toohello con l'API REST.</span><span class="sxs-lookup"><span data-stu-id="48814-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="48814-122">Creare un nuovo asset e caricare un file video con l'API REST.</span><span class="sxs-lookup"><span data-stu-id="48814-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="48814-123">Codificare il file di origine hello in un set di file MP4 a velocità in bit adattiva con l'API REST.</span><span class="sxs-lookup"><span data-stu-id="48814-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="48814-124">Pubblicare l'asset hello e get streaming e gli URL di download progressivo con l'API REST.</span><span class="sxs-lookup"><span data-stu-id="48814-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="48814-125">Riprodurre i contenuti.</span><span class="sxs-lookup"><span data-stu-id="48814-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="48814-126">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="48814-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="48814-127">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="48814-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="48814-128">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="48814-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="48814-129">Per altre informazioni sulle entità di REST AMS usate in questo argomento, vedere [Informazioni generali sull'API REST di Servizi multimediali](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="48814-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="48814-130">Vedere anche [Concetti relativi ai Servizi multimediali di Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="48814-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="48814-131">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="48814-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="48814-132">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="48814-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="48814-133">Avviare lo streaming di endpoint che utilizzano hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="48814-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="48814-134">Quando si lavora con uno degli scenari più comuni di hello recapita video tramite velocità in bit adattive servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="48814-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="48814-135">Servizi multimediali fornisce creazione dinamica dei pacchetti, che consente di toodeliver la velocità in bit adattiva contenuto MP4 in formato con codificata in streaming formati supportati da servizi multimediali (MPEG DASH, HLS, Smooth Streaming) just-in-time, senza che sia necessario toostore preconfezionata versioni di ciascuno di questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="48814-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="48814-136">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="48814-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="48814-137">lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="48814-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="48814-138">toostart hello endpoint di streaming, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="48814-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="48814-139">Accedere all'indirizzo hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="48814-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="48814-140">Nella finestra Impostazioni hello, fare clic su endpoint di Streaming.</span><span class="sxs-lookup"><span data-stu-id="48814-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="48814-141">Fare clic su predefinito hello endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="48814-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="48814-142">verrà visualizzata la finestra Dettagli dell'ENDPOINT di STREAMING predefinito Hello.</span><span class="sxs-lookup"><span data-stu-id="48814-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="48814-143">Fare clic sull'icona di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="48814-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="48814-144">Fare clic su toosave pulsante di hello Salva le modifiche.</span><span class="sxs-lookup"><span data-stu-id="48814-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="48814-145"><a id="connect"></a>Connettere l'account di servizi multimediali di toohello con l'API REST</span><span class="sxs-lookup"><span data-stu-id="48814-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="48814-146">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="48814-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="48814-147">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="48814-148">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="48814-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="48814-149">Ad esempio, se dopo aver tentato tooconnect, ottenuto dall'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="48814-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="48814-150">Si consiglia di pubblicare le successive toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ chiamate API.</span><span class="sxs-lookup"><span data-stu-id="48814-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="48814-151"><a id="upload"></a>Creare un nuovo asset e caricare un file video con l'API REST</span><span class="sxs-lookup"><span data-stu-id="48814-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="48814-152">In Servizi multimediali è possibile caricare i file digitali in un asset.</span><span class="sxs-lookup"><span data-stu-id="48814-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="48814-153">Hello **Asset** entità può contenere video, audio, immagini, raccolte di anteprime, testo tracce e sottotitoli file (e relativi metadati hello.)  Una volta caricati i file hello in asset hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso.</span><span class="sxs-lookup"><span data-stu-id="48814-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="48814-154">Uno dei valori di hello di aver tooprovide durante la creazione di un asset è opzioni di creazione di asset.</span><span class="sxs-lookup"><span data-stu-id="48814-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="48814-155">Hello **opzioni** proprietà è un valore di enumerazione che descrive le opzioni di crittografia hello che è possibile creare un Asset con.</span><span class="sxs-lookup"><span data-stu-id="48814-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="48814-156">Un valore valido è uno dei valori hello hello seguente elenco, non una combinazione di valori dell'elenco:</span><span class="sxs-lookup"><span data-stu-id="48814-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="48814-157">**None** = **0**: non viene usata alcuna crittografia.</span><span class="sxs-lookup"><span data-stu-id="48814-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="48814-158">Quando si usa questa opzione il contenuto non è protetto durante il transito, né nell'archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="48814-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="48814-159">Se si prevede di toodeliver un file MP4 tramite download progressivo, usare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="48814-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="48814-160">**StorageEncrypted** = **1** : consente di crittografare il contenuto non crittografato in locale utilizzando la crittografia AES a 256 bit e quindi lo carica tooAzure archiviazione dove viene archiviato in forma crittografata.</span><span class="sxs-lookup"><span data-stu-id="48814-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="48814-161">Gli asset protetti con crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file crittografato sistema precedente tooencoding e, facoltativamente, crittografare nuovamente toouploading precedente come nuovo asset di output.</span><span class="sxs-lookup"><span data-stu-id="48814-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="48814-162">Hello primario per la crittografia di archiviazione viene usata quando si desidera toosecure i file multimediali di input di alta qualità con la crittografia avanzata inattivi sul disco.</span><span class="sxs-lookup"><span data-stu-id="48814-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="48814-163">**CommonEncryptionProtected** = **2**: usare questa opzione per caricare contenuti già crittografati e protetti con Common Encryption o PlayReady DRM (ad esempio, Smooth Streaming protetto con PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="48814-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="48814-164">**EnvelopeEncryptionProtected** = **4**: usare questa opzione se si stanno caricando contenuti HLS crittografati con AES.</span><span class="sxs-lookup"><span data-stu-id="48814-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="48814-165">file Hello devono sono stati codificati e crittografati da Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="48814-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="48814-166">Creare un asset</span><span class="sxs-lookup"><span data-stu-id="48814-166">Create an asset</span></span>
<span data-ttu-id="48814-167">Un asset è un contenitore di più tipi o set di oggetti in Servizi multimediali, inclusi elementi video e audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli chiusi.</span><span class="sxs-lookup"><span data-stu-id="48814-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="48814-168">Nell'API REST, creazione di un Asset richiede l'invio di POST hello richiedere servizi tooMedia e inserire informazioni delle proprietà relative all'asset nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="48814-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="48814-169">Hello seguente esempio viene illustrato come toocreate un asset.</span><span class="sxs-lookup"><span data-stu-id="48814-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="48814-170">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="48814-171">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-171">**HTTP Response**</span></span>

<span data-ttu-id="48814-172">Se ha esito positivo, viene restituito l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="48814-172">If successful, hello following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="48814-173">Creare un'entità AssetFile</span><span class="sxs-lookup"><span data-stu-id="48814-173">Create an AssetFile</span></span>
<span data-ttu-id="48814-174">Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entità rappresenta un file video o audio che viene archiviato in un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="48814-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="48814-175">Un file di asset è sempre associato a un asset e un asset può contenere uno o più file.</span><span class="sxs-lookup"><span data-stu-id="48814-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="48814-176">attività di Media Services Encoder Hello non riesce se un oggetto di file di asset non è associato a un file digitale in un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="48814-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="48814-177">Dopo aver caricato il file multimediale digitale in un contenitore blob, utilizzare hello **MERGE** hello tooupdate HTTP richiesta AssetFile con le informazioni nel file multimediale (come illustrato più avanti nell'argomento hello).</span><span class="sxs-lookup"><span data-stu-id="48814-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="48814-178">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="48814-179">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-179">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="48814-180">Creazione di hello AccessPolicy con autorizzazioni di scrittura</span><span class="sxs-lookup"><span data-stu-id="48814-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="48814-181">Prima di caricare i file nell'archiviazione blob, impostare l'accesso hello diritti sui criteri per la scrittura di tooan asset.</span><span class="sxs-lookup"><span data-stu-id="48814-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="48814-182">Imposta toodo che, invia un toohello di richiesta HTTP entità AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="48814-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="48814-183">Definire un valore DurationInMinutes durante la creazione. In caso contrario, si riceverà il messaggio di errore interno 500 del server in risposta.</span><span class="sxs-lookup"><span data-stu-id="48814-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="48814-184">Per altre informazioni su AccessPolicies, vedere [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="48814-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="48814-185">Hello seguente esempio viene illustrato come un'entità AccessPolicy toocreate:</span><span class="sxs-lookup"><span data-stu-id="48814-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="48814-186">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="48814-187">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-187">**HTTP Response**</span></span>

<span data-ttu-id="48814-188">Se ha esito positivo, viene restituito hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="48814-188">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a><span data-ttu-id="48814-189">Ottenere hello caricare URL</span><span class="sxs-lookup"><span data-stu-id="48814-189">Get hello Upload URL</span></span>

<span data-ttu-id="48814-190">tooreceive hello URL di caricamento effettivo, creare un localizzatore SAS.</span><span class="sxs-lookup"><span data-stu-id="48814-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="48814-191">I localizzatori definiscono l'ora di inizio hello e il tipo di endpoint di connessione per i client che desidera tooaccess i file in un Asset.</span><span class="sxs-lookup"><span data-stu-id="48814-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="48814-192">È possibile creare più entità Locator per un determinato AccessPolicy e Asset coppia toohandle diversi client richieste e alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="48814-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="48814-193">Ogni localizzatore Usa i valori di StartTime hello e DurationInMinutes di hello di hello AccessPolicy toodetermine hello periodo di tempo che è possibile utilizzare un URL.</span><span class="sxs-lookup"><span data-stu-id="48814-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="48814-194">Per altre informazioni, vedere [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="48814-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="48814-195">Un URL SAS è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="48814-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="48814-196">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="48814-196">Some considerations apply:</span></span>

* <span data-ttu-id="48814-197">Non è possibile avere più di cinque localizzatori univoci associati contemporaneamente a un determinato asset.</span><span class="sxs-lookup"><span data-stu-id="48814-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="48814-198">Per altre informazioni, vedere Locator.</span><span class="sxs-lookup"><span data-stu-id="48814-198">For more information, see Locator.</span></span>
* <span data-ttu-id="48814-199">Se occorre tooupload i file immediatamente, è necessario impostare i minuti di toofive valore StartTime prima hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="48814-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="48814-200">Potrebbe infatti essere presente una leggera differenza di orario tra il computer client e Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="48814-201">Inoltre, il valore StartTime deve essere nel seguente formato DateTime hello: aaaa-MM-ddTHH (ad esempio, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="48814-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="48814-202">Potrebbe esserci un 30-40 secondi ritardare dopo la creazione di un indicatore di posizione toowhen è disponibile per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="48814-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="48814-203">Questo problema si applica tooboth URL SAS e localizzatori di origine.</span><span class="sxs-lookup"><span data-stu-id="48814-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="48814-204">Per altre informazioni sui localizzatori della firma di accesso condiviso, vedere [questo](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="48814-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="48814-205">Hello di esempio seguente viene illustrato come un localizzatore URL SAS, come definito da toocreate hello proprietà del tipo nel corpo della richiesta hello ("1" per un localizzatore SAS) e "2" per un localizzatore di origine su richiesta.</span><span class="sxs-lookup"><span data-stu-id="48814-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="48814-206">Hello **percorso** proprietà restituita contiene hello URL che è necessario utilizzare tooupload il file.</span><span class="sxs-lookup"><span data-stu-id="48814-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="48814-207">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="48814-208">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-208">**HTTP Response**</span></span>

<span data-ttu-id="48814-209">Se ha esito positivo, viene restituito hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="48814-209">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="48814-210">Caricare un file in un contenitore di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="48814-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="48814-211">Dopo aver creato AccessPolicy hello e set di localizzazione, file effettivo hello è contenitore di archiviazione blob di Azure caricati tooan utilizzando hello API REST dell'archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="48814-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="48814-212">È necessario caricare il file hello come BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="48814-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="48814-213">I BLOB di pagine non sono supportati da Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="48814-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="48814-214">È necessario aggiungere il nome di file hello per file hello desiderato tooupload toohello localizzatore **percorso** valore ricevuto nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="48814-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="48814-215">Ad esempio, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="48814-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="48814-216">.</span><span class="sxs-lookup"><span data-stu-id="48814-216">.</span></span> <span data-ttu-id="48814-217">.</span><span class="sxs-lookup"><span data-stu-id="48814-217">.</span></span> <span data-ttu-id="48814-218">.</span><span class="sxs-lookup"><span data-stu-id="48814-218">.</span></span>
>
>

<span data-ttu-id="48814-219">Per altre informazioni sull'uso dei BLOB di Archiviazione di Azure, vedere [API REST del servizio BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="48814-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="48814-220">Aggiornare hello AssetFile</span><span class="sxs-lookup"><span data-stu-id="48814-220">Update hello AssetFile</span></span>
<span data-ttu-id="48814-221">Ora che è stato caricato il file, è possibile aggiornare le informazioni di FileAsset dimensioni (e altri) hello.</span><span class="sxs-lookup"><span data-stu-id="48814-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="48814-222">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="48814-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="48814-223">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-223">**HTTP Response**</span></span>

<span data-ttu-id="48814-224">Se ha esito positivo, viene restituito l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="48814-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="48814-225">Eliminare hello localizzatore e AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="48814-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="48814-226">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="48814-227">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-227">**HTTP Response**</span></span>

<span data-ttu-id="48814-228">Se ha esito positivo, viene restituito l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="48814-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="48814-229">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="48814-230">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-230">**HTTP Response**</span></span>

<span data-ttu-id="48814-231">Se ha esito positivo, viene restituito l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="48814-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="48814-232"><a id="encode"></a>Codificare il file di origine hello in un set di file MP4 a velocità in bit adattiva</span><span class="sxs-lookup"><span data-stu-id="48814-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="48814-233">Dopo l'inserimento di che asset in servizi multimediali, i supporti possono essere codificati, transmux filigrana e così via, prima che esso venga recapitato tooclients.</span><span class="sxs-lookup"><span data-stu-id="48814-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="48814-234">Queste attività vengono pianificate e vengono eseguite più background ruolo istanze tooensure ad alte prestazioni e disponibilità.</span><span class="sxs-lookup"><span data-stu-id="48814-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="48814-235">Queste attività sono denominate processi e ogni processo è costituito da attività atomiche che hello operazioni effettive sul file di Asset hello (per ulteriori informazioni, vedere [processo](/rest/api/media/services/job), [attività](/rest/api/media/services/task) descrizioni).</span><span class="sxs-lookup"><span data-stu-id="48814-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="48814-236">Come accennato in precedenza, quando l'utilizzo di servizi multimediali di Azure uno degli scenari più comuni di hello recapita velocità in bit adattive tooyour client.</span><span class="sxs-lookup"><span data-stu-id="48814-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="48814-237">Servizi multimediali può pacchetto in modo dinamico un set di file MP4 a velocità in bit adattiva in uno dei seguenti formati hello: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="48814-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="48814-238">Hello seguente sezione viene illustrato come toocreate un processo che contiene una codifica attività.</span><span class="sxs-lookup"><span data-stu-id="48814-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="48814-239">Hello attività specifica tootranscode hello in formato intermedio in file in un set di velocità in bit adattiva MP4s utilizzando **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="48814-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="48814-240">sezione di Hello viene inoltre illustrato come toomonitor hello avanzamento l'elaborazione del processo.</span><span class="sxs-lookup"><span data-stu-id="48814-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="48814-241">Una volta completato il processo di hello, sarebbe toocreate in grado di localizzatori che sono necessari tooget accesso tooyour asset.</span><span class="sxs-lookup"><span data-stu-id="48814-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="48814-242">Ottenere un processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-242">Get a media processor</span></span>
<span data-ttu-id="48814-243">In Servizi multimediali un processore di contenuti multimediali è un componente che gestisce un'attività di elaborazione specifica, ad esempio la codifica, la conversione del formato, la crittografia o la decrittografia di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="48814-244">Per hello codifica attività visualizzate in questa esercitazione, verrà hello toouse Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="48814-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="48814-245">id del codificatore hello le richieste di codice seguente di Hello.</span><span class="sxs-lookup"><span data-stu-id="48814-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="48814-246">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="48814-247">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="48814-248">Creare un processo</span><span class="sxs-lookup"><span data-stu-id="48814-248">Create a job</span></span>
<span data-ttu-id="48814-249">Ogni processo può avere uno o più attività in base al tipo di hello di elaborazione che si desidera tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="48814-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="48814-250">Tramite hello API REST, è possibile creare processi e le attività correlate in uno dei due modi: le attività possono essere definite inline tramite la proprietà di navigazione attività hello in entità Job oppure tramite l'elaborazione batch OData.</span><span class="sxs-lookup"><span data-stu-id="48814-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="48814-251">Hello Media Services SDK utilizza l'elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="48814-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="48814-252">Tuttavia, per migliorare la leggibilità hello hello gli esempi di codice in questo argomento, attività sono definite inline.</span><span class="sxs-lookup"><span data-stu-id="48814-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="48814-253">Per informazioni sull'elaborazione batch, vedere l'articolo relativo all' [elaborazione batch OData (Open Data Protocol)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="48814-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="48814-254">Hello di esempio seguente vengono visualizzati è come toocreate e post un processo con una sola attività tooencode un video a una risoluzione specifico e di qualità.</span><span class="sxs-lookup"><span data-stu-id="48814-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="48814-255">Hello seguendo una sezione di documentazione contiene l'elenco di hello di hello tutti [attività predefiniti](http://msdn.microsoft.com/library/mt269960) supportate dal processore Media Encoder Standard hello.</span><span class="sxs-lookup"><span data-stu-id="48814-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="48814-256">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="48814-257">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-257">**HTTP Response**</span></span>

<span data-ttu-id="48814-258">Se ha esito positivo, viene restituito hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="48814-258">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="48814-259">Esistono alcuni aspetti importanti toonote in una richiesta di processo:</span><span class="sxs-lookup"><span data-stu-id="48814-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="48814-260">Proprietà TaskBody devono usare numero hello toodefine letterale XML di input o di asset di output usati da attività hello.</span><span class="sxs-lookup"><span data-stu-id="48814-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="48814-261">argomento di attività Hello contiene hello definizione dello Schema XML per hello XML.</span><span class="sxs-lookup"><span data-stu-id="48814-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="48814-262">In definizione TaskBody hello, valore di ogni interna di <inputAsset> e <outputAsset> deve essere impostato come JobInputAsset(value) o JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="48814-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="48814-263">Un'attività può avere più asset di output.</span><span class="sxs-lookup"><span data-stu-id="48814-263">A task can have multiple output assets.</span></span> <span data-ttu-id="48814-264">Un oggetto JobOutputAsset(x) può essere usato solo una volta come output di un'attività in un processo.</span><span class="sxs-lookup"><span data-stu-id="48814-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="48814-265">È possibile specificare JobInputAsset o JobOutputAsset come asset di input di un'attività.</span><span class="sxs-lookup"><span data-stu-id="48814-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="48814-266">Le attività non devono formare un ciclo.</span><span class="sxs-lookup"><span data-stu-id="48814-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="48814-267">il parametro di valore Hello passato tooJobInputAsset o JobOutputAsset rappresenta il valore di indice hello per un Asset.</span><span class="sxs-lookup"><span data-stu-id="48814-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="48814-268">Hello asset effettivi vengono definiti nelle proprietà di navigazione InputMediaAssets e OutputMediaAssets di hello sull'hello definizione entità del processo.</span><span class="sxs-lookup"><span data-stu-id="48814-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="48814-269">Poiché servizi multimediali si basa su OData versione 3, hello ai singoli asset nelle InputMediaAssets e OutputMediaAssets raccolte di proprietà di navigazione vengono fatto riferimento tramite un " Metadata: uri" coppia nome-valore.</span><span class="sxs-lookup"><span data-stu-id="48814-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="48814-270">Proprietà InputMediaAssets è mappata tooone o più asset creati in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="48814-271">OutputMediaAssets vengono create dal sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="48814-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="48814-272">Non fanno riferimento a un asset esistente.</span><span class="sxs-lookup"><span data-stu-id="48814-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="48814-273">Può essere denominato OutputMediaAssets utilizzando l'attributo assetName hello.</span><span class="sxs-lookup"><span data-stu-id="48814-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="48814-274">Se questo attributo non è presente, il nome di hello di hello Outputmediaassets indipendentemente dal valore di testo interno hello di hello <outputAsset> elemento è con un suffisso del valore del nome di processo hello o valore di Id di processo hello (in caso di hello in hello Nome proprietà non è definita).</span><span class="sxs-lookup"><span data-stu-id="48814-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="48814-275">Ad esempio, se si imposta un valore per assetName troppo "Sample", quindi è necessario impostare la proprietà Name di Outputmediaassets hello troppo "Sample".</span><span class="sxs-lookup"><span data-stu-id="48814-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="48814-276">Tuttavia, se non si ha impostato un valore per assetName ma è stato impostato il nome di processo hello troppo "NewJob", quindi hello Name di Outputmediaassets sarebbe "JobOutputAsset (valore) newjob".</span><span class="sxs-lookup"><span data-stu-id="48814-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="48814-277">Hello di esempio seguente viene illustrato come tooset hello attributo assetName:</span><span class="sxs-lookup"><span data-stu-id="48814-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="48814-278">tooenable concatenamenti di attività:</span><span class="sxs-lookup"><span data-stu-id="48814-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="48814-279">Un processo deve avere almeno due attività</span><span class="sxs-lookup"><span data-stu-id="48814-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="48814-280">Deve esserci almeno un'attività il cui input è l'output di un'altra attività nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="48814-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="48814-281">Per ulteriori informazioni, vedere [creazione di un processo di codifica con hello API REST di servizi multimediali](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="48814-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="48814-282">Monitorare lo stato di avanzamento dell'elaborazione</span><span class="sxs-lookup"><span data-stu-id="48814-282">Monitor Processing Progress</span></span>
<span data-ttu-id="48814-283">È possibile recuperare lo stato del processo hello utilizzando la proprietà State hello, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="48814-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="48814-284">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="48814-285">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-285">**HTTP Response**</span></span>

<span data-ttu-id="48814-286">Se ha esito positivo, viene restituito hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="48814-286">If successful, hello following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="48814-287">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="48814-287">Cancel a job</span></span>
<span data-ttu-id="48814-288">Servizi multimediali consente toocancel processi in esecuzione tramite hello funzione CancelJob.</span><span class="sxs-lookup"><span data-stu-id="48814-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="48814-289">Questa chiamata restituisce un codice di 400 errore se si tenta di toocancel un processo quando lo stato è annullato, annullamento, errore o terminato.</span><span class="sxs-lookup"><span data-stu-id="48814-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="48814-290">Hello seguente esempio viene illustrato come toocall CancelJob.</span><span class="sxs-lookup"><span data-stu-id="48814-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="48814-291">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="48814-292">Se l'esito è positivo, viene restituito un codice di risposta 204 senza il corpo di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="48814-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="48814-293">È necessario applicare la codifica URL id processo hello (in genere jid: somevalue) quando viene passato come un parametro tooCancelJob.</span><span class="sxs-lookup"><span data-stu-id="48814-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="48814-294">Ottenere l'asset di output di hello</span><span class="sxs-lookup"><span data-stu-id="48814-294">Get hello output asset</span></span>
<span data-ttu-id="48814-295">Hello codice seguente viene illustrato come l'output di hello toorequest ID dell'asset.</span><span class="sxs-lookup"><span data-stu-id="48814-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="48814-296">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="48814-297">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="48814-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="48814-298"><a id="publish_get_urls"></a>Pubblicare l'asset hello e get streaming e gli URL di download progressivo con l'API REST</span><span class="sxs-lookup"><span data-stu-id="48814-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="48814-299">toostream o scarica un asset, è innanzitutto necessario troppo "pubblicarlo" tramite la creazione di un indicatore di posizione.</span><span class="sxs-lookup"><span data-stu-id="48814-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="48814-300">I localizzatori forniscono accesso toofiles contenuti in hello asset.</span><span class="sxs-lookup"><span data-stu-id="48814-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="48814-301">Servizi multimediali sono supportati due tipi di localizzatori: OnDemandOrigin localizzatori, supporto toostream utilizzato (ad esempio, MPEG DASH, HLS o Smooth Streaming) e localizzatori di firma di accesso (SAS), utilizzato file multimediali toodownload.</span><span class="sxs-lookup"><span data-stu-id="48814-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="48814-302">Per altre informazioni sui localizzatori della firma di accesso condiviso, vedere [questo](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="48814-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="48814-303">Dopo aver creato i localizzatori hello, è possibile compilare hello URL vengono utilizzati toostream o scaricare i file.</span><span class="sxs-lookup"><span data-stu-id="48814-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="48814-304">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="48814-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="48814-305">lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="48814-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="48814-306">Un URL di streaming per Smooth Streaming è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="48814-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="48814-307">Un URL di streaming per HLS è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="48814-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="48814-308">Un URL di streaming per MPEG DASH è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="48814-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="48814-309">Un file toodownload URL SAS usato è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="48814-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="48814-310">In questa sezione viene illustrato come tooperform hello seguenti attività necessarie troppo asset "pubblica".</span><span class="sxs-lookup"><span data-stu-id="48814-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="48814-311">Creazione di hello AccessPolicy con autorizzazioni di lettura</span><span class="sxs-lookup"><span data-stu-id="48814-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="48814-312">Creazione di un URL di firma di accesso condiviso per il download di contenuti</span><span class="sxs-lookup"><span data-stu-id="48814-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="48814-313">Creazione di un URL di origine per la trasmissione di contenuti in streaming</span><span class="sxs-lookup"><span data-stu-id="48814-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="48814-314">Creazione di hello AccessPolicy con autorizzazioni di lettura</span><span class="sxs-lookup"><span data-stu-id="48814-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="48814-315">Prima di scaricare o lo streaming di contenuto multimediale, innanzitutto definire un'entità AccessPolicy con autorizzazioni di lettura e creare entità Locator appropriata hello che specifica il tipo di hello del meccanismo di recapito si desidera tooenable per i client.</span><span class="sxs-lookup"><span data-stu-id="48814-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="48814-316">Per ulteriori informazioni sulle proprietà hello disponibili, vedere [proprietà dell'entità AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="48814-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="48814-317">Hello di esempio seguente viene illustrato come toospecify hello AccessPolicy per le autorizzazioni di lettura per un determinato Asset.</span><span class="sxs-lookup"><span data-stu-id="48814-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="48814-318">Se ha esito positivo, viene restituito un codice di 201 riuscita che descrivono entità AccessPolicy hello creato.</span><span class="sxs-lookup"><span data-stu-id="48814-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="48814-319">È quindi possibile utilizzare hello Id di AccessPolicy insieme hello Id Asset di hello che contiene file hello da entità Locator di hello toocreate toodeliver (ad esempio un asset di output).</span><span class="sxs-lookup"><span data-stu-id="48814-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="48814-320">Questo flusso di lavoro di base è hello come caricare un file durante l'inserimento di un Asset (come illustrato in precedenza in questo argomento).</span><span class="sxs-lookup"><span data-stu-id="48814-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="48814-321">Inoltre, come per il caricamento file, se l'utente (o i client) necessario tooaccess i file immediatamente, impostare i minuti di toofive valore StartTime prima hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="48814-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="48814-322">Questa azione è necessaria perché potrebbero essere presenti clock sfasamento di orario tra il client hello e di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="48814-323">Hello valore StartTime deve essere nel seguente formato DateTime hello: aaaa-MM-ddTHH (ad esempio, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="48814-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="48814-324">Creazione di un URL di firma di accesso condiviso per il download di contenuti</span><span class="sxs-lookup"><span data-stu-id="48814-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="48814-325">Hello seguente codice mostra come tooget un URL che può essere utilizzati toodownload un file multimediale creato e caricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="48814-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="48814-326">Hello AccessPolicy dispone di autorizzazioni di lettura impostate e percorso del localizzatore hello fa riferimento l'URL di download tooa SAS.</span><span class="sxs-lookup"><span data-stu-id="48814-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="48814-327">Se ha esito positivo, viene restituito hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="48814-327">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="48814-328">Hello restituito **percorso** proprietà contiene hello URL SAS.</span><span class="sxs-lookup"><span data-stu-id="48814-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="48814-329">Se si scarica il contenuto crittografato di archiviazione, è necessario decrittografarlo prima di eseguirne il rendering manualmente o utilizzare hello MediaProcessor la decrittografia di archiviazione in un toooutput di attività di elaborazione elaborato i file in tooan crittografato hello OutputAsset e quindi scaricare da tale Asset.</span><span class="sxs-lookup"><span data-stu-id="48814-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="48814-330">Per ulteriori informazioni sull'elaborazione, vedere Creazione di un processo di codifica con hello API REST di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="48814-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="48814-331">Inoltre, i localizzatori URL di firma di accesso condiviso non possono essere aggiornati dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="48814-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="48814-332">Ad esempio, non è possibile riutilizzare hello stesso localizzatore con un valore StartTime aggiornato.</span><span class="sxs-lookup"><span data-stu-id="48814-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="48814-333">Ciò è dovuto al modo hello che vengono creati gli URL di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="48814-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="48814-334">Se si vuole tooaccess un asset per il download dopo un localizzatore è scaduto, è necessario creare uno nuovo con un nuovo valore StartTime.</span><span class="sxs-lookup"><span data-stu-id="48814-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="48814-335">Download dei file</span><span class="sxs-lookup"><span data-stu-id="48814-335">Download files</span></span>
<span data-ttu-id="48814-336">Dopo aver creato AccessPolicy hello e set di localizzazione, è possibile scaricare file utilizzando hello API REST dell'archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="48814-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="48814-337">È necessario aggiungere il nome di file hello per file hello desiderato toodownload toohello localizzatore **percorso** valore ricevuto nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="48814-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="48814-338">Ad esempio, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="48814-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="48814-339">.</span><span class="sxs-lookup"><span data-stu-id="48814-339">.</span></span> <span data-ttu-id="48814-340">.</span><span class="sxs-lookup"><span data-stu-id="48814-340">.</span></span> <span data-ttu-id="48814-341">.</span><span class="sxs-lookup"><span data-stu-id="48814-341">.</span></span>
>
>

<span data-ttu-id="48814-342">Per altre informazioni sull'uso dei BLOB di Archiviazione di Azure, vedere [API REST del servizio BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="48814-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="48814-343">In seguito a hello codifica processo eseguito in precedenza (codifica in formato adattivo MP4 set), si dispone di più file MP4 che è possibile scaricare progressivamente.</span><span class="sxs-lookup"><span data-stu-id="48814-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="48814-344">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="48814-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="48814-345">Creazione di un URL di streaming per la trasmissione di contenuti in streaming</span><span class="sxs-lookup"><span data-stu-id="48814-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="48814-346">Hello seguente codice mostra come toocreate un localizzatore URL di streaming:</span><span class="sxs-lookup"><span data-stu-id="48814-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="48814-347">Se ha esito positivo, viene restituito hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="48814-347">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="48814-348">toostream un URL di origine Smooth Streaming in un lettore multimediale di flusso, è necessario aggiungere una proprietà del percorso con nome hello di hello Smooth Streaming manifesto file, seguito da "/manifest" hello.</span><span class="sxs-lookup"><span data-stu-id="48814-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="48814-349">aggiungere toostream HLS (formato = m3u8-aapl) dopo hello "/manifest".</span><span class="sxs-lookup"><span data-stu-id="48814-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="48814-350">toostream MPEG DASH, accodare (formato = mpd-tempo-csf) dopo hello "/manifest".</span><span class="sxs-lookup"><span data-stu-id="48814-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="48814-351"><a id="play"></a>Riprodurre i contenuti</span><span class="sxs-lookup"><span data-stu-id="48814-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="48814-352">toostream video, utilizzare [lettore servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="48814-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="48814-353">tootest progressivo scaricare, incollare un URL in un browser (ad esempio, Internet Explorer, Chrome e Safari).</span><span class="sxs-lookup"><span data-stu-id="48814-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="48814-354">Passaggi successivi: Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="48814-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="48814-355">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="48814-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
