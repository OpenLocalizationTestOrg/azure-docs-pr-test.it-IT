---
title: aaaProtect del contenuto HLS con Microsoft PlayReady o Apple FairPlay - Azure | Documenti Microsoft
description: Questo argomento viene fornita una panoramica e illustra come crittografare i contenuti FairPlay Apple HTTP Live Streaming (HLS) toouse toodynamically di servizi multimediali di Azure. Viene inoltre illustrato come toouse hello servizi multimediali di licenza del servizio di recapito toodeliver tooclients licenze FairPlay.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Proteggere il contenuto HLS con Apple FairPlay o Microsoft PlayReady
Azure consente di servizi multimediali è toodynamically crittografare il contenuto HTTP Live Streaming (HLS) tramite hello seguenti formati:  

* **Chiave envelope non crittografata AES-128**

    Hello intero blocco verrà crittografato tramite hello **CBC AES-128** modalità. decrittografia di Hello del flusso di hello è supportata da iOS e Windows Media player OS X in modo nativo. Per altre informazioni, vedere [Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi](media-services-protect-with-aes128.md).
* **Apple FairPlay**

    Hello singolo video e audio esempi vengono crittografati tramite hello **CBC AES-128** modalità. **Streaming FairPlay** (FPS) è integrato nei sistemi operativi per dispositivi hello, con il supporto nativo in iOS e Apple TV. Safari su OS X consente FPS usando il supporto di interfaccia di hello crittografati supporti le estensioni (EME).
* **Microsoft PlayReady**

Hello immagine seguente viene illustrato hello **HLS + FairPlay o PlayReady crittografia dinamica** flusso di lavoro.

![Diagramma del flusso di lavoro della crittografia dinamica](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

In questo argomento viene illustrato come crittografare il contenuto HLS con Apple FairPlay i toouse toodynamically di servizi multimediali. Viene inoltre illustrato come toouse hello servizi multimediali di licenza del servizio di recapito toodeliver tooclients licenze FairPlay.

> [!NOTE]
> Se si desidera tooencrypt il contenuto HLS contenuto con PlayReady, è necessario toocreate una chiave simmetrica comune e associarlo all'asset. È inoltre necessario criteri di autorizzazione tooconfigure hello della chiave simmetrica, come descritto in [PlayReady usando la crittografia dinamica comune](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Problemi e considerazioni

di seguito Hello sono necessarie quando si usa servizi multimediali toodeliver che HLS crittografato con FairPlay e licenze FairPlay toodeliver:

  * Un account Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di prova gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
  * Account di Servizi multimediali. toocreate uno, vedere [creare un account di servizi multimediali di Azure tramite il portale di Azure hello](media-services-portal-create-account.md).
  * Eseguire l'iscrizione all' [Apple Development Program](https://developer.apple.com/).
  * Apple richiede hello tooobtain proprietario del contenuto di hello [pacchetto di distribuzione](https://developer.apple.com/contact/fps/). Stato che già stata implementata chiave protezione modulo (KSM) con servizi multimediali e che si sta richiedendo pacchetto FPS finale hello. Sono disponibili istruzioni hello FPS finale pacchetto certificazione toogenerate e ottenere hello chiave segreto applicazione (ricerca). Consente di chiedere tooconfigure FairPlay.
  * Azure Media Services .NET SDK versione **3.6.0** o successiva.

sul lato di distribuzione delle chiavi di servizi multimediali, è necessario impostare Hello seguenti operazioni:

  * **App del certificato (CA)**: si tratta di un file con estensione pfx che contiene la chiave privata di hello. Creare il file e crittografarlo con una password.

       Quando si configura un criterio di distribuzione delle chiavi, è necessario fornire il file con estensione pfx hello e password in formato base 64.

      Hello alla procedura seguente viene descritto come file di toogenerate un certificato PFX per FairPlay:

    1. Installare OpenSSL da https://slproweb.com/products/Win32OpenSSL.html.

        Passare toohello cartella in cui il certificato di FairPlay hello e altri file recapitati da Apple.
    2. Eseguire hello comando seguente dalla riga di comando hello. Consente di convertire il file con estensione PEM tooa di hello. cer file.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem
    3. Eseguire hello comando seguente dalla riga di comando hello. Consente di convertire file con estensione pfx tooa file con estensione PEM hello con la chiave privata di hello. password Hello per file con estensione pfx hello viene quindi richiesto da OpenSSL.

        "C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt
  * **La password del certificato app**: password hello per la creazione di file con estensione pfx hello.
  * **ID della password di App Cert**: È necessario caricare password hello, toohow simile caricamento altre chiavi di servizi multimediali. Hello utilizzare **ContentKeyType.FairPlayPfxPassword** hello tooget valore di enumerazione ID servizi multimediali Questo è ciò che richiedono toouse all'interno di opzione del criterio hello distribuzione delle chiavi.
  * **iv**: valore casuale di 16 byte Deve corrispondere hello iv in Criteri di distribuzione di asset hello. Generare hello iv e inserirlo in entrambe le posizioni: criteri di distribuzione di asset hello e l'opzione criteri di distribuzione delle chiavi hello.
  * **CHIEDERE**: questa chiave viene ricevuta quando si genera certificazione hello tramite hello Apple Developer portal. Ogni team di sviluppo riceve una chiave ASK univoca. Salvare una copia di hello chiedere e archiviarlo in un luogo sicuro. È necessario chiedere tooconfigure come FairPlayAsk tooMedia servizi in un secondo momento.
  * **ID ASK**: ID ottenuto quando si carica la chiave privata dell'applicazione in Servizi multimediali. È necessario caricare chiedere utilizzando hello **ContentKeyType.FairPlayAsk** valore enum. Di conseguenza hello, viene restituito l'ID di servizi multimediali hello e questo è ciò che deve essere utilizzato quando l'impostazione di opzione di criteri di distribuzione delle chiavi hello.

Hello operazioni indicate di seguito devono essere impostate dal lato client FPS hello:

  * **App del certificato (CA)**: si tratta di un file.cer/.der contenente hello chiave pubblica, il sistema operativo hello utilizza tooencrypt alcuni payload. Servizi multimediali deve tooknow su di esso perché è richiesto da Windows Media player hello. il servizio di distribuzione delle chiavi Hello decrittografa usando la chiave privata corrispondente di hello.

tooplay un flusso crittografato FairPlay, ottenere una reale chiedere prima e quindi generare un certificato reale. Questo processo crea tutte le 3 parti:

  * file con estensione der
  * file con estensione pfx
  * password per PFX hello

i seguenti client Hello supporta contenuto HLS con **CBC AES-128** crittografia: Safari su OS X, Apple TV, iOS.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>Configurare la crittografia dinamica FairPlay e i servizi di distribuzione delle licenze
di seguito Hello sono passaggi generali per proteggere gli asset con FairPlay utilizzando hello licenza recapito servizi multimediali e usando la crittografia dinamica.

1. Creare un asset e caricare i file nell'asset hello.
2. Codificare asset hello contenente hello file toohello velocità in bit adattiva che set MP4.
3. Creare una chiave simmetrica e associarlo all'asset codificato hello.  
4. Configurare criteri di autorizzazione della chiave simmetrica hello. Specificare hello seguenti:

   * metodo di recapito Hello (in questo caso, FairPlay).
   * configurazione delle opzioni dei criteri FairPlay. Per informazioni dettagliate su come tooconfigure FairPlay, vedere hello **ConfigureFairPlayPolicyOptions()** metodo esempio hello riportato di seguito.

     > [!NOTE]
     > In genere, è opportuno tooconfigure FairPlay criteri opzioni una sola volta, poiché è solo un set di un certificato e una ricerca.
     >
     >
   * Restrizioni aperte o token.
   * Tipo distribuzione delle chiavi specifico toohello informazioni che definisce come chiave hello viene recapitato toohello client.
5. Configurare i criteri di distribuzione di asset hello. configurazione dei criteri di recapito Hello include:

   * protocollo di recapito Hello (HLS).
   * tipo di Hello di crittografia dinamica (crittografia CBC comune).
   * URL di acquisizione della licenza Hello.

     > [!NOTE]
     > Se si desidera toodeliver un flusso che viene crittografato con FairPlay e un altro sistema di Digital Rights Management (DRM), si dispone di criteri di recapito di tooconfigure:
     >
     > * Un tooconfigure IAssetDeliveryPolicy lo Streaming adattivo dinamica su HTTP (trattino) con CENC (Common Encryption) (PlayReady + Widevine) e Smooth Streaming con PlayReady
     > * Un altro IAssetDeliveryPolicy tooconfigure FairPlay per HLS
     >
     >
6. Creare un tooget localizzatore OnDemand un URL di streaming.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>Usare la distribuzione delle chiavi FairPlay con applicazioni lettore
È possibile sviluppare applicazioni di Windows Media player utilizzando hello iOS SDK. toobe tooplay in grado di FairPlay contenuto, è necessario protocollo di scambio tooimplement hello licenza. Questo protocollo non è specificato da Apple. È la distribuzione delle chiavi toosend richiede backup tooeach app. Hello del servizio di distribuzione delle chiavi di Media Services FairPlay hello SPC toocome previsto è un messaggio post codificati www-form-url hello seguente formato:

    spc=<Base64 encoded SPC>

> [!NOTE]
> Azure Media Player non supporta la riproduzione di FairPlay predefinito hello. riproduzione di FairPlay tooget su MAC OS X, ottenere il lettore di esempio hello da hello account per sviluppatori di Apple.
>
>

## <a name="streaming-urls"></a>URL di streaming
Se l'asset è stata crittografata con più DRM, è necessario utilizzare un tag di crittografia nell'URL di streaming hello: (formato = 'm3u8-aapl', crittografia = 'xxx').

si applica Hello seguenti considerazioni:

* Può essere specificato solo un tipo di crittografia oppure nessuno.
* tipo di crittografia Hello privo di toobe specificata nell'URL di hello se solo uno di crittografia è stata applicata toohello asset.
* tipo di crittografia Hello viene fatta distinzione tra maiuscole e minuscole.
* è possibile specificare i seguenti tipi di crittografia Hello:  
  * **cenc**: crittografia comune (PlayReady o Widevine)
  * **cbcs-aapl**: FairPlay
  * **cbc**: crittografia busta AES

## <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

1. Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 
2. Aggiungere i seguenti elementi troppo hello**appSettings** definiti nel file app. config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Esempio

Hello seguente esempio viene illustrato hello possibilità toouse toodeliver di servizi multimediali del contenuto crittografato con FairPlay. Questa funzionalità è stata introdotta in hello Azure Media Services SDK per .NET versione 3.6.0. 

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
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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


## <a name="next-steps-media-services-learning-paths"></a>Passaggi successivi: Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
