---
title: Connessione a un account di Servizi multimediali mediante l'API REST | Microsoft Docs
description: Questo argomento illustra come connettersi a Servizi multimediali mediante l'API REST.
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
ms.openlocfilehash: 4feb0eb81823835e8e0b701463d85b27f5598019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a><span data-ttu-id="5aaa5-103">Connessione a un account di Servizi multimediali mediante l'API REST di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5aaa5-103">Connecting to Media Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5aaa5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="5aaa5-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="5aaa5-105">REST</span><span class="sxs-lookup"><span data-stu-id="5aaa5-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="5aaa5-106">Questo argomento descrive come ottenere una connessione a Servizi multimediali di Microsoft Azure a livello di codice quando si programma con l'API REST di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services REST API.</span></span>

<span data-ttu-id="5aaa5-107">Quando si accede a Servizi multimediali di Microsoft Azure sono necessari due elementi: un token di accesso fornito da Servizi di controllo di accesso di Azure e l'URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and the URI of Media Services itself.</span></span> <span data-ttu-id="5aaa5-108">Per creare queste richieste è possibile procedere come si preferisce, ma è necessario specificare i valori di intestazione corretti e passare correttamente il token di accesso quando si esegue una chiamata in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-108">You can use any means you want when creating these requests as long as you specify the correct header values and pass in the access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="5aaa5-109">I seguenti passaggi descrivono i flussi di lavoro comuni relativi all'uso dell'API REST per connettersi a Servizi multimediali:</span><span class="sxs-lookup"><span data-stu-id="5aaa5-109">The following steps describe the most common workflow when using the Media Services REST API to connect to Media Services:</span></span>

1. <span data-ttu-id="5aaa5-110">Recupero di un token di accesso</span><span class="sxs-lookup"><span data-stu-id="5aaa5-110">Getting an access token</span></span> 
2. <span data-ttu-id="5aaa5-111">Connessione all'URI di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5aaa5-111">Connecting to the Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="5aaa5-112">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="5aaa5-113">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-113">You must make subsequent calls to the new URI.</span></span>
   > <span data-ttu-id="5aaa5-114">È anche possibile ricevere una risposta HTTP/1.1 200 contenente la descrizione dei metadati dell'API ODATA.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-114">You may also receive a HTTP/1.1 200 response that contains the ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="5aaa5-115">Inviare le successive chiamate API al nuovo URL.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-115">Post your subsequent API calls to the new URL.</span></span> 
   
    <span data-ttu-id="5aaa5-116">Se, ad esempio, dopo aver tentato la connessione si ottiene la seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5aaa5-116">For example, if after trying to connect, you got the following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="5aaa5-117">Si consiglia di inviare le successive chiamate API a https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-117">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="5aaa5-118">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="5aaa5-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="5aaa5-119">Usare lo stesso ID criterio se si usano sempre gli stessi giorni/autorizzazioni di accesso, come nel cado di criteri per i localizzatori che devono rimanere attivi per molto tempo (criteri di non caricamento).</span><span class="sxs-lookup"><span data-stu-id="5aaa5-119">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="5aaa5-120">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="5aaa5-121">Indirizzo del controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="5aaa5-121">Access control address</span></span>
<span data-ttu-id="5aaa5-122">L'indirizzo del controllo di accesso di Servizi multimediali è https://wamsprodglobal001acs.accesscontrol.windows.net, eccetto per la Cina settentrionale, dove è https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="5aaa5-123">Recupero di un token di accesso</span><span class="sxs-lookup"><span data-stu-id="5aaa5-123">Getting an access token</span></span>
<span data-ttu-id="5aaa5-124">Per accedere a Servizi multimediali direttamente dall'API REST, recuperare un token di accesso da Servizi di controllo di accesso e usarlo per ogni richiesta HTTP effettuata nel servizio.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-124">To access Media Services directly through the REST API, retrieve an access token from ACS and use it during every HTTP request you make into the service.</span></span> <span data-ttu-id="5aaa5-125">Questo token è simile ad altri token forniti da Servizi di controllo di accesso in base alle attestazioni di accesso riportate nell'intestazione di una richiesta HTTP che usano il protocollo OAuth versione 2.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-125">This token is similar to other tokens provided by ACS based on access claims provided in the header of an HTTP request and using the OAuth v2 protocol.</span></span> <span data-ttu-id="5aaa5-126">Non sono previsti altri prerequisiti per connettersi direttamente a Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-126">You do not need any other prerequisites before directly connecting to Media Services.</span></span>

<span data-ttu-id="5aaa5-127">Il seguente esempio illustra l'intestazione e il corpo della richiesta HTTP usati per recuperare un token.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-127">The following example shows the HTTP request header and body used to retrieve a token.</span></span>

<span data-ttu-id="5aaa5-128">**Intestazione**:</span><span class="sxs-lookup"><span data-stu-id="5aaa5-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="5aaa5-129">**Corpo**:</span><span class="sxs-lookup"><span data-stu-id="5aaa5-129">**Body**:</span></span>

<span data-ttu-id="5aaa5-130">È necessario verificare i valori client_id e client_secret nel corpo di questa richiesta. client_id e client_secret corrispondono rispettivamente ai valori AccountName e AccountKey.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-130">You need to prove the client_id and client_secret values in the body of this request; client_id and client_secret correspond to the AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="5aaa5-131">Questi valori vengono forniti da Servizi multimediali quando si configura l'account.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-131">These values are provided to you by Media Services when you set up your account.</span></span> 

<span data-ttu-id="5aaa5-132">Si noti che il valore AccountKey per l'account di Servizi multimediali deve essere codificato nell'URL. Vedere [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) quando viene usato come valore client_secret nella richiesta del token di accesso.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-132">Note that the AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as the client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="5aaa5-133">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5aaa5-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="5aaa5-134">Il seguente esempio illustra la risposta HTTP contenente il token di accesso nel corpo della risposta.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-134">The following example shows the HTTP response that contains the access token in the response body.</span></span>

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
> <span data-ttu-id="5aaa5-135">È consigliabile memorizzare nella cache i valori "access_token" e "expires_in" usando una risorsa di archiviazione esterna.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-135">It is recommended to cache the "access_token " and "expires_in " values to an external storage.</span></span> <span data-ttu-id="5aaa5-136">I dati del token potranno quindi essere recuperati da tale risorsa e riusati nelle chiamate all'API REST di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-136">The token data could later be retrieved from the storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="5aaa5-137">Ciò è particolarmente utile in scenari in cui il token può essere condiviso in modo sicuro tra più processi o computer.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-137">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="5aaa5-138">Assicurarsi di monitorare il valore "expires_in" del token di accesso e di aggiornare le chiamate all'API REST con i nuovi token a seconda delle esigenze.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-138">Make sure to monitor the "expires_in" value of the access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-to-the-media-services-uri"></a><span data-ttu-id="5aaa5-139">Connessione all'URI di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5aaa5-139">Connecting to the Media Services URI</span></span>
<span data-ttu-id="5aaa5-140">L'URI radice per Servizi multimediali è https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-140">The root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="5aaa5-141">Connettersi inizialmente a questo URI. Se si ottiene un reindirizzamento 301 come risposta, effettuare le chiamate successive al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-141">You should initially connect to this URI, and if you get a 301 redirect back in response, you should make subsequent calls to the new URI.</span></span> <span data-ttu-id="5aaa5-142">Inoltre, evitare di usare la logica di reindirizzamento automatico/collegamento nelle richieste.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="5aaa5-143">I corpi delle richieste e i verbi HTTP non verranno inoltrati al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-143">HTTP verbs and request bodies will not be forwarded to the new URI.</span></span>

<span data-ttu-id="5aaa5-144">Si noti che l'URI radice per il caricamento e il download di file di Asset è https://yourstorageaccount.blob.core.windows.net/, dove il nome dell'account di archiviazione corrisponde a quello usato durante la configurazione dell'account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-144">Note that the root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where the storage account name is the same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="5aaa5-145">L'esempio seguente illustra la richiesta HTTP all'URI radice di Servizi multimediali (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="5aaa5-145">The following example demonstrates HTTP request to the Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="5aaa5-146">La richiesta ottiene un reindirizzamento 301 come risposta.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-146">The request gets a 301 redirect back in response.</span></span> <span data-ttu-id="5aaa5-147">La richiesta successiva usa il nuovo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="5aaa5-147">The subsequent request is using the new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="5aaa5-148">**Richiesta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="5aaa5-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="5aaa5-149">**Risposta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="5aaa5-149">**HTTP Response**:</span></span>

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
    <h2>Object moved to <a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="5aaa5-150">**Richiesta HTTP** (con il nuovo URI):</span><span class="sxs-lookup"><span data-stu-id="5aaa5-150">**HTTP Request** (using the new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="5aaa5-151">**Risposta HTTP**:</span><span class="sxs-lookup"><span data-stu-id="5aaa5-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="5aaa5-152">Il nuovo URI ottenuto è quello da usare per comunicare con Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5aaa5-152">Once you get the new URI, that is the URI that should be used to communicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="5aaa5-153">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="5aaa5-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5aaa5-154">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="5aaa5-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

