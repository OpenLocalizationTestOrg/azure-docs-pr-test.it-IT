---
title: Configurazione dei criteri di distribuzione degli asset usando l'API REST di Servizi multimediali | Microsoft Docs
description: Questo argomento illustra come configurare criteri di distribuzione degli asset differenti utilizzando l'API REST di Servizi multimediali.
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
ms.openlocfilehash: 7ffbde11b943961dd3a3b5edebd0cfd52429e845
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="9c311-103">Configurazione dei criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="9c311-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="9c311-104">Se si prevede di distribuire asset crittografati in modo dinamico, uno dei passaggi del flusso di lavoro di distribuzione dei contenuti in Servizi multimediali consiste nella configurazione dei criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="9c311-104">If you plan to deliver dynamically encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="9c311-105">Questi criteri indicano a Servizi multimediali la modalità di distribuzione di un asset, ovvero il protocollo di streaming da usare per la creazione dinamica dei pacchetti (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), se l'asset deve essere crittografato dinamicamente e l'eventuale modalità di crittografia (envelope o common).</span><span class="sxs-lookup"><span data-stu-id="9c311-105">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="9c311-106">Questo argomento illustra perché e come creare i criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="9c311-106">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="9c311-107">Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="9c311-107">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="9c311-108">Per avviare lo streaming del contenuto e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming da cui si vuole trasmettere il contenuto deve essere nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="9c311-108">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="9c311-109">Per usare la creazione dinamica dei pacchetti e la crittografia dinamica, l'asset deve contenere un set di file MP4 o Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="9c311-109">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="9c311-110">È possibile applicare criteri differenti allo stesso asset.</span><span class="sxs-lookup"><span data-stu-id="9c311-110">You could apply different policies to the same asset.</span></span> <span data-ttu-id="9c311-111">È ad esempio possibile applicare la crittografia PlayReady a Smooth Streaming e la crittografia envelope AES (Advanced Encryption Standard) a MPEG DASH e HLS.</span><span class="sxs-lookup"><span data-stu-id="9c311-111">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="9c311-112">Gli eventuali protocolli non definiti nei criteri di distribuzione (ad esempio quando si aggiunge un singolo criterio che specifica soltanto HLS come protocollo) verranno esclusi dallo streaming.</span><span class="sxs-lookup"><span data-stu-id="9c311-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="9c311-113">Questo comportamento non si verifica quando non è presente alcun criterio di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="9c311-113">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="9c311-114">In tal caso, sono consentiti tutti i protocolli in chiaro.</span><span class="sxs-lookup"><span data-stu-id="9c311-114">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="9c311-115">Se si desidera distribuire un asset con memoria crittografata, è necessario configurare i criteri di distribuzione appropriati.</span><span class="sxs-lookup"><span data-stu-id="9c311-115">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="9c311-116">Prima di trasmettere in streaming l'asset in base ai criteri specificati, il server rimuove la crittografia di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9c311-116">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="9c311-117">Ad esempio, per distribuire l'asset crittografato con una chiave di crittografia envelope AES (Advanced Encryption Standard), impostare il tipo di criteri su **DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="9c311-117">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="9c311-118">Per rimuovere la crittografia di archiviazione e trasmettere l'asset in chiaro, impostare il tipo di criteri su **NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="9c311-118">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="9c311-119">I seguenti esempi mostrano come configurare questi tipi di criteri.</span><span class="sxs-lookup"><span data-stu-id="9c311-119">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="9c311-120">A seconda della modalità di configurazione dei criteri di distribuzione degli asset, sarà possibile creare dinamicamente i pacchetti, applicare la crittografia dinamica e trasmettere i protocolli di streaming seguenti: Smooth Streaming, HLS e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="9c311-120">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="9c311-121">L'elenco seguente mostra i formati usati per i flussi Smooth, HLS e DASH.</span><span class="sxs-lookup"><span data-stu-id="9c311-121">The following list shows the formats that you use to stream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="9c311-122">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="9c311-122">Smooth Streaming:</span></span>

<span data-ttu-id="9c311-123">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="9c311-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="9c311-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="9c311-124">HLS:</span></span>

<span data-ttu-id="9c311-125">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="9c311-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="9c311-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="9c311-126">MPEG DASH</span></span>

<span data-ttu-id="9c311-127">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="9c311-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="9c311-128">Per istruzioni su come pubblicare un asset e creare un URL di streaming, vedere la sezione [Creare URL di streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="9c311-128">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="9c311-129">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="9c311-129">Considerations</span></span>
* <span data-ttu-id="9c311-130">Non è possbile eliminare un AssetDeliveryPolicy con un asset se esiste un localizzatore OnDemand (streaming) per quell’asset.</span><span class="sxs-lookup"><span data-stu-id="9c311-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="9c311-131">Si suggerisce di rimuovere il criterio dall'asset prima di eliminare il criterio.</span><span class="sxs-lookup"><span data-stu-id="9c311-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="9c311-132">Non è possibile creare un localizzatore di streaming in un asset crittografato per l’archiviazione se non è impostato alcun criterio di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="9c311-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="9c311-133">Se l'asset non è crittografato per l'archiviazione, il sistema consentirà di creare un localizzatore ed eseguire in streaming l'asset in chiaro senza un criterio di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="9c311-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="9c311-134">È possibile avere più criteri di distribuzione degli asset associati a un singolo asset, ma è possibile specificare solo un modo per gestire un determinato AssetDeliveryProtocol.</span><span class="sxs-lookup"><span data-stu-id="9c311-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="9c311-135">Ciò significa che se si tenta di collegare due criteri di distribuzione che specificano il protocollo AssetDeliveryProtocol.SmoothStreaming, verrà generato un errore perché il sistema non sa quale applicare quando un client effettua una richiesta di Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="9c311-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="9c311-136">Se si dispone di un asset con un localizzatore di streaming esistente, non è possibile collegare un nuovo criterio all'asset, scollegare un criterio esistente dall'asset, o aggiornare un criterio di distribuzione associato all'asset.</span><span class="sxs-lookup"><span data-stu-id="9c311-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset, unlink an existing policy from the asset, or update a delivery policy associated with the asset.</span></span>  <span data-ttu-id="9c311-137">È innanzitutto necessario rimuovere il localizzatore di streaming, modificare i criteri e quindi creare nuovamente il localizzatore di streaming.</span><span class="sxs-lookup"><span data-stu-id="9c311-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="9c311-138">È possibile utilizzare lo stesso ID quando si ricrea il localizzatore di streaming, ma è necessario assicurarsi che questo non causi problemi per i client poiché il contenuto può essere memorizzato nella cache per l'origine o una rete CDN a valle.</span><span class="sxs-lookup"><span data-stu-id="9c311-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="9c311-139">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="9c311-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="9c311-140">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9c311-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="9c311-141">Connettersi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="9c311-141">Connect to Media Services</span></span>

<span data-ttu-id="9c311-142">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="9c311-142">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="9c311-143">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="9c311-143">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="9c311-144">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="9c311-144">You must make subsequent calls to the new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="9c311-145">Criteri di distribuzione degli asset Clear</span><span class="sxs-lookup"><span data-stu-id="9c311-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="9c311-146"><a id="create_asset_delivery_policy"></a>Creare criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="9c311-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="9c311-147">La seguente richiesta HTTP crea criteri di distribuzione degli asset che indicano di non applicare la crittografia dinamica e di distribuire il flusso con uno dei seguenti protocolli: MPEG DASH, HLS e Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="9c311-147">The following HTTP request creates an asset delivery policy that specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="9c311-148">Per informazioni sui valori che è possibile specificare quando si crea un oggetto AssetDeliveryPolicy, vedere la sezione [Tipi usati durante la definizione di AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="9c311-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="9c311-149">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="9c311-149">Request:</span></span>

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

<span data-ttu-id="9c311-150">Risposta:</span><span class="sxs-lookup"><span data-stu-id="9c311-150">Response:</span></span>

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

### <span data-ttu-id="9c311-151"><a id="link_asset_with_asset_delivery_policy"></a>Collegare un asset ai criteri di distribuzione</span><span class="sxs-lookup"><span data-stu-id="9c311-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="9c311-152">La seguente richiesta HTTP collega l'asset specificato ai relativi criteri di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9c311-152">The following HTTP request links the specified asset to the asset delivery policy to.</span></span>

<span data-ttu-id="9c311-153">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="9c311-153">Request:</span></span>

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

<span data-ttu-id="9c311-154">Risposta:</span><span class="sxs-lookup"><span data-stu-id="9c311-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="9c311-155">Criteri di distribuzione degli asset DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="9c311-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-envelopeencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="9c311-156">Creare una chiave simmetrica di tipo EnvelopeEncryption e collegarla all'asset</span><span class="sxs-lookup"><span data-stu-id="9c311-156">Create content key of the EnvelopeEncryption type and link it to the asset</span></span>
<span data-ttu-id="9c311-157">Quando si specificano criteri di distribuzione DynamicEnvelopeEncryption, è necessario assicurarsi di collegare l'asset a una chiave simmetrica di tipo EnvelopeEncryption.</span><span class="sxs-lookup"><span data-stu-id="9c311-157">When specifying DynamicEnvelopeEncryption delivery policy, you need to make sure to link your asset to a content key of the EnvelopeEncryption type.</span></span> <span data-ttu-id="9c311-158">Per altre informazioni, vedere [Creazione di una chiave simmetrica](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="9c311-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="9c311-159"><a id="get_delivery_url"></a>Ottenere l'URL di distribuzione</span><span class="sxs-lookup"><span data-stu-id="9c311-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="9c311-160">Ottenere l'URL relativo al metodo di distribuzione specificato per la chiave simmetrica creata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="9c311-160">Get the delivery URL for the specified delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="9c311-161">Un client usa l'URL restituito per richiedere una chiave AES oppure una licenza PlayReady allo scopo di riprodurre contenuto protetto.</span><span class="sxs-lookup"><span data-stu-id="9c311-161">A client uses the returned URL to request an AES key or a PlayReady license in order to playback the protected content.</span></span>

<span data-ttu-id="9c311-162">Specificare il tipo di URL da ottenere nel corpo della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="9c311-162">Specify the type of the URL to get in the body of the HTTP request.</span></span> <span data-ttu-id="9c311-163">Se si desidera proteggere i contenuti con PlayReady, richiedere un URL di acquisizione licenza di PlayReady per Servizi multimediali, usando 1 per keyDeliveryType: {"keyDeliveryType":1}.</span><span class="sxs-lookup"><span data-stu-id="9c311-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for the keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="9c311-164">Se si desidera proteggere i contenuti con la crittografia envelope, richiedere un URL di acquisizione chiave specificando 2 per keyDeliveryType: {"keyDeliveryType":2}.</span><span class="sxs-lookup"><span data-stu-id="9c311-164">If you are protecting your content with the envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="9c311-165">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="9c311-165">Request:</span></span>

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

<span data-ttu-id="9c311-166">Risposta:</span><span class="sxs-lookup"><span data-stu-id="9c311-166">Response:</span></span>

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


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="9c311-167">Creare criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="9c311-167">Create asset delivery policy</span></span>
<span data-ttu-id="9c311-168">La seguente richiesta HTTP crea l'oggetto **AssetDeliveryPolicy** configurato in modo da applicare la crittografia envelope dinamica (**DynamicEnvelopeEncryption**) al protocollo **HLS** (in questo esempio, gli altri protocolli vengono esclusi dallo streaming).</span><span class="sxs-lookup"><span data-stu-id="9c311-168">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to the **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="9c311-169">Per informazioni sui valori che è possibile specificare quando si crea un oggetto AssetDeliveryPolicy, vedere la sezione [Tipi usati durante la definizione di AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="9c311-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="9c311-170">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="9c311-170">Request:</span></span>

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


<span data-ttu-id="9c311-171">Risposta:</span><span class="sxs-lookup"><span data-stu-id="9c311-171">Response:</span></span>

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


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="9c311-172">Collegare un asset ai criteri di distribuzione</span><span class="sxs-lookup"><span data-stu-id="9c311-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="9c311-173">Vedere [Collegare un asset ai criteri di distribuzione](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="9c311-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="9c311-174">Criteri di distribuzione degli asset DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="9c311-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-commonencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="9c311-175">Creare una chiave simmetrica di tipo CommonEncryption e collegarla all'asset</span><span class="sxs-lookup"><span data-stu-id="9c311-175">Create content key of the CommonEncryption type and link it to the asset</span></span>
<span data-ttu-id="9c311-176">Quando si specificano criteri di distribuzione DynamicEnvelopeEncryption, è necessario assicurarsi di collegare l'asset a una chiave simmetrica di tipo CommonEncryption.</span><span class="sxs-lookup"><span data-stu-id="9c311-176">When specifying DynamicCommonEncryption delivery policy, you need to make sure to link your asset to a content key of the CommonEncryption type.</span></span> <span data-ttu-id="9c311-177">Per altre informazioni, vedere [Creazione di una chiave simmetrica](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="9c311-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="9c311-178">Ottenere l'URL di distribuzione</span><span class="sxs-lookup"><span data-stu-id="9c311-178">Get Delivery URL</span></span>
<span data-ttu-id="9c311-179">Ottenere l'URL relativo al metodo di distribuzione PlayReady per la chiave simmetrica creata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="9c311-179">Get the delivery URL for the PlayReady delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="9c311-180">Un client usa l'URL restituito per richiedere una licenza PlayReady allo scopo di riprodurre contenuto protetto.</span><span class="sxs-lookup"><span data-stu-id="9c311-180">A client uses the returned URL to request a PlayReady license in order to playback the protected content.</span></span> <span data-ttu-id="9c311-181">Per altre informazioni, vedere [Ottenere l'URL di distribuzione](#get_delivery_url).</span><span class="sxs-lookup"><span data-stu-id="9c311-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="9c311-182">Creare criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="9c311-182">Create asset delivery policy</span></span>
<span data-ttu-id="9c311-183">La seguente richiesta HTTP crea l'oggetto **AssetDeliveryPolicy** configurato in modo da applicare la crittografia common dinamica (**DynamicCommonEncryption**) al protocollo **Smooth Streaming** (in questo esempio, gli altri protocolli vengono esclusi dallo streaming).</span><span class="sxs-lookup"><span data-stu-id="9c311-183">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to the **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="9c311-184">Per informazioni sui valori che è possibile specificare quando si crea un oggetto AssetDeliveryPolicy, vedere la sezione [Tipi usati durante la definizione di AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="9c311-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="9c311-185">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="9c311-185">Request:</span></span>

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


<span data-ttu-id="9c311-186">Se si desidera proteggere il contenuto utilizzando DRM Widevine, aggiornare i valori AssetDeliveryConfiguration per utilizzare WidevineLicenseAcquisitionUrl (che ha il valore 7) e specificare l'URL di un servizio di recapito di licenza.</span><span class="sxs-lookup"><span data-stu-id="9c311-186">If you want to protect your content using Widevine DRM, update the AssetDeliveryConfiguration values to use WidevineLicenseAcquisitionUrl (which has the value of 7) and specify the URL of a license delivery service.</span></span> <span data-ttu-id="9c311-187">Per distribuire le licenze Widevine, è possibile ricorrere ai seguenti partner AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="9c311-187">You can use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="9c311-188">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9c311-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="9c311-189">Durante la crittografia con Widevine, si sarebbe in grado di recapitare utilizzando DASH.</span><span class="sxs-lookup"><span data-stu-id="9c311-189">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="9c311-190">Assicurarsi di specificare il protocollo di recapito asset DASH (2).</span><span class="sxs-lookup"><span data-stu-id="9c311-190">Make sure to specify DASH (2) in the asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="9c311-191">Collegare un asset ai criteri di distribuzione</span><span class="sxs-lookup"><span data-stu-id="9c311-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="9c311-192">Vedere [Collegare un asset ai criteri di distribuzione](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="9c311-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="9c311-193"><a id="types"></a></span><span class="sxs-lookup"><span data-stu-id="9c311-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="9c311-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="9c311-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="9c311-195">L'enumerazione seguente descrive i valori che è possibile impostare per il protocollo di recapito di risorse.</span><span class="sxs-lookup"><span data-stu-id="9c311-195">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="9c311-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="9c311-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="9c311-197">L'enumerazione seguente descrive i valori che è possibile impostare per il tipo di criterio di recapito.</span><span class="sxs-lookup"><span data-stu-id="9c311-197">The following enum describes values you can set for the asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

### <a name="contentkeydeliverytype"></a><span data-ttu-id="9c311-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="9c311-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="9c311-199">L'enumerazione seguente descrive i valori che è possibile usare per configurare il metodo di recapito della chiave simmetrica al client.</span><span class="sxs-lookup"><span data-stu-id="9c311-199">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="9c311-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="9c311-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="9c311-201">L'enumerazione seguente descrive i valori che è possibile impostare per configurare le chiavi usate per ottenere una configurazione specifica per un criterio di recapito di risorse.</span><span class="sxs-lookup"><span data-stu-id="9c311-201">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="9c311-202">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="9c311-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9c311-203">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="9c311-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

