---
title: Configurare i criteri di autorizzazione della chiave simmetrica mediante l'SDK di Servizi multimediali per .NET | Microsoft Docs
description: Informazioni su come configurare i criteri di autorizzazione per una chiave simmetrica utilizzando .NET SDK di Servizi multimediali.
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: 75dd9107dca215a0b31db3d44bada69210fe9ac6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="861e0-103">Crittografia dinamica: configurare i criteri di autorizzazione della chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="861e0-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="861e0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="861e0-104">Overview</span></span>
<span data-ttu-id="861e0-105">Servizi multimediali di Microsoft Azure consente di distribuire flussi MPEG-DASH, Smooth Streaming e HTTP-Live-Streaming (HLS) protetti con Advanced Encryption Standard (AES) con chiavi di crittografia a 128 bit o [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="861e0-105">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="861e0-106">AMS consente anche di recapitare flussi DASH crittografati con Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="861e0-106">AMS also enables you to deliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="861e0-107">PlayReady e Widewine vengono crittografati in base alle specifiche della crittografia comune (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="861e0-107">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="861e0-108">Servizi multimediali offre anche un **servizio di distribuzione di chiavi/licenze** dal quale i client possono ottenere chiavi AES o licenze PlayReady/Widevine per riprodurre contenuti crittografati.</span><span class="sxs-lookup"><span data-stu-id="861e0-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span></span>

<span data-ttu-id="861e0-109">Se si desidera crittografare un asset per Servizi multimediali, è necessario associare una chiave di crittografia (**CommonEncryption** o **EnvelopeEncryption**) all'asset (come descritto [qui](media-services-dotnet-create-contentkey.md)) e anche configurare criteri di autorizzazione per la chiave, (come descritto in questo articolo).</span><span class="sxs-lookup"><span data-stu-id="861e0-109">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="861e0-110">Quando un flusso viene richiesto da un lettore, Servizi multimediali usa la chiave specificata per crittografare dinamicamente i contenuti mediante la crittografia DRM o AES.</span><span class="sxs-lookup"><span data-stu-id="861e0-110">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="861e0-111">Per decrittografare il flusso, il lettore richiederà la chiave dal servizio di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="861e0-111">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="861e0-112">Per decidere se l'utente è autorizzato a ottenere la chiave, il servizio valuta i criteri di autorizzazione specificati.</span><span class="sxs-lookup"><span data-stu-id="861e0-112">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="861e0-113">Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi.</span><span class="sxs-lookup"><span data-stu-id="861e0-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="861e0-114">I criteri di autorizzazione delle chiavi simmetriche possono avere una o più restrizioni di tipo **Open** o **Token**.</span><span class="sxs-lookup"><span data-stu-id="861e0-114">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="861e0-115">I criteri con restrizione Token devono essere accompagnati da un token rilasciato da un servizio STS (Secure Token Service, servizio token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="861e0-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="861e0-116">Servizi multimediali supporta i token nei formati **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) e **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)).</span><span class="sxs-lookup"><span data-stu-id="861e0-116">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="861e0-117">Servizi multimediali non fornisce servizi token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="861e0-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="861e0-118">Per il rilascio di token è possibile creare un servizio token di sicurezza personalizzato oppure usare il Servizio di controllo di accesso di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="861e0-118">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="861e0-119">Il servizio token di sicurezza deve essere configurato in modo da creare un token firmato con la chiave specificata e rilasciare le attestazioni specificate nella configurazione della restrizione Token, come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="861e0-119">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="861e0-120">Il servizio di distribuzione delle chiavi di Servizi multimediali restituisce la chiave di crittografia al client se il token è valido e le attestazioni nel token corrispondono a quelle configurate per la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="861e0-120">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="861e0-121">Per altre informazioni, vedere</span><span class="sxs-lookup"><span data-stu-id="861e0-121">For more information, see</span></span>

[<span data-ttu-id="861e0-122">Autenticazione tramite token JWT</span><span class="sxs-lookup"><span data-stu-id="861e0-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="861e0-123">[Integrare l'app basata su OWIN MVC di Servizi multimediali di Azure con Azure Active Directory e limitare la distribuzione di chiavi simmetriche in base ad attestazioni JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="861e0-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="861e0-124">[Usare il Servizio di controllo di accesso di Azure per il rilascio di token](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="861e0-124">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="861e0-125">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="861e0-125">Some considerations apply:</span></span>
* <span data-ttu-id="861e0-126">Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="861e0-126">When your AMS account is created a **default** streaming endpoint is added  to your account in the **Stopped** state.</span></span> <span data-ttu-id="861e0-127">Per avviare lo streaming dei contenuti e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming deve trovarsi nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="861e0-127">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has to be in the **Running** state.</span></span> 
* <span data-ttu-id="861e0-128">L'asset deve contenere un set di file MP4 o Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="861e0-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="861e0-129">Per altre informazioni, vedere l'articolo relativo alla [codifica di un asset](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="861e0-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="861e0-130">Caricare e codificare gli asset mediante l'opzione **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="861e0-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="861e0-131">Se si prevede di avere più chiavi simmetriche che richiedono una stessa configurazione di criteri, è consigliabile creare un singolo criterio di autorizzazione e applicarlo a più chiavi simmetriche.</span><span class="sxs-lookup"><span data-stu-id="861e0-131">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="861e0-132">Il servizio di distribuzione delle chiavi memorizza nella cache l'oggetto ContentKeyAuthorizationPolicy e gli oggetti correlati (opzioni e restrizioni) per 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="861e0-132">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="861e0-133">Se si crea un oggetto ContentKeyAuthorizationPolicy e si specifica di usare una restrizione Token, quindi si esegue il test della configurazione e si aggiornano i criteri impostando una restrizione Open, il passaggio dei criteri alla versione Open richiede circa 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="861e0-133">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="861e0-134">Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.</span><span class="sxs-lookup"><span data-stu-id="861e0-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="861e0-135">Attualmente, non è possibile crittografare i download progressivi.</span><span class="sxs-lookup"><span data-stu-id="861e0-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="861e0-136">Crittografia dinamica AES-128</span><span class="sxs-lookup"><span data-stu-id="861e0-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="861e0-137">Restrizione Open</span><span class="sxs-lookup"><span data-stu-id="861e0-137">Open Restriction</span></span>
<span data-ttu-id="861e0-138">Se si applica una restrizione Open, il sistema distribuirà la chiave a chiunque ne faccia richiesta.</span><span class="sxs-lookup"><span data-stu-id="861e0-138">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="861e0-139">Questa restrizione può essere utile a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="861e0-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="861e0-140">Il seguente esempio crea un criterio di autorizzazione Open e lo aggiunge alla chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="861e0-140">The following example creates an open authorization policy and adds it to the content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="861e0-141">Restrizione Token</span><span class="sxs-lookup"><span data-stu-id="861e0-141">Token Restriction</span></span>
<span data-ttu-id="861e0-142">Questa sezione descrive come creare un criterio di autorizzazione per una chiave simmetrica e associarlo a tale chiave.</span><span class="sxs-lookup"><span data-stu-id="861e0-142">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="861e0-143">I criteri di autorizzazione definiscono i requisiti di autorizzazione che devono essere soddisfatti per determinare se l'utente è autorizzato a ricevere la chiave (ad esempio, se l'elenco di chiavi di verifica contiene la chiave con cui è stato firmato il token).</span><span class="sxs-lookup"><span data-stu-id="861e0-143">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="861e0-144">Per configurare l'opzione di restrizione Token, è necessario usare un file XML per descrivere i requisiti di autorizzazione del token.</span><span class="sxs-lookup"><span data-stu-id="861e0-144">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="861e0-145">Il file XML di configurazione della restrizione Token deve essere conforme al seguente schema XML.</span><span class="sxs-lookup"><span data-stu-id="861e0-145">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="861e0-146"><a id="schema"></a>Schema di restrizione Token</span><span class="sxs-lookup"><span data-stu-id="861e0-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="861e0-147">Quando si configurano i criteri di limitazione del **token**, è necessario specificare i parametri primary **verification key**, **issuer** e **audience**.</span><span class="sxs-lookup"><span data-stu-id="861e0-147">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="861e0-148">Il parametro **primary verification key** include la chiave usata per firmare il token. Il parametro **issuer** è il servizio token di sicurezza che emette il token.</span><span class="sxs-lookup"><span data-stu-id="861e0-148">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="861e0-149">Il parametro **audience** (talvolta denominato **scope**) descrive l'ambito del token o la risorsa a cui il token autorizza l'accesso.</span><span class="sxs-lookup"><span data-stu-id="861e0-149">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="861e0-150">Il servizio di distribuzione delle chiavi di Servizi multimediali verifica che i valori nel token corrispondano ai valori nel modello.</span><span class="sxs-lookup"><span data-stu-id="861e0-150">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="861e0-151">Se si usa **Media Services SDK per .NET**, è possibile usare la classe **TokenRestrictionTemplate** per generare il token della restrizione.</span><span class="sxs-lookup"><span data-stu-id="861e0-151">When using **Media Services SDK for .NET**, you can use the **TokenRestrictionTemplate** class to generate the restriction token.</span></span>
<span data-ttu-id="861e0-152">Il seguente esempio crea un criterio di autorizzazione con una restrizione Token.</span><span class="sxs-lookup"><span data-stu-id="861e0-152">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="861e0-153">In questo esempio il client deve presentare un token contenente i seguenti dati: chiave di firma (VerificationKey), autorità emittente del token e attestazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="861e0-153">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <span data-ttu-id="861e0-154"><a id="test"></a>Token di test</span><span class="sxs-lookup"><span data-stu-id="861e0-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="861e0-155">Per ottenere un token di test basato sulla restrizione Token usata per i criteri di autorizzazione della chiave, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="861e0-155">To get a test token based on the token restriction that was used for the key authorization policy, do the following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the the data in the given TokenRestrictionTemplate.
    // Note, you need to pass the key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="861e0-156">Crittografia dinamica PlayReady</span><span class="sxs-lookup"><span data-stu-id="861e0-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="861e0-157">Servizi multimediali consente di configurare i diritti e le restrizioni che il runtime di PlayReady DRM deve applicare quando l'utente prova a riprodurre contenuti protetti.</span><span class="sxs-lookup"><span data-stu-id="861e0-157">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="861e0-158">Quando si protegge il contenuto con PlayReady, è necessario includere nei criteri di autorizzazione una stringa XML che definisce il [modello di licenza PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="861e0-158">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="861e0-159">Per definire più facilmente questo modello, è possibile usare le classi **PlayReadyLicenseResponseTemplate** e **PlayReadyLicenseTemplate** incluse in Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="861e0-159">In Media Services SDK for .NET, the **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define the PlayReady License Template.</span></span>

<span data-ttu-id="861e0-160">[Questo argomento](media-services-protect-with-drm.md) illustra come crittografare i contenuti con **PlayReady** e **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="861e0-160">[This topic](media-services-protect-with-drm.md) shows how to encrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="861e0-161">Restrizione Open</span><span class="sxs-lookup"><span data-stu-id="861e0-161">Open Restriction</span></span>
<span data-ttu-id="861e0-162">Se si applica una restrizione Open, il sistema distribuirà la chiave a chiunque ne faccia richiesta.</span><span class="sxs-lookup"><span data-stu-id="861e0-162">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="861e0-163">Questa restrizione può essere utile a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="861e0-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="861e0-164">Il seguente esempio crea un criterio di autorizzazione Open e lo aggiunge alla chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="861e0-164">The following example creates an open authorization policy and adds it to the content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="861e0-165">Restrizione Token</span><span class="sxs-lookup"><span data-stu-id="861e0-165">Token Restriction</span></span>
<span data-ttu-id="861e0-166">Per configurare l'opzione di restrizione Token, è necessario usare un file XML per descrivere i requisiti di autorizzazione del token.</span><span class="sxs-lookup"><span data-stu-id="861e0-166">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="861e0-167">Il file XML di configurazione della restrizione Token deve essere conforme allo schema XML illustrato in [questa](#schema) sezione.</span><span class="sxs-lookup"><span data-stu-id="861e0-167">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // The following code configures PlayReady License Template using .NET classes
        // and returns the XML string.

        //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user. 
        //It contains a field for a custom data string between the license server and the application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // to be returned to the end users. 
        //It contains the data on the content key in the license and any rights or restrictions to be 
        //enforced by the PlayReady DRM runtime when using the content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether the license is persistent (saved in persistent storage on the client) 
        //or non-persistent (only held in memory while the player is using the license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use the license or not.  
        // If true, the MinimumSecurityLevel property of the license
        // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
        // It grants the user the ability to playback the content subject to the zero or more restrictions 
        // configured in the license and on the PlayRight itself (for playback specific policy). 
        // Much of the policy on the PlayRight has to do with output restrictions 
        // which control the types of outputs that the content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
        //then the DRM runtime will only allow the video to be displayed over digital outputs 
        //(analog video outputs won’t be allowed to pass the content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience. 
        // If the output protections are configured too restrictive, 
        // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="861e0-168">Per ottenere un token di test basato sulla restrizione Token usata per i criteri di autorizzazione della chiave, vedere [questa](#test) sezione.</span><span class="sxs-lookup"><span data-stu-id="861e0-168">To get a test token based on the token restriction that was used for the key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="861e0-169"><a id="types"></a>Tipi usati durante la definizione di ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="861e0-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="861e0-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="861e0-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="861e0-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="861e0-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="861e0-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="861e0-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="861e0-173">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="861e0-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="861e0-174">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="861e0-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="861e0-175">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="861e0-175">Next step</span></span>
<span data-ttu-id="861e0-176">Dopo aver configurato i criteri di autorizzazione della chiave simmetrica, passare all'argomento [Come configurare i criteri di distribuzione degli asset](media-services-dotnet-configure-asset-delivery-policy.md) .</span><span class="sxs-lookup"><span data-stu-id="861e0-176">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

