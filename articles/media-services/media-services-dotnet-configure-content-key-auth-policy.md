---
title: i criteri di autorizzazione chiave del contenuto aaaConfigure mediante Media Services .NET SDK | Documenti Microsoft
description: Informazioni su come tooconfigure criteri di autorizzazione per una chiave simmetrica mediante Media Services .NET SDK.
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
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="65f25-103">Crittografia dinamica: configurare i criteri di autorizzazione della chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="65f25-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="65f25-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="65f25-104">Overview</span></span>
<span data-ttu-id="65f25-105">Servizi multimediali di Microsoft Azure consente toodeliver MPEG-DASH, Smooth Streaming e i flussi HTTP-Live-Streaming (HLS) protetti con Advanced Encryption Standard (AES) (utilizzando le chiavi di crittografia a 128 bit) o [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="65f25-105">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="65f25-106">AMS consente inoltre di toodeliver DASH streams crittografato con DRM Widevine.</span><span class="sxs-lookup"><span data-stu-id="65f25-106">AMS also enables you toodeliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="65f25-107">PlayReady sia Widevine vengono crittografati in base hello specifica la crittografia comune (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="65f25-107">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="65f25-108">Servizi multimediali fornisce inoltre un **servizio di distribuzione chiave licenza** da cui i client possono ottenere chiavi AES o PlayReady/Widevine licenze tooplay hello contenuto crittografato.</span><span class="sxs-lookup"><span data-stu-id="65f25-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses tooplay hello encrypted content.</span></span>

<span data-ttu-id="65f25-109">Se si desidera per servizi multimediali tooencrypt un asset, è necessario tooassociate una chiave di crittografia (**CommonEncryption** o **EnvelopeEncryption**) con asset hello (come descritto [qui](media-services-dotnet-create-contentkey.md)) e inoltre configurare criteri di autorizzazione per la chiave di hello (come descritto in questo articolo).</span><span class="sxs-lookup"><span data-stu-id="65f25-109">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="65f25-110">Quando un flusso è richiesto da un lettore, servizi multimediali Usa hello specificato toodynamically chiave crittografare il contenuto utilizzando la crittografia AES o DRM.</span><span class="sxs-lookup"><span data-stu-id="65f25-110">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="65f25-111">flusso di hello toodecrypt, hello lettore richiederà chiave hello dal servizio di distribuzione delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="65f25-111">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="65f25-112">Se è o meno utente hello toodecide autorizzato chiave hello tooget, servizio hello valuta i criteri di autorizzazione hello specificato per la chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="65f25-112">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="65f25-113">Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi.</span><span class="sxs-lookup"><span data-stu-id="65f25-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="65f25-114">Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: **aprire** o **token** restrizione.</span><span class="sxs-lookup"><span data-stu-id="65f25-114">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="65f25-115">criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="65f25-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="65f25-116">Servizi multimediali supporta i token in hello **token Web semplici** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato e **Token Web JSON** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) formato.</span><span class="sxs-lookup"><span data-stu-id="65f25-116">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="65f25-117">Servizi multimediali non fornisce servizi token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="65f25-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="65f25-118">È possibile creare un servizio token di sicurezza personalizzato o utilizzare i token tooissue ACS di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="65f25-118">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="65f25-119">Hello servizio token di sicurezza deve essere configurato toocreate un token firmato con la chiave specificata hello e rilasciano le attestazioni specificate nella configurazione della restrizione token hello (come descritto in questo articolo).</span><span class="sxs-lookup"><span data-stu-id="65f25-119">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="65f25-120">Hello servizio di distribuzione delle chiavi di servizi multimediali restituirà client toohello chiave di crittografia hello se hello token è valido e hello attestazioni nel token hello corrispondono a quelli configurati per la chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="65f25-120">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="65f25-121">Per altre informazioni, vedere</span><span class="sxs-lookup"><span data-stu-id="65f25-121">For more information, see</span></span>

[<span data-ttu-id="65f25-122">Autenticazione tramite token JWT</span><span class="sxs-lookup"><span data-stu-id="65f25-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="65f25-123">[Integrare l'app basata su OWIN MVC di Servizi multimediali di Azure con Azure Active Directory e limitare la distribuzione di chiavi simmetriche in base ad attestazioni JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="65f25-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="65f25-124">[Utilizzare i token ACS di Azure tooissue](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="65f25-124">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="65f25-125">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="65f25-125">Some considerations apply:</span></span>
* <span data-ttu-id="65f25-126">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="65f25-126">When your AMS account is created a **default** streaming endpoint is added  tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="65f25-127">toostart streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, l'endpoint di streaming è toobe in hello **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="65f25-127">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has toobe in hello **Running** state.</span></span> 
* <span data-ttu-id="65f25-128">L'asset deve contenere un set di file MP4 o Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="65f25-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="65f25-129">Per altre informazioni, vedere l'articolo relativo alla [codifica di un asset](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="65f25-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="65f25-130">Caricare e codificare gli asset mediante l'opzione **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="65f25-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="65f25-131">Se si prevede di toohave più chiavi simmetriche che richiedono hello stessa configurazione dei criteri, è fortemente consigliabile toocreate un singolo criterio di autorizzazione e applicarlo a più chiavi simmetriche.</span><span class="sxs-lookup"><span data-stu-id="65f25-131">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="65f25-132">Hello del servizio di distribuzione delle chiavi memorizza nella cache ContentKeyAuthorizationPolicy e gli oggetti correlati (opzioni di criteri e restrizioni) per 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="65f25-132">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="65f25-133">Se si crea un oggetto ContentKeyAuthorizationPolicy e specifica toouse una restrizione "Token", quindi eseguirne il test e si aggiornano i criteri di hello troppo "aperto" restrizione, richiederà circa 15 minuti prima di hello criteri commutatori toohello "Aperto" versione di hello criterio.</span><span class="sxs-lookup"><span data-stu-id="65f25-133">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="65f25-134">Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.</span><span class="sxs-lookup"><span data-stu-id="65f25-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="65f25-135">Attualmente, non è possibile crittografare i download progressivi.</span><span class="sxs-lookup"><span data-stu-id="65f25-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="65f25-136">Crittografia dinamica AES-128</span><span class="sxs-lookup"><span data-stu-id="65f25-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="65f25-137">Restrizione Open</span><span class="sxs-lookup"><span data-stu-id="65f25-137">Open Restriction</span></span>
<span data-ttu-id="65f25-138">Restrizione Open, il sistema di hello distribuirà tooanyone di chiave hello che effettua una richiesta di chiave.</span><span class="sxs-lookup"><span data-stu-id="65f25-138">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="65f25-139">Questa restrizione può essere utile a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="65f25-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="65f25-140">Hello di esempio seguente crea un criterio open authorization e lo aggiunge la chiave simmetrica toohello.</span><span class="sxs-lookup"><span data-stu-id="65f25-140">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="65f25-141">Restrizione Token</span><span class="sxs-lookup"><span data-stu-id="65f25-141">Token Restriction</span></span>
<span data-ttu-id="65f25-142">In questa sezione viene descritto come toocreate un contenuto criteri di autorizzazione della chiave e associarlo a una chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="65f25-142">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="65f25-143">criteri di autorizzazione Hello descrive i requisiti di autorizzazione devono essere soddisfatto toodetermine se hello utente chiave hello tooreceive autorizzati (ad esempio, è l'elenco di "chiave di verifica" hello contenere chiave hello token hello è stato firmato con).</span><span class="sxs-lookup"><span data-stu-id="65f25-143">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="65f25-144">opzione di restrizione token tooconfigure hello, è necessario un XML toouse requisiti di autorizzazione del token di toodescribe hello.</span><span class="sxs-lookup"><span data-stu-id="65f25-144">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="65f25-145">configurazione della restrizione token Hello XML deve essere conforme toohello segue uno schema XML.</span><span class="sxs-lookup"><span data-stu-id="65f25-145">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="65f25-146"><a id="schema"></a>Schema di restrizione Token</span><span class="sxs-lookup"><span data-stu-id="65f25-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="65f25-147">Quando si configura hello **token** con restrizioni di criteri, è necessario specificare hello primario * * verifica chiave * *, **dell'autorità di certificazione** e **destinatari** parametri.</span><span class="sxs-lookup"><span data-stu-id="65f25-147">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="65f25-148">Hello * * chiave di verifica primaria * * contiene chiave hello hello token è stato firmato con, **dell'autorità di certificazione** è servizio di token di sicurezza di hello token hello problemi.</span><span class="sxs-lookup"><span data-stu-id="65f25-148">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="65f25-149">Hello **destinatari** (detto anche **ambito**) descrive hello scopo del token hello o della risorsa hello hello token autorizza l'accesso.</span><span class="sxs-lookup"><span data-stu-id="65f25-149">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="65f25-150">Hello servizio di distribuzione delle chiavi di servizi multimediali verifica che i valori nel token hello corrispondano valori hello hello modello.</span><span class="sxs-lookup"><span data-stu-id="65f25-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="65f25-151">Quando si utilizza **Media Services SDK per .NET**, è possibile utilizzare hello **TokenRestrictionTemplate** token restrizione hello toogenerate della classe.</span><span class="sxs-lookup"><span data-stu-id="65f25-151">When using **Media Services SDK for .NET**, you can use hello **TokenRestrictionTemplate** class toogenerate hello restriction token.</span></span>
<span data-ttu-id="65f25-152">Hello di esempio seguente crea un criterio di autorizzazione con una restrizione token.</span><span class="sxs-lookup"><span data-stu-id="65f25-152">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="65f25-153">In questo esempio, il client hello avrebbe toopresent un token contenente: la firma (VerificationKey) chiave autorità emittente del token e attestazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="65f25-153">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

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

#### <span data-ttu-id="65f25-154"><a id="test"></a>Token di test</span><span class="sxs-lookup"><span data-stu-id="65f25-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="65f25-155">tooget un token di test basato su hello limitazione del token è stato utilizzato per i criteri di autorizzazione chiave hello, hello seguente.</span><span class="sxs-lookup"><span data-stu-id="65f25-155">tooget a test token based on hello token restriction that was used for hello key authorization policy, do hello following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="65f25-156">Crittografia dinamica PlayReady</span><span class="sxs-lookup"><span data-stu-id="65f25-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="65f25-157">Servizi multimediali consente di diritti di hello tooconfigure e le restrizioni che si desidera per hello tooenforce di runtime di PlayReady DRM quando un utente tenta tooplay nuovo contenuto protetto.</span><span class="sxs-lookup"><span data-stu-id="65f25-157">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="65f25-158">Quando si proteggono i contenuti con PlayReady, una delle operazioni di hello è necessario toospecify nei criteri di autorizzazione è una stringa XML che definisce hello [modello di licenza PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65f25-158">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="65f25-159">In Media Services SDK per .NET, hello **PlayReadyLicenseResponseTemplate** e **PlayReadyLicenseTemplate** classi consentono di definire il modello di licenza PlayReady hello.</span><span class="sxs-lookup"><span data-stu-id="65f25-159">In Media Services SDK for .NET, hello **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define hello PlayReady License Template.</span></span>

<span data-ttu-id="65f25-160">[In questo argomento](media-services-protect-with-drm.md) viene illustrato come tooencrypt il contenuto con **PlayReady** e **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="65f25-160">[This topic](media-services-protect-with-drm.md) shows how tooencrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="65f25-161">Restrizione Open</span><span class="sxs-lookup"><span data-stu-id="65f25-161">Open Restriction</span></span>
<span data-ttu-id="65f25-162">Restrizione Open, il sistema di hello distribuirà tooanyone di chiave hello che effettua una richiesta di chiave.</span><span class="sxs-lookup"><span data-stu-id="65f25-162">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="65f25-163">Questa restrizione può essere utile a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="65f25-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="65f25-164">Hello di esempio seguente crea un criterio open authorization e lo aggiunge la chiave simmetrica toohello.</span><span class="sxs-lookup"><span data-stu-id="65f25-164">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="65f25-165">Restrizione Token</span><span class="sxs-lookup"><span data-stu-id="65f25-165">Token Restriction</span></span>
<span data-ttu-id="65f25-166">opzione di restrizione token tooconfigure hello, è necessario un XML toouse requisiti di autorizzazione del token di toodescribe hello.</span><span class="sxs-lookup"><span data-stu-id="65f25-166">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="65f25-167">configurazione della restrizione token Hello XML deve essere conforme toohello XML schema nella [questo](#schema) sezione.</span><span class="sxs-lookup"><span data-stu-id="65f25-167">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
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
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="65f25-168">un token di test in base alle restrizione token hello che è stato usato per vedere criteri di autorizzazione della chiave hello tooget [questo](#test) sezione.</span><span class="sxs-lookup"><span data-stu-id="65f25-168">tooget a test token based on hello token restriction that was used for hello key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="65f25-169"><a id="types"></a>Tipi usati durante la definizione di ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="65f25-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="65f25-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="65f25-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="65f25-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="65f25-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="65f25-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="65f25-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="65f25-173">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="65f25-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="65f25-174">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="65f25-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="65f25-175">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="65f25-175">Next step</span></span>
<span data-ttu-id="65f25-176">Ora che sono stati configurati criteri di autorizzazione della chiave simmetrica, visitare toohello [come criterio di recapito degli asset tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="65f25-176">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

