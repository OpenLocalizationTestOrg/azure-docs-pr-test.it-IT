---
title: aaaUse servizi multimediali di Azure toodeliver DRM licenze o chiavi AES
description: "In questo articolo viene descritto come è possibile utilizzare le licenze PlayReady e/o Widevine toodeliver di servizi multimediali di Azure (AMS) e chiavi AES ma hello rest (codifica, crittografia, streaming) utilizzando il server locale."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 8546c2c1-430b-4254-a88d-4436a83f9192
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: a81da2973c79e5182ae58aeca7a0f14f3fc7c9ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-services-toodeliver-drm-licenses-or-aes-keys"></a><span data-ttu-id="020b7-103">Utilizzare licenze di servizi multimediali di Azure toodeliver DRM o chiavi AES</span><span class="sxs-lookup"><span data-stu-id="020b7-103">Use Azure Media Services toodeliver DRM licenses or AES keys</span></span>
<span data-ttu-id="020b7-104">Azure Media Services (AMS) consente tooingest, codificare, aggiungere la protezione del contenuto e lo streaming del contenuto (vedere [questo](media-services-protect-with-drm.md) articolo per informazioni dettagliate).</span><span class="sxs-lookup"><span data-stu-id="020b7-104">Azure Media Services (AMS) enables you tooingest, encode, add content protection, and stream your content (see [this](media-services-protect-with-drm.md) article for details).</span></span> <span data-ttu-id="020b7-105">Esistono, tuttavia, i clienti che hanno solo licenze toodeliver AMS di toouse e/o le chiavi ed eseguire la codifica, crittografia e streaming mediante i server locali.</span><span class="sxs-lookup"><span data-stu-id="020b7-105">However, there are customers who only want toouse AMS toodeliver licenses and/or keys and do encoding, encrypting and streaming using their on-premises servers.</span></span> <span data-ttu-id="020b7-106">Questo articolo descrive come utilizzare AMS toodeliver PlayReady e/o licenze Widevine ma hello rest con i server locali.</span><span class="sxs-lookup"><span data-stu-id="020b7-106">This article describes how you can use AMS toodeliver PlayReady and/or Widevine licenses but do hello rest with your on-premises servers.</span></span> 

## <a name="overview"></a><span data-ttu-id="020b7-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="020b7-107">Overview</span></span>
<span data-ttu-id="020b7-108">Servizi multimediali rende disponibili servizi per la distribuzione di licenze DRM PlayReady e Widevine e chiavi AES-128.</span><span class="sxs-lookup"><span data-stu-id="020b7-108">Media Services provides a service for delivering PlayReady and Widevine DRM licenses and AES-128 keys.</span></span> <span data-ttu-id="020b7-109">Servizi multimediali fornisce inoltre API che consentono di configurare i diritti di hello e le limitazioni desiderati per hello DRM runtime tooenforce quando un utente riproduce un contenuto protetto con DRM hello.</span><span class="sxs-lookup"><span data-stu-id="020b7-109">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello DRM runtime tooenforce when a user plays back hello DRM protected content.</span></span> <span data-ttu-id="020b7-110">Quando un hello richieste utente contenuto protetto, un'applicazione hello player richiede una licenza dal servizio di licenza hello AMS.</span><span class="sxs-lookup"><span data-stu-id="020b7-110">When a user requests hello protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="020b7-111">Servizio licenze Hello AMS emetterà player toohello di hello licenza (se autorizzato).</span><span class="sxs-lookup"><span data-stu-id="020b7-111">hello AMS license service will issue hello license toohello player (if it is authorized).</span></span> <span data-ttu-id="020b7-112">le licenze PlayReady e Widevine Hello contengono la chiave di decrittografia hello che può essere utilizzata da hello client player toodecrypt e flusso hello contenuto.</span><span class="sxs-lookup"><span data-stu-id="020b7-112">hello PlayReady and Widevine licenses contain hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="020b7-113">Servizi multimediali supporta più modalità di autenticazione degli utenti che richiedono licenze o chiavi.</span><span class="sxs-lookup"><span data-stu-id="020b7-113">Media Services supports multiple ways of authorizing users who make license or key requests.</span></span> <span data-ttu-id="020b7-114">Configurare i criteri di autorizzazione della chiave simmetrica hello e criteri hello potrebbe avere una o più restrizioni: apertura o la limitazione del token.</span><span class="sxs-lookup"><span data-stu-id="020b7-114">You configure hello content key's authorization policy and hello policy could have one or more restrictions: open or token restriction.</span></span> <span data-ttu-id="020b7-115">criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="020b7-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="020b7-116">Servizi multimediali supporta i token in formato JSON Web Token (JWT) e i token SWT (Simple Web token) hello.</span><span class="sxs-lookup"><span data-stu-id="020b7-116">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span>

<span data-ttu-id="020b7-117">Hello diagramma seguente illustra i passaggi principali hello è necessario tootake toouse AMS toodeliver PlayReady e/o licenze Widevine ma hello rest con i server locali.</span><span class="sxs-lookup"><span data-stu-id="020b7-117">hello following diagram shows hello main steps you need tootake toouse AMS toodeliver PlayReady and/or Widevine licenses but do hello rest with your on-premises servers.</span></span>

![Protezione con PlayReady](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a><span data-ttu-id="020b7-119">Scaricare un esempio</span><span class="sxs-lookup"><span data-stu-id="020b7-119">Download sample</span></span>
<span data-ttu-id="020b7-120">È possibile scaricare l'esempio hello descritto in questo articolo da [qui](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span><span class="sxs-lookup"><span data-stu-id="020b7-120">You can download hello sample described in this article from [here](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="020b7-121">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="020b7-121">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="020b7-122">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="020b7-122">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="020b7-123">Aggiungere i seguenti elementi troppo hello**appSettings** definiti nel file app. config:</span><span class="sxs-lookup"><span data-stu-id="020b7-123">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

    <span data-ttu-id="020b7-124"><add key="Issuer" value="http://testacs.com"/><add key="Audience" value="urn:test"/></span><span class="sxs-lookup"><span data-stu-id="020b7-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span></span>

## <a name="net-code-example"></a><span data-ttu-id="020b7-125">Esempio di codice .NET</span><span class="sxs-lookup"><span data-stu-id="020b7-125">.NET code example</span></span>

<span data-ttu-id="020b7-126">Hello esempio di codice seguente viene illustrato come un comune toocreate chiave simmetrica e ottenere l'URL di acquisizione di licenze PlayReady o Widevine.</span><span class="sxs-lookup"><span data-stu-id="020b7-126">hello following code example shows how toocreate a common content key and get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="020b7-127">È necessario tooget hello in seguito le informazioni dal sistema AMS e configurare il server locale: **chiave simmetrica**, **id chiave**, **URL di acquisizione della licenza**.</span><span class="sxs-lookup"><span data-stu-id="020b7-127">You need tooget hello following pieces of information from AMS and configure your on-premises server: **content key**, **key id**, **license acquisition URL**.</span></span> <span data-ttu-id="020b7-128">Dopo aver configurato il server locale, è possibile effettuare lo streaming dal server locale destinato a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="020b7-128">Once you configure your on-premises server, you could stream from your own streaming server.</span></span> <span data-ttu-id="020b7-129">Dal server licenze punti tooAMS flusso crittografato hello lettore richiederà una licenza dal sistema AMS.</span><span class="sxs-lookup"><span data-stu-id="020b7-129">Since hello encrypted stream points tooAMS license server, your player will request a license from AMS.</span></span> <span data-ttu-id="020b7-130">Se si sceglie l'autenticazione del token, server licenze hello AMS convaliderà token hello che è stata inviata tramite HTTPS e (se valido) garantirà player tooyour indietro di hello licenza.</span><span class="sxs-lookup"><span data-stu-id="020b7-130">If you choose token authentication, hello AMS license server will validate hello token you sent through HTTPS and (if valid) will deliver hello license back tooyour player.</span></span> <span data-ttu-id="020b7-131">(esempio di codice hello illustra solo come toocreate un comune chiave simmetrica e ottenere l'URL di acquisizione di licenze PlayReady o Widevine.</span><span class="sxs-lookup"><span data-stu-id="020b7-131">(hello code example only shows how toocreate a common content key and  get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="020b7-132">Se si desidera chiavi toodelivery AES-128, è necessario toocreate una chiave simmetrica envelope e ottenere un URL di acquisizione chiave e [questo](media-services-protect-with-aes128.md) articolo viene illustrato come toodo,).</span><span class="sxs-lookup"><span data-stu-id="020b7-132">If you want toodelivery AES-128 keys, you need toocreate an envelope content key and get a key acquisition URL and [this](media-services-protect-with-aes128.md) article shows how toodo it).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DeliverDRMLicenses
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static readonly Uri _sampleIssuer =
                new Uri(ConfigurationManager.AppSettings["Issuer"]);
            private static readonly Uri _sampleAudience =
                new Uri(ConfigurationManager.AppSettings["Audience"]);

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                bool tokenRestriction = true;
                string tokenTemplateString = null;


                IContentKey key = CreateCommonTypeContentKey();

                // Print out hello key ID and Key in base64 string format
                Console.WriteLine("Created key {0} with key value {1} ",
                    key.Id, System.Convert.ToBase64String(key.GetClearKeyValue()));

                Console.WriteLine("PlayReady License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));

                Console.WriteLine("Widevine License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine));

                if (tokenRestriction)
                    tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
                else
                    AddOpenAuthorizationPolicy(key);

                Console.WriteLine("Added authorization policy: {0}",
                    key.AuthorizationPolicyId);
                Console.WriteLine();
                Console.ReadLine();
            }

            static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
            {

                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Open",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                            Requirements = null
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.Widevine,
                        restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
            {
                string tokenTemplateString = GenerateTokenRequirements();

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Token Authorization Policy",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                            Requirements = tokenTemplateString,
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.Widevine,
                            restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with token restrictions").
                            Result;

                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

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

                //hello PlayReadyLicenseResponseTemplate class represents hello template 
                //for hello response sent back toohello end user. 
                //It contains a field for a custom data string between hello license server 
                //and hello application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // hello PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // toobe returned toohello end users. 
                // It contains hello data on hello content key in hello license 
                // and any rights or restrictions toobe 
                // enforced by hello PlayReady DRM runtime when using hello content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether hello license is persistent 
                // (saved in persistent storage on hello client) 
                // or non-persistent (only held in memory while hello player is using hello license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use hello license or not.  
                // If true, hello MinimumSecurityLevel property of hello license
                // is set too150.  If false (hello default), 
                // hello MinimumSecurityLevel property of hello license is set too2000.
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

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect hello consumer experience. 
                // If hello output protections are configured too restrictive, 
                // hello content might be unplayable on some clients. 
                // For more information, see hello PlayReady Compliance Rules document.

                // For example:
                //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }


            private static string ConfigureWidevineLicenseTemplate()
            {
                var template = new WidevineMessage
                {
                    allowed_track_types = AllowedTrackTypes.SD_HD,
                    content_key_specs = new[]
                    {
                            new ContentKeySpecs
                            {
                                required_output_protection =
                                    new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                                security_level = 1,
                                track_type = "SD"
                            }
                        },
                    policy_overrides = new
                    {
                        can_play = true,
                        can_persist = true,
                        can_renew = false
                    }
                };

                string configuration = JsonConvert.SerializeObject(template);
                return configuration;
            }


            static public IContentKey CreateCommonTypeContentKey()
            {
                // Create envelope encryption content key
                Guid keyId = Guid.NewGuid();
                byte[] contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="020b7-133">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="020b7-133">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="020b7-134">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="020b7-134">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="020b7-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="020b7-135">See also</span></span>
[<span data-ttu-id="020b7-136">Uso della crittografia comune dinamica PlayReady e/o Widevine</span><span class="sxs-lookup"><span data-stu-id="020b7-136">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="020b7-137">Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi</span><span class="sxs-lookup"><span data-stu-id="020b7-137">Using AES-128 Dynamic Encryption and Key Delivery Service</span></span>](media-services-protect-with-aes128.md)

[<span data-ttu-id="020b7-138">Con i partner toodeliver Widevine licenze tooAzure servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="020b7-138">Using partners toodeliver Widevine licenses tooAzure Media Services</span></span>](media-services-licenses-partner-integration.md)

