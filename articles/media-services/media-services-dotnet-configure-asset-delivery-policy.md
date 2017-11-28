---
title: Configurare i criteri di distribuzione degli asset con .NET SDK | Microsoft Docs
description: Questo argomento illustra come configurare criteri di distribuzione degli asset differenti con Servizi multimediali di Azure .NET SDK.
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: 282fd9e24dc147e31613469926128894d48366f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="621c2-103">Configurare i criteri di distribuzione degli asset con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="621c2-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="621c2-104">Overview</span><span class="sxs-lookup"><span data-stu-id="621c2-104">Overview</span></span>
<span data-ttu-id="621c2-105">Se si prevede di distribuire dinamicamente asset crittografati in modo dinamico, uno dei passaggi del flusso di lavoro di distribuzione dei contenuti in Servizi multimediali consiste nella configurazione dei criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="621c2-105">If you plan to delivery encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="621c2-106">Questi criteri indicano a Servizi multimediali la modalità di distribuzione di un asset, ovvero il protocollo di streaming da usare per la creazione dinamica dei pacchetti (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), se l'asset deve essere crittografato dinamicamente e l'eventuale modalità di crittografia (envelope o common).</span><span class="sxs-lookup"><span data-stu-id="621c2-106">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="621c2-107">Questo argomento illustra perché e come creare i criteri di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="621c2-107">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="621c2-108">Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="621c2-108">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="621c2-109">Per avviare lo streaming del contenuto e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming da cui si vuole trasmettere il contenuto deve essere nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="621c2-109">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="621c2-110">Per usare la creazione dinamica dei pacchetti e la crittografia dinamica, l'asset deve contenere un set di file MP4 o Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="621c2-110">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="621c2-111">È possibile applicare criteri differenti allo stesso asset.</span><span class="sxs-lookup"><span data-stu-id="621c2-111">You could apply different policies to the same asset.</span></span> <span data-ttu-id="621c2-112">È ad esempio possibile applicare la crittografia PlayReady a Smooth Streaming e la crittografia envelope AES (Advanced Encryption Standard) a MPEG DASH e HLS.</span><span class="sxs-lookup"><span data-stu-id="621c2-112">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="621c2-113">Gli eventuali protocolli non definiti nei criteri di distribuzione (ad esempio quando si aggiunge un singolo criterio che specifica soltanto HLS come protocollo) verranno esclusi dallo streaming.</span><span class="sxs-lookup"><span data-stu-id="621c2-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="621c2-114">Questo comportamento non si verifica quando non è presente alcun criterio di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="621c2-114">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="621c2-115">In tal caso, sono consentiti tutti i protocolli in chiaro.</span><span class="sxs-lookup"><span data-stu-id="621c2-115">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="621c2-116">Se si desidera distribuire un asset con memoria crittografata, è necessario configurare i criteri di distribuzione appropriati.</span><span class="sxs-lookup"><span data-stu-id="621c2-116">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="621c2-117">Prima di trasmettere in streaming l'asset in base ai criteri specificati, il server rimuove la crittografia di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="621c2-117">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="621c2-118">Ad esempio, per distribuire l'asset crittografato con una chiave di crittografia envelope AES (Advanced Encryption Standard), impostare il tipo di criteri su **DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="621c2-118">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="621c2-119">Per rimuovere la crittografia di archiviazione e trasmettere l'asset in chiaro, impostare il tipo di criteri su **NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="621c2-119">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="621c2-120">I seguenti esempi mostrano come configurare questi tipi di criteri.</span><span class="sxs-lookup"><span data-stu-id="621c2-120">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="621c2-121">A seconda della modalità di configurazione dei criteri di distribuzione degli asset, sarà possibile creare dinamicamente i pacchetti, applicare la crittografia dinamica e trasmettere i protocolli di streaming seguenti: Smooth Streaming, HLS e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="621c2-121">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="621c2-122">L'elenco seguente mostra i formati usati per i flussi Smooth, HLS e DASH.</span><span class="sxs-lookup"><span data-stu-id="621c2-122">The following list shows the formats that you use to stream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="621c2-123">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="621c2-123">Smooth Streaming:</span></span>

<span data-ttu-id="621c2-124">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="621c2-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="621c2-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="621c2-125">HLS:</span></span>

<span data-ttu-id="621c2-126">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="621c2-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="621c2-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="621c2-127">MPEG DASH</span></span>

<span data-ttu-id="621c2-128">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="621c2-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="621c2-129">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="621c2-129">Considerations</span></span>
* <span data-ttu-id="621c2-130">Non è possbile eliminare un AssetDeliveryPolicy con un asset se esiste un localizzatore OnDemand (streaming) per quell’asset.</span><span class="sxs-lookup"><span data-stu-id="621c2-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="621c2-131">Si suggerisce di rimuovere il criterio dall'asset prima di eliminare il criterio.</span><span class="sxs-lookup"><span data-stu-id="621c2-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="621c2-132">Non è possibile creare un localizzatore di streaming in un asset crittografato per l’archiviazione se non è impostato alcun criterio di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="621c2-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="621c2-133">Se l'asset non è crittografato per l'archiviazione, il sistema consentirà di creare un localizzatore ed eseguire in streaming l'asset in chiaro senza un criterio di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="621c2-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="621c2-134">È possibile avere più criteri di distribuzione degli asset associati a un singolo asset, ma è possibile specificare solo un modo per gestire un determinato AssetDeliveryProtocol.</span><span class="sxs-lookup"><span data-stu-id="621c2-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="621c2-135">Ciò significa che se si tenta di collegare due criteri di distribuzione che specificano il protocollo AssetDeliveryProtocol.SmoothStreaming, verrà generato un errore perché il sistema non sa quale applicare quando un client effettua una richiesta di Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="621c2-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="621c2-136">Se si dispone di un asset con un localizzatore di streaming esistente, non è possibile collegare un nuovo criterio all'asset (è possibile scollegare un criterio esistente dall'asset, o aggiornare un criterio di distribuzione associato all'asset).</span><span class="sxs-lookup"><span data-stu-id="621c2-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset (you can either unlink an existing policy from the asset, or update a delivery policy associated with the asset).</span></span>  <span data-ttu-id="621c2-137">È innanzitutto necessario rimuovere il localizzatore di streaming, modificare i criteri e quindi creare nuovamente il localizzatore di streaming.</span><span class="sxs-lookup"><span data-stu-id="621c2-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="621c2-138">È possibile utilizzare lo stesso ID quando si ricrea il localizzatore di streaming, ma è necessario assicurarsi che questo non causi problemi per i client poiché il contenuto può essere memorizzato nella cache per l'origine o una rete CDN a valle.</span><span class="sxs-lookup"><span data-stu-id="621c2-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="621c2-139">Criteri di distribuzione degli asset Clear</span><span class="sxs-lookup"><span data-stu-id="621c2-139">Clear asset delivery policy</span></span>

<span data-ttu-id="621c2-140">Il metodo **ConfigureClearAssetDeliveryPolicy** seguente specifica di non applicare la crittografia dinamica e di distribuire il flusso con uno dei protocolli seguenti: MPEG DASH, HLS e Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="621c2-140">The following **ConfigureClearAssetDeliveryPolicy** method specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="621c2-141">È possibile applicare questo criterio alle risorse crittografate di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="621c2-141">You might want to apply this policy to your storage encrypted assets.</span></span>

<span data-ttu-id="621c2-142">Per informazioni sui valori che è possibile specificare quando si crea un oggetto AssetDeliveryPolicy, vedere la sezione [Tipi usati durante la definizione di AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="621c2-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="621c2-143">Criteri di distribuzione degli asset DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="621c2-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="621c2-144">Il metodo **CreateAssetDeliveryPolicy** seguente crea l'oggetto **AssetDeliveryPolicy** configurato in modo da applicare la crittografia dinamica di tipo common (**DynamicCommonEncryption**) a un protocollo Smooth Streaming (gli altri protocolli vengono esclusi dallo streaming).</span><span class="sxs-lookup"><span data-stu-id="621c2-144">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to a smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="621c2-145">Il metodo accetta due parametri: **Asset**, cioè l'asset a cui applicare i criteri di distribuzione, e **IContentKey**, cioè la chiave simmetrica del tipo **CommonEncryption**. Per altre informazioni, vedere l'articolo relativo alla [creazione di una chiave simmetrica](media-services-dotnet-create-contentkey.md#common_contentkey).</span><span class="sxs-lookup"><span data-stu-id="621c2-145">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="621c2-146">Per informazioni sui valori che è possibile specificare quando si crea un oggetto AssetDeliveryPolicy, vedere la sezione [Tipi usati durante la definizione di AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="621c2-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="621c2-147">Servizi multimediali di Azure consente inoltre di aggiungere la crittografia Widevine.</span><span class="sxs-lookup"><span data-stu-id="621c2-147">Azure Media Services also enables you to add Widevine encryption.</span></span> <span data-ttu-id="621c2-148">Nell'esempio seguente viene illustrato sia PlayReady che Widevine da aggiungere al criterio di recapito di asset.</span><span class="sxs-lookup"><span data-stu-id="621c2-148">The following example demonstrates both PlayReady and Widevine being added to the asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get the PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // to append /? KID =< keyId > to the end of the url when creating the manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="621c2-149">Durante la crittografia con Widevine, si sarebbe in grado di recapitare utilizzando DASH.</span><span class="sxs-lookup"><span data-stu-id="621c2-149">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="621c2-150">Assicurarsi di specificare il protocollo di recapito asset DASH.</span><span class="sxs-lookup"><span data-stu-id="621c2-150">Make sure to specify DASH in the asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="621c2-151">Criteri di distribuzione degli asset DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="621c2-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="621c2-152">Il metodo **CreateAssetDeliveryPolicy** seguente crea l'oggetto **AssetDeliveryPolicy** configurato in modo da applicare la crittografia envelope dinamica (**DynamicEnvelopeEncryption**) ai protocolli Smooth Streaming, HLS e DASH (se si decide di non specificare alcuni protocolli, questi saranno esclusi dallo streaming).</span><span class="sxs-lookup"><span data-stu-id="621c2-152">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to Smooth Streaming, HLS, and DASH protocols (if you decide to not specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="621c2-153">Il metodo accetta due parametri: **Asset**, cioè l'asset a cui applicare i criteri di distribuzione, e **IContentKey**, cioè la chiave simmetrica del tipo **EnvelopeEncryption**. Per altre informazioni, vedere l'articolo relativo alla [creazione di una chiave simmetrica](media-services-dotnet-create-contentkey.md#envelope_contentkey).</span><span class="sxs-lookup"><span data-stu-id="621c2-153">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="621c2-154">Per informazioni sui valori che è possibile specificare quando si crea un oggetto AssetDeliveryPolicy, vedere la sezione [Tipi usati durante la definizione di AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="621c2-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get the Key Delivery Base Url by removing the Query parameter.  The Dynamic Encryption service will
        //  automatically add the correct key identifier to the url when it generates the Envelope encrypted content
        //  manifest.  Omitting the IV will also cause the Dynamice Encryption service to generate a deterministic
        //  IV for the content automatically.  By using the EnvelopeBaseKeyAcquisitionUrl and omitting the IV, this
        //  allows the AssetDelivery policy to be reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // The following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended to the envelope and
        //   the Initialization Vector (IV) to use for the envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="621c2-155"><a id="types"></a></span><span class="sxs-lookup"><span data-stu-id="621c2-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="621c2-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="621c2-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="621c2-157">L'enumerazione seguente descrive i valori che è possibile impostare per il protocollo di recapito di risorse.</span><span class="sxs-lookup"><span data-stu-id="621c2-157">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <span data-ttu-id="621c2-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="621c2-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="621c2-159">L'enumerazione seguente descrive i valori che è possibile impostare per il tipo di criterio di recapito.</span><span class="sxs-lookup"><span data-stu-id="621c2-159">The following enum describes values you can set for the asset delivery policy type.</span></span>  

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

### <span data-ttu-id="621c2-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="621c2-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="621c2-161">L'enumerazione seguente descrive i valori che è possibile usare per configurare il metodo di recapito della chiave simmetrica al client.</span><span class="sxs-lookup"><span data-stu-id="621c2-161">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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

### <span data-ttu-id="621c2-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="621c2-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="621c2-163">L'enumerazione seguente descrive i valori che è possibile impostare per configurare le chiavi usate per ottenere una configurazione specifica per un criterio di recapito di risorse.</span><span class="sxs-lookup"><span data-stu-id="621c2-163">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="621c2-164">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="621c2-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="621c2-165">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="621c2-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

