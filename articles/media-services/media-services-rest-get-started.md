---
title: Introduzione alla distribuzione di contenuto su richiesta tramite REST| Microsoft Docs
description: Questa esercitazione illustra il processo di implementazione di un'applicazione di distribuzione di contenuti su richiesta con Servizi multimediali di Azure tramite REST API.
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
ms.openlocfilehash: f304f7671465862123f64c8b0f9af95a7c828cc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="5394f-103">Introduzione alla distribuzione di contenuti su richiesta usando REST</span><span class="sxs-lookup"><span data-stu-id="5394f-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="5394f-104">Questa guida introduttiva illustra il processo di implementazione di un'applicazione di distribuzione di contenuti Video on Demand (VoD) usando le API REST di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="5394f-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="5394f-105">L'esercitazione descrive il flusso di lavoro di base di Servizi multimediali nonché gli oggetti e le attività di programmazione usati più di frequente per lo sviluppo basato su Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="5394f-106">Al termine dell'esercitazione sarà possibile eseguire lo streaming o il download progressivo di un file multimediale di esempio caricato, codificato e scaricato.</span><span class="sxs-lookup"><span data-stu-id="5394f-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="5394f-107">L'immagine seguente illustra alcuni degli oggetti più comuni usati durante lo sviluppo di applicazioni VoD rispetto al modello OData di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="5394f-108">Fare clic sull'immagine per visualizzarla a schermo intero.</span><span class="sxs-lookup"><span data-stu-id="5394f-108">Click the image to view it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="5394f-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5394f-109">Prerequisites</span></span>
<span data-ttu-id="5394f-110">Per iniziare l'attività di sviluppo con Servizi multimediali e le API REST sono previsti i seguenti prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="5394f-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="5394f-111">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="5394f-111">An Azure account.</span></span> <span data-ttu-id="5394f-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5394f-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5394f-113">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-113">A Media Services account.</span></span> <span data-ttu-id="5394f-114">Per creare un account Servizi multimediali, vedere [Creare un account Servizi multimediali di Azure con il portale di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="5394f-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="5394f-115">Informazioni su come eseguire attività di sviluppo con l'API REST di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="5394f-116">Per altre informazioni, vedere [Informazioni generali sull'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="5394f-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="5394f-117">Un'applicazione di propria scelta per l'invio di richieste e risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="5394f-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="5394f-118">In questa esercitazione viene usato [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="5394f-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="5394f-119">Questa guida introduttiva illustra come effettuare le seguenti attività.</span><span class="sxs-lookup"><span data-stu-id="5394f-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="5394f-120">Avviare l'endpoint di streaming usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5394f-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="5394f-121">Connettersi all'account di Servizi multimediali con l'API REST.</span><span class="sxs-lookup"><span data-stu-id="5394f-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="5394f-122">Creare un nuovo asset e caricare un file video con l'API REST.</span><span class="sxs-lookup"><span data-stu-id="5394f-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="5394f-123">Codificare il file di origine in un set di file MP4 a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="5394f-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="5394f-124">Pubblicare l'asset e ottenere gli URL di streaming e di download progressivo con l'API REST.</span><span class="sxs-lookup"><span data-stu-id="5394f-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="5394f-125">Riprodurre i contenuti.</span><span class="sxs-lookup"><span data-stu-id="5394f-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="5394f-126">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="5394f-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="5394f-127">Usare lo stesso ID criterio se si usano sempre gli stessi giorni/autorizzazioni di accesso, come nel cado di criteri per i localizzatori che devono rimanere attivi per molto tempo (criteri di non caricamento).</span><span class="sxs-lookup"><span data-stu-id="5394f-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="5394f-128">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="5394f-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="5394f-129">Per altre informazioni sulle entità di REST AMS usate in questo argomento, vedere [Informazioni generali sull'API REST di Servizi multimediali](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="5394f-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="5394f-130">Vedere anche [Concetti relativi ai Servizi multimediali di Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="5394f-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="5394f-131">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="5394f-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="5394f-132">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="5394f-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="5394f-133">Avviare endpoint di streaming usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5394f-133">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="5394f-134">Uno degli scenari più frequenti dell'uso di Servizi multimediali di Azure riguarda la distribuzione di contenuto video in streaming a bitrate adattivo.</span><span class="sxs-lookup"><span data-stu-id="5394f-134">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="5394f-135">Servizi multimediali include la funzionalità per la creazione dinamica dei pacchetti, che consente di distribuire contenuto con codifica MP4 a bitrate adattivo nei formati supportati da Servizi multimediali, come MPEG DASH, HLS e Smooth Streaming in modalità JIT, senza dover archiviare le versioni predefinite di ognuno di questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="5394f-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="5394f-136">Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="5394f-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="5394f-137">Per avviare lo streaming del contenuto e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming da cui si vuole trasmettere il contenuto deve essere nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="5394f-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="5394f-138">Per avviare l'endpoint di streaming, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="5394f-138">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="5394f-139">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5394f-139">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5394f-140">Nella finestra Impostazioni fare clic su Endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="5394f-140">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="5394f-141">Fare clic sull'endpoint di streaming predefinito.</span><span class="sxs-lookup"><span data-stu-id="5394f-141">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="5394f-142">Verrà visualizzata la finestra DETTAGLI ENDPOINT DI STREAMING PREDEFINITO.</span><span class="sxs-lookup"><span data-stu-id="5394f-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="5394f-143">Fare clic sull'icona di avvio.</span><span class="sxs-lookup"><span data-stu-id="5394f-143">Click the Start icon.</span></span>
5. <span data-ttu-id="5394f-144">Fare clic sul pulsante Salva per salvare le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="5394f-144">Click the Save button to save your changes.</span></span>

## <span data-ttu-id="5394f-145"><a id="connect"></a>Connettersi all'account di servizi multimediali con l'API REST</span><span class="sxs-lookup"><span data-stu-id="5394f-145"><a id="connect"></a>Connect to the Media Services account with REST API</span></span>

<span data-ttu-id="5394f-146">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="5394f-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="5394f-147">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-147">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="5394f-148">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="5394f-148">You must make subsequent calls to the new URI.</span></span>

<span data-ttu-id="5394f-149">Se, ad esempio, dopo aver tentato la connessione si ottiene la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-149">For example, if after trying to connect, you got the following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="5394f-150">Si consiglia di inviare le successive chiamate API a https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="5394f-150">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="5394f-151"><a id="upload"></a>Creare un nuovo asset e caricare un file video con l'API REST</span><span class="sxs-lookup"><span data-stu-id="5394f-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="5394f-152">In Servizi multimediali è possibile caricare i file digitali in un asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="5394f-153">L'entità **Asset** può contenere video, audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli codificati, oltre ai metadati relativi a questi file.  Dopo il caricamento dei file nell'asset, i contenuti vengono archiviati in modo sicuro nel cloud per altre operazioni di elaborazione e streaming.</span><span class="sxs-lookup"><span data-stu-id="5394f-153">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="5394f-154">Quando si crea un asset è necessario specificare le opzioni correlate.</span><span class="sxs-lookup"><span data-stu-id="5394f-154">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="5394f-155">La proprietà **Options** è un valore di enumerazione che descrive le opzioni di crittografia da usare per la creazione di un asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-155">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="5394f-156">Nel seguente elenco sono riportati i valori validi, che è possibile specificare singolarmente, non in combinazione:</span><span class="sxs-lookup"><span data-stu-id="5394f-156">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="5394f-157">**None** = **0**: non viene usata alcuna crittografia.</span><span class="sxs-lookup"><span data-stu-id="5394f-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="5394f-158">Quando si usa questa opzione il contenuto non è protetto durante il transito, né nell'archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="5394f-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="5394f-159">Se si pianifica la distribuzione di un file MP4 con il download progressivo, usare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="5394f-159">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="5394f-160">**StorageEncrypted** = **1**: crittografa il contenuto non crittografato localmente usando la crittografia AES a 256 bit, quindi li carica in Archiviazione di Azure dove vengono archiviati con crittografia in modo inattivo.</span><span class="sxs-lookup"><span data-stu-id="5394f-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="5394f-161">Gli asset protetti con la crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file system crittografato prima della codifica, quindi ricrittografati facoltativamente prima di essere ricaricati di nuovo come nuovo asset di output.</span><span class="sxs-lookup"><span data-stu-id="5394f-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="5394f-162">La crittografia di archiviazione viene usata principalmente quando si vogliono proteggere i file multimediali con input di alta qualità con una crittografia avanzata sul disco locale.</span><span class="sxs-lookup"><span data-stu-id="5394f-162">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="5394f-163">**CommonEncryptionProtected** = **2**: usare questa opzione per caricare contenuti già crittografati e protetti con Common Encryption o PlayReady DRM (ad esempio, Smooth Streaming protetto con PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="5394f-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="5394f-164">**EnvelopeEncryptionProtected** = **4**: usare questa opzione se si stanno caricando contenuti HLS crittografati con AES.</span><span class="sxs-lookup"><span data-stu-id="5394f-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="5394f-165">I file devono essere stati codificati e crittografati da Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="5394f-165">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="5394f-166">Creare un asset</span><span class="sxs-lookup"><span data-stu-id="5394f-166">Create an asset</span></span>
<span data-ttu-id="5394f-167">Un asset è un contenitore di più tipi o set di oggetti in Servizi multimediali, inclusi elementi video e audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli chiusi.</span><span class="sxs-lookup"><span data-stu-id="5394f-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="5394f-168">Nell'API REST, la creazione di un asset richiede l'invio di una richiesta POST a Servizi multimediali e l'inserimento di tutte le informazioni sulle proprietà relative all'asset nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5394f-168">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="5394f-169">Il seguente esempio mostra come creare un asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-169">The following example shows how to create an asset.</span></span>

<span data-ttu-id="5394f-170">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-170">**HTTP Request**</span></span>

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


<span data-ttu-id="5394f-171">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-171">**HTTP Response**</span></span>

<span data-ttu-id="5394f-172">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-172">If successful, the following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="5394f-173">Creare un'entità AssetFile</span><span class="sxs-lookup"><span data-stu-id="5394f-173">Create an AssetFile</span></span>
<span data-ttu-id="5394f-174">L'entità [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) rappresenta un file video o audio archiviato in un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="5394f-174">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="5394f-175">Un file di asset è sempre associato a un asset e un asset può contenere uno o più file.</span><span class="sxs-lookup"><span data-stu-id="5394f-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="5394f-176">Se un oggetto di file di asset non è associato a un file digitale in un contenitore BLOB, l'attività del codificatore di Servizi multimediali restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="5394f-176">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="5394f-177">Dopo avere caricato il file multimediale digitale in un contenitore BLOB, è necessario usare la richiesta HTTP **MERGE** per aggiornare l'entità AssetFile con le informazioni relative al file multimediale, come illustrato più avanti nell'argomento.</span><span class="sxs-lookup"><span data-stu-id="5394f-177">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="5394f-178">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-178">**HTTP Request**</span></span>

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


<span data-ttu-id="5394f-179">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-179">**HTTP Response**</span></span>

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


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="5394f-180">Creazione dell'entità AccessPolicy con autorizzazioni di scrittura</span><span class="sxs-lookup"><span data-stu-id="5394f-180">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="5394f-181">Prima di caricare i file nell'archiviazione BLOB, impostare i diritti dei criteri di accesso per la scrittura in un asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-181">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="5394f-182">A questo scopo, inviare una richiesta HTTP al set di entità AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="5394f-182">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="5394f-183">Definire un valore DurationInMinutes durante la creazione. In caso contrario, si riceverà il messaggio di errore interno 500 del server in risposta.</span><span class="sxs-lookup"><span data-stu-id="5394f-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="5394f-184">Per altre informazioni su AccessPolicies, vedere [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="5394f-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="5394f-185">Il seguente esempio mostra come creare un'entità AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="5394f-185">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="5394f-186">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-186">**HTTP Request**</span></span>

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

<span data-ttu-id="5394f-187">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-187">**HTTP Response**</span></span>

<span data-ttu-id="5394f-188">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-188">If successful, the following response is returned:</span></span>

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

### <a name="get-the-upload-url"></a><span data-ttu-id="5394f-189">Ottenere l'URL di caricamento</span><span class="sxs-lookup"><span data-stu-id="5394f-189">Get the Upload URL</span></span>

<span data-ttu-id="5394f-190">Per ricevere l'URL di caricamento effettivo, creare un localizzatore di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5394f-190">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="5394f-191">I localizzatori definiscono l'ora di inizio e il tipo di endpoint della connessione per i client che richiedono l'accesso ai file in un asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-191">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="5394f-192">È possibile creare più entità Locator per una specifica coppia AccessPolicy e Asset in modo da gestire le diverse richieste ed esigenze dei client.</span><span class="sxs-lookup"><span data-stu-id="5394f-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="5394f-193">Ogni localizzatore usa i valori StartTime e DurationInMinutes di AccessPolicy per determinare la durata d'uso di un URL.</span><span class="sxs-lookup"><span data-stu-id="5394f-193">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="5394f-194">Per altre informazioni, vedere [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="5394f-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="5394f-195">Un URL di firma di accesso condiviso ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="5394f-195">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="5394f-196">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="5394f-196">Some considerations apply:</span></span>

* <span data-ttu-id="5394f-197">Non è possibile avere più di cinque localizzatori univoci associati contemporaneamente a un determinato asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="5394f-198">Per altre informazioni, vedere Locator.</span><span class="sxs-lookup"><span data-stu-id="5394f-198">For more information, see Locator.</span></span>
* <span data-ttu-id="5394f-199">Se è necessario caricare i file immediatamente, impostare il valore StartTime su cinque minuti prima dell'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="5394f-199">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="5394f-200">Potrebbe infatti essere presente una leggera differenza di orario tra il computer client e Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="5394f-201">Inoltre, il formato DateTime del valore StartTime deve essere il seguente: AAAA-MM-GGTHH:mm:ssZ (ad esempio, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="5394f-201">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="5394f-202">Può verificarsi un ritardo di 30-40 secondi tra la creazione di un localizzatore e la relativa disponibilità per l'uso.</span><span class="sxs-lookup"><span data-stu-id="5394f-202">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="5394f-203">Questo problema si verifica sia per i localizzatori URL di firma di accesso condiviso sia per i localizzatori di origine.</span><span class="sxs-lookup"><span data-stu-id="5394f-203">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="5394f-204">Per altre informazioni sui localizzatori della firma di accesso condiviso, vedere [questo](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="5394f-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="5394f-205">Il seguente esempio mostra come creare un localizzatore URL di firma di accesso condiviso, come definito dalla proprietà Type nel corpo della richiesta ("1" per un localizzatore di firma di accesso condiviso e "2" per un localizzatore di origine su richiesta).</span><span class="sxs-lookup"><span data-stu-id="5394f-205">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="5394f-206">La proprietà **Path** restituita contiene l'URL da usare per caricare il file.</span><span class="sxs-lookup"><span data-stu-id="5394f-206">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="5394f-207">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-207">**HTTP Request**</span></span>

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


<span data-ttu-id="5394f-208">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-208">**HTTP Response**</span></span>

<span data-ttu-id="5394f-209">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-209">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="5394f-210">Caricare un file in un contenitore di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="5394f-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="5394f-211">Una volta impostati AccessPolicy e Locator, il file effettivo viene caricato nel contenitore di archiviazione BLOB di Azure usando le API REST di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5394f-211">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="5394f-212">È necessario caricare i file come BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="5394f-212">You must upload the files as block blobs.</span></span> <span data-ttu-id="5394f-213">I BLOB di pagine non sono supportati da Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="5394f-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="5394f-214">È necessario aggiungere il nome del file da caricare nel valore **Path** di Locator ricevuto nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="5394f-214">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="5394f-215">Ad esempio, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="5394f-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="5394f-216">.</span><span class="sxs-lookup"><span data-stu-id="5394f-216">.</span></span> <span data-ttu-id="5394f-217">.</span><span class="sxs-lookup"><span data-stu-id="5394f-217">.</span></span> <span data-ttu-id="5394f-218">.</span><span class="sxs-lookup"><span data-stu-id="5394f-218">.</span></span>
>
>

<span data-ttu-id="5394f-219">Per altre informazioni sull'uso dei BLOB di Archiviazione di Azure, vedere [API REST del servizio BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="5394f-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="5394f-220">Aggiornare l'entità AssetFile</span><span class="sxs-lookup"><span data-stu-id="5394f-220">Update the AssetFile</span></span>
<span data-ttu-id="5394f-221">Una volta caricato il file, è possibile aggiornare la dimensione dell'entità FileAsset e altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="5394f-221">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="5394f-222">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5394f-222">For example:</span></span>

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


<span data-ttu-id="5394f-223">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-223">**HTTP Response**</span></span>

<span data-ttu-id="5394f-224">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-224">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="5394f-225">Eliminare le entità Locator e AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="5394f-225">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="5394f-226">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="5394f-227">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-227">**HTTP Response**</span></span>

<span data-ttu-id="5394f-228">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-228">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="5394f-229">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="5394f-230">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-230">**HTTP Response**</span></span>

<span data-ttu-id="5394f-231">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-231">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="5394f-232"><a id="encode"></a>Codificare il file di origine in un set di file MP4 a velocità in bit adattiva</span><span class="sxs-lookup"><span data-stu-id="5394f-232"><a id="encode"></a>Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="5394f-233">Dopo aver inserito gli asset in Servizi multimediali, i file multimediali possono essere codificati, sottoposti a transmux e all'applicazione di filigrana e così via prima di essere distribuiti ai client.</span><span class="sxs-lookup"><span data-stu-id="5394f-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="5394f-234">Queste attività vengono pianificate ed eseguite in più istanze del ruolo in background per assicurare prestazioni e disponibilità elevate.</span><span class="sxs-lookup"><span data-stu-id="5394f-234">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="5394f-235">Queste attività vengono chiamate processi. Ogni processo è formato da attività atomiche che svolgono le procedure effettive nel file di asset (per altre informazioni, vedere le descrizioni di [processi](/rest/api/media/services/job) e [attività](/rest/api/media/services/task)).</span><span class="sxs-lookup"><span data-stu-id="5394f-235">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="5394f-236">Come indicato prima, quando si usa Servizi multimediali di Azure, uno degli scenari più frequenti consiste nella distribuzione di contenuti in streaming a velocità in bit adattiva ai client.</span><span class="sxs-lookup"><span data-stu-id="5394f-236">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="5394f-237">Servizi multimediali può creare dinamicamente un pacchetto di un set di file MP4 a bitrate adattivo in uno dei formati seguenti: HTTP Live Streaming (HLS), Smooth Streaming e MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="5394f-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="5394f-238">La seguente sezione mostra come creare un processo contenente una singola attività di codifica,</span><span class="sxs-lookup"><span data-stu-id="5394f-238">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="5394f-239">che indica di transcodificare il file in formato intermedio in un set di file MP4 a velocità in bit adattiva con **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="5394f-239">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="5394f-240">Mostra inoltre come monitorare lo stato di avanzamento dell'elaborazione del processo.</span><span class="sxs-lookup"><span data-stu-id="5394f-240">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="5394f-241">Una volta completato il processo, sarà possibile creare i localizzatori necessari per ottenere l'accesso agli asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-241">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="5394f-242">Ottenere un processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-242">Get a media processor</span></span>
<span data-ttu-id="5394f-243">In Servizi multimediali un processore di contenuti multimediali è un componente che gestisce un'attività di elaborazione specifica, ad esempio la codifica, la conversione del formato, la crittografia o la decrittografia di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="5394f-244">Per l'attività di codifica illustrata in questa esercitazione verrà usato Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="5394f-244">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="5394f-245">Il seguente codice include la richiesta dell'ID del codificatore.</span><span class="sxs-lookup"><span data-stu-id="5394f-245">The following code requests the encoder's id.</span></span>

<span data-ttu-id="5394f-246">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="5394f-247">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-247">**HTTP Response**</span></span>

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

### <a name="create-a-job"></a><span data-ttu-id="5394f-248">Creare un processo</span><span class="sxs-lookup"><span data-stu-id="5394f-248">Create a job</span></span>
<span data-ttu-id="5394f-249">Ogni processo può includere una o più attività in base al tipo di elaborazione che si desidera eseguire.</span><span class="sxs-lookup"><span data-stu-id="5394f-249">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="5394f-250">Tramite l'API REST è possibile creare processi e le attività correlate in due modi: le attività possono essere definite inline mediante la proprietà di navigazione Tasks in entità Job o mediante l'elaborazione batch OData.</span><span class="sxs-lookup"><span data-stu-id="5394f-250">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="5394f-251">Media Services SDK usa l'elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="5394f-251">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="5394f-252">Tuttavia, per semplificare la leggibilità degli esempi di codice inclusi in questo argomento le attività sono state definite inline.</span><span class="sxs-lookup"><span data-stu-id="5394f-252">However, for the readability of the code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="5394f-253">Per informazioni sull'elaborazione batch, vedere l'articolo relativo all' [elaborazione batch OData (Open Data Protocol)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="5394f-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="5394f-254">Il seguente esempio mostra come creare e pubblicare un processo con un'attività impostata per codificare un video con determinati valori di risoluzione e qualità.</span><span class="sxs-lookup"><span data-stu-id="5394f-254">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="5394f-255">La sezione di documentazione seguente contiene l'elenco di tutti i [set di impostazioni di attività](http://msdn.microsoft.com/library/mt269960) supportati dal processore di Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="5394f-255">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="5394f-256">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-256">**HTTP Request**</span></span>

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

<span data-ttu-id="5394f-257">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-257">**HTTP Response**</span></span>

<span data-ttu-id="5394f-258">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-258">If successful, the following response is returned:</span></span>

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


<span data-ttu-id="5394f-259">È necessario tenere conto di alcuni aspetti importanti in una richiesta di processo:</span><span class="sxs-lookup"><span data-stu-id="5394f-259">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="5394f-260">Le proprietà TaskBody DEVONO usare codice XML letterale per definire il numero di asset di input o di output che vengono usati dall'attività.</span><span class="sxs-lookup"><span data-stu-id="5394f-260">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="5394f-261">L'argomento Task contiene la definizione dello schema XML per il codice XML.</span><span class="sxs-lookup"><span data-stu-id="5394f-261">The Task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="5394f-262">Nella definizione TaskBody ogni valore interno per <inputAsset> e <outputAsset>deve essere impostato come JobInputAsset(value) o JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="5394f-262">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="5394f-263">Un'attività può avere più asset di output.</span><span class="sxs-lookup"><span data-stu-id="5394f-263">A task can have multiple output assets.</span></span> <span data-ttu-id="5394f-264">Un oggetto JobOutputAsset(x) può essere usato solo una volta come output di un'attività in un processo.</span><span class="sxs-lookup"><span data-stu-id="5394f-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="5394f-265">È possibile specificare JobInputAsset o JobOutputAsset come asset di input di un'attività.</span><span class="sxs-lookup"><span data-stu-id="5394f-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="5394f-266">Le attività non devono formare un ciclo.</span><span class="sxs-lookup"><span data-stu-id="5394f-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="5394f-267">Il parametro value passato a JobInputAsset o JobOutputAsset rappresenta il valore di indice di un asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-267">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="5394f-268">Gli asset effettivi vengono definiti nelle proprietà di navigazione InputMediaAssets e OutputMediaAssets nella definizione dell'entità Job.</span><span class="sxs-lookup"><span data-stu-id="5394f-268">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="5394f-269">Poiché Servizi multimediali si basa su OData versione 3, i riferimenti ai singoli asset nelle raccolte delle proprietà di navigazione InputMediaAssets e OutputMediaAssets vengono definiti mediante una coppia nome/valore "__metadata : uri".</span><span class="sxs-lookup"><span data-stu-id="5394f-269">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="5394f-270">La proprietà InputMediaAssets è mappata a uno o più asset creati in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-270">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="5394f-271">Le proprietà OutputMediaAssets vengono create dal sistema.</span><span class="sxs-lookup"><span data-stu-id="5394f-271">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="5394f-272">Non fanno riferimento a un asset esistente.</span><span class="sxs-lookup"><span data-stu-id="5394f-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="5394f-273">Per assegnare un nome a OutputMediaAssets è possibile usare l'attributo assetName.</span><span class="sxs-lookup"><span data-stu-id="5394f-273">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="5394f-274">Se questo attributo non è presente, il nome della proprietà OutputMediaAssets corrisponde al valore del testo interno dell'elemento <outputAsset> preceduto dal nome o dall'ID del processo, nel caso in cui la proprietà Name non sia definita.</span><span class="sxs-lookup"><span data-stu-id="5394f-274">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="5394f-275">Se ad esempio si è impostato "Sample" come valore di assetName, la proprietà Name di OutputMediaAssets sarà impostata su "Sample".</span><span class="sxs-lookup"><span data-stu-id="5394f-275">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="5394f-276">Se invece non si è impostato un valore per assetName, ma si è impostato "NewJob" come nome del processo, il nome di OutputMediaAssets sarà "JobOutputAsset(value)_NewJob".</span><span class="sxs-lookup"><span data-stu-id="5394f-276">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="5394f-277">Il seguente esempio mostra impostare l'attributo assetName:</span><span class="sxs-lookup"><span data-stu-id="5394f-277">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="5394f-278">Per abilitare il concatenamento di attività:</span><span class="sxs-lookup"><span data-stu-id="5394f-278">To enable task chaining:</span></span>

  * <span data-ttu-id="5394f-279">Un processo deve avere almeno due attività</span><span class="sxs-lookup"><span data-stu-id="5394f-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="5394f-280">Deve essere presente almeno un'attività il cui input viene usato come output di un'altra attività nel processo.</span><span class="sxs-lookup"><span data-stu-id="5394f-280">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="5394f-281">Per altre informazioni, vedere [Creazione di un processo di codifica con l'API REST di Servizi multimediali](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="5394f-281">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="5394f-282">Monitorare lo stato di avanzamento dell'elaborazione</span><span class="sxs-lookup"><span data-stu-id="5394f-282">Monitor Processing Progress</span></span>
<span data-ttu-id="5394f-283">È possibile recuperare lo stato di un processo usando la proprietà State, come illustrato nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="5394f-283">You can retrieve the Job status by using the State property, as shown in the following example.</span></span>

<span data-ttu-id="5394f-284">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="5394f-285">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-285">**HTTP Response**</span></span>

<span data-ttu-id="5394f-286">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-286">If successful, the following response is returned:</span></span>

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


### <a name="cancel-a-job"></a><span data-ttu-id="5394f-287">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="5394f-287">Cancel a job</span></span>
<span data-ttu-id="5394f-288">Servizi multimediali consente di annullare i processi in esecuzione mediante la funzione CancelJob.</span><span class="sxs-lookup"><span data-stu-id="5394f-288">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="5394f-289">Questa chiamata restituisce un codice di errore 400 se si tenta di annullare un processo il cui stato è annullato, in fase di annullamento, con errore o terminato.</span><span class="sxs-lookup"><span data-stu-id="5394f-289">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="5394f-290">Il seguente esempio mostra come chiamare la funzione CancelJob.</span><span class="sxs-lookup"><span data-stu-id="5394f-290">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="5394f-291">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="5394f-292">Se l'esito è positivo, viene restituito un codice di risposta 204 senza il corpo di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="5394f-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="5394f-293">È necessario codificare in URL l'ID del processo (in genere nb:jid:UUID: valore) quando viene passato come parametro a CancelJob.</span><span class="sxs-lookup"><span data-stu-id="5394f-293">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="5394f-294">Ottenere l'asset di output</span><span class="sxs-lookup"><span data-stu-id="5394f-294">Get the output asset</span></span>
<span data-ttu-id="5394f-295">Il seguente codice mostra come richiedere l'ID dell'asset di output.</span><span class="sxs-lookup"><span data-stu-id="5394f-295">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="5394f-296">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="5394f-297">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="5394f-297">**HTTP Response**</span></span>

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



## <span data-ttu-id="5394f-298"><a id="publish_get_urls"></a>Pubblicare l'asset e ottenere gli URL di streaming e di download progressivo con l'API REST</span><span class="sxs-lookup"><span data-stu-id="5394f-298"><a id="publish_get_urls"></a>Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="5394f-299">Per eseguire lo streaming o il download di un asset è necessario prima "pubblicarlo" creando un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="5394f-299">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="5394f-300">I localizzatori forniscono l'accesso ai file contenuti nell'asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-300">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="5394f-301">Servizi multimediali supporta due tipi di localizzatori: localizzatori OnDemandOrigin, usati per lo streaming dei file multimediali (ad esempio, MPEG DASH, HLS o Smooth Streaming) e localizzatori di firma di accesso condiviso, usati per scaricare i file multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-301">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> <span data-ttu-id="5394f-302">Per altre informazioni sui localizzatori della firma di accesso condiviso, vedere [questo](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="5394f-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="5394f-303">Dopo aver creato i localizzatori è possibile compilare gli URL usati per eseguire lo streaming o il download dei file.</span><span class="sxs-lookup"><span data-stu-id="5394f-303">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="5394f-304">Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="5394f-304">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="5394f-305">Per avviare lo streaming del contenuto e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming da cui si vuole trasmettere il contenuto deve essere nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="5394f-305">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="5394f-306">Un URL di streaming per Smooth Streaming ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="5394f-306">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="5394f-307">Un URL di streaming per HLS ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="5394f-307">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="5394f-308">Un URL di streaming per MPEG DASH ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="5394f-308">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="5394f-309">Un URL di firma di accesso condiviso usato per scaricare i file ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="5394f-309">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="5394f-310">Questa sezione illustra come eseguire le seguenti attività per "pubblicare" gli asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-310">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="5394f-311">Creazione dell'entità AccessPolicy con autorizzazioni di lettura</span><span class="sxs-lookup"><span data-stu-id="5394f-311">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="5394f-312">Creazione di un URL di firma di accesso condiviso per il download di contenuti</span><span class="sxs-lookup"><span data-stu-id="5394f-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="5394f-313">Creazione di un URL di origine per la trasmissione di contenuti in streaming</span><span class="sxs-lookup"><span data-stu-id="5394f-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="5394f-314">Creazione dell'entità AccessPolicy con autorizzazioni di lettura</span><span class="sxs-lookup"><span data-stu-id="5394f-314">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="5394f-315">Prima di scaricare o trasmettere contenuti multimediali in streaming, definire un'entità AccessPolicy con autorizzazioni di lettura e creare l'entità Locator appropriata che specifichi il tipo di meccanismo di distribuzione che si desidera abilitare per i client.</span><span class="sxs-lookup"><span data-stu-id="5394f-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="5394f-316">Per altre informazioni sulle proprietà disponibili, vedere [Proprietà dell'entità AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="5394f-316">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="5394f-317">Il seguente esempio mostra come specificare l'entità AccessPolicy per le autorizzazioni di lettura per un asset specifico.</span><span class="sxs-lookup"><span data-stu-id="5394f-317">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

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

<span data-ttu-id="5394f-318">Se l'esito è positivo, viene restituito un codice di riuscita 201 in cui viene descritta l'entità AccessPolicy creata.</span><span class="sxs-lookup"><span data-stu-id="5394f-318">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="5394f-319">Si userà quindi l'ID AccessPolicy insieme all'ID asset in cui è contenuto il file che si vuole distribuire (ad esempio un asset di output) per creare l'entità Locator.</span><span class="sxs-lookup"><span data-stu-id="5394f-319">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="5394f-320">Questo flusso di lavoro di base è lo stesso previsto per il caricamento di un file durante l'inserimento di un asset, come illustrato in precedenza in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="5394f-320">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="5394f-321">Come per il caricamento dei file, se l'utente o i relativi client desiderano accedere immediatamente ai file, impostare il valore StartTime su cinque minuti prima dell'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="5394f-321">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="5394f-322">Questa operazione è necessaria perché potrebbe essere presente una leggera differenza di orario tra il computer client e Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-322">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="5394f-323">Il formato DateTime del valore StartTime deve essere il seguente: AAAA-MM-GGTHH:mm:ssZ (ad esempio, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="5394f-323">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="5394f-324">Creazione di un URL di firma di accesso condiviso per il download di contenuti</span><span class="sxs-lookup"><span data-stu-id="5394f-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="5394f-325">Il seguente codice mostra come ottenere un URL da usare per il download di un file multimediale creato e caricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5394f-325">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="5394f-326">Per l'entità AccessPolicy sono impostate autorizzazioni di lettura e il percorso del localizzatore fa riferimento a un URL di download di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5394f-326">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

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

<span data-ttu-id="5394f-327">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-327">If successful, the following response is returned:</span></span>

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


<span data-ttu-id="5394f-328">La proprietà **Path** restituita contiene l'URL di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5394f-328">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="5394f-329">Se si scaricano contenuti a cui è stata applicata la crittografia di archiviazione, sarà necessario decrittografarli manualmente prima di eseguirne il rendering oppure usare il processore di contenuti multimediali Storage Decryption in un'attività di elaborazione per generare file elaborati non crittografati in un'entità OutputAsset e quindi eseguire il download da tale asset.</span><span class="sxs-lookup"><span data-stu-id="5394f-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="5394f-330">Per altre informazioni sull'elaborazione, vedere Creazione di un processo di codifica con l'API REST di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5394f-330">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="5394f-331">Inoltre, i localizzatori URL di firma di accesso condiviso non possono essere aggiornati dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="5394f-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="5394f-332">Ad esempio, non è possibile usare nuovamente lo stesso localizzatore con un valore StartTime aggiornato.</span><span class="sxs-lookup"><span data-stu-id="5394f-332">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="5394f-333">Questo è dovuto al modo in cui vengono creati gli URL di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5394f-333">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="5394f-334">Se si desidera accedere a un asset per il download dopo la scadenza di un localizzatore, sarà necessario crearne uno nuovo con un nuovo valore StartTime.</span><span class="sxs-lookup"><span data-stu-id="5394f-334">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="5394f-335">Download dei file</span><span class="sxs-lookup"><span data-stu-id="5394f-335">Download files</span></span>
<span data-ttu-id="5394f-336">Una volta impostate le entità AccessPolicy e Locator, è possibile scaricare i file mediante le API REST di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5394f-336">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="5394f-337">È necessario aggiungere il nome del file da scaricare nel valore **Path** di Locator ricevuto nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="5394f-337">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="5394f-338">Ad esempio, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="5394f-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="5394f-339">.</span><span class="sxs-lookup"><span data-stu-id="5394f-339">.</span></span> <span data-ttu-id="5394f-340">.</span><span class="sxs-lookup"><span data-stu-id="5394f-340">.</span></span> <span data-ttu-id="5394f-341">.</span><span class="sxs-lookup"><span data-stu-id="5394f-341">.</span></span>
>
>

<span data-ttu-id="5394f-342">Per altre informazioni sull'uso dei BLOB di Archiviazione di Azure, vedere [API REST del servizio BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="5394f-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="5394f-343">Come risultato del processo di codifica eseguito in precedenza (in un set MP4 a velocità adattiva), si hanno più file MP4 di cui è possibile eseguire il download progressivo.</span><span class="sxs-lookup"><span data-stu-id="5394f-343">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="5394f-344">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5394f-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="5394f-345">Creazione di un URL di streaming per la trasmissione di contenuti in streaming</span><span class="sxs-lookup"><span data-stu-id="5394f-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="5394f-346">Il seguente codice mostra come creare un localizzatore URL di streaming:</span><span class="sxs-lookup"><span data-stu-id="5394f-346">The following code shows how to create a streaming URL Locator:</span></span>

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

<span data-ttu-id="5394f-347">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5394f-347">If successful, the following response is returned:</span></span>

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

<span data-ttu-id="5394f-348">Per trasmettere in streaming un URL di origine Smooth Streaming in un lettore multimediale, è necessario aggiungere la proprietà Path con il nome del file manifesto Smooth Streaming seguito da "/manifest".</span><span class="sxs-lookup"><span data-stu-id="5394f-348">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="5394f-349">Per trasmettere in streaming contenuti HLS, aggiungere (format=m3u8-aapl) dopo "/manifest".</span><span class="sxs-lookup"><span data-stu-id="5394f-349">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="5394f-350">Per trasmettere in streaming contenuti MPEG DASH, aggiungere (format=mpd-time-csf) dopo "/manifest".</span><span class="sxs-lookup"><span data-stu-id="5394f-350">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="5394f-351"><a id="play"></a>Riprodurre i contenuti</span><span class="sxs-lookup"><span data-stu-id="5394f-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="5394f-352">Per riprodurre il video, utilizzare [Lettore di Servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="5394f-352">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="5394f-353">Per testare il download progressivo, incollare un URL in un browser (ad esempio, IE, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="5394f-353">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="5394f-354">Passaggi successivi: Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5394f-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5394f-355">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="5394f-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
