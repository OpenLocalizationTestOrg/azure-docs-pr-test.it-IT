---
title: criteri di recapito di asset aaaConfigure con .NET SDK | Documenti Microsoft
description: Questo argomento viene illustrato come i criteri di distribuzione diversi asset tooconfigure con Azure Media Services .NET SDK.
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
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="c2432-103">Configurare i criteri di distribuzione degli asset con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c2432-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="c2432-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c2432-104">Overview</span></span>
<span data-ttu-id="c2432-105">Se si prevede di asset toodelivery crittografati, uno di hello passaggi hello contenuto di flusso di lavoro di recapito consiste nella configurazione di criteri di distribuzione per gli asset di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="c2432-105">If you plan toodelivery encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="c2432-106">criteri di distribuzione di asset Hello indicano a servizi multimediali la modalità desiderata per l'asset toobe recapitati: in quale protocollo di streaming deve l'asset essere dinamicamente incluso nel pacchetto (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), se si desidera toodynamically o meno crittografare l'asset e come (busta o la crittografia comune).</span><span class="sxs-lookup"><span data-stu-id="c2432-106">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="c2432-107">In questo argomento viene descritto come e perché toocreate e configurare i criteri di recapito di asset.</span><span class="sxs-lookup"><span data-stu-id="c2432-107">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="c2432-108">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="c2432-108">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="c2432-109">lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="c2432-109">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="c2432-110">Inoltre, toobe toouse in grado di creazione dinamica dei pacchetti e la crittografia dinamica dell'asset deve contenere un set di velocità in bit adattiva MP4s o file Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="c2432-110">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="c2432-111">È possibile applicare criteri diversi toohello stesso asset.</span><span class="sxs-lookup"><span data-stu-id="c2432-111">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="c2432-112">Ad esempio, è possibile applicare PlayReady crittografia tooSmooth Streaming ed Envelope AES crittografia tooMPEG DASH e HLS.</span><span class="sxs-lookup"><span data-stu-id="c2432-112">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="c2432-113">Tutti i protocolli che non sono definiti in un criterio di recapito (ad esempio, aggiungere un singolo criterio che specifica solo HLS come protocollo di hello) verrà impedito lo streaming.</span><span class="sxs-lookup"><span data-stu-id="c2432-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="c2432-114">toothis eccezione Hello è se non sono presenti criteri di recapito di asset definito in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="c2432-114">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="c2432-115">Quindi, saranno possibile tutti i protocolli in crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="c2432-115">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="c2432-116">Se si desidera toodeliver asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset hello.</span><span class="sxs-lookup"><span data-stu-id="c2432-116">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="c2432-117">Prima dell'asset può essere trasmesso, hello streaming flussi e crittografia di archiviazione hello viene rimosso il server dei contenuti usando hello specificati criteri di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c2432-117">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="c2432-118">Ad esempio, toodeliver l'asset crittografato con una chiave di crittografia envelope Advanced Encryption Standard (AES), impostare il tipo di criteri di hello troppo**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="c2432-118">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="c2432-119">crittografia di archiviazione tooremove e le risorse hello flusso hello chiara, impostare il tipo di criteri di hello troppo**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="c2432-119">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="c2432-120">Esempi che illustrano come tooconfigure questi tipi di criteri seguono.</span><span class="sxs-lookup"><span data-stu-id="c2432-120">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="c2432-121">A seconda della configurazione di criteri di distribuzione di hello asset si sarebbe toodynamically in grado di pacchetto, in modo dinamico crittografare ed eseguire il flusso hello seguenti protocolli di streaming: flussi MPEG DASH, HLS e Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="c2432-121">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="c2432-122">Hello seguito sono elencati i formati di hello utilizzare toostream Smooth, HLS e DASH.</span><span class="sxs-lookup"><span data-stu-id="c2432-122">hello following list shows hello formats that you use toostream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="c2432-123">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="c2432-123">Smooth Streaming:</span></span>

<span data-ttu-id="c2432-124">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="c2432-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="c2432-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="c2432-125">HLS:</span></span>

<span data-ttu-id="c2432-126">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="c2432-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="c2432-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="c2432-127">MPEG DASH</span></span>

<span data-ttu-id="c2432-128">{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="c2432-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="c2432-129">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="c2432-129">Considerations</span></span>
* <span data-ttu-id="c2432-130">Non è possbile eliminare un AssetDeliveryPolicy con un asset se esiste un localizzatore OnDemand (streaming) per quell’asset.</span><span class="sxs-lookup"><span data-stu-id="c2432-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="c2432-131">criteri di hello tooremove da asset hello Hello consiglia prima di eliminare i criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="c2432-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="c2432-132">Non è possibile creare un localizzatore di streaming in un asset crittografato per l’archiviazione se non è impostato alcun criterio di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="c2432-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="c2432-133">Se non è hello Asset crittografato di archiviazione, sistema hello consentirà di creare un asset di hello localizzatore e il flusso in hello deselezionare senza un criterio di recapito di asset.</span><span class="sxs-lookup"><span data-stu-id="c2432-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="c2432-134">È possibile avere più criteri di recapito di asset associati a un singolo asset, ma è possibile specificare solo un modo toohandle AssetDeliveryProtocol un determinato.</span><span class="sxs-lookup"><span data-stu-id="c2432-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="c2432-135">Vale a dire se si tenta di toolink due criteri di recapito che specificare hello AssetDeliveryProtocol.SmoothStreaming protocollo che verrà generato un errore perché il sistema di hello non sapere quale si desidera che tooapply quando un client effettua una richiesta di Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="c2432-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="c2432-136">Se si dispone di un asset con un localizzatore di streaming esistente, non è possibile collegare un nuovo asset toohello criteri (è possibile scollegare un criterio esistente da asset hello, o aggiornare i criteri di recapito associato hello asset).</span><span class="sxs-lookup"><span data-stu-id="c2432-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset (you can either unlink an existing policy from hello asset, or update a delivery policy associated with hello asset).</span></span>  <span data-ttu-id="c2432-137">Prima hanno localizzatore di streaming hello tooremove, modificare criteri hello e quindi ricreare hello localizzatore di streaming.</span><span class="sxs-lookup"><span data-stu-id="c2432-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="c2432-138">È possibile utilizzare hello locatorId stesso quando si ricrea hello streaming localizzatore, ma è necessario assicurarsi che non causino problemi per i client poiché il contenuto può essere memorizzato nella cache dall'origine hello o una rete CDN a valle.</span><span class="sxs-lookup"><span data-stu-id="c2432-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="c2432-139">Criteri di distribuzione degli asset Clear</span><span class="sxs-lookup"><span data-stu-id="c2432-139">Clear asset delivery policy</span></span>

<span data-ttu-id="c2432-140">esempio Hello **ConfigureClearAssetDeliveryPolicy** metodo specifica toonot applicare la crittografia dinamica e protocolli di flusso hello toodeliver in uno dei seguenti hello: protocolli MPEG DASH, HLS e Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="c2432-140">hello following **ConfigureClearAssetDeliveryPolicy** method specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="c2432-141">È possibile tooapply questo asset crittografato di archiviazione tooyour di criteri.</span><span class="sxs-lookup"><span data-stu-id="c2432-141">You might want tooapply this policy tooyour storage encrypted assets.</span></span>

<span data-ttu-id="c2432-142">Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.</span><span class="sxs-lookup"><span data-stu-id="c2432-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="c2432-143">Criteri di distribuzione degli asset DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="c2432-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="c2432-144">esempio Hello **CreateAssetDeliveryPolicy** metodo crea hello **AssetDeliveryPolicy** ovvero tooapply configurato comuni crittografia dinamica (**DynamicCommonEncryption**) tooa smooth streaming protocollo (altri protocolli verranno impediti lo streaming).</span><span class="sxs-lookup"><span data-stu-id="c2432-144">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="c2432-145">metodo Hello accetta due parametri: **Asset** (hello toowhich asset si vuole tooapply hello recapito criterio) e **IContentKey** (chiave simmetrica di hello di hello **CommonEncryption**dei tipi, per ulteriori informazioni, vedere: [la creazione di una chiave simmetrica](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="c2432-145">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="c2432-146">Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.</span><span class="sxs-lookup"><span data-stu-id="c2432-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

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
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="c2432-147">Servizi multimediali di Azure consente inoltre tooadd Widevine crittografia.</span><span class="sxs-lookup"><span data-stu-id="c2432-147">Azure Media Services also enables you tooadd Widevine encryption.</span></span> <span data-ttu-id="c2432-148">Hello seguente viene illustrato sia PlayReady e l'aggiunta di criteri di distribuzione di asset toohello Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2432-148">hello following example demonstrates both PlayReady and Widevine being added toohello asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

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


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="c2432-149">Durante la crittografia con Widevine, sarà solo in grado di toodeliver utilizzando trattino.</span><span class="sxs-lookup"><span data-stu-id="c2432-149">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="c2432-150">Verificare che toospecify trattino nel protocollo di recapito di asset hello.</span><span class="sxs-lookup"><span data-stu-id="c2432-150">Make sure toospecify DASH in hello asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="c2432-151">Criteri di distribuzione degli asset DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="c2432-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="c2432-152">esempio Hello **CreateAssetDeliveryPolicy** metodo crea hello **AssetDeliveryPolicy** ovvero crittografia envelope dinamici di tooapply configurato (**DynamicEnvelopeEncryption** ) tooSmooth i protocolli di Streaming, HLS e DASH (se si decide toonot specificare alcuni protocolli, verranno bloccati dal flusso).</span><span class="sxs-lookup"><span data-stu-id="c2432-152">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) tooSmooth Streaming, HLS, and DASH protocols (if you decide toonot specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="c2432-153">metodo Hello accetta due parametri: **Asset** (hello toowhich asset si vuole tooapply hello recapito criterio) e **IContentKey** (chiave simmetrica di hello di hello **EnvelopeEncryption**dei tipi, per ulteriori informazioni, vedere: [la creazione di una chiave simmetrica](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="c2432-153">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="c2432-154">Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.</span><span class="sxs-lookup"><span data-stu-id="c2432-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
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

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="c2432-155"><a id="types"></a></span><span class="sxs-lookup"><span data-stu-id="c2432-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="c2432-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="c2432-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="c2432-157">Hello enum seguente descrive i possibili valori per il protocollo di recapito hello asset.</span><span class="sxs-lookup"><span data-stu-id="c2432-157">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <span data-ttu-id="c2432-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="c2432-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="c2432-159">Hello enum seguente vengono descritti i possibili valori per tipo di criterio di recapito asset hello.</span><span class="sxs-lookup"><span data-stu-id="c2432-159">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <span data-ttu-id="c2432-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="c2432-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="c2432-161">Hello enum seguente descrive i valori è possibile utilizzare metodo di recapito tooconfigure hello del client toohello chiave contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="c2432-161">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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

### <span data-ttu-id="c2432-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="c2432-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="c2432-163">Hello enum seguente descrive i possibili valori tooconfigure le chiavi usate tooget configurazione specifica per un criterio di recapito di asset.</span><span class="sxs-lookup"><span data-stu-id="c2432-163">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="c2432-164">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="c2432-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c2432-165">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="c2432-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

