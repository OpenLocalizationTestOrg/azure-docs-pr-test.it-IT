---
title: Configurare i criteri di autorizzazione della chiave dei contenuti con REST - Azure | Documentazione Microsoft
description: Informazioni su come configurare i criteri di autorizzazione per una chiave simmetrica utilizzando API REST di Servizi multimediali.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7af5f9e2-8ed8-43f2-843b-580ce8759fd4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: ed20fca35070c190bb63925d0a57cf919bcdd96c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="b0f9a-103">Crittografia dinamica: configurare i criteri di autorizzazione della chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="b0f9a-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="b0f9a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b0f9a-104">Overview</span></span>
<span data-ttu-id="b0f9a-105">Servizi multimediali di Microsoft Azure consente di distribuire contenuti crittografati dinamicamente con AES (Advanced Encryption Standard), tramite chiavi di crittografia a 128 bit e con PlayReady o Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-105">Microsoft Azure Media Services enables you to deliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="b0f9a-106">Servizi multimediali offre anche un servizio per la distribuzione di chiavi e licenze PlayReady/Widevine ai client autorizzati.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses to authorized clients.</span></span>

<span data-ttu-id="b0f9a-107">Se si desidera crittografare un asset per Servizi multimediali, è necessario associare una chiave di crittografia (**CommonEncryption** o **EnvelopeEncryption**) all'asset (come descritto [qui](media-services-rest-create-contentkey.md)) e anche configurare criteri di autorizzazione per la chiave, (come descritto in questo articolo).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-107">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="b0f9a-108">Quando un flusso viene richiesto da un lettore, Servizi multimediali usa la chiave specificata per crittografare dinamicamente i contenuti mediante AES o PlayReady.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-108">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="b0f9a-109">Per decrittografare il flusso, il lettore richiederà la chiave dal servizio di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-109">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="b0f9a-110">Per decidere se l'utente è autorizzato a ottenere la chiave, il servizio valuta i criteri di autorizzazione specificati.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-110">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="b0f9a-111">Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="b0f9a-112">I criteri di autorizzazione delle chiavi simmetriche possono avere una o più restrizioni di tipo **Open** o **Token**.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-112">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="b0f9a-113">I criteri con restrizione Token devono essere accompagnati da un token rilasciato da un servizio STS (Secure Token Service, servizio token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-113">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="b0f9a-114">Servizi multimediali supporta i token nei formati **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) e **JSON Web Token** (JWT).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-114">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="b0f9a-115">Servizi multimediali non fornisce servizi token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="b0f9a-116">Per il rilascio di token è possibile creare un servizio token di sicurezza personalizzato oppure usare il Servizio di controllo di accesso di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-116">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="b0f9a-117">Il servizio token di sicurezza deve essere configurato in modo da creare un token firmato con la chiave specificata e rilasciare le attestazioni specificate nella configurazione della restrizione Token, come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-117">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="b0f9a-118">Il servizio di distribuzione delle chiavi di Servizi multimediali restituisce la chiave di crittografia al client se il token è valido e le attestazioni nel token corrispondono a quelle configurate per la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-118">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="b0f9a-119">Per altre informazioni, vedere</span><span class="sxs-lookup"><span data-stu-id="b0f9a-119">For more information, see</span></span>

[<span data-ttu-id="b0f9a-120">Autenticazione tramite token JWT</span><span class="sxs-lookup"><span data-stu-id="b0f9a-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="b0f9a-121">[Integrare l'app basata su OWIN MVC di Servizi multimediali di Azure con Azure Active Directory e limitare la distribuzione di chiavi simmetriche in base ad attestazioni JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="b0f9a-122">[Usare il Servizio di controllo di accesso di Azure per il rilascio di token](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-122">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="b0f9a-123">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-123">Some considerations apply:</span></span>
* <span data-ttu-id="b0f9a-124">Per usare la creazione dinamica dei pacchetti e la crittografia dinamica, verificare che l'endpoint di streaming da cui si intende trasmettere i contenuti si trovi nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-124">To be able to use dynamic packaging and dynamic encryption, make sure the streaming endpoint from which you want to stream  your content is in the **Running** state.</span></span>
* <span data-ttu-id="b0f9a-125">L'asset deve contenere un set di file MP4 o Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="b0f9a-126">Per altre informazioni, vedere l'articolo relativo alla [codifica di un asset](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="b0f9a-127">Caricare e codificare gli asset mediante l'opzione **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="b0f9a-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="b0f9a-128">Se si prevede di avere più chiavi simmetriche che richiedono una stessa configurazione di criteri, è consigliabile creare un singolo criterio di autorizzazione e applicarlo a più chiavi simmetriche.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-128">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="b0f9a-129">Il servizio di distribuzione delle chiavi memorizza nella cache l'oggetto ContentKeyAuthorizationPolicy e gli oggetti correlati (opzioni e restrizioni) per 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-129">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="b0f9a-130">Se si crea un oggetto ContentKeyAuthorizationPolicy e si specifica di usare una restrizione Token, quindi si esegue il test della configurazione e si aggiornano i criteri impostando una restrizione Open, il passaggio dei criteri alla versione Open richiede circa 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-130">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="b0f9a-131">Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="b0f9a-132">Attualmente, non è possibile crittografare i download progressivi.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="b0f9a-133">Crittografia dinamica AES-128</span><span class="sxs-lookup"><span data-stu-id="b0f9a-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="b0f9a-134">Quando si usa l'API REST di Servizi multimediali, tenere presenti le seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-134">When working with the Media Services REST API, the following considerations apply:</span></span>
> 
> <span data-ttu-id="b0f9a-135">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="b0f9a-136">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="b0f9a-137">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-137">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="b0f9a-138">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-138">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="b0f9a-139">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-139">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="b0f9a-140">Restrizione Open</span><span class="sxs-lookup"><span data-stu-id="b0f9a-140">Open Restriction</span></span>
<span data-ttu-id="b0f9a-141">Se si applica una restrizione Open, il sistema distribuirà la chiave a chiunque ne faccia richiesta.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-141">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="b0f9a-142">Questa restrizione può essere utile a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="b0f9a-143">Il seguente esempio crea un criterio di autorizzazione Open e lo aggiunge alla chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-143">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <span data-ttu-id="b0f9a-144"><a id="ContentKeyAuthorizationPolicies"></a>Creare ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="b0f9a-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="b0f9a-145">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-145">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423578086&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lZlyQ2%2bvH73qtJsb42%2fH3xF7r7EvQFR3UXyezuDENFU%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 36

    {"Name":"Open Authorization Policy"}

<span data-ttu-id="b0f9a-146">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-146">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 211
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Adb4593da-f4d1-4cc5-a92a-d20eacbabee4')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    x-ms-request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:25:56 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:db4593da-f4d1-4cc5-a92a-d20eacbabee4","Name":"Open Authorization Policy"}

#### <span data-ttu-id="b0f9a-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Creare ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="b0f9a-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="b0f9a-148">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-148">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 168

    {"Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="b0f9a-149">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-149">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 349
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    x-ms-request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:56:40 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:57829b17-1101-4797-919b-f816f4a007b7","Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

#### <span data-ttu-id="b0f9a-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Collegare ContentKeyAuthorizationPolicies con opzioni</span><span class="sxs-lookup"><span data-stu-id="b0f9a-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="b0f9a-151">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-151">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3A0baa438b-8ac2-4c40-a53c-4d4722b78715')/$links/Options HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9847f705-f2ca-4e95-a478-8f823dbbaa29
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 154

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')"}

<span data-ttu-id="b0f9a-152">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="b0f9a-153"><a id="AddAuthorizationPolicyToKey"></a>Aggiungere criteri di autorizzazione alla chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="b0f9a-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy to the content key</span></span>
<span data-ttu-id="b0f9a-154">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-154">Request:</span></span>

    PUT https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A2e6d36a7-a17c-4e9a-830d-eca23ad1a6f9') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: e613efff-cb6a-41b4-984a-f4f8fb6e76a4
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 78

    {"AuthorizationPolicyId":"nb:ckpid:UUID:c06cebb8-c4f0-4d1a-ba00-3273fb2bc3ad"}

<span data-ttu-id="b0f9a-155">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="b0f9a-156">Restrizione Token</span><span class="sxs-lookup"><span data-stu-id="b0f9a-156">Token Restriction</span></span>
<span data-ttu-id="b0f9a-157">Questa sezione descrive come creare un criterio di autorizzazione per una chiave simmetrica e associarlo a tale chiave.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-157">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="b0f9a-158">I criteri di autorizzazione definiscono i requisiti di autorizzazione che devono essere soddisfatti per determinare se l'utente è autorizzato a ricevere la chiave (ad esempio, se l'elenco di chiavi di verifica contiene la chiave con cui è stato firmato il token).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-158">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="b0f9a-159">Per configurare l'opzione di restrizione Token, è necessario usare un file XML per descrivere i requisiti di autorizzazione del token.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-159">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="b0f9a-160">Il file XML di configurazione della restrizione Token deve essere conforme al seguente schema XML.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-160">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="b0f9a-161"><a id="schema"></a>Schema di restrizione Token</span><span class="sxs-lookup"><span data-stu-id="b0f9a-161"><a id="schema"></a>Token restriction schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

<span data-ttu-id="b0f9a-162">Quando si configurano i criteri di limitazione del **token**, è necessario specificare i parametri primary **verification key**, **issuer** e **audience**.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-162">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="b0f9a-163">Il parametro **primary verification key** include la chiave usata per firmare il token. Il parametro **issuer** è il servizio token di sicurezza che emette il token.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-163">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="b0f9a-164">Il parametro **audience** (talvolta denominato **scope**) descrive l'ambito del token o la risorsa a cui il token autorizza l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-164">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="b0f9a-165">Il servizio di distribuzione delle chiavi di Servizi multimediali verifica che i valori nel token corrispondano ai valori nel modello.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-165">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="b0f9a-166">Il seguente esempio crea un criterio di autorizzazione con una restrizione Token.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-166">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="b0f9a-167">In questo esempio il client deve presentare un token contenente i seguenti dati: chiave di firma (VerificationKey), autorità emittente del token e attestazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-167">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="b0f9a-168">Creare ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="b0f9a-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="b0f9a-169">Creare i "criteri di restrizione Token", come mostrato [qui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-169">Create the "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="b0f9a-170">Creare ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="b0f9a-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="b0f9a-171">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-171">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580720&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5LsNu%2b0D4eD3UOP3BviTLDkUjaErdUx0ekJ8402xidQ%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1079

    {"Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="b0f9a-172">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-172">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1260
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae1ef6145-46e8-4ee6-9756-b1cf96328c23')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    x-ms-request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:10:37 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e1ef6145-46e8-4ee6-9756-b1cf96328c23","Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="b0f9a-173">Collegare ContentKeyAuthorizationPolicies con opzioni</span><span class="sxs-lookup"><span data-stu-id="b0f9a-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="b0f9a-174">Collegare ContentKeyAuthorizationPolicies con opzioni, come mostrato [qui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="b0f9a-175">Aggiungere criteri di autorizzazione alla chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="b0f9a-175">Add authorization policy to the content key</span></span>
<span data-ttu-id="b0f9a-176">Aggiungere criteri di autorizzazione alla chiave simmetrica, come mostrato [qui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-176">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="b0f9a-177">Crittografia dinamica PlayReady</span><span class="sxs-lookup"><span data-stu-id="b0f9a-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="b0f9a-178">Servizi multimediali consente di configurare i diritti e le restrizioni che il runtime di PlayReady DRM deve applicare quando l'utente prova a riprodurre contenuti protetti.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-178">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="b0f9a-179">Quando si protegge il contenuto con PlayReady, è necessario includere nei criteri di autorizzazione una stringa XML che definisce il [modello di licenza PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-179">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="b0f9a-180">Restrizione Open</span><span class="sxs-lookup"><span data-stu-id="b0f9a-180">Open Restriction</span></span>
<span data-ttu-id="b0f9a-181">Se si applica una restrizione Open, il sistema distribuirà la chiave a chiunque ne faccia richiesta.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-181">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="b0f9a-182">Questa restrizione può essere utile a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="b0f9a-183">Il seguente esempio crea un criterio di autorizzazione Open e lo aggiunge alla chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-183">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <span data-ttu-id="b0f9a-184"><a id="ContentKeyAuthorizationPolicies2"></a>Creare ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="b0f9a-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="b0f9a-185">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-185">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 58

    {"Name":"Deliver Common Content Key"}

<span data-ttu-id="b0f9a-186">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-186">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 233
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Acc3c64a8-e2fc-4e09-bf60-ac954251a387')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    x-ms-request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:26:00 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:cc3c64a8-e2fc-4e09-bf60-ac954251a387","Name":"Deliver Common Content Key"}


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="b0f9a-187">Creare ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="b0f9a-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="b0f9a-188">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-188">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 593

    {"Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="b0f9a-189">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-189">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 774
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A1052308c-4df7-4fdb-8d21-4d2141fc2be0')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    x-ms-request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:23:24 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:1052308c-4df7-4fdb-8d21-4d2141fc2be0","Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="b0f9a-190">Collegare ContentKeyAuthorizationPolicies con opzioni</span><span class="sxs-lookup"><span data-stu-id="b0f9a-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="b0f9a-191">Collegare ContentKeyAuthorizationPolicies con opzioni, come mostrato [qui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="b0f9a-192">Aggiungere criteri di autorizzazione alla chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="b0f9a-192">Add authorization policy to the content key</span></span>
<span data-ttu-id="b0f9a-193">Aggiungere criteri di autorizzazione alla chiave simmetrica, come mostrato [qui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-193">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="b0f9a-194">Restrizione Token</span><span class="sxs-lookup"><span data-stu-id="b0f9a-194">Token Restriction</span></span>
<span data-ttu-id="b0f9a-195">Per configurare l'opzione di restrizione Token, è necessario usare un file XML per descrivere i requisiti di autorizzazione del token.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-195">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="b0f9a-196">Il file XML di configurazione della restrizione Token deve essere conforme allo schema XML illustrato in [questa](#schema) sezione.</span><span class="sxs-lookup"><span data-stu-id="b0f9a-196">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="b0f9a-197">Creare ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="b0f9a-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="b0f9a-198">Creare ContentKeyAuthorizationPolicies, come mostrato [qui](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="b0f9a-199">Creare ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="b0f9a-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="b0f9a-200">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-200">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423583561&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5eZnkOsSv%2fLLEKmS%2bWObBlsNYyee8BQlp%2bUYbjugcJg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1525

    {"Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="b0f9a-201">Risposta:</span><span class="sxs-lookup"><span data-stu-id="b0f9a-201">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1706
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae42bbeae-de42-4077-90e9-a844f297ef70')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    x-ms-request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:58:47 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e42bbeae-de42-4077-90e9-a844f297ef70","Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="b0f9a-202">Collegare ContentKeyAuthorizationPolicies con opzioni</span><span class="sxs-lookup"><span data-stu-id="b0f9a-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="b0f9a-203">Collegare ContentKeyAuthorizationPolicies con opzioni, come mostrato [qui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="b0f9a-204">Aggiungere criteri di autorizzazione alla chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="b0f9a-204">Add authorization policy to the content key</span></span>
<span data-ttu-id="b0f9a-205">Aggiungere criteri di autorizzazione alla chiave simmetrica, come mostrato [qui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="b0f9a-205">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="b0f9a-206"><a id="types"></a>Tipi usati durante la definizione di ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="b0f9a-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="b0f9a-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="b0f9a-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="b0f9a-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="b0f9a-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="b0f9a-209">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b0f9a-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b0f9a-210">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b0f9a-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b0f9a-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0f9a-211">Next Steps</span></span>
<span data-ttu-id="b0f9a-212">Dopo aver configurato i criteri di autorizzazione della chiave simmetrica, passare all'argomento [Come configurare i criteri di distribuzione degli asset](media-services-rest-configure-asset-delivery-policy.md) .</span><span class="sxs-lookup"><span data-stu-id="b0f9a-212">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

