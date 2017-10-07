---
title: aaaConnecting tooMedia Account di servizi tramite l'API REST | Documenti Microsoft
description: In questo argomento viene illustrato come tooconnect tooMedia servizi abbonamento REST API.
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>Connessione tooMedia Account di servizi tramite l'API REST di servizi multimediali
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

In questo argomento viene descritto come tooobtain tooMicrosoft una connessione a livello di codice servizi multimediali di Azure quando si programma con hello API REST di servizi multimediali.

Quando si accede a servizi multimediali di Microsoft Azure, sono necessari due elementi: un token di accesso fornito da Azure Access Control Services (ACS) e hello URI di servizi multimediali di se stesso. È possibile utilizzare qualsiasi modo desiderato per la creazione di queste richieste, purché specificano valori di intestazione corretti hello e passare il token di accesso di hello correttamente quando si chiama in servizi multimediali.

Hello alla procedura seguente viene descritto del flusso di lavoro più comune di hello quando utilizzando hello API REST di servizi multimediali tooconnect tooMedia Services:

1. Recupero di un token di accesso 
2. Connessione toohello URI di servizi multimediali 
   
   > [!NOTE]
   > Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali. È necessario effettuare le chiamate successive toohello nuovo URI.
   > Viene visualizzato anche una risposta HTTP/1.1 200 contenente hello descrizione dei metadati API ODATA.
   > 
   > 
3. Registra le successive chiamate API toohello nuovo URL. 
   
    Ad esempio, se dopo aver tentato tooconnect, ottenuto dall'esempio hello:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Si consiglia di pubblicare le successive toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ chiamate API.

    >[!NOTE]
    >È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy). È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri). Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.

## <a name="access-control-address"></a>Indirizzo del controllo di accesso
L'indirizzo del controllo di accesso di Servizi multimediali è https://wamsprodglobal001acs.accesscontrol.windows.net, eccetto per la Cina settentrionale, dove è https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.

## <a name="getting-an-access-token"></a>Recupero di un token di accesso
Servizi multimediali tooaccess direttamente tramite hello API REST, recuperare un token di accesso da ACS e usarlo per ogni richiesta HTTP effettuata nel servizio hello. Questo token è simile tooother i token forniti dal servizio ACS in base alle attestazioni di accesso fornite nell'intestazione di hello di una richiesta HTTP utilizzando il protocollo OAuth v2 hello. Altri prerequisiti non è necessario prima di connettersi direttamente tooMedia servizi.

Hello riportato di seguito intestazione della richiesta HTTP hello e tooretrieve corpo utilizzato un token.

**Intestazione**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Corpo**:

Sono necessari valori tooprove hello client_id e client_secret nel corpo di hello della richiesta; client_id e client_secret corrispondono toohello AccountName e AccountKey valori, rispettivamente. Questi valori vengono forniti tooyou da servizi multimediali quando si configura l'account. 

Si noti che hello AccountKey per l'account di servizi multimediali deve essere codificato in URL (vedere [codifica percentuale](http://tools.ietf.org/html/rfc3986#section-2.1) viene utilizzato come valore client_secret hello nella richiesta di token di accesso.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


ad esempio: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Hello riportato di seguito risposta HTTP hello contenente accesso hello token nel corpo della risposta hello.

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> È consigliabile toocache hello "access_token" e "expires_in" valori tooan archiviazione esterna. dati del token Hello in seguito recuperati dall'archivio hello e usati nuovamente nelle chiamate API REST di servizi multimediali. Ciò è particolarmente utile per scenari in cui il token hello può essere condiviso in modo sicuro tra più processi o computer.
> 
> 

Verificare token di accesso hello che un valore "expires_in" hello toomonitor e aggiornare le chiamate API REST con i nuovi token in base alle esigenze.

### <a name="connecting-toohello-media-services-uri"></a>Connessione toohello URI di servizi multimediali
Hello URI radice per servizi multimediali è https://media.windows.net/. È necessario connettersi inizialmente toothis URI e se viene visualizzato un reindirizzamento 301 in risposta, è necessario effettuare le chiamate successive toohello nuovo URI. Inoltre, evitare di usare la logica di reindirizzamento automatico/collegamento nelle richieste. Verbi HTTP e i testi delle richieste non verranno inoltrati toohello nuovo URI.

Si noti che radice hello URI per il caricamento e download di file di Asset è https://yourstorageaccount.blob.core.windows.net/, dove nome account di archiviazione hello è identico a quello usato durante la configurazione dell'account servizi multimediali hello.

Hello di esempio seguente viene illustrato l'URI (https://media.windows.net/) radice servizi multimediali toohello di richiesta HTTP. richiesta di Hello Ottiene un reindirizzamento 301 restituite nella risposta. Hello richiesta successiva utilizza hello nuovo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).     

**Richiesta HTTP**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**Risposta HTTP**:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**Richiesta HTTP** (utilizzando hello nuovo URI):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**Risposta HTTP**:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> Dopo aver hello nuovo URI, che è hello URI che deve essere toocommunicate usato con servizi multimediali. 
> 
> 

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

