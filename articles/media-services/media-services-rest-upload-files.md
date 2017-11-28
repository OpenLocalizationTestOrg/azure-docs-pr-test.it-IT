---
title: i file in un account di servizi multimediali con REST aaaUpload | Documenti Microsoft
description: Informazioni su come tooget multimediali in servizi multimediali tramite la creazione e caricamento di asset.
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
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="a4c86-103">Caricare file in un account di Servizi multimediali mediante REST</span><span class="sxs-lookup"><span data-stu-id="a4c86-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4c86-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a4c86-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="a4c86-105">REST</span><span class="sxs-lookup"><span data-stu-id="a4c86-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="a4c86-106">Portale</span><span class="sxs-lookup"><span data-stu-id="a4c86-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="a4c86-107">In Servizi multimediali è possibile caricare i file digitali in un asset.</span><span class="sxs-lookup"><span data-stu-id="a4c86-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="a4c86-108">Hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entità può contenere video, audio, immagini, raccolte di anteprime, testo tracce e sottotitoli file (e relativi metadati hello.)  Una volta caricati i file hello in asset hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso.</span><span class="sxs-lookup"><span data-stu-id="a4c86-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="a4c86-109">si applica Hello seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="a4c86-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="a4c86-110">Servizi multimediali Usa valore hello hello IAssetFile.Name proprietà durante la creazione di URL per hello streaming del contenuto (ad esempio, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Per questo motivo, la codifica percentuale non è consentita.</span><span class="sxs-lookup"><span data-stu-id="a4c86-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="a4c86-111">valore di hello Hello **nome** proprietà non può avere uno dei seguenti hello [% riservati per la codifica caratteri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="a4c86-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="a4c86-112">Inoltre, può essere presente solo uno '.' per l'estensione del nome file hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="a4c86-113">lunghezza Hello del nome di hello non deve essere maggiore di 260 caratteri.</span><span class="sxs-lookup"><span data-stu-id="a4c86-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="a4c86-114">È una limite toohello dimensione massima supportata per l'elaborazione in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="a4c86-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="a4c86-115">Vedere [questo](media-services-quotas-and-limitations.md) per informazioni sulla limitazione delle dimensioni del file hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="a4c86-116">flusso di lavoro base Hello per il caricamento delle risorse è suddivisa in hello le sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4c86-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="a4c86-117">Creare un asset</span><span class="sxs-lookup"><span data-stu-id="a4c86-117">Create an Asset</span></span>
* <span data-ttu-id="a4c86-118">Crittografare un asset (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="a4c86-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="a4c86-119">Caricare un archivio di file tooblob</span><span class="sxs-lookup"><span data-stu-id="a4c86-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="a4c86-120">AMS consente inoltre asset tooupload in blocco.</span><span class="sxs-lookup"><span data-stu-id="a4c86-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="a4c86-121">Per altre informazioni, vedere [questa](media-services-rest-upload-files.md#upload_in_bulk) sezione.</span><span class="sxs-lookup"><span data-stu-id="a4c86-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="a4c86-122">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="a4c86-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a4c86-123">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a4c86-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="a4c86-124">Connessione dei servizi tooMedia</span><span class="sxs-lookup"><span data-stu-id="a4c86-124">Connect tooMedia Services</span></span>

<span data-ttu-id="a4c86-125">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a4c86-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a4c86-126">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="a4c86-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a4c86-127">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="a4c86-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="a4c86-128">Caricare gli asset</span><span class="sxs-lookup"><span data-stu-id="a4c86-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="a4c86-129">Creare un asset</span><span class="sxs-lookup"><span data-stu-id="a4c86-129">Create an asset</span></span>

<span data-ttu-id="a4c86-130">Un asset è un contenitore di più tipi o set di oggetti in Servizi multimediali, inclusi elementi video e audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli chiusi.</span><span class="sxs-lookup"><span data-stu-id="a4c86-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="a4c86-131">Nell'API REST, creazione di un Asset richiede l'invio di POST hello richiedere servizi tooMedia e inserire informazioni delle proprietà relative all'asset nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="a4c86-132">Una delle proprietà hello che è possibile specificare quando la creazione di un asset è **opzioni**.</span><span class="sxs-lookup"><span data-stu-id="a4c86-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="a4c86-133">**Opzioni** è un valore di enumerazione che descrive le opzioni di crittografia hello che è possibile creare un Asset con.</span><span class="sxs-lookup"><span data-stu-id="a4c86-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="a4c86-134">Un valore valido è uno dei valori hello dall'elenco di hello riportato di seguito, non una combinazione di valori.</span><span class="sxs-lookup"><span data-stu-id="a4c86-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="a4c86-135">**None** = **0**: non viene applicata alcuna crittografia.</span><span class="sxs-lookup"><span data-stu-id="a4c86-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="a4c86-136">Questo è il valore di predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-136">This is hello default value.</span></span> <span data-ttu-id="a4c86-137">Quando si usa questa opzione, il contenuto non è protetto durante il transito, né nell'archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="a4c86-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="a4c86-138">Se si prevede di toodeliver un file MP4 tramite download progressivo, usare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="a4c86-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="a4c86-139">**StorageEncrypted** = **1**: specificare se si desidera per toobe i file crittografati con crittografia AES-256 bit per il caricamento e archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a4c86-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="a4c86-140">Se l'asset è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="a4c86-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="a4c86-141">Per altre informazioni, vedere [Procedura: Configurare i criteri di distribuzione degli asset](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a4c86-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="a4c86-142">**CommonEncryptionProtected** = **2**: consente di specificare se si desidera caricare i file protetti con un metodo di crittografia comune (ad esempio PlayReady).</span><span class="sxs-lookup"><span data-stu-id="a4c86-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="a4c86-143">**EnvelopeEncryptionProtected** = **4**: consente di specificare se si stanno caricando file HLS crittografati con AES.</span><span class="sxs-lookup"><span data-stu-id="a4c86-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="a4c86-144">Si noti che i file hello devono sono stati codificati e crittografati da Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="a4c86-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="a4c86-145">Se nell'asset verrà usata la crittografia, è necessario creare un **ContentKey** e collegarla tooyour asset come descritto nel seguente argomento hello:[come un'entità ContentKey toocreate](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="a4c86-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="a4c86-146">Si noti che dopo aver caricato il file hello in asset hello, è necessario tooupdate hello crittografia proprietà hello **AssetFile** entità con valori di hello ottenuto durante hello **Asset** crittografia.</span><span class="sxs-lookup"><span data-stu-id="a4c86-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="a4c86-147">Eseguire questa operazione utilizzando hello **MERGE** richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="a4c86-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="a4c86-148">Hello seguente esempio viene illustrato come toocreate un asset.</span><span class="sxs-lookup"><span data-stu-id="a4c86-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="a4c86-149">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-149">**HTTP Request**</span></span>

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

<span data-ttu-id="a4c86-150">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-150">**HTTP Response**</span></span>

<span data-ttu-id="a4c86-151">Se ha esito positivo, viene restituito l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="a4c86-151">If successful, hello following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="a4c86-152">Creare un'entità AssetFile</span><span class="sxs-lookup"><span data-stu-id="a4c86-152">Create an AssetFile</span></span>
<span data-ttu-id="a4c86-153">Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entità rappresenta un file video o audio che viene archiviato in un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="a4c86-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="a4c86-154">Un file di asset è sempre associato a un asset e un asset può contenere uno o più file.</span><span class="sxs-lookup"><span data-stu-id="a4c86-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="a4c86-155">attività di Media Services Encoder Hello non riesce se un oggetto di file di asset non è associato a un file digitale in un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="a4c86-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="a4c86-156">Si noti che hello **AssetFile** istanza e hello effettivo file multimediale sono due oggetti distinti.</span><span class="sxs-lookup"><span data-stu-id="a4c86-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="a4c86-157">istanza di AssetFile Hello contiene i metadati relativi a file di supporto hello, mentre i file di supporto hello contiene hello effettivo contenuto multimediale.</span><span class="sxs-lookup"><span data-stu-id="a4c86-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="a4c86-158">Dopo aver caricato il file multimediale digitale in un contenitore blob, si utilizzerà hello **MERGE** hello tooupdate HTTP richiesta AssetFile con le informazioni nel file multimediale (come illustrato più avanti nell'argomento hello).</span><span class="sxs-lookup"><span data-stu-id="a4c86-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="a4c86-159">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-159">**HTTP Request**</span></span>

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

<span data-ttu-id="a4c86-160">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-160">**HTTP Response**</span></span>

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="a4c86-161">Creazione di hello AccessPolicy con autorizzazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="a4c86-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="a4c86-162">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a4c86-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a4c86-163">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="a4c86-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a4c86-164">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="a4c86-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="a4c86-165">Prima di caricare i file nell'archiviazione blob, impostare l'accesso hello diritti sui criteri per la scrittura di tooan asset.</span><span class="sxs-lookup"><span data-stu-id="a4c86-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="a4c86-166">Imposta toodo che, invia un toohello di richiesta HTTP entità AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="a4c86-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="a4c86-167">Definire un valore DurationInMinutes durante la creazione. In caso contrario, si riceverà un messaggio di errore interno del server 500 in risposta.</span><span class="sxs-lookup"><span data-stu-id="a4c86-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="a4c86-168">Per altre informazioni su AccessPolicies, vedere [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="a4c86-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="a4c86-169">Hello seguente esempio viene illustrato come un'entità AccessPolicy toocreate:</span><span class="sxs-lookup"><span data-stu-id="a4c86-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="a4c86-170">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-170">**HTTP Request**</span></span>

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

<span data-ttu-id="a4c86-171">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="a4c86-172">Ottenere hello caricare URL</span><span class="sxs-lookup"><span data-stu-id="a4c86-172">Get hello Upload URL</span></span>
<span data-ttu-id="a4c86-173">tooreceive hello URL di caricamento effettivo, creare un localizzatore SAS.</span><span class="sxs-lookup"><span data-stu-id="a4c86-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="a4c86-174">I localizzatori definiscono l'ora di inizio hello e il tipo di endpoint di connessione per i client che desidera tooaccess i file in un Asset.</span><span class="sxs-lookup"><span data-stu-id="a4c86-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="a4c86-175">È possibile creare più entità Locator per un determinato AccessPolicy e Asset coppia toohandle diversi client richieste e alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="a4c86-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="a4c86-176">Ognuno di questi localizzatori utilizzare valori di StartTime hello e DurationInMinutes di hello di hello AccessPolicy toodetermine hello periodo di tempo è possibile utilizzare un URL.</span><span class="sxs-lookup"><span data-stu-id="a4c86-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="a4c86-177">Per altre informazioni, vedere [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="a4c86-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="a4c86-178">Un URL SAS è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="a4c86-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="a4c86-179">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="a4c86-179">Some considerations apply:</span></span>

* <span data-ttu-id="a4c86-180">Non è possibile avere più di cinque localizzatori univoci associati contemporaneamente a un determinato asset.</span><span class="sxs-lookup"><span data-stu-id="a4c86-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="a4c86-181">Per altre informazioni, vedere Locator.</span><span class="sxs-lookup"><span data-stu-id="a4c86-181">For more information, see Locator.</span></span>
* <span data-ttu-id="a4c86-182">Se occorre tooupload i file immediatamente, è necessario impostare i minuti di toofive valore StartTime prima hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="a4c86-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="a4c86-183">Potrebbe infatti essere presente una leggera differenza di orario tra il computer client e Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="a4c86-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="a4c86-184">Inoltre, il valore StartTime deve essere nel seguente formato DateTime hello: aaaa-MM-ddTHH (ad esempio, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="a4c86-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="a4c86-185">Potrebbe esserci un 30-40 secondi ritardare dopo la creazione di un indicatore di posizione toowhen è disponibile per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="a4c86-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="a4c86-186">Questo problema si applica tooboth URL SAS e localizzatori di origine.</span><span class="sxs-lookup"><span data-stu-id="a4c86-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="a4c86-187">Hello di esempio seguente viene illustrato come un localizzatore URL SAS, come definito da toocreate hello proprietà del tipo nel corpo della richiesta hello ("1" per un localizzatore SAS) e "2" per un localizzatore di origine su richiesta.</span><span class="sxs-lookup"><span data-stu-id="a4c86-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="a4c86-188">Hello **percorso** proprietà restituita contiene hello URL che è necessario utilizzare tooupload il file.</span><span class="sxs-lookup"><span data-stu-id="a4c86-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="a4c86-189">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-189">**HTTP Request**</span></span>

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

<span data-ttu-id="a4c86-190">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-190">**HTTP Response**</span></span>

<span data-ttu-id="a4c86-191">Se ha esito positivo, viene restituito hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="a4c86-191">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="a4c86-192">Caricare un file in un contenitore di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="a4c86-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="a4c86-193">Dopo aver creato AccessPolicy hello e set di localizzazione, file effettivo hello è il contenitore di archiviazione Blob di Azure tooan caricato utilizzando hello API REST dell'archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c86-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="a4c86-194">È necessario caricare il file hello come BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="a4c86-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="a4c86-195">I BLOB di pagine non sono supportati da Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c86-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="a4c86-196">È necessario aggiungere il nome di file hello per file hello desiderato tooupload toohello localizzatore **percorso** valore ricevuto nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="a4c86-197">Ad esempio, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="a4c86-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="a4c86-198">.</span><span class="sxs-lookup"><span data-stu-id="a4c86-198">.</span></span> <span data-ttu-id="a4c86-199">.</span><span class="sxs-lookup"><span data-stu-id="a4c86-199">.</span></span> <span data-ttu-id="a4c86-200">.</span><span class="sxs-lookup"><span data-stu-id="a4c86-200">.</span></span> 
> 
> 

<span data-ttu-id="a4c86-201">Per altre informazioni sull'uso dei BLOB di Archiviazione di Azure, vedere [API REST del servizio BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="a4c86-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="a4c86-202">Aggiornare hello AssetFile</span><span class="sxs-lookup"><span data-stu-id="a4c86-202">Update hello AssetFile</span></span>
<span data-ttu-id="a4c86-203">Ora che è stato caricato il file, è possibile aggiornare le informazioni di FileAsset dimensioni (e altri) hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="a4c86-204">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a4c86-204">For example:</span></span>

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


<span data-ttu-id="a4c86-205">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-205">**HTTP Response**</span></span>

<span data-ttu-id="a4c86-206">Se ha esito positivo, seguito hello viene restituito: HTTP/1.1 204 Nessun contenuto</span><span class="sxs-lookup"><span data-stu-id="a4c86-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="a4c86-207">Eliminare hello localizzatore e AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="a4c86-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="a4c86-208">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="a4c86-209">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-209">**HTTP Response**</span></span>

<span data-ttu-id="a4c86-210">Se ha esito positivo, viene restituito l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="a4c86-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="a4c86-211">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="a4c86-212">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-212">**HTTP Response**</span></span>

<span data-ttu-id="a4c86-213">Se ha esito positivo, viene restituito l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="a4c86-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="a4c86-214"><a id="upload_in_bulk"></a>Caricare gli asset in blocco</span><span class="sxs-lookup"><span data-stu-id="a4c86-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="a4c86-215">Creare hello entità IngestManifest</span><span class="sxs-lookup"><span data-stu-id="a4c86-215">Create hello IngestManifest</span></span>
<span data-ttu-id="a4c86-216">Hello entità IngestManifest è un contenitore per un set di asset, file di asset e informazioni statistiche che possono essere utilizzato lo stato di avanzamento di toodetermine hello l'inserimento in blocco per il set di hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="a4c86-217">**Richiesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-217">**HTTP Request**</span></span>

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

### <a name="create-assets"></a><span data-ttu-id="a4c86-218">Creare gli asset</span><span class="sxs-lookup"><span data-stu-id="a4c86-218">Create assets</span></span>
<span data-ttu-id="a4c86-219">Prima di creare hello entità IngestManifestAsset, è necessario toocreate hello Asset che verrà completato usando l'inserimento in blocco.</span><span class="sxs-lookup"><span data-stu-id="a4c86-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="a4c86-220">Un asset è un contenitore di più tipi o set di oggetti in Servizi multimediali, inclusi elementi video e audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli chiusi.</span><span class="sxs-lookup"><span data-stu-id="a4c86-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="a4c86-221">In hello API REST, la creazione di un Asset richiede l'invio di un tooMicrosoft di richiesta HTTP POST servizi multimediali di Azure e inserire informazioni delle proprietà relative all'asset nel corpo della richiesta hello. In questo esempio hello Asset viene creato utilizzando l'opzione StorageEncrption(1) hello incluso con il corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="a4c86-222">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-222">**HTTP Response**</span></span>

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

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="a4c86-223">Creare le entità Ingestmanifestasset hello</span><span class="sxs-lookup"><span data-stu-id="a4c86-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="a4c86-224">Le entità IngestManifestAsset rappresentano gli asset all'interno dell'entità IngestManifest usati durante l'inserimento in blocco.</span><span class="sxs-lookup"><span data-stu-id="a4c86-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="a4c86-225">Hello fondamentalmente manifesto toohello asset hello del collegamento.</span><span class="sxs-lookup"><span data-stu-id="a4c86-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="a4c86-226">Servizi multimediali di Azure controlla internamente il caricamento di file hello in base alle entità Ingestmanifestfile insieme toohello entità IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="a4c86-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="a4c86-227">Una volta che questi file vengono caricati, asset hello viene completata.</span><span class="sxs-lookup"><span data-stu-id="a4c86-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="a4c86-228">È possibile creare una nuova entità IngestManifestAsset mediante una richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a4c86-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="a4c86-229">Nel corpo della richiesta hello, includere hello IngestManifest Id e hello Id Asset che hello essere collegati da IngestManifestAsset per l'inserimento in blocco.</span><span class="sxs-lookup"><span data-stu-id="a4c86-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="a4c86-230">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-230">**HTTP Response**</span></span>

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


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="a4c86-231">Creare le entità Ingestmanifestfile hello per ogni Asset</span><span class="sxs-lookup"><span data-stu-id="a4c86-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="a4c86-232">Un'entità IngestManifestFile rappresenta un oggetto BLOB audio o video che verrà caricato nel corso del caricamento in blocco di un asset.</span><span class="sxs-lookup"><span data-stu-id="a4c86-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="a4c86-233">Proprietà non sono necessarie a meno che non utilizza un'opzione di crittografia asset hello relative a crittografia.</span><span class="sxs-lookup"><span data-stu-id="a4c86-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="a4c86-234">esempio Hello utilizzato in questa sezione viene illustrato come la creazione di un'entità IngestManifestFile che usa StorageEncryption per hello che asset creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4c86-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="a4c86-235">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-235">**HTTP Response**</span></span>

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

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="a4c86-236">Caricare i file di hello tooBlob archiviazione</span><span class="sxs-lookup"><span data-stu-id="a4c86-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="a4c86-237">È possibile utilizzare qualsiasi applicazione client ad alta velocità in grado di caricare hello asset file toohello contenitore di archiviazione blob Uri fornito da hello proprietà BlobStorageUriForUpload di hello entità IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="a4c86-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="a4c86-238">Un servizio di caricamento ad alta velocità consigliato è l'applicazione [Aspera On Demand for Azure](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="a4c86-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="a4c86-239">Monitorare lo stato di avanzamento dell'inserimento in blocco</span><span class="sxs-lookup"><span data-stu-id="a4c86-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="a4c86-240">È possibile monitorare lo stato di avanzamento hello di inserimento di operazioni per un'entità IngestManifest eseguendo il polling delle proprietà di hello Statistics di IngestManifest hello in blocco.</span><span class="sxs-lookup"><span data-stu-id="a4c86-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="a4c86-241">Tale proprietà è un tipo complesso, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="a4c86-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="a4c86-242">hello toopoll proprietà Statistics, inviare una richiesta HTTP GET passando hello ID di IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="a4c86-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="a4c86-243">Creare chiavi simmetriche per la crittografia</span><span class="sxs-lookup"><span data-stu-id="a4c86-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="a4c86-244">Se nell'asset verrà usata la crittografia, è necessario creare hello ContentKey toobe utilizzata per la crittografia prima di creare file di asset di hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="a4c86-245">Per la crittografia di archiviazione, hello proprietà seguenti devono essere incluse nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="a4c86-246">Proprietà del corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="a4c86-246">Request body property</span></span> | <span data-ttu-id="a4c86-247">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4c86-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a4c86-248">ID</span><span class="sxs-lookup"><span data-stu-id="a4c86-248">Id</span></span> |<span data-ttu-id="a4c86-249">Hello ContentKey Id che viene generato effettuata utilizzando hello seguente formato, "NB:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="a4c86-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="a4c86-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="a4c86-250">ContentKeyType</span></span> |<span data-ttu-id="a4c86-251">Questo è il tipo di chiave simmetrica di hello come numero intero per questa chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="a4c86-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="a4c86-252">Passato valore hello 1 per la crittografia di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a4c86-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="a4c86-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="a4c86-253">EncryptedContentKey</span></span> |<span data-ttu-id="a4c86-254">Viene creato un nuovo valore di chiave simmetrica che corrisponde a un valore a 256 bit (32 byte).</span><span class="sxs-lookup"><span data-stu-id="a4c86-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="a4c86-255">crittografia della chiave Hello mediante hello certificato crittografia di archiviazione x. 509 che viene recuperato da servizi multimediali di Microsoft Azure tramite l'esecuzione di una richiesta HTTP GET per hello GetProtectionKeyId e GetProtectionKey metodi.</span><span class="sxs-lookup"><span data-stu-id="a4c86-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="a4c86-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="a4c86-256">ProtectionKeyId</span></span> |<span data-ttu-id="a4c86-257">Questo è hello id chiave di protezione per hello certificato crittografia di archiviazione x. 509 che è stato utilizzato tooencrypt la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="a4c86-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="a4c86-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="a4c86-258">ProtectionKeyType</span></span> |<span data-ttu-id="a4c86-259">Questo è il tipo di crittografia per la chiave di protezione hello che è stato utilizzato tooencrypt chiave simmetrica di hello hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="a4c86-260">Per l'esempio questo valore è StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="a4c86-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="a4c86-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="a4c86-261">Checksum</span></span> |<span data-ttu-id="a4c86-262">checksum calcolato di Hello MD5 per la chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="a4c86-263">Viene calcolato crittografando l'Id contenuto hello con chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="a4c86-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="a4c86-264">codice di esempio Hello viene illustrato come toocalculate hello checksum.</span><span class="sxs-lookup"><span data-stu-id="a4c86-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="a4c86-265">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-265">**HTTP Response**</span></span>

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

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="a4c86-266">Collegamento hello ContentKey toohello Asset</span><span class="sxs-lookup"><span data-stu-id="a4c86-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="a4c86-267">Hello ContentKey è tooone associato o più asset inviando una richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a4c86-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="a4c86-268">richiesta seguente Hello è un esempio toolink hello esempio ContentKey toohello esempio asset da ID.</span><span class="sxs-lookup"><span data-stu-id="a4c86-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="a4c86-269">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-269">**HTTP Response**</span></span>

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

<span data-ttu-id="a4c86-270">**Risposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="a4c86-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="a4c86-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4c86-271">Next steps</span></span>

<span data-ttu-id="a4c86-272">Ora è possibile codificare gli asset caricati.</span><span class="sxs-lookup"><span data-stu-id="a4c86-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="a4c86-273">Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).</span><span class="sxs-lookup"><span data-stu-id="a4c86-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="a4c86-274">È possibile utilizzare anche funzioni Azure tootrigger un processo di codifica in base a un file in arrivo nel contenitore hello configurato.</span><span class="sxs-lookup"><span data-stu-id="a4c86-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="a4c86-275">Per altre informazioni, vedere [questo esempio](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="a4c86-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a4c86-276">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a4c86-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a4c86-277">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="a4c86-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

