---
title: aaaUsing PlayReady e/o Widevine comune crittografia dinamica | Documenti Microsoft
description: Servizi multimediali di Microsoft Azure consente di toodeliver MPEG-DASH, Smooth Streaming e Http-Live-Streaming (HLS) flussi protetti con Microsoft PlayReady DRM. Consente inoltre toodelivery DASH crittografati con DRM Widevine. Questo argomento viene illustrato come crittografare i toodynamically e Widevine DRM PlayReady.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>Uso della crittografia comune dinamica PlayReady e/o Widevine

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Servizi multimediali di Microsoft Azure consente toodeliver MPEG-DASH, Smooth Streaming e i flussi HTTP-Live-Streaming (HLS) protetti con [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). Consente inoltre flussi DASH toodeliver crittografati con licenze Widevine DRM. PlayReady sia Widevine vengono crittografati in base hello specifica la crittografia comune (ISO/IEC 23001-7 CENC). È possibile utilizzare [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (a partire dalla versione di hello 3.5.1) o REST API tooconfigure il toouse AssetDeliveryConfiguration Widevine.

Servizi multimediali rende disponibili servizi per la distribuzione di licenze DRM Widevine e PlayReady. Servizi multimediali fornisce inoltre API che consentono di configurare i diritti di hello e le limitazioni desiderati per hello PlayReady o DRM Widevine al tooenforce di runtime quando un utente riproduce un contenuto protetto. Quando un utente richiede un contenuto protetto con DRM, un'applicazione hello lettore richiederà una licenza dal servizio licenze hello AMS. il servizio licenze AMS Hello emetterà un lettore toohello licenza se è stato autorizzato. Una licenza PlayReady o Widevine contiene la chiave di decrittografia hello che può essere utilizzata da hello client player toodecrypt e flusso hello contenuto.

È inoltre possibile utilizzare hello seguente toohelp partner AMS di consegnare licenze Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Per altre informazioni, vedere gli articoli relativi all'integrazione con [Axinom](media-services-axinom-integration.md) e [castLabs](media-services-castlabs-integration.md).

Servizi multimediali supporta più modalità di autenticazione degli utenti che richiedono le chiavi. Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: apertura o la limitazione del token. criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza). Servizi multimediali supporta i token in hello [token Web semplici](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) e [Token Web JSON](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT). Per ulteriori informazioni, vedere criteri di autorizzazione Configura hello della chiave simmetrica.

Il vantaggio di tootake di crittografia dinamica, è necessario toohave un asset che contiene un set di file MP4 a più velocità in bit o file di origine Smooth Streaming con più velocità in bit. È necessario anche i criteri di distribuzione hello tooconfigure per asset hello (descritta più avanti in questo argomento). Quindi, basato sul formato di hello specificato nell'URL di streaming hello, il server di Streaming On Demand hello garantisce che tale flusso hello venga distribuito nel protocollo hello scelto. Di conseguenza, è necessario solo toostore e pagare per i file hello in un unico formato di archiviazione e servizi multimediali creerà e fornirà una risposta HTTP appropriato hello in base a ogni richiesta da un client.

In questo argomento sarebbe utile toodevelopers di applicazioni che offrono supporto protetto da più DRMs, ad esempio PlayReady e Widevine. Hello argomento viene illustrato come tooconfigure hello servizio di distribuzione di licenze PlayReady con criteri di autorizzazione in modo che solo i client autorizzati potrebbero ricevere licenze PlayReady o Widevine. Viene inoltre illustrato come toouse la crittografia di crittografia dinamica con PlayReady o DRM Widevine su trattino.

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 

## <a name="download-sample"></a>Scaricare un esempio
È possibile scaricare l'esempio hello descritto in questo articolo da [qui](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>Configurazione della crittografia comune dinamica e dei servizi di distribuzione delle licenze DRM

di seguito Hello sono passaggi generali che è necessario tooperform per proteggere gli asset con PlayReady, usando hello licenza recapito servizi multimediali e anche la crittografia dinamica.

1. Creare un asset e caricare i file nell'asset hello.
2. Codificare hello asset contenente hello file toohello velocità in bit adattiva che set MP4.
3. Creare una chiave simmetrica e associarlo all'asset codificato hello. In servizi multimediali, la chiave simmetrica hello contiene la chiave di crittografia dell'asset hello.
4. Configurare criteri di autorizzazione della chiave simmetrica hello. criteri di autorizzazione chiave del contenuto Hello devono essere configurato dall'utente e soddisfatti dal client hello affinché hello contenuto toobe chiave toohello recapitato client.

    Quando si creano criteri di autorizzazione chiave del contenuto di hello, è necessario seguente hello toospecify: metodo (PlayReady o Widevine), le restrizioni di recapito (aperte o token) e tipo di distribuzione delle chiavi specifico toohello informazioni che definisce la modalità di recapito chiave hello client toohello ([PlayReady](media-services-playready-license-template-overview.md) o [Widevine](media-services-widevine-license-template-overview.md) modello di licenza).

5. Configurare i criteri di distribuzione hello per un asset. configurazione dei criteri recapito Hello include: hello di protocollo di recapito (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), tipo di crittografia dinamica (ad esempio, la crittografia comune), PlayReady o Widevine URL di acquisizione della licenza.

    È possibile applicare protocollo tooeach criteri diversi in hello stesso asset. Ad esempio, è possibile applicare PlayReady crittografia tooSmooth/DASH e tooHLS Envelope AES. Tutti i protocolli che non sono definiti in un criterio di recapito (ad esempio, aggiungere un singolo criterio che specifica solo HLS come protocollo di hello) verrà impedito lo streaming. toothis eccezione Hello è se non sono presenti criteri di recapito di asset definito in alcun modo. Quindi, saranno possibile tutti i protocolli in crittografato hello.

6. Creare un localizzatore OnDemand in ordine tooget un URL di streaming.

Si noterà un esempio completo di .NET alla fine di hello di hello argomento.

Hello seguente immagine illustra del flusso di lavoro hello descritto in precedenza. Token hello qui viene utilizzato per l'autenticazione.

![Protezione con PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

rest Hello di questo argomento fornisce spiegazioni dettagliate, esempi di codice e collegamenti tootopics che mostrano come tooachieve hello attività descritte in precedenza.

## <a name="current-limitations"></a>Limitazioni correnti
Se si aggiunge o aggiorna un criterio di recapito di asset, è necessario eliminare il localizzatore hello associato (se presente) e crearne uno nuovo.

Limitazione per la crittografia tramite Widevine con Servizi multimediali di Azure: attualmente non sono supportate più chiavi simmetriche.

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>Creare un asset e caricare i file nell'asset hello
In ordine toomanage, codificare e trasmettere in flusso i video, è innanzitutto necessario caricare il contenuto in servizi multimediali di Microsoft Azure. Una volta caricato, il contenuto è archiviato in modo sicuro nel cloud hello per un'ulteriore elaborazione e il flusso.

Per informazioni dettagliate, vedere [Carica file in un account di servizi multimediali](media-services-dotnet-upload-files.md).

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>Codificare hello asset contenente hello file toohello velocità in bit adattiva che set MP4
Con la crittografia dinamica è sufficiente toocreate un asset che contiene un set di file MP4 a più velocità in bit o file di origine Smooth Streaming con più velocità in bit. Quindi, base hello formato specificato nel manifesto hello e frammentazione richiesta, hello server ti garantisce che il flusso di hello nel protocollo hello che si è scelto di Streaming On Demand. Di conseguenza, è necessario solo toostore e pagare per i file hello in unico formato di archiviazione e servizi multimediali creerà e fornirà hello risposta appropriata in base alle richieste da un client. Per ulteriori informazioni, vedere hello [Panoramica della creazione di pacchetti dinamica](media-services-dynamic-packaging-overview.md) argomento.

Per istruzioni su come tooencode, vedere [come tooencode un asset con Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Creare una chiave simmetrica e associarlo all'asset codificato hello
In servizi multimediali, la chiave simmetrica hello contiene chiave hello che si desidera tooencrypt un asset con.

Per informazioni dettagliate, vedere [Creare una chiave simmetrica](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Configurare i criteri di autorizzazione della chiave simmetrica hello
Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi. criteri di autorizzazione chiave del contenuto Hello devono essere configurato dall'utente e soddisfatti dal client hello (lettore) affinché toobe chiave di hello recapitati toohello client. Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: apertura o la limitazione del token.

Per informazioni dettagliate, vedere l'argomento [Configurare i criteri di autorizzazione della chiave simmetrica](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).

## <a id="configure_asset_delivery_policy"></a>Configurare i criteri di distribuzione dell'asset
Configurare i criteri di distribuzione hello dell'asset. Le operazioni che hello configurazione dei criteri di recapito di asset include:

* URL di acquisizione licenza DRM Hello.
* Hello asset protocollo di recapito (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti).
* tipo di Hello di crittografia dinamica (in questo caso, la crittografia comune).

Per informazioni dettagliate, vedere [Configurare i criteri di distribuzione degli asset ](media-services-rest-configure-asset-delivery-policy.md).

## <a id="create_locator"></a>Creare un OnDemand streaming locator in ordine tooget un URL di streaming
Sarà necessario tooprovide l'utente con hello streaming URL per Smooth, DASH o HLS.

> [!NOTE]
> Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.
>
>

Per istruzioni su come toopublish un asset e compilare un URL di streaming, vedere [compilare un URL di streaming](media-services-deliver-streaming-content.md).

## <a name="get-a-test-token"></a>Ottenere un token di test
Ottenere un token di test in base a una restrizione token hello che è stata utilizzata per i criteri di autorizzazione chiave hello.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


È possibile utilizzare hello [Player AMS](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest il flusso.

## <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

1. Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 
2. Aggiungere i seguenti elementi troppo hello**appSettings** definiti nel file app. config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Esempio

Hello esempio riportato di seguito la funzionalità che è stata introdotta in Azure Media Services SDK per .net-versione 3.5.2 (in particolare, hello possibilità toodefine un Widevine modello di licenza e richiedere una licenza Widevine da servizi multimediali di Azure).

Sovrascrivere il codice hello nel file Program.cs con il codice di hello illustrato in questa sezione.

>[!NOTE]
>È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy). È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri). Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.

Rendere le variabili tooupdate che toopoint toofolders in cui si trovano i file di input.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
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

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
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


## <a name="next-step"></a>Passaggio successivo
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[CENC con Multi-DRM e controllo di accesso](media-services-cenc-with-multidrm-access-control.md)

[Configurare i pacchetti Widevine con AMS](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[Annuncio dei servizi di distribuzione delle licenze Google Widevine in Servizi multimediali di Azure](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
