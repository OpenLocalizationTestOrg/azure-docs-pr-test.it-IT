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
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>Configurare i criteri di distribuzione degli asset con .NET SDK
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>Panoramica
Se si prevede di asset toodelivery crittografati, uno di hello passaggi hello contenuto di flusso di lavoro di recapito consiste nella configurazione di criteri di distribuzione per gli asset di servizi multimediali. criteri di distribuzione di asset Hello indicano a servizi multimediali la modalità desiderata per l'asset toobe recapitati: in quale protocollo di streaming deve l'asset essere dinamicamente incluso nel pacchetto (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), se si desidera toodynamically o meno crittografare l'asset e come (busta o la crittografia comune).

In questo argomento viene descritto come e perché toocreate e configurare i criteri di recapito di asset.

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 
>
>Inoltre, toobe toouse in grado di creazione dinamica dei pacchetti e la crittografia dinamica dell'asset deve contenere un set di velocità in bit adattiva MP4s o file Smooth Streaming a velocità in bit adattiva.


È possibile applicare criteri diversi toohello stesso asset. Ad esempio, è possibile applicare PlayReady crittografia tooSmooth Streaming ed Envelope AES crittografia tooMPEG DASH e HLS. Tutti i protocolli che non sono definiti in un criterio di recapito (ad esempio, aggiungere un singolo criterio che specifica solo HLS come protocollo di hello) verrà impedito lo streaming. toothis eccezione Hello è se non sono presenti criteri di recapito di asset definito in alcun modo. Quindi, saranno possibile tutti i protocolli in crittografato hello.

Se si desidera toodeliver asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset hello. Prima dell'asset può essere trasmesso, hello streaming flussi e crittografia di archiviazione hello viene rimosso il server dei contenuti usando hello specificati criteri di distribuzione. Ad esempio, toodeliver l'asset crittografato con una chiave di crittografia envelope Advanced Encryption Standard (AES), impostare il tipo di criteri di hello troppo**DynamicEnvelopeEncryption**. crittografia di archiviazione tooremove e le risorse hello flusso hello chiara, impostare il tipo di criteri di hello troppo**NoDynamicEncryption**. Esempi che illustrano come tooconfigure questi tipi di criteri seguono.

A seconda della configurazione di criteri di distribuzione di hello asset si sarebbe toodynamically in grado di pacchetto, in modo dinamico crittografare ed eseguire il flusso hello seguenti protocolli di streaming: flussi MPEG DASH, HLS e Smooth Streaming.

Hello seguito sono elencati i formati di hello utilizzare toostream Smooth, HLS e DASH.

Smooth Streaming:

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest

HLS:

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=mpd-time-csf)


## <a name="considerations"></a>Considerazioni
* Non è possbile eliminare un AssetDeliveryPolicy con un asset se esiste un localizzatore OnDemand (streaming) per quell’asset. criteri di hello tooremove da asset hello Hello consiglia prima di eliminare i criteri di hello.
* Non è possibile creare un localizzatore di streaming in un asset crittografato per l’archiviazione se non è impostato alcun criterio di distribuzione degli asset.  Se non è hello Asset crittografato di archiviazione, sistema hello consentirà di creare un asset di hello localizzatore e il flusso in hello deselezionare senza un criterio di recapito di asset.
* È possibile avere più criteri di recapito di asset associati a un singolo asset, ma è possibile specificare solo un modo toohandle AssetDeliveryProtocol un determinato.  Vale a dire se si tenta di toolink due criteri di recapito che specificare hello AssetDeliveryProtocol.SmoothStreaming protocollo che verrà generato un errore perché il sistema di hello non sapere quale si desidera che tooapply quando un client effettua una richiesta di Smooth Streaming.
* Se si dispone di un asset con un localizzatore di streaming esistente, non è possibile collegare un nuovo asset toohello criteri (è possibile scollegare un criterio esistente da asset hello, o aggiornare i criteri di recapito associato hello asset).  Prima hanno localizzatore di streaming hello tooremove, modificare criteri hello e quindi ricreare hello localizzatore di streaming.  È possibile utilizzare hello locatorId stesso quando si ricrea hello streaming localizzatore, ma è necessario assicurarsi che non causino problemi per i client poiché il contenuto può essere memorizzato nella cache dall'origine hello o una rete CDN a valle.

## <a name="clear-asset-delivery-policy"></a>Criteri di distribuzione degli asset Clear

esempio Hello **ConfigureClearAssetDeliveryPolicy** metodo specifica toonot applicare la crittografia dinamica e protocolli di flusso hello toodeliver in uno dei seguenti hello: protocolli MPEG DASH, HLS e Smooth Streaming. È possibile tooapply questo asset crittografato di archiviazione tooyour di criteri.

Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Criteri di distribuzione degli asset DynamicCommonEncryption

esempio Hello **CreateAssetDeliveryPolicy** metodo crea hello **AssetDeliveryPolicy** ovvero tooapply configurato comuni crittografia dinamica (**DynamicCommonEncryption**) tooa smooth streaming protocollo (altri protocolli verranno impediti lo streaming). metodo Hello accetta due parametri: **Asset** (hello toowhich asset si vuole tooapply hello recapito criterio) e **IContentKey** (chiave simmetrica di hello di hello **CommonEncryption**dei tipi, per ulteriori informazioni, vedere: [la creazione di una chiave simmetrica](media-services-dotnet-create-contentkey.md#common_contentkey)).

Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.

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

Servizi multimediali di Azure consente inoltre tooadd Widevine crittografia. Hello seguente viene illustrato sia PlayReady e l'aggiunta di criteri di distribuzione di asset toohello Widevine.

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
> Durante la crittografia con Widevine, sarà solo in grado di toodeliver utilizzando trattino. Verificare che toospecify trattino nel protocollo di recapito di asset hello.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Criteri di distribuzione degli asset DynamicEnvelopeEncryption
esempio Hello **CreateAssetDeliveryPolicy** metodo crea hello **AssetDeliveryPolicy** ovvero crittografia envelope dinamici di tooapply configurato (**DynamicEnvelopeEncryption** ) tooSmooth i protocolli di Streaming, HLS e DASH (se si decide toonot specificare alcuni protocolli, verranno bloccati dal flusso). metodo Hello accetta due parametri: **Asset** (hello toowhich asset si vuole tooapply hello recapito criterio) e **IContentKey** (chiave simmetrica di hello di hello **EnvelopeEncryption**dei tipi, per ulteriori informazioni, vedere: [la creazione di una chiave simmetrica](media-services-dotnet-create-contentkey.md#envelope_contentkey)).

Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.   

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


## <a id="types"></a>

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

Hello enum seguente descrive i possibili valori per il protocollo di recapito hello asset.

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

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

Hello enum seguente vengono descritti i possibili valori per tipo di criterio di recapito asset hello.  

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

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

Hello enum seguente descrive i valori è possibile utilizzare metodo di recapito tooconfigure hello del client toohello chiave contenuto hello.
    
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

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

Hello enum seguente descrive i possibili valori tooconfigure le chiavi usate tooget configurazione specifica per un criterio di recapito di asset.

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

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

