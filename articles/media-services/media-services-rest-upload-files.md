---
title: Caricare file in un account di Servizi multimediali mediante REST | Microsoft Docs
description: Informazioni su come ottenere contenuti multimediali in Servizi multimediali creando e caricando asset.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 955356ffe6fc524c1528364add7e2c2a336137b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="d0717-103">Caricare file in un account di Servizi multimediali mediante REST</span><span class="sxs-lookup"><span data-stu-id="d0717-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d0717-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d0717-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="d0717-105">REST</span><span class="sxs-lookup"><span data-stu-id="d0717-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="d0717-106">Portale</span><span class="sxs-lookup"><span data-stu-id="d0717-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="d0717-107">In Servizi multimediali è possibile caricare i file digitali in un asset.</span><span class="sxs-lookup"><span data-stu-id="d0717-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="d0717-108">L'entità [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) può contenere video, audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli codificati, oltre ai metadati relativi a questi file.  Dopo il caricamento dei file nell'asset, i contenuti vengono archiviati in modo sicuro nel cloud per altre operazioni di elaborazione e streaming.</span><span class="sxs-lookup"><span data-stu-id="d0717-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="d0717-109">Si applicano le considerazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0717-109">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="d0717-110">Servizi multimediali usa il valore della proprietà IAssetFile.Name durante la creazione di URL per i contenuti in streaming, ad esempio http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters. Per questo motivo, la codifica percentuale non è consentita.</span><span class="sxs-lookup"><span data-stu-id="d0717-110">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="d0717-111">Il valore della proprietà **Name** non può contenere i [caratteri riservati per la codifica percentuale](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters) seguenti: !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="d0717-111">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="d0717-112">L'estensione del nome di file, inoltre, può essere preceduta da un solo punto (.).</span><span class="sxs-lookup"><span data-stu-id="d0717-112">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="d0717-113">La lunghezza del nome non deve essere superare i 260 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d0717-113">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="d0717-114">È previsto un limite per le dimensioni massime dei file supportate per l'elaborazione in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d0717-114">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="d0717-115">Vedere [questo](media-services-quotas-and-limitations.md) argomento per informazioni dettagliate sulla limitazione per le dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="d0717-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> 

<span data-ttu-id="d0717-116">Il flusso di lavoro di base per il caricamento degli asset si divide nelle sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0717-116">The basic workflow for uploading Assets is divided into the following sections:</span></span>

* <span data-ttu-id="d0717-117">Creare un asset</span><span class="sxs-lookup"><span data-stu-id="d0717-117">Create an Asset</span></span>
* <span data-ttu-id="d0717-118">Crittografare un asset (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="d0717-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="d0717-119">Caricare un file nell'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="d0717-119">Upload a file to blob storage</span></span>

<span data-ttu-id="d0717-120">AMS consente anche di caricare gli asset in blocco.</span><span class="sxs-lookup"><span data-stu-id="d0717-120">AMS also enables you to upload assets in bulk.</span></span> <span data-ttu-id="d0717-121">Per altre informazioni, vedere [questa](media-services-rest-upload-files.md#upload_in_bulk) sezione.</span><span class="sxs-lookup"><span data-stu-id="d0717-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="d0717-122">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="d0717-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d0717-123">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d0717-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="d0717-124">Connettersi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="d0717-124">Connect to Media Services</span></span>

<span data-ttu-id="d0717-125">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d0717-125">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d0717-126">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d0717-126">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d0717-127">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="d0717-127">You must make subsequent calls to the new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="d0717-128">Caricare gli asset</span><span class="sxs-lookup"><span data-stu-id="d0717-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="d0717-129">Creare un asset</span><span class="sxs-lookup"><span data-stu-id="d0717-129">Create an asset</span></span>

<span data-ttu-id="d0717-130">Un asset è un contenitore di più tipi o set di oggetti in Servizi multimediali, inclusi elementi video e audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli chiusi.</span><span class="sxs-lookup"><span data-stu-id="d0717-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="d0717-131">Nell'API REST, la creazione di un asset richiede l'invio di una richiesta POST a Servizi multimediali e l'inserimento di tutte le informazioni sulle proprietà relative all'asset nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d0717-131">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="d0717-132">Una delle proprietà che è possibile specificare quando si crea un asset è **Options**.</span><span class="sxs-lookup"><span data-stu-id="d0717-132">One of the properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="d0717-133">**Options** è un valore di enumerazione che descrive le opzioni di crittografia da usare per la creazione di un asset.</span><span class="sxs-lookup"><span data-stu-id="d0717-133">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="d0717-134">Nel seguente elenco sono riportati i valori validi, che è possibile specificare singolarmente, non in combinazione.</span><span class="sxs-lookup"><span data-stu-id="d0717-134">A valid value is one of the values from the list below, not a combination of values.</span></span> 

* <span data-ttu-id="d0717-135">**None** = **0**: non viene applicata alcuna crittografia.</span><span class="sxs-lookup"><span data-stu-id="d0717-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="d0717-136">Si tratta del valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="d0717-136">This is the default value.</span></span> <span data-ttu-id="d0717-137">Quando si usa questa opzione, il contenuto non è protetto durante il transito, né nell'archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="d0717-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="d0717-138">Se si pianifica la distribuzione di un file MP4 con il download progressivo, usare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="d0717-138">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="d0717-139">**StorageEncrypted** = **1**: consente di specificare se si desidera applicare la crittografia AES a 256 bit per il caricamento e l'archiviazione dei file.</span><span class="sxs-lookup"><span data-stu-id="d0717-139">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="d0717-140">Se l'asset è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="d0717-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="d0717-141">Per altre informazioni, vedere [Procedura: Configurare i criteri di distribuzione degli asset](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d0717-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="d0717-142">**CommonEncryptionProtected** = **2**: consente di specificare se si desidera caricare i file protetti con un metodo di crittografia comune (ad esempio PlayReady).</span><span class="sxs-lookup"><span data-stu-id="d0717-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="d0717-143">**EnvelopeEncryptionProtected** = **4**: consente di specificare se si stanno caricando file HLS crittografati con AES.</span><span class="sxs-lookup"><span data-stu-id="d0717-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="d0717-144">I file devono essere stati codificati e crittografati da Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="d0717-144">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="d0717-145">Se nell'asset verrà usata la crittografia, è necessario creare un'entità **ContentKey** e collegarla all'asset, come descritto nell'argomento relativo alla[creazione di un'entità ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="d0717-145">If your asset will use encryption, you must create a **ContentKey** and link it to your asset as described in the following topic:[How to create a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="d0717-146">Tenere presente che, dopo il caricamento dei file nell'asset, è necessario aggiornare le proprietà di crittografia nell'entità **AssetFile** con i valori ottenuti durante la crittografia dell'entità **Asset**.</span><span class="sxs-lookup"><span data-stu-id="d0717-146">Note that after you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span></span> <span data-ttu-id="d0717-147">Effettuare questa operazione usando la richiesta HTTP **MERGE** .</span><span class="sxs-lookup"><span data-stu-id="d0717-147">Do it by using the **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="d0717-148">Il seguente esempio mostra come creare un asset.</span><span class="sxs-lookup"><span data-stu-id="d0717-148">The following example shows how to create an asset.</span></span>

<span data-ttu-id="d0717-149">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="d0717-150">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-150">**HTTP Response**</span></span>

<span data-ttu-id="d0717-151">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="d0717-151">If successful, the following is returned:</span></span>

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="d0717-152">Creare un'entità AssetFile</span><span class="sxs-lookup"><span data-stu-id="d0717-152">Create an AssetFile</span></span>
<span data-ttu-id="d0717-153">L'entità [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) rappresenta un file video o audio archiviato in un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0717-153">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="d0717-154">Un file di asset è sempre associato a un asset e un asset può contenere uno o più file.</span><span class="sxs-lookup"><span data-stu-id="d0717-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="d0717-155">Se un oggetto di file di asset non è associato a un file digitale in un contenitore BLOB, l'attività del codificatore di Servizi multimediali restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="d0717-155">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="d0717-156">Si noti che l'istanza di **AssetFile** e l'effettivo file multimediale sono due oggetti distinti.</span><span class="sxs-lookup"><span data-stu-id="d0717-156">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="d0717-157">L'istanza di AssetFile contiene metadati relativi al file multimediale, mentre quest'ultimo contiene l'effettivo contenuto multimediale.</span><span class="sxs-lookup"><span data-stu-id="d0717-157">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="d0717-158">Dopo avere caricato il file multimediale digitale in un contenitore BLOB, è necessario usare la richiesta HTTP **MERGE** per aggiornare l'entità AssetFile con le informazioni relative al file multimediale, come illustrato più avanti nell'argomento.</span><span class="sxs-lookup"><span data-stu-id="d0717-158">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span> 

<span data-ttu-id="d0717-159">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="d0717-160">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-160">**HTTP Response**</span></span>

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

### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="d0717-161">Creazione dell'entità AccessPolicy con autorizzazioni di scrittura</span><span class="sxs-lookup"><span data-stu-id="d0717-161">Creating the AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="d0717-162">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="d0717-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d0717-163">Usare lo stesso ID criterio se si usano sempre gli stessi giorni/autorizzazioni di accesso, come nel cado di criteri per i localizzatori che devono rimanere attivi per molto tempo (criteri di non caricamento).</span><span class="sxs-lookup"><span data-stu-id="d0717-163">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d0717-164">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="d0717-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="d0717-165">Prima di caricare i file nell'archiviazione BLOB, impostare i diritti dei criteri di accesso per la scrittura in un asset.</span><span class="sxs-lookup"><span data-stu-id="d0717-165">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="d0717-166">A questo scopo, inviare una richiesta HTTP al set di entità AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="d0717-166">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="d0717-167">Definire un valore DurationInMinutes durante la creazione. In caso contrario, si riceverà un messaggio di errore interno del server 500 in risposta.</span><span class="sxs-lookup"><span data-stu-id="d0717-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="d0717-168">Per altre informazioni su AccessPolicies, vedere [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="d0717-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="d0717-169">Il seguente esempio mostra come creare un'entità AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="d0717-169">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="d0717-170">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="d0717-171">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-171">**HTTP Request**</span></span>

    If successful, the following response is returned:

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

### <a name="get-the-upload-url"></a><span data-ttu-id="d0717-172">Ottenere l'URL di caricamento</span><span class="sxs-lookup"><span data-stu-id="d0717-172">Get the Upload URL</span></span>
<span data-ttu-id="d0717-173">Per ricevere l'URL di caricamento effettivo, creare un localizzatore di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="d0717-173">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="d0717-174">I localizzatori definiscono l'ora di inizio e il tipo di endpoint della connessione per i client che richiedono l'accesso ai file in un asset.</span><span class="sxs-lookup"><span data-stu-id="d0717-174">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="d0717-175">È possibile creare più entità Locator per una specifica coppia AccessPolicy e Asset in modo da gestire le diverse richieste ed esigenze dei client.</span><span class="sxs-lookup"><span data-stu-id="d0717-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="d0717-176">Ogni localizzatore usa i valori StartTime e DurationInMinutes di AccessPolicy per determinare la durata d'uso di un URL.</span><span class="sxs-lookup"><span data-stu-id="d0717-176">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="d0717-177">Per altre informazioni, vedere [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="d0717-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="d0717-178">Un URL di firma di accesso condiviso ha il seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d0717-178">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="d0717-179">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="d0717-179">Some considerations apply:</span></span>

* <span data-ttu-id="d0717-180">Non è possibile avere più di cinque localizzatori univoci associati contemporaneamente a un determinato asset.</span><span class="sxs-lookup"><span data-stu-id="d0717-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="d0717-181">Per altre informazioni, vedere Locator.</span><span class="sxs-lookup"><span data-stu-id="d0717-181">For more information, see Locator.</span></span>
* <span data-ttu-id="d0717-182">Se è necessario caricare i file immediatamente, impostare il valore StartTime su cinque minuti prima dell'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="d0717-182">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="d0717-183">Potrebbe infatti essere presente una leggera differenza di orario tra il computer client e Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d0717-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="d0717-184">Inoltre, il formato DateTime del valore StartTime deve essere il seguente: AAAA-MM-GGTHH:mm:ssZ (ad esempio, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="d0717-184">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="d0717-185">Può verificarsi un ritardo di 30-40 secondi tra la creazione di un localizzatore e la relativa disponibilità per l'uso.</span><span class="sxs-lookup"><span data-stu-id="d0717-185">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="d0717-186">Questo problema si verifica sia per i localizzatori URL di firma di accesso condiviso sia per i localizzatori di origine.</span><span class="sxs-lookup"><span data-stu-id="d0717-186">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="d0717-187">Il seguente esempio mostra come creare un localizzatore URL di firma di accesso condiviso, come definito dalla proprietà Type nel corpo della richiesta ("1" per un localizzatore di firma di accesso condiviso e "2" per un localizzatore di origine su richiesta).</span><span class="sxs-lookup"><span data-stu-id="d0717-187">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="d0717-188">La proprietà **Path** restituita contiene l'URL da usare per caricare il file.</span><span class="sxs-lookup"><span data-stu-id="d0717-188">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="d0717-189">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="d0717-190">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-190">**HTTP Response**</span></span>

<span data-ttu-id="d0717-191">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="d0717-191">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="d0717-192">Caricare un file in un contenitore di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="d0717-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="d0717-193">Una volta impostati AccessPolicy e Locator, il file effettivo viene caricato nel contenitore di archiviazione BLOB di Azure usando le API REST di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0717-193">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="d0717-194">È necessario caricare i file come BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="d0717-194">You must upload the files as block blobs.</span></span> <span data-ttu-id="d0717-195">I BLOB di pagine non sono supportati da Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0717-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="d0717-196">È necessario aggiungere il nome del file da caricare nel valore **Path** di Locator ricevuto nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="d0717-196">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="d0717-197">Ad esempio, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="d0717-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="d0717-198">.</span><span class="sxs-lookup"><span data-stu-id="d0717-198">.</span></span> <span data-ttu-id="d0717-199">.</span><span class="sxs-lookup"><span data-stu-id="d0717-199">.</span></span> <span data-ttu-id="d0717-200">.</span><span class="sxs-lookup"><span data-stu-id="d0717-200">.</span></span> 
> 
> 

<span data-ttu-id="d0717-201">Per altre informazioni sull'uso dei BLOB di Archiviazione di Azure, vedere [API REST del servizio BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="d0717-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="d0717-202">Aggiornare l'entità AssetFile</span><span class="sxs-lookup"><span data-stu-id="d0717-202">Update the AssetFile</span></span>
<span data-ttu-id="d0717-203">Una volta caricato il file, è possibile aggiornare la dimensione dell'entità FileAsset e altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="d0717-203">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="d0717-204">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0717-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="d0717-205">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-205">**HTTP Response**</span></span>

<span data-ttu-id="d0717-206">Se l'esito è positivo, viene restituita la seguente risposta: HTTP/1.1 204 - Nessun contenuto</span><span class="sxs-lookup"><span data-stu-id="d0717-206">If successful, the following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="d0717-207">Eliminare le entità Locator e AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="d0717-207">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="d0717-208">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="d0717-209">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-209">**HTTP Response**</span></span>

<span data-ttu-id="d0717-210">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="d0717-210">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="d0717-211">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="d0717-212">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-212">**HTTP Response**</span></span>

<span data-ttu-id="d0717-213">Se l'esito è positivo, viene restituita la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="d0717-213">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="d0717-214"><a id="upload_in_bulk"></a>Caricare gli asset in blocco</span><span class="sxs-lookup"><span data-stu-id="d0717-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-the-ingestmanifest"></a><span data-ttu-id="d0717-215">Creare l'entità IngestManifest</span><span class="sxs-lookup"><span data-stu-id="d0717-215">Create the IngestManifest</span></span>
<span data-ttu-id="d0717-216">IngestManifest è un contenitore per un set di asset, file di asset e informazioni statistiche che possono essere usate per determinare lo stato di avanzamento dell'inserimento in blocco del set.</span><span class="sxs-lookup"><span data-stu-id="d0717-216">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span></span>

<span data-ttu-id="d0717-217">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="d0717-218">Creare gli asset</span><span class="sxs-lookup"><span data-stu-id="d0717-218">Create assets</span></span>
<span data-ttu-id="d0717-219">Prima di creare l'entità IngestManifestAsset, è necessario creare l'asset che verrà completato mediante l'inserimento in blocco.</span><span class="sxs-lookup"><span data-stu-id="d0717-219">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="d0717-220">Un asset è un contenitore di più tipi o set di oggetti in Servizi multimediali, inclusi elementi video e audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli chiusi.</span><span class="sxs-lookup"><span data-stu-id="d0717-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="d0717-221">Nell'API REST, per creare un asset, è necessario inviare una richiesta HTTP POST a Servizi multimediali di Microsoft Azure e inserire le informazioni relative alle proprietà dell'asset nel corpo della richiesta. In questo esempio l'asset viene creato usando l'opzione StorageEncrption(1) inclusa nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d0717-221">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span></span>

<span data-ttu-id="d0717-222">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-the-ingestmanifestassets"></a><span data-ttu-id="d0717-223">Creare le entità IngestManifestAsset</span><span class="sxs-lookup"><span data-stu-id="d0717-223">Create the IngestManifestAssets</span></span>
<span data-ttu-id="d0717-224">Le entità IngestManifestAsset rappresentano gli asset all'interno dell'entità IngestManifest usati durante l'inserimento in blocco.</span><span class="sxs-lookup"><span data-stu-id="d0717-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="d0717-225">Esse in pratica collegano l'asset al manifesto.</span><span class="sxs-lookup"><span data-stu-id="d0717-225">The basically link the asset to the manifest.</span></span> <span data-ttu-id="d0717-226">Servizi multimediali di Azure controlla internamente il caricamento dei file in base alla raccolta IngestManifestFiles associata all'entità IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="d0717-226">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span></span> <span data-ttu-id="d0717-227">Dopo il caricamento dei file, l'asset è completato.</span><span class="sxs-lookup"><span data-stu-id="d0717-227">Once these files are uploaded, the asset is completed.</span></span> <span data-ttu-id="d0717-228">È possibile creare una nuova entità IngestManifestAsset mediante una richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d0717-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="d0717-229">Nel corpo della richiesta è necessario includere l'ID dell'entità IngestManifest e l'ID dell'asset da collegare insieme tramite IngestManifestAsset per l'inserimento in blocco.</span><span class="sxs-lookup"><span data-stu-id="d0717-229">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="d0717-230">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-the-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="d0717-231">Creare le entità IngestManifestFile per ogni asset</span><span class="sxs-lookup"><span data-stu-id="d0717-231">Create the IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="d0717-232">Un'entità IngestManifestFile rappresenta un oggetto BLOB audio o video che verrà caricato nel corso del caricamento in blocco di un asset.</span><span class="sxs-lookup"><span data-stu-id="d0717-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="d0717-233">Le proprietà relative alla crittografia sono necessarie solo se per l'asset viene usata un'opzione di crittografia.</span><span class="sxs-lookup"><span data-stu-id="d0717-233">Encryption related properties are not required unless the asset is using an encryption option.</span></span> <span data-ttu-id="d0717-234">L'esempio riportato in questa sezione mostra come creare un'entità IngestManifestFile che usa l'entità StorageEncryption per l'asset creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d0717-234">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span></span>

<span data-ttu-id="d0717-235">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-the-files-to-blob-storage"></a><span data-ttu-id="d0717-236">Caricare i file in Archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="d0717-236">Upload the Files to Blob Storage</span></span>
<span data-ttu-id="d0717-237">È possibile usare qualsiasi applicazione client ad alta velocità in grado di caricare i file di asset nell'URI del contenitore di archiviazione BLOB fornito dalla proprietà BlobStorageUriForUpload di IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="d0717-237">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span></span> <span data-ttu-id="d0717-238">Un servizio di caricamento ad alta velocità consigliato è l'applicazione [Aspera On Demand for Azure](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="d0717-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="d0717-239">Monitorare lo stato di avanzamento dell'inserimento in blocco</span><span class="sxs-lookup"><span data-stu-id="d0717-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="d0717-240">È possibile monitorare lo stato di avanzamento delle operazioni di inserimento in blocco per un'entità IngestManifest eseguendo il polling della proprietà Statistics di IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="d0717-240">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span></span> <span data-ttu-id="d0717-241">Tale proprietà è un tipo complesso, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="d0717-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="d0717-242">Per eseguire il polling della proprietà Statistics, inviare una richiesta HTTP GET passando l'ID IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="d0717-242">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="d0717-243">Creare chiavi simmetriche per la crittografia</span><span class="sxs-lookup"><span data-stu-id="d0717-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="d0717-244">Se per l'asset verrà usata la crittografia, è necessario creare l'entità ContentKey da usare a tale scopo prima di creare i file di asset.</span><span class="sxs-lookup"><span data-stu-id="d0717-244">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="d0717-245">Per la crittografia di archiviazione, nel corpo della richiesta devono essere incluse le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="d0717-245">For storage encryption, the following properties should be included in the request body.</span></span>

| <span data-ttu-id="d0717-246">Proprietà del corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="d0717-246">Request body property</span></span> | <span data-ttu-id="d0717-247">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d0717-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d0717-248">ID</span><span class="sxs-lookup"><span data-stu-id="d0717-248">Id</span></span> |<span data-ttu-id="d0717-249">ID della chiave simmetrica generato dall'utente con il formato seguente: "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="d0717-249">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="d0717-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="d0717-250">ContentKeyType</span></span> |<span data-ttu-id="d0717-251">Tipo di chiave simmetrica, ovvero un numero intero per la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="d0717-251">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="d0717-252">Per la crittografia di archiviazione viene passato il valore 1.</span><span class="sxs-lookup"><span data-stu-id="d0717-252">We pass the value 1 for storage encryption.</span></span> |
| <span data-ttu-id="d0717-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="d0717-253">EncryptedContentKey</span></span> |<span data-ttu-id="d0717-254">Viene creato un nuovo valore di chiave simmetrica che corrisponde a un valore a 256 bit (32 byte).</span><span class="sxs-lookup"><span data-stu-id="d0717-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="d0717-255">La chiave viene crittografata mediante il certificato X.509 di crittografia di archiviazione recuperato da Servizi multimediali di Microsoft Azure eseguendo una richiesta HTTP GET per i metodi GetProtectionKeyId e GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="d0717-255">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="d0717-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="d0717-256">ProtectionKeyId</span></span> |<span data-ttu-id="d0717-257">ID della chiave di protezione per il certificato X.509 di crittografia di archiviazione usato per crittografare la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="d0717-257">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span> |
| <span data-ttu-id="d0717-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="d0717-258">ProtectionKeyType</span></span> |<span data-ttu-id="d0717-259">Tipo di crittografia per la chiave di protezione usata per crittografare la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="d0717-259">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="d0717-260">Per l'esempio questo valore è StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="d0717-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="d0717-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="d0717-261">Checksum</span></span> |<span data-ttu-id="d0717-262">Checksum MD5 calcolato per la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="d0717-262">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="d0717-263">Viene ricavato crittografando l'ID contenuto con la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="d0717-263">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="d0717-264">Il codice di esempio mostra come calcolare il checksum.</span><span class="sxs-lookup"><span data-stu-id="d0717-264">The example code demonstrates how to calculate the checksum.</span></span> |

<span data-ttu-id="d0717-265">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-the-contentkey-to-the-asset"></a><span data-ttu-id="d0717-266">Collegare l'entità ContentKey all'asset</span><span class="sxs-lookup"><span data-stu-id="d0717-266">Link the ContentKey to the Asset</span></span>
<span data-ttu-id="d0717-267">L'entità ContentKey viene associata a uno o più asset mediante l'invio di una richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d0717-267">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="d0717-268">La richiesta seguente fornisce un esempio di come collegare l'entità ContentKey di esempio all'asset di esempio in base all'ID.</span><span class="sxs-lookup"><span data-stu-id="d0717-268">The following request is an example to link the example ContentKey to the example asset by Id.</span></span>

<span data-ttu-id="d0717-269">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="d0717-270">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="d0717-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="d0717-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0717-271">Next steps</span></span>

<span data-ttu-id="d0717-272">Ora è possibile codificare gli asset caricati.</span><span class="sxs-lookup"><span data-stu-id="d0717-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="d0717-273">Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).</span><span class="sxs-lookup"><span data-stu-id="d0717-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="d0717-274">È anche possibile usare Funzioni di Azure per attivare un processo di codifica basato su un file che arriva nel contenitore configurato.</span><span class="sxs-lookup"><span data-stu-id="d0717-274">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="d0717-275">Per altre informazioni, vedere [questo esempio](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="d0717-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d0717-276">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="d0717-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d0717-277">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d0717-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How to Get a Media Processor]: media-services-get-media-processor.md

