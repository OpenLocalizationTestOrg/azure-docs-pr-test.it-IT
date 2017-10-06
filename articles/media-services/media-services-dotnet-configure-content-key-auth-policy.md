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
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a>Crittografia dinamica: configurare i criteri di autorizzazione della chiave simmetrica
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Panoramica
Servizi multimediali di Microsoft Azure consente toodeliver MPEG-DASH, Smooth Streaming e i flussi HTTP-Live-Streaming (HLS) protetti con Advanced Encryption Standard (AES) (utilizzando le chiavi di crittografia a 128 bit) o [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS consente inoltre di toodeliver DASH streams crittografato con DRM Widevine. PlayReady sia Widevine vengono crittografati in base hello specifica la crittografia comune (ISO/IEC 23001-7 CENC).

Servizi multimediali fornisce inoltre un **servizio di distribuzione chiave licenza** da cui i client possono ottenere chiavi AES o PlayReady/Widevine licenze tooplay hello contenuto crittografato.

Se si desidera per servizi multimediali tooencrypt un asset, è necessario tooassociate una chiave di crittografia (**CommonEncryption** o **EnvelopeEncryption**) con asset hello (come descritto [qui](media-services-dotnet-create-contentkey.md)) e inoltre configurare criteri di autorizzazione per la chiave di hello (come descritto in questo articolo).

Quando un flusso è richiesto da un lettore, servizi multimediali Usa hello specificato toodynamically chiave crittografare il contenuto utilizzando la crittografia AES o DRM. flusso di hello toodecrypt, hello lettore richiederà chiave hello dal servizio di distribuzione delle chiavi hello. Se è o meno utente hello toodecide autorizzato chiave hello tooget, servizio hello valuta i criteri di autorizzazione hello specificato per la chiave di hello.

Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi. Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: **aprire** o **token** restrizione. criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza). Servizi multimediali supporta i token in hello **token Web semplici** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato e **Token Web JSON** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) formato.

Servizi multimediali non fornisce servizi token di sicurezza. È possibile creare un servizio token di sicurezza personalizzato o utilizzare i token tooissue ACS di Microsoft Azure. Hello servizio token di sicurezza deve essere configurato toocreate un token firmato con la chiave specificata hello e rilasciano le attestazioni specificate nella configurazione della restrizione token hello (come descritto in questo articolo). Hello servizio di distribuzione delle chiavi di servizi multimediali restituirà client toohello chiave di crittografia hello se hello token è valido e hello attestazioni nel token hello corrispondono a quelli configurati per la chiave simmetrica hello.

Per altre informazioni, vedere

[Autenticazione tramite token JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Integrare l'app basata su OWIN MVC di Servizi multimediali di Azure con Azure Active Directory e limitare la distribuzione di chiavi simmetriche in base ad attestazioni JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Utilizzare i token ACS di Azure tooissue](http://mingfeiy.com/acs-with-key-services).

### <a name="some-considerations-apply"></a>Considerazioni applicabili:
* Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. toostart streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, l'endpoint di streaming è toobe in hello **esecuzione** stato. 
* L'asset deve contenere un set di file MP4 o Smooth Streaming a velocità in bit adattiva. Per altre informazioni, vedere l'articolo relativo alla [codifica di un asset](media-services-encode-asset.md).
* Caricare e codificare gli asset mediante l'opzione **AssetCreationOptions.StorageEncrypted** .
* Se si prevede di toohave più chiavi simmetriche che richiedono hello stessa configurazione dei criteri, è fortemente consigliabile toocreate un singolo criterio di autorizzazione e applicarlo a più chiavi simmetriche.
* Hello del servizio di distribuzione delle chiavi memorizza nella cache ContentKeyAuthorizationPolicy e gli oggetti correlati (opzioni di criteri e restrizioni) per 15 minuti.  Se si crea un oggetto ContentKeyAuthorizationPolicy e specifica toouse una restrizione "Token", quindi eseguirne il test e si aggiornano i criteri di hello troppo "aperto" restrizione, richiederà circa 15 minuti prima di hello criteri commutatori toohello "Aperto" versione di hello criterio.
* Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.
* Attualmente, non è possibile crittografare i download progressivi.

## <a name="aes-128-dynamic-encryption"></a>Crittografia dinamica AES-128
### <a name="open-restriction"></a>Restrizione Open
Restrizione Open, il sistema di hello distribuirà tooanyone di chiave hello che effettua una richiesta di chiave. Questa restrizione può essere utile a scopo di test.

Hello di esempio seguente crea un criterio open authorization e lo aggiunge la chiave simmetrica toohello.

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


### <a name="token-restriction"></a>Restrizione Token
In questa sezione viene descritto come toocreate un contenuto criteri di autorizzazione della chiave e associarlo a una chiave simmetrica hello. criteri di autorizzazione Hello descrive i requisiti di autorizzazione devono essere soddisfatto toodetermine se hello utente chiave hello tooreceive autorizzati (ad esempio, è l'elenco di "chiave di verifica" hello contenere chiave hello token hello è stato firmato con).

opzione di restrizione token tooconfigure hello, è necessario un XML toouse requisiti di autorizzazione del token di toodescribe hello. configurazione della restrizione token Hello XML deve essere conforme toohello segue uno schema XML.

#### <a id="schema"></a>Schema di restrizione Token
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

Quando si configura hello **token** con restrizioni di criteri, è necessario specificare hello primario * * verifica chiave * *, **dell'autorità di certificazione** e **destinatari** parametri. Hello * * chiave di verifica primaria * * contiene chiave hello hello token è stato firmato con, **dell'autorità di certificazione** è servizio di token di sicurezza di hello token hello problemi. Hello **destinatari** (detto anche **ambito**) descrive hello scopo del token hello o della risorsa hello hello token autorizza l'accesso. Hello servizio di distribuzione delle chiavi di servizi multimediali verifica che i valori nel token hello corrispondano valori hello hello modello. 

Quando si utilizza **Media Services SDK per .NET**, è possibile utilizzare hello **TokenRestrictionTemplate** token restrizione hello toogenerate della classe.
Hello di esempio seguente crea un criterio di autorizzazione con una restrizione token. In questo esempio, il client hello avrebbe toopresent un token contenente: la firma (VerificationKey) chiave autorità emittente del token e attestazioni necessarie.

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

#### <a id="test"></a>Token di test
tooget un token di test basato su hello limitazione del token è stato utilizzato per i criteri di autorizzazione chiave hello, hello seguente.

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


## <a name="playready-dynamic-encryption"></a>Crittografia dinamica PlayReady
Servizi multimediali consente di diritti di hello tooconfigure e le restrizioni che si desidera per hello tooenforce di runtime di PlayReady DRM quando un utente tenta tooplay nuovo contenuto protetto. 

Quando si proteggono i contenuti con PlayReady, una delle operazioni di hello è necessario toospecify nei criteri di autorizzazione è una stringa XML che definisce hello [modello di licenza PlayReady](media-services-playready-license-template-overview.md). In Media Services SDK per .NET, hello **PlayReadyLicenseResponseTemplate** e **PlayReadyLicenseTemplate** classi consentono di definire il modello di licenza PlayReady hello.

[In questo argomento](media-services-protect-with-drm.md) viene illustrato come tooencrypt il contenuto con **PlayReady** e **Widevine**.

### <a name="open-restriction"></a>Restrizione Open
Restrizione Open, il sistema di hello distribuirà tooanyone di chiave hello che effettua una richiesta di chiave. Questa restrizione può essere utile a scopo di test.

Hello di esempio seguente crea un criterio open authorization e lo aggiunge la chiave simmetrica toohello.

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

### <a name="token-restriction"></a>Restrizione Token
opzione di restrizione token tooconfigure hello, è necessario un XML toouse requisiti di autorizzazione del token di toodescribe hello. configurazione della restrizione token Hello XML deve essere conforme toohello XML schema nella [questo](#schema) sezione.

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


un token di test in base alle restrizione token hello che è stato usato per vedere criteri di autorizzazione della chiave hello tooget [questo](#test) sezione. 

## <a id="types"></a>Tipi usati durante la definizione di ContentKeyAuthorizationPolicy
### <a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <a id="TokenType"></a>TokenType
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Passaggio successivo
Ora che sono stati configurati criteri di autorizzazione della chiave simmetrica, visitare toohello [come criterio di recapito degli asset tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) argomento.

