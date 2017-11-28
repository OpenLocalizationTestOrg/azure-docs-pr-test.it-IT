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
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="1e925-103">Connessione tooMedia Account di servizi tramite l'API REST di servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1e925-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e925-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1e925-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="1e925-105">REST</span><span class="sxs-lookup"><span data-stu-id="1e925-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="1e925-106">In questo argomento viene descritto come tooobtain tooMicrosoft una connessione a livello di codice servizi multimediali di Azure quando si programma con hello API REST di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1e925-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="1e925-107">Quando si accede a servizi multimediali di Microsoft Azure, sono necessari due elementi: un token di accesso fornito da Azure Access Control Services (ACS) e hello URI di servizi multimediali di se stesso.</span><span class="sxs-lookup"><span data-stu-id="1e925-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="1e925-108">È possibile utilizzare qualsiasi modo desiderato per la creazione di queste richieste, purché specificano valori di intestazione corretti hello e passare il token di accesso di hello correttamente quando si chiama in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1e925-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="1e925-109">Hello alla procedura seguente viene descritto del flusso di lavoro più comune di hello quando utilizzando hello API REST di servizi multimediali tooconnect tooMedia Services:</span><span class="sxs-lookup"><span data-stu-id="1e925-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="1e925-110">Recupero di un token di accesso</span><span class="sxs-lookup"><span data-stu-id="1e925-110">Getting an access token</span></span> 
2. <span data-ttu-id="1e925-111">Connessione toohello URI di servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1e925-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="1e925-112">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1e925-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="1e925-113">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="1e925-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="1e925-114">Viene visualizzato anche una risposta HTTP/1.1 200 contenente hello descrizione dei metadati API ODATA.</span><span class="sxs-lookup"><span data-stu-id="1e925-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="1e925-115">Registra le successive chiamate API toohello nuovo URL.</span><span class="sxs-lookup"><span data-stu-id="1e925-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="1e925-116">Ad esempio, se dopo aver tentato tooconnect, ottenuto dall'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="1e925-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="1e925-117">Si consiglia di pubblicare le successive toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ chiamate API.</span><span class="sxs-lookup"><span data-stu-id="1e925-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="1e925-118">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="1e925-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="1e925-119">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="1e925-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="1e925-120">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="1e925-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="1e925-121">Indirizzo del controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="1e925-121">Access control address</span></span>
<span data-ttu-id="1e925-122">L'indirizzo del controllo di accesso di Servizi multimediali è https://wamsprodglobal001acs.accesscontrol.windows.net, eccetto per la Cina settentrionale, dove è https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="1e925-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="1e925-123">Recupero di un token di accesso</span><span class="sxs-lookup"><span data-stu-id="1e925-123">Getting an access token</span></span>
<span data-ttu-id="1e925-124">Servizi multimediali tooaccess direttamente tramite hello API REST, recuperare un token di accesso da ACS e usarlo per ogni richiesta HTTP effettuata nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="1e925-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="1e925-125">Questo token è simile tooother i token forniti dal servizio ACS in base alle attestazioni di accesso fornite nell'intestazione di hello di una richiesta HTTP utilizzando il protocollo OAuth v2 hello.</span><span class="sxs-lookup"><span data-stu-id="1e925-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="1e925-126">Altri prerequisiti non è necessario prima di connettersi direttamente tooMedia servizi.</span><span class="sxs-lookup"><span data-stu-id="1e925-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="1e925-127">Hello riportato di seguito intestazione della richiesta HTTP hello e tooretrieve corpo utilizzato un token.</span><span class="sxs-lookup"><span data-stu-id="1e925-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="1e925-128">**Intestazione**:</span><span class="sxs-lookup"><span data-stu-id="1e925-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="1e925-129">**Corpo**:</span><span class="sxs-lookup"><span data-stu-id="1e925-129">**Body**:</span></span>

<span data-ttu-id="1e925-130">Sono necessari valori tooprove hello client_id e client_secret nel corpo di hello della richiesta; client_id e client_secret corrispondono toohello AccountName e AccountKey valori, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="1e925-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="1e925-131">Questi valori vengono forniti tooyou da servizi multimediali quando si configura l'account.</span><span class="sxs-lookup"><span data-stu-id="1e925-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="1e925-132">Si noti che hello AccountKey per l'account di servizi multimediali deve essere codificato in URL (vedere [codifica percentuale](http://tools.ietf.org/html/rfc3986#section-2.1) viene utilizzato come valore client_secret hello nella richiesta di token di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e925-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="1e925-133">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1e925-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="1e925-134">Hello riportato di seguito risposta HTTP hello contenente accesso hello token nel corpo della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="1e925-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

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
> <span data-ttu-id="1e925-135">È consigliabile toocache hello "access_token" e "expires_in" valori tooan archiviazione esterna.</span><span class="sxs-lookup"><span data-stu-id="1e925-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="1e925-136">dati del token Hello in seguito recuperati dall'archivio hello e usati nuovamente nelle chiamate API REST di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1e925-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="1e925-137">Ciò è particolarmente utile per scenari in cui il token hello può essere condiviso in modo sicuro tra più processi o computer.</span><span class="sxs-lookup"><span data-stu-id="1e925-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="1e925-138">Verificare token di accesso hello che un valore "expires_in" hello toomonitor e aggiornare le chiamate API REST con i nuovi token in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1e925-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="1e925-139">Connessione toohello URI di servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1e925-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="1e925-140">Hello URI radice per servizi multimediali è https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="1e925-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="1e925-141">È necessario connettersi inizialmente toothis URI e se viene visualizzato un reindirizzamento 301 in risposta, è necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="1e925-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="1e925-142">Inoltre, evitare di usare la logica di reindirizzamento automatico/collegamento nelle richieste.</span><span class="sxs-lookup"><span data-stu-id="1e925-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="1e925-143">Verbi HTTP e i testi delle richieste non verranno inoltrati toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="1e925-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="1e925-144">Si noti che radice hello URI per il caricamento e download di file di Asset è https://yourstorageaccount.blob.core.windows.net/, dove nome account di archiviazione hello è identico a quello usato durante la configurazione dell'account servizi multimediali hello.</span><span class="sxs-lookup"><span data-stu-id="1e925-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="1e925-145">Hello di esempio seguente viene illustrato l'URI (https://media.windows.net/) radice servizi multimediali toohello di richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="1e925-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="1e925-146">richiesta di Hello Ottiene un reindirizzamento 301 restituite nella risposta.</span><span class="sxs-lookup"><span data-stu-id="1e925-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="1e925-147">Hello richiesta successiva utilizza hello nuovo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="1e925-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="1e925-148">**Richiesta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="1e925-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="1e925-149">**Risposta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="1e925-149">**HTTP Response**:</span></span>

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


<span data-ttu-id="1e925-150">**Richiesta HTTP** (utilizzando hello nuovo URI):</span><span class="sxs-lookup"><span data-stu-id="1e925-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="1e925-151">**Risposta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="1e925-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="1e925-152">Dopo aver hello nuovo URI, che è hello URI che deve essere toocommunicate usato con servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1e925-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="1e925-153">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1e925-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1e925-154">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1e925-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

