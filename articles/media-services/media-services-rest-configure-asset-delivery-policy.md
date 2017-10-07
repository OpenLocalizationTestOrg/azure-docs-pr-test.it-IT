---
title: i criteri di distribuzione aaaConfiguring asset usando l'API REST di servizi multimediali | Documenti Microsoft
description: Questo argomento viene illustrato come i criteri di distribuzione diversi asset tooconfigure utilizzando l'API REST di servizi multimediali.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="d8d4b-103">Configurazione dei criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="d8d4b-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="d8d4b-104">Se si prevede di asset toodeliver crittografati in modo dinamico, uno di hello passaggi hello contenuto di flusso di lavoro di recapito consiste nella configurazione di criteri di distribuzione per gli asset di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="d8d4b-105">criteri di distribuzione di asset Hello indicano a servizi multimediali la modalità desiderata per l'asset toobe recapitati: in quale protocollo di streaming deve l'asset essere dinamicamente incluso nel pacchetto (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), se si desidera toodynamically o meno crittografare l'asset e come (busta o la crittografia comune).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="d8d4b-106">In questo argomento viene descritto come e perché toocreate e configurare i criteri di recapito di asset.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="d8d4b-107">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d8d4b-108">lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="d8d4b-109">Inoltre, toobe toouse in grado di creazione dinamica dei pacchetti e la crittografia dinamica dell'asset deve contenere un set di velocità in bit adattiva MP4s o file Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="d8d4b-110">È possibile applicare criteri diversi toohello stesso asset.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="d8d4b-111">Ad esempio, è possibile applicare PlayReady crittografia tooSmooth Streaming ed Envelope AES crittografia tooMPEG DASH e HLS.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="d8d4b-112">Tutti i protocolli che non sono definiti in un criterio di recapito (ad esempio, aggiungere un singolo criterio che specifica solo HLS come protocollo di hello) verrà impedito lo streaming.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="d8d4b-113">toothis eccezione Hello è se non sono presenti criteri di recapito di asset definito in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="d8d4b-114">Quindi, saranno possibile tutti i protocolli in crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="d8d4b-115">Se si desidera toodeliver asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset hello.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="d8d4b-116">Prima dell'asset può essere trasmesso, hello streaming flussi e crittografia di archiviazione hello viene rimosso il server dei contenuti usando hello specificati criteri di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="d8d4b-117">Ad esempio, toodeliver l'asset crittografato con una chiave di crittografia envelope Advanced Encryption Standard (AES), impostare il tipo di criteri di hello troppo**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="d8d4b-118">crittografia di archiviazione tooremove e le risorse hello flusso hello chiara, impostare il tipo di criteri di hello troppo**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="d8d4b-119">Esempi che illustrano come tooconfigure questi tipi di criteri seguono.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="d8d4b-120">A seconda della configurazione di criteri di distribuzione di hello asset si sarebbe toodynamically in grado di pacchetto, in modo dinamico crittografare ed eseguire il flusso hello seguenti protocolli di streaming: Smooth Streaming, HLS, flussi MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="d8d4b-121">Dopo l'elenco Mostra hello Hello formatta utilizzare toostream Smooth, HLS, DASH.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="d8d4b-122">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-122">Smooth Streaming:</span></span>

<span data-ttu-id="d8d4b-123">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="d8d4b-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="d8d4b-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-124">HLS:</span></span>

<span data-ttu-id="d8d4b-125">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="d8d4b-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="d8d4b-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="d8d4b-126">MPEG DASH</span></span>

<span data-ttu-id="d8d4b-127">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="d8d4b-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="d8d4b-128">Per istruzioni su come toopublish un asset e compilare un URL di streaming, vedere [compilare un URL di streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="d8d4b-129">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="d8d4b-129">Considerations</span></span>
* <span data-ttu-id="d8d4b-130">Non è possbile eliminare un AssetDeliveryPolicy con un asset se esiste un localizzatore OnDemand (streaming) per quell’asset.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="d8d4b-131">criteri di hello tooremove da asset hello Hello consiglia prima di eliminare i criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="d8d4b-132">Non è possibile creare un localizzatore di streaming in un asset crittografato per l’archiviazione se non è impostato alcun criterio di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="d8d4b-133">Se non è hello Asset crittografato di archiviazione, sistema hello consentirà di creare un asset di hello localizzatore e il flusso in hello deselezionare senza un criterio di recapito di asset.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="d8d4b-134">È possibile avere più criteri di recapito di asset associati a un singolo asset, ma è possibile specificare solo un modo toohandle AssetDeliveryProtocol un determinato.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="d8d4b-135">Vale a dire se si tenta di toolink due criteri di recapito che specificare hello AssetDeliveryProtocol.SmoothStreaming protocollo che verrà generato un errore perché il sistema di hello non sapere quale si desidera che tooapply quando un client effettua una richiesta di Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="d8d4b-136">Se si dispone di un asset con un localizzatore di streaming esistente, non è possibile collegare un nuovo asset toohello criteri, scollegare un criterio esistente da asset hello o aggiornare i criteri di recapito associato hello asset.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="d8d4b-137">Prima hanno localizzatore di streaming hello tooremove, modificare criteri hello e quindi ricreare hello localizzatore di streaming.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="d8d4b-138">È possibile utilizzare hello locatorId stesso quando si ricrea hello streaming localizzatore, ma è necessario assicurarsi che non causino problemi per i client poiché il contenuto può essere memorizzato nella cache dall'origine hello o una rete CDN a valle.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="d8d4b-139">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d8d4b-140">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="d8d4b-141">Connessione dei servizi tooMedia</span><span class="sxs-lookup"><span data-stu-id="d8d4b-141">Connect tooMedia Services</span></span>

<span data-ttu-id="d8d4b-142">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d8d4b-143">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d8d4b-144">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="d8d4b-145">Criteri di distribuzione degli asset Clear</span><span class="sxs-lookup"><span data-stu-id="d8d4b-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="d8d4b-146"><a id="create_asset_delivery_policy"></a>Creare criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="d8d4b-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="d8d4b-147">richiesta HTTP seguente Hello crea un criterio di recapito di asset che specifica toonot applicare la crittografia dinamica e protocolli di flusso hello toodeliver in uno dei seguenti hello: protocolli MPEG DASH, HLS e Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="d8d4b-148">Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="d8d4b-149">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-149">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

<span data-ttu-id="d8d4b-150">Risposta:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-150">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <span data-ttu-id="d8d4b-151"><a id="link_asset_with_asset_delivery_policy"></a>Collegare un asset ai criteri di distribuzione</span><span class="sxs-lookup"><span data-stu-id="d8d4b-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="d8d4b-152">Hello hello collegamenti di richiesta HTTP seguente specifica criteri di distribuzione di asset toohello asset per.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="d8d4b-153">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-153">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

<span data-ttu-id="d8d4b-154">Risposta:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="d8d4b-155">Criteri di distribuzione degli asset DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="d8d4b-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="d8d4b-156">Creare la chiave simmetrica di tipo EnvelopeEncryption hello e collegarlo toohello asset</span><span class="sxs-lookup"><span data-stu-id="d8d4b-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="d8d4b-157">Quando si specificano i criteri di distribuzione DynamicEnvelopeEncryption, è necessario toolink che toomake la chiave simmetrica tooa di asset di hello EnvelopeEncryption tipo.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="d8d4b-158">Per altre informazioni, vedere [Creazione di una chiave simmetrica](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="d8d4b-159"><a id="get_delivery_url"></a>Ottenere l'URL di distribuzione</span><span class="sxs-lookup"><span data-stu-id="d8d4b-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="d8d4b-160">Metodo di distribuzione della chiave simmetrica di hello creato nel passaggio precedente hello specificare l'URL di recapito di hello get per hello.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="d8d4b-161">Un client utilizza hello restituito toorequest URL contenuto protetto da una chiave AES o una licenza PlayReady in hello tooplayback ordine.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="d8d4b-162">Specificare il tipo di hello di hello URL tooget nel corpo di hello della richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="d8d4b-163">Se si desidera proteggere i contenuti con PlayReady, richiedere un URL di acquisizione di licenze PlayReady di servizi multimediali, con 1 per keyDeliveryType hello: {"keyDeliveryType": 1}.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="d8d4b-164">Se si desidera proteggere i contenuti con crittografia envelope hello, richiedere un URL di acquisizione chiave specificando 2 per keyDeliveryType: {"keyDeliveryType": 2}.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="d8d4b-165">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-165">Request:</span></span>

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

<span data-ttu-id="d8d4b-166">Risposta:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-166">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="d8d4b-167">Creare criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="d8d4b-167">Create asset delivery policy</span></span>
<span data-ttu-id="d8d4b-168">richiesta HTTP seguente Hello crea hello **AssetDeliveryPolicy** ovvero crittografia envelope dinamici di tooapply configurato (**DynamicEnvelopeEncryption**) toohello **HLS**protocollo (in questo esempio, gli altri protocolli verranno impediti lo streaming).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="d8d4b-169">Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="d8d4b-170">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-170">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


<span data-ttu-id="d8d4b-171">Risposta:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-171">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="d8d4b-172">Collegare un asset ai criteri di distribuzione</span><span class="sxs-lookup"><span data-stu-id="d8d4b-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="d8d4b-173">Vedere [Collegare un asset ai criteri di distribuzione](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="d8d4b-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="d8d4b-174">Criteri di distribuzione degli asset DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="d8d4b-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="d8d4b-175">Creare la chiave simmetrica di tipo CommonEncryption hello e collegarlo toohello asset</span><span class="sxs-lookup"><span data-stu-id="d8d4b-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="d8d4b-176">Quando si specificano i criteri di distribuzione DynamicCommonEncryption, è necessario toolink che toomake la chiave simmetrica tooa di asset di hello CommonEncryption tipo.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="d8d4b-177">Per altre informazioni, vedere [Creazione di una chiave simmetrica](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="d8d4b-178">Ottenere l'URL di distribuzione</span><span class="sxs-lookup"><span data-stu-id="d8d4b-178">Get Delivery URL</span></span>
<span data-ttu-id="d8d4b-179">Ottenere un URL di recapito hello hello PlayReady del metodo di consegna della chiave di hello contenuto creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="d8d4b-180">Un client utilizza hello restituito toorequest URL protetto da una licenza PlayReady in hello tooplayback order content.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="d8d4b-181">Per altre informazioni, vedere [Ottenere l'URL di distribuzione](#get_delivery_url).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="d8d4b-182">Creare criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="d8d4b-182">Create asset delivery policy</span></span>
<span data-ttu-id="d8d4b-183">richiesta HTTP seguente Hello crea hello **AssetDeliveryPolicy** ovvero tooapply configurato comuni crittografia dinamica (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocollo (in questo esempio, gli altri protocolli verranno impediti lo streaming).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="d8d4b-184">Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="d8d4b-185">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-185">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


<span data-ttu-id="d8d4b-186">Se si desidera tooprotect il contenuto con DRM Widevine, aggiornare hello AssetDeliveryConfiguration valori toouse WidevineLicenseAcquisitionUrl (che presenta il valore di hello pari a 7) e specificare hello URL di un servizio di recapito di licenza.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="d8d4b-187">È possibile utilizzare hello seguente toohelp partner AMS di consegnare licenze Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="d8d4b-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="d8d4b-188">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d8d4b-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="d8d4b-189">Durante la crittografia con Widevine, sarà solo in grado di toodeliver utilizzando trattino.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="d8d4b-190">Verificare che toospecify DASH (2) hello in asset il protocollo di recapito.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="d8d4b-191">Collegare un asset ai criteri di distribuzione</span><span class="sxs-lookup"><span data-stu-id="d8d4b-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="d8d4b-192">Vedere [Collegare un asset ai criteri di distribuzione](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="d8d4b-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="d8d4b-193"><a id="types"></a></span><span class="sxs-lookup"><span data-stu-id="d8d4b-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="d8d4b-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="d8d4b-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="d8d4b-195">Hello enum seguente descrive i possibili valori per il protocollo di recapito hello asset.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="d8d4b-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="d8d4b-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="d8d4b-197">Hello enum seguente vengono descritti i possibili valori per tipo di criterio di recapito asset hello.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a><span data-ttu-id="d8d4b-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="d8d4b-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="d8d4b-199">Hello enum seguente descrive i valori è possibile utilizzare metodo di recapito tooconfigure hello del client toohello chiave contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="d8d4b-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="d8d4b-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="d8d4b-201">Hello enum seguente descrive i possibili valori tooconfigure le chiavi usate tooget configurazione specifica per un criterio di recapito di asset.</span><span class="sxs-lookup"><span data-stu-id="d8d4b-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="d8d4b-202">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="d8d4b-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d8d4b-203">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d8d4b-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

