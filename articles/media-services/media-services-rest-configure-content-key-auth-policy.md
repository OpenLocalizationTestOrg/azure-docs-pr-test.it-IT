---
title: criteri di autorizzazione chiave del contenuto aaaConfigure con REST - Azure | Documenti Microsoft
description: Informazioni su come tooconfigure criteri di autorizzazione per una chiave simmetrica utilizzando l'API REST di servizi multimediali.
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
ms.openlocfilehash: c058b7682bcbfb736faba18ec7fce33f2f2acb49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="c2480-103">Crittografia dinamica: configurare i criteri di autorizzazione della chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="c2480-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="c2480-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c2480-104">Overview</span></span>
<span data-ttu-id="c2480-105">Servizi multimediali di Microsoft Azure consente di toodeliver il contenuto crittografato (in modo dinamico) con Advanced Encryption Standard (AES) (utilizzando le chiavi di crittografia a 128 bit) e PlayReady oppure Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="c2480-105">Microsoft Azure Media Services enables you toodeliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="c2480-106">Servizi multimediali fornisce anche un servizio per il recapito di chiavi e licenze PlayReady/Widevine tooauthorized client.</span><span class="sxs-lookup"><span data-stu-id="c2480-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses tooauthorized clients.</span></span>

<span data-ttu-id="c2480-107">Se si desidera per servizi multimediali tooencrypt un asset, è necessario tooassociate una chiave di crittografia (**CommonEncryption** o **EnvelopeEncryption**) con asset hello (come descritto [qui](media-services-rest-create-contentkey.md)) e inoltre configurare criteri di autorizzazione per la chiave di hello (come descritto in questo articolo).</span><span class="sxs-lookup"><span data-stu-id="c2480-107">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="c2480-108">Quando un flusso è richiesto da un lettore, servizi multimediali Usa hello specificato toodynamically chiave crittografare il contenuto usando la crittografia AES o PlayReady.</span><span class="sxs-lookup"><span data-stu-id="c2480-108">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="c2480-109">flusso di hello toodecrypt, hello lettore richiederà chiave hello dal servizio di distribuzione delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="c2480-109">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="c2480-110">Se è o meno utente hello toodecide autorizzato chiave hello tooget, servizio hello valuta i criteri di autorizzazione hello specificato per la chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="c2480-110">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="c2480-111">Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi.</span><span class="sxs-lookup"><span data-stu-id="c2480-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="c2480-112">Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: **aprire** o **token** restrizione.</span><span class="sxs-lookup"><span data-stu-id="c2480-112">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="c2480-113">criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="c2480-113">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="c2480-114">Servizi multimediali supporta i token in hello **token Web semplici** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato e * * formato **(JWT) Token Web JSON.</span><span class="sxs-lookup"><span data-stu-id="c2480-114">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="c2480-115">Servizi multimediali non fornisce servizi token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c2480-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="c2480-116">È possibile creare un servizio token di sicurezza personalizzato o utilizzare i token tooissue ACS di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c2480-116">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="c2480-117">Hello servizio token di sicurezza deve essere configurato toocreate un token firmato con la chiave specificata hello e rilasciano le attestazioni specificate nella configurazione della restrizione token hello (come descritto in questo articolo).</span><span class="sxs-lookup"><span data-stu-id="c2480-117">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="c2480-118">Hello servizio di distribuzione delle chiavi di servizi multimediali restituirà client toohello chiave di crittografia hello se hello token è valido e hello attestazioni nel token hello corrispondono a quelli configurati per la chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="c2480-118">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="c2480-119">Per altre informazioni, vedere</span><span class="sxs-lookup"><span data-stu-id="c2480-119">For more information, see</span></span>

[<span data-ttu-id="c2480-120">Autenticazione tramite token JWT</span><span class="sxs-lookup"><span data-stu-id="c2480-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="c2480-121">[Integrare l'app basata su OWIN MVC di Servizi multimediali di Azure con Azure Active Directory e limitare la distribuzione di chiavi simmetriche in base ad attestazioni JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="c2480-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="c2480-122">[Utilizzare i token ACS di Azure tooissue](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="c2480-122">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="c2480-123">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="c2480-123">Some considerations apply:</span></span>
* <span data-ttu-id="c2480-124">toobe toouse in grado di creazione dinamica dei pacchetti e la crittografia dinamica, verificare che sia di streaming dei contenuti di endpoint da cui si desidera toostream hello in hello **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="c2480-124">toobe able toouse dynamic packaging and dynamic encryption, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>
* <span data-ttu-id="c2480-125">L'asset deve contenere un set di file MP4 o Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="c2480-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="c2480-126">Per altre informazioni, vedere l'articolo relativo alla [codifica di un asset](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="c2480-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="c2480-127">Caricare e codificare gli asset mediante l'opzione **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="c2480-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="c2480-128">Se si prevede di toohave più chiavi simmetriche che richiedono hello stessa configurazione dei criteri, è fortemente consigliabile toocreate un singolo criterio di autorizzazione e applicarlo a più chiavi simmetriche.</span><span class="sxs-lookup"><span data-stu-id="c2480-128">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="c2480-129">Hello del servizio di distribuzione delle chiavi memorizza nella cache ContentKeyAuthorizationPolicy e gli oggetti correlati (opzioni di criteri e restrizioni) per 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="c2480-129">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="c2480-130">Se si crea un oggetto ContentKeyAuthorizationPolicy e specifica toouse una restrizione "Token", quindi eseguirne il test e si aggiornano i criteri di hello troppo "aperto" restrizione, richiederà circa 15 minuti prima di hello criteri commutatori toohello "Aperto" versione di hello criterio.</span><span class="sxs-lookup"><span data-stu-id="c2480-130">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="c2480-131">Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.</span><span class="sxs-lookup"><span data-stu-id="c2480-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="c2480-132">Attualmente, non è possibile crittografare i download progressivi.</span><span class="sxs-lookup"><span data-stu-id="c2480-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="c2480-133">Crittografia dinamica AES-128</span><span class="sxs-lookup"><span data-stu-id="c2480-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="c2480-134">Quando si utilizzano le API REST di servizi multimediali, hello hello seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="c2480-134">When working with hello Media Services REST API, hello following considerations apply:</span></span>
> 
> <span data-ttu-id="c2480-135">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="c2480-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="c2480-136">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c2480-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="c2480-137">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="c2480-137">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="c2480-138">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="c2480-138">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="c2480-139">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="c2480-139">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="c2480-140">Restrizione Open</span><span class="sxs-lookup"><span data-stu-id="c2480-140">Open Restriction</span></span>
<span data-ttu-id="c2480-141">Restrizione Open, il sistema di hello distribuirà tooanyone di chiave hello che effettua una richiesta di chiave.</span><span class="sxs-lookup"><span data-stu-id="c2480-141">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="c2480-142">Questa restrizione può essere utile a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="c2480-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="c2480-143">Hello di esempio seguente crea un criterio open authorization e lo aggiunge la chiave simmetrica toohello.</span><span class="sxs-lookup"><span data-stu-id="c2480-143">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="c2480-144"><a id="ContentKeyAuthorizationPolicies"></a>Creare ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="c2480-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="c2480-145">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="c2480-145">Request:</span></span>

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

<span data-ttu-id="c2480-146">Risposta:</span><span class="sxs-lookup"><span data-stu-id="c2480-146">Response:</span></span>

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

#### <span data-ttu-id="c2480-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Creare ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="c2480-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="c2480-148">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="c2480-148">Request:</span></span>

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

<span data-ttu-id="c2480-149">Risposta:</span><span class="sxs-lookup"><span data-stu-id="c2480-149">Response:</span></span>    

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

#### <span data-ttu-id="c2480-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Collegare ContentKeyAuthorizationPolicies con opzioni</span><span class="sxs-lookup"><span data-stu-id="c2480-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="c2480-151">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="c2480-151">Request:</span></span>

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

<span data-ttu-id="c2480-152">Risposta:</span><span class="sxs-lookup"><span data-stu-id="c2480-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="c2480-153"><a id="AddAuthorizationPolicyToKey"></a>Aggiungere una chiave simmetrica toohello criteri di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="c2480-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy toohello content key</span></span>
<span data-ttu-id="c2480-154">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="c2480-154">Request:</span></span>

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

<span data-ttu-id="c2480-155">Risposta:</span><span class="sxs-lookup"><span data-stu-id="c2480-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="c2480-156">Restrizione Token</span><span class="sxs-lookup"><span data-stu-id="c2480-156">Token Restriction</span></span>
<span data-ttu-id="c2480-157">In questa sezione viene descritto come toocreate un contenuto criteri di autorizzazione della chiave e associarlo a una chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="c2480-157">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="c2480-158">criteri di autorizzazione Hello descrive i requisiti di autorizzazione devono essere soddisfatto toodetermine se hello utente chiave hello tooreceive autorizzati (ad esempio, è l'elenco di "chiave di verifica" hello contenere chiave hello token hello è stato firmato con).</span><span class="sxs-lookup"><span data-stu-id="c2480-158">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="c2480-159">opzione di restrizione token tooconfigure hello, è necessario un XML toouse requisiti di autorizzazione del token di toodescribe hello.</span><span class="sxs-lookup"><span data-stu-id="c2480-159">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="c2480-160">configurazione della restrizione token Hello XML deve essere conforme toohello segue uno schema XML.</span><span class="sxs-lookup"><span data-stu-id="c2480-160">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="c2480-161"><a id="schema"></a>Schema di restrizione Token</span><span class="sxs-lookup"><span data-stu-id="c2480-161"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="c2480-162">Quando si configura hello **token** con restrizioni di criteri, è necessario specificare hello primario * * verifica chiave * *, **dell'autorità di certificazione** e **destinatari** parametri.</span><span class="sxs-lookup"><span data-stu-id="c2480-162">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="c2480-163">Hello * * chiave di verifica primaria * * contiene chiave hello hello token è stato firmato con, **dell'autorità di certificazione** è servizio di token di sicurezza di hello token hello problemi.</span><span class="sxs-lookup"><span data-stu-id="c2480-163">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="c2480-164">Hello **destinatari** (detto anche **ambito**) descrive hello scopo del token hello o della risorsa hello hello token autorizza l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c2480-164">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="c2480-165">Hello servizio di distribuzione delle chiavi di servizi multimediali verifica che i valori nel token hello corrispondano valori hello hello modello.</span><span class="sxs-lookup"><span data-stu-id="c2480-165">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="c2480-166">Hello di esempio seguente crea un criterio di autorizzazione con una restrizione token.</span><span class="sxs-lookup"><span data-stu-id="c2480-166">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="c2480-167">In questo esempio, il client hello avrebbe toopresent un token contenente: la firma (VerificationKey) chiave autorità emittente del token e attestazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="c2480-167">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="c2480-168">Creare ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="c2480-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="c2480-169">Creare "Criteri di restrizione Token" hello, come illustrato [qui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="c2480-169">Create hello "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="c2480-170">Creare ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="c2480-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="c2480-171">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="c2480-171">Request:</span></span>

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

<span data-ttu-id="c2480-172">Risposta:</span><span class="sxs-lookup"><span data-stu-id="c2480-172">Response:</span></span>    

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

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="c2480-173">Collegare ContentKeyAuthorizationPolicies con opzioni</span><span class="sxs-lookup"><span data-stu-id="c2480-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="c2480-174">Collegare ContentKeyAuthorizationPolicies con opzioni, come mostrato [qui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="c2480-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="c2480-175">Aggiungere una chiave simmetrica toohello criteri di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="c2480-175">Add authorization policy toohello content key</span></span>
<span data-ttu-id="c2480-176">Aggiungere AuthorizationPolicy toohello ContentKey, come illustrato [qui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="c2480-176">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="c2480-177">Crittografia dinamica PlayReady</span><span class="sxs-lookup"><span data-stu-id="c2480-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="c2480-178">Servizi multimediali consente di diritti di hello tooconfigure e le restrizioni che si desidera per hello tooenforce di runtime di PlayReady DRM quando un utente tenta tooplay nuovo contenuto protetto.</span><span class="sxs-lookup"><span data-stu-id="c2480-178">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="c2480-179">Quando si proteggono i contenuti con PlayReady, una delle operazioni di hello è necessario toospecify nei criteri di autorizzazione è una stringa XML che definisce hello [modello di licenza PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2480-179">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="c2480-180">Restrizione Open</span><span class="sxs-lookup"><span data-stu-id="c2480-180">Open Restriction</span></span>
<span data-ttu-id="c2480-181">Restrizione Open, il sistema di hello distribuirà tooanyone di chiave hello che effettua una richiesta di chiave.</span><span class="sxs-lookup"><span data-stu-id="c2480-181">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="c2480-182">Questa restrizione può essere utile a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="c2480-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="c2480-183">Hello di esempio seguente crea un criterio open authorization e lo aggiunge la chiave simmetrica toohello.</span><span class="sxs-lookup"><span data-stu-id="c2480-183">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="c2480-184"><a id="ContentKeyAuthorizationPolicies2"></a>Creare ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="c2480-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="c2480-185">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="c2480-185">Request:</span></span>

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

<span data-ttu-id="c2480-186">Risposta:</span><span class="sxs-lookup"><span data-stu-id="c2480-186">Response:</span></span>

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


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="c2480-187">Creare ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="c2480-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="c2480-188">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="c2480-188">Request:</span></span>

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

<span data-ttu-id="c2480-189">Risposta:</span><span class="sxs-lookup"><span data-stu-id="c2480-189">Response:</span></span>

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

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="c2480-190">Collegare ContentKeyAuthorizationPolicies con opzioni</span><span class="sxs-lookup"><span data-stu-id="c2480-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="c2480-191">Collegare ContentKeyAuthorizationPolicies con opzioni, come mostrato [qui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="c2480-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="c2480-192">Aggiungere una chiave simmetrica toohello criteri di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="c2480-192">Add authorization policy toohello content key</span></span>
<span data-ttu-id="c2480-193">Aggiungere AuthorizationPolicy toohello ContentKey, come illustrato [qui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="c2480-193">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="c2480-194">Restrizione Token</span><span class="sxs-lookup"><span data-stu-id="c2480-194">Token Restriction</span></span>
<span data-ttu-id="c2480-195">opzione di restrizione token tooconfigure hello, è necessario un XML toouse requisiti di autorizzazione del token di toodescribe hello.</span><span class="sxs-lookup"><span data-stu-id="c2480-195">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="c2480-196">configurazione della restrizione token Hello XML deve essere conforme toohello XML schema nella [questo](#schema) sezione.</span><span class="sxs-lookup"><span data-stu-id="c2480-196">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="c2480-197">Creare ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="c2480-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="c2480-198">Creare ContentKeyAuthorizationPolicies, come mostrato [qui](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="c2480-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="c2480-199">Creare ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="c2480-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="c2480-200">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="c2480-200">Request:</span></span>

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

<span data-ttu-id="c2480-201">Risposta:</span><span class="sxs-lookup"><span data-stu-id="c2480-201">Response:</span></span>

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

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="c2480-202">Collegare ContentKeyAuthorizationPolicies con opzioni</span><span class="sxs-lookup"><span data-stu-id="c2480-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="c2480-203">Collegare ContentKeyAuthorizationPolicies con opzioni, come mostrato [qui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="c2480-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="c2480-204">Aggiungere una chiave simmetrica toohello criteri di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="c2480-204">Add authorization policy toohello content key</span></span>
<span data-ttu-id="c2480-205">Aggiungere AuthorizationPolicy toohello ContentKey, come illustrato [qui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="c2480-205">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="c2480-206"><a id="types"></a>Tipi usati durante la definizione di ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="c2480-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="c2480-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="c2480-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="c2480-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="c2480-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="c2480-209">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="c2480-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c2480-210">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="c2480-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c2480-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2480-211">Next Steps</span></span>
<span data-ttu-id="c2480-212">Ora che sono stati configurati criteri di autorizzazione della chiave simmetrica, visitare toohello [come criterio di recapito degli asset tooconfigure](media-services-rest-configure-asset-delivery-policy.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="c2480-212">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

