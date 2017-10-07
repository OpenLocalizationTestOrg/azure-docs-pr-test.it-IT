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
# <a name="configuring-asset-delivery-policies"></a>Configurazione dei criteri di distribuzione degli asset
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

Se si prevede di asset toodeliver crittografati in modo dinamico, uno di hello passaggi hello contenuto di flusso di lavoro di recapito consiste nella configurazione di criteri di distribuzione per gli asset di servizi multimediali. criteri di distribuzione di asset Hello indicano a servizi multimediali la modalità desiderata per l'asset toobe recapitati: in quale protocollo di streaming deve l'asset essere dinamicamente incluso nel pacchetto (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), se si desidera toodynamically o meno crittografare l'asset e come (busta o la crittografia comune).

In questo argomento viene descritto come e perché toocreate e configurare i criteri di recapito di asset.

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 
>
>Inoltre, toobe toouse in grado di creazione dinamica dei pacchetti e la crittografia dinamica dell'asset deve contenere un set di velocità in bit adattiva MP4s o file Smooth Streaming a velocità in bit adattiva.

È possibile applicare criteri diversi toohello stesso asset. Ad esempio, è possibile applicare PlayReady crittografia tooSmooth Streaming ed Envelope AES crittografia tooMPEG DASH e HLS. Tutti i protocolli che non sono definiti in un criterio di recapito (ad esempio, aggiungere un singolo criterio che specifica solo HLS come protocollo di hello) verrà impedito lo streaming. toothis eccezione Hello è se non sono presenti criteri di recapito di asset definito in alcun modo. Quindi, saranno possibile tutti i protocolli in crittografato hello.

Se si desidera toodeliver asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset hello. Prima dell'asset può essere trasmesso, hello streaming flussi e crittografia di archiviazione hello viene rimosso il server dei contenuti usando hello specificati criteri di distribuzione. Ad esempio, toodeliver l'asset crittografato con una chiave di crittografia envelope Advanced Encryption Standard (AES), impostare il tipo di criteri di hello troppo**DynamicEnvelopeEncryption**. crittografia di archiviazione tooremove e le risorse hello flusso hello chiara, impostare il tipo di criteri di hello troppo**NoDynamicEncryption**. Esempi che illustrano come tooconfigure questi tipi di criteri seguono.

A seconda della configurazione di criteri di distribuzione di hello asset si sarebbe toodynamically in grado di pacchetto, in modo dinamico crittografare ed eseguire il flusso hello seguenti protocolli di streaming: Smooth Streaming, HLS, flussi MPEG DASH.

Dopo l'elenco Mostra hello Hello formatta utilizzare toostream Smooth, HLS, DASH.

Smooth Streaming:

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest

HLS:

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{nome endpoint di streaming-nome account servizi multimediali}.streaming.mediaservices.windows.net/{ID localizzatore}/{nome file}.ism/Manifest(format=mpd-time-csf)


Per istruzioni su come toopublish un asset e compilare un URL di streaming, vedere [compilare un URL di streaming](media-services-deliver-streaming-content.md).

## <a name="considerations"></a>Considerazioni
* Non è possbile eliminare un AssetDeliveryPolicy con un asset se esiste un localizzatore OnDemand (streaming) per quell’asset. criteri di hello tooremove da asset hello Hello consiglia prima di eliminare i criteri di hello.
* Non è possibile creare un localizzatore di streaming in un asset crittografato per l’archiviazione se non è impostato alcun criterio di distribuzione degli asset.  Se non è hello Asset crittografato di archiviazione, sistema hello consentirà di creare un asset di hello localizzatore e il flusso in hello deselezionare senza un criterio di recapito di asset.
* È possibile avere più criteri di recapito di asset associati a un singolo asset, ma è possibile specificare solo un modo toohandle AssetDeliveryProtocol un determinato.  Vale a dire se si tenta di toolink due criteri di recapito che specificare hello AssetDeliveryProtocol.SmoothStreaming protocollo che verrà generato un errore perché il sistema di hello non sapere quale si desidera che tooapply quando un client effettua una richiesta di Smooth Streaming.
* Se si dispone di un asset con un localizzatore di streaming esistente, non è possibile collegare un nuovo asset toohello criteri, scollegare un criterio esistente da asset hello o aggiornare i criteri di recapito associato hello asset.  Prima hanno localizzatore di streaming hello tooremove, modificare criteri hello e quindi ricreare hello localizzatore di streaming.  È possibile utilizzare hello locatorId stesso quando si ricrea hello streaming localizzatore, ma è necessario assicurarsi che non causino problemi per i client poiché il contenuto può essere memorizzato nella cache dall'origine hello o una rete CDN a valle.

>[!NOTE]

>Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP. Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Connessione dei servizi tooMedia

Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali. È necessario effettuare le chiamate successive toohello nuovo URI.

## <a name="clear-asset-delivery-policy"></a>Criteri di distribuzione degli asset Clear
### <a id="create_asset_delivery_policy"></a>Creare criteri di distribuzione degli asset
richiesta HTTP seguente Hello crea un criterio di recapito di asset che specifica toonot applicare la crittografia dinamica e protocolli di flusso hello toodeliver in uno dei seguenti hello: protocolli MPEG DASH, HLS e Smooth Streaming. 

Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.   

Richiesta:

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

Risposta:

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

### <a id="link_asset_with_asset_delivery_policy"></a>Collegare un asset ai criteri di distribuzione
Hello hello collegamenti di richiesta HTTP seguente specifica criteri di distribuzione di asset toohello asset per.

Richiesta:

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

Risposta:

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Criteri di distribuzione degli asset DynamicEnvelopeEncryption
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>Creare la chiave simmetrica di tipo EnvelopeEncryption hello e collegarlo toohello asset
Quando si specificano i criteri di distribuzione DynamicEnvelopeEncryption, è necessario toolink che toomake la chiave simmetrica tooa di asset di hello EnvelopeEncryption tipo. Per altre informazioni, vedere [Creazione di una chiave simmetrica](media-services-rest-create-contentkey.md)).

### <a id="get_delivery_url"></a>Ottenere l'URL di distribuzione
Metodo di distribuzione della chiave simmetrica di hello creato nel passaggio precedente hello specificare l'URL di recapito di hello get per hello. Un client utilizza hello restituito toorequest URL contenuto protetto da una chiave AES o una licenza PlayReady in hello tooplayback ordine.

Specificare il tipo di hello di hello URL tooget nel corpo di hello della richiesta HTTP hello. Se si desidera proteggere i contenuti con PlayReady, richiedere un URL di acquisizione di licenze PlayReady di servizi multimediali, con 1 per keyDeliveryType hello: {"keyDeliveryType": 1}. Se si desidera proteggere i contenuti con crittografia envelope hello, richiedere un URL di acquisizione chiave specificando 2 per keyDeliveryType: {"keyDeliveryType": 2}.

Richiesta:

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

Risposta:

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


### <a name="create-asset-delivery-policy"></a>Creare criteri di distribuzione degli asset
richiesta HTTP seguente Hello crea hello **AssetDeliveryPolicy** ovvero crittografia envelope dinamici di tooapply configurato (**DynamicEnvelopeEncryption**) toohello **HLS**protocollo (in questo esempio, gli altri protocolli verranno impediti lo streaming). 

Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.   

Richiesta:

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


Risposta:

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


### <a name="link-asset-with-asset-delivery-policy"></a>Collegare un asset ai criteri di distribuzione
Vedere [Collegare un asset ai criteri di distribuzione](#link_asset_with_asset_delivery_policy)

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Criteri di distribuzione degli asset DynamicCommonEncryption
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>Creare la chiave simmetrica di tipo CommonEncryption hello e collegarlo toohello asset
Quando si specificano i criteri di distribuzione DynamicCommonEncryption, è necessario toolink che toomake la chiave simmetrica tooa di asset di hello CommonEncryption tipo. Per altre informazioni, vedere [Creazione di una chiave simmetrica](media-services-rest-create-contentkey.md)).

### <a name="get-delivery-url"></a>Ottenere l'URL di distribuzione
Ottenere un URL di recapito hello hello PlayReady del metodo di consegna della chiave di hello contenuto creato nel passaggio precedente hello. Un client utilizza hello restituito toorequest URL protetto da una licenza PlayReady in hello tooplayback order content. Per altre informazioni, vedere [Ottenere l'URL di distribuzione](#get_delivery_url).

### <a name="create-asset-delivery-policy"></a>Creare criteri di distribuzione degli asset
richiesta HTTP seguente Hello crea hello **AssetDeliveryPolicy** ovvero tooapply configurato comuni crittografia dinamica (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocollo (in questo esempio, gli altri protocolli verranno impediti lo streaming). 

Per informazioni sui valori è possono specificare durante la creazione di un AssetDeliveryPolicy, vedere hello [tipi utilizzati durante la definizione di AssetDeliveryPolicy](#types) sezione.   

Richiesta:

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


Se si desidera tooprotect il contenuto con DRM Widevine, aggiornare hello AssetDeliveryConfiguration valori toouse WidevineLicenseAcquisitionUrl (che presenta il valore di hello pari a 7) e specificare hello URL di un servizio di recapito di licenza. È possibile utilizzare hello seguente toohelp partner AMS di consegnare licenze Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

ad esempio: 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> Durante la crittografia con Widevine, sarà solo in grado di toodeliver utilizzando trattino. Verificare che toospecify DASH (2) hello in asset il protocollo di recapito.
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>Collegare un asset ai criteri di distribuzione
Vedere [Collegare un asset ai criteri di distribuzione](#link_asset_with_asset_delivery_policy)

## <a id="types"></a>

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

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

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

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

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

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


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

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

