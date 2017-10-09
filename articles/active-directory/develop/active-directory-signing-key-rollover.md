---
title: Rollover della chiave di Azure AD aaaSigning | Documenti Microsoft
description: Questo articolo illustra hello consigliate rollover della chiave di firma per Azure Active Directory
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Rollover della chiave di firma in Azure Active Directory
In questo argomento viene illustrato cosa occorre tooknow sulle chiavi pubbliche hello utilizzati nei token di sicurezza di Azure Active Directory (Azure AD) toosign. È importante toonote che questi rollover delle chiavi su base periodica e, in caso di emergenza, potrebbe essere eseguito il rollover immediatamente. Tutte le applicazioni che usano Azure AD devono essere in grado di tooprogrammatically handle hello rollover della chiave processo o stabilire un processo di rollover manuale periodico. Continuare la lettura toounderstand il funzionamento delle chiavi di hello, come tooassess hello impatto di un'applicazione hello rollover tooyour e come tooupdate l'applicazione o stabilire un rollover della chiave toohandle processo periodico di attivazione manuale, se necessario.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Informazioni generali sulle chiavi di firma in Azure AD
Azure AD Usa la crittografia a chiave pubblica basata su trust tooestablish standard di settore tra l'elemento e hello applicazioni che lo utilizzano. In pratica, questo procedimento funziona nel seguente modo hello: Azure AD Usa una chiave di firma costituita da una coppia di chiavi pubblica e privata. Quando un utente accede tooan applicazione che usa Azure AD per l'autenticazione, Azure AD crea un token di sicurezza che contiene informazioni sull'utente hello. Questo token viene firmato da Azure AD usando la relativa chiave privata prima di inviarlo applicazione toohello indietro. tooverify che hello token sia valido e provenga effettivamente da Azure AD, l'applicazione hello deve convalidare firma del token hello con la chiave pubblica di hello esposta da Azure Active Directory nel tenant di hello [documento di individuazione OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) o SAML/WS-Fed [documento metadati federazione](active-directory-federation-metadata.md).

Per motivi di sicurezza, esegue il rollback chiave su base periodica e, nel caso di hello di un'emergenza, di firma di Azure AD può essere eseguito il rollover immediatamente. Qualsiasi applicazione che si integra con Azure AD deve essere preparata toohandle un evento di rollover della chiave non è rilevante la frequenza con cui può verificarsi. Ciò non accade, se l'applicazione tenta di toouse una firma di hello scaduti tooverify chiave su un token, richiesta di accesso hello avrà esito negativo.

Non esiste più di una chiave valida è sempre disponibile nel documento di individuazione OpenID Connect hello e documento di metadati di federazione hello. L'applicazione deve essere preparata toouse qualsiasi chiave hello specificato nel documento hello, poiché una chiave può essere implementata a breve, un altro può essere relativa sostituzione e così via.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>Come tooassess se l'applicazione sarà interessata e quale toodo su di esso
Il modo in cui l'applicazione gestisce il rollover della chiave dipende da variabili quali il tipo di hello di applicazione o il protocollo di identità e la libreria è stata utilizzata. Hello nelle sezioni seguenti vengono valutare se i tipi più comuni di hello delle applicazioni sono interessati da rollover della chiave hello e forniscono indicazioni su come tooupdate il rollover automatico toosupport applicazione hello o aggiornare manualmente la chiave di hello.

* [Applicazioni client native che accedono alle risorse](#nativeclient)
* [API / applicazioni Web che accedono alle risorse](#webclient)
* [API / applicazioni Web che proteggono le risorse e sono state compilate con i servizi app di Azure](#appservices)
* [API / applicazioni Web che proteggono le risorse usando middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication](#owin)
* [API / applicazioni Web che proteggono le risorse usando middleware .NET Core OpenID Connect o JwtBearerAuthentication](#owincore)
* [API / applicazioni Web che proteggono le risorse usando il modulo Node.js passport-azure-ad](#passport)
* [API/applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2015 o Visual Studio 2017](#vs2015)
* [Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2013](#vs2013)
* [API Web che proteggono le risorse e sono state create con Visual Studio 2013](#vs2013_webapi)
* [Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2012](#vs2012)
* [Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2010 o 2008 o con Windows Identity Foundation](#vs2010)
* [Applicazioni Web / API di protezione delle risorse utilizzando qualsiasi altre librerie o implementare manualmente uno di hello protocolli supportati](#other)

Queste indicazioni **non** sono valide per:

* Applicazioni aggiunte dalla raccolta di applicazioni AD Azure (incluso personalizzato) hanno apposite istruzioni con relativamente toosigning chiavi. [Altre informazioni.](../active-directory-sso-certs.md)
* Locale non dispone di applicazioni pubblicate tramite proxy applicazione tooworry sulle chiavi di firma.

### <a name="nativeclient"></a>Applicazioni client native che accedono alle risorse
Le applicazioni che si limitano ad accedere alle risorse, come Microsoft Graph, KeyVault, API di Outlook e altre APIs Microsoft) in genere solo ottenere un token e passarlo lungo toohello proprietario della risorsa. Dato che non sono per proteggere le risorse, non controllano il token hello e pertanto non è necessario tooensure che è firmato correttamente.

Le applicazioni client native, se i computer desktop o portatile, in questa categoria rientrano e sono pertanto non è interessate da rollover hello.

### <a name="webclient"></a>API / applicazioni Web che accedono alle risorse
Le applicazioni che si limitano ad accedere alle risorse, come Microsoft Graph, KeyVault, API di Outlook e altre APIs Microsoft) in genere solo ottenere un token e passarlo lungo toohello proprietario della risorsa. Dato che non sono per proteggere le risorse, non controllano il token hello e pertanto non è necessario tooensure che è firmato correttamente.

Le applicazioni Web e le API web che utilizzano il flusso solo app hello (credenziali client / certificato client), in questa categoria rientrano e sono pertanto non è interessato da rollover hello.

### <a name="appservices"></a>API / applicazioni Web che proteggono le risorse e sono state compilate con i servizi app di Azure
L'autenticazione di Azure i servizi App / funzionalità di autorizzazione (EasyAuth) dispone già di rollover della chiave toohandle logica necessaria hello automaticamente.

### <a name="owin"></a>API / applicazioni Web che proteggono le risorse usando middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication
Se l'applicazione utilizza hello .NET OWIN OpenID Connect, WS-Fed o middleware WindowsAzureActiveDirectoryBearerAuthentication, contiene già il rollover della chiave toohandle logica necessaria hello automaticamente.

È possibile verificare che l'applicazione utilizza uno di questi mediante la ricerca di uno qualsiasi dei seguenti frammenti di codice in Startup.cs o Startup.Auth.cs dell'applicazione hello

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>API / applicazioni Web che proteggono le risorse usando middleware .NET Core OpenID Connect o JwtBearerAuthentication
Se l'applicazione utilizza hello .NET Core OWIN OpenID Connect o middleware JwtBearerAuthentication, contiene già il rollover della chiave toohandle logica necessaria hello automaticamente.

È possibile verificare che l'applicazione utilizza uno di questi mediante la ricerca di uno qualsiasi dei seguenti frammenti di codice in Startup.cs o Startup.Auth.cs dell'applicazione hello

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>API / applicazioni Web che proteggono le risorse usando il modulo Node.js passport-azure-ad
Se l'applicazione utilizza hello Node.js passport ad modulo, contiene già il rollover della chiave toohandle logica necessaria hello automaticamente.

È possibile verificare che l'applicazione Active Directory a passport cercando hello seguente frammento di in app.js dell'applicazione

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>API/applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2015 o Visual Studio 2017
Se l'applicazione è stato creato utilizzando un modello di applicazione web in Visual Studio 2015 o Visual Studio 2017 ed è stata selezionata **di lavoro e l'account dell'istituto di istruzione** da hello **Modifica autenticazione** menu, ha già dispone automaticamente di rollover della chiave toohandle hello logica necessaria. Questa logica incorporata nel middleware OWIN OpenID Connect hello, recupera e memorizza nella cache le chiavi di hello dal documento di individuazione OpenID Connect hello e vengono aggiornati periodicamente.

Se si aggiunta manualmente soluzione tooyour di autenticazione, l'applicazione non dispone della logica di rollover della chiave necessario hello. Sarà necessario toowrite, oppure hello seguire i passaggi [applicazioni Web API con tutte le altre librerie o implementare manualmente uno di hello supportati i protocolli.](#other).

### <a name="vs2013"></a>Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2013
Se l'applicazione è stato creato utilizzando un modello di applicazione web in Visual Studio 2013 ed è stata selezionata **account aziendali** da hello **Modifica autenticazione** menu contiene già hello necessario rollover della chiave automaticamente toohandle logica. Tale logica archivia l'identificatore univoco dell'organizzazione e la firma delle informazioni chiave in due tabelle di database associati al progetto hello hello. È possibile trovare la stringa di connessione hello per database hello nel file Web. config del progetto hello.

Se si aggiunta manualmente soluzione tooyour di autenticazione, l'applicazione non dispone della logica di rollover della chiave necessario hello. Sarà necessario toowrite, oppure hello seguire i passaggi [applicazioni Web API con tutte le altre librerie o implementare manualmente uno di hello supportati i protocolli.](#other).

Hello alla procedura seguente consente di verificare il corretto funzionamento di logica di hello nell'applicazione.

1. In Visual Studio 2013, aprire la soluzione hello e quindi fare clic su hello **Esplora Server** scheda nella finestra di destra hello.
2. Espandere **Connessioni dati**, **DefaultConnection** e quindi **Tabelle**. Individuare hello **tenant** tabella pulsante destro del mouse e quindi fare clic su **Mostra dati tabella**.
3. In hello **tenant** tabella, sarà presente almeno una riga, che corrisponde a toohello valore di identificazione personale per la chiave di hello. Eliminare tutte le righe nella tabella hello.
4. Pulsante destro del mouse hello **tenant** tabella e quindi fare clic su **Mostra dati tabella**.
5. In hello **tenant** tabella, sarà presente almeno una riga, che corrisponde l'identificatore del tenant tooa directory univoco. Eliminare tutte le righe nella tabella hello. Se non si elimina righe hello in entrambi hello **tenant** tabella e **tenant** tabella, si verificherà un errore in fase di esecuzione.
6. Compilare ed eseguire un'applicazione hello. Dopo aver eseguito l'accesso in tooyour account, è possibile arrestare l'applicazione hello.
7. Restituire toohello **Esplora Server** ed esaminare i valori hello in hello **tenant** e **tenant** tabella. Si noterà sono stati inseriti automaticamente con le informazioni appropriate hello dal documento di metadati di federazione hello.

### <a name="vs2013"></a>API Web che proteggono le risorse e sono state create con Visual Studio 2013
Se si creato un'applicazione API web in Visual Studio 2013 mediante il modello di API Web hello e quindi selezionato **account aziendali** da hello **Modifica autenticazione** menu già avere hello logica necessaria nell'applicazione.

Se è stato configurato manualmente authentication, attenersi alle istruzioni hello seguenti toolearn come tooconfigure tooautomatically l'API Web aggiornare le informazioni sulla chiave.

Hello frammento di codice seguente viene illustrato come tooget hello chiavi più recenti dal documento di metadati di federazione hello e quindi utilizzare hello [gestore dei Token JWT](https://msdn.microsoft.com/library/dn205065.aspx) token hello toovalidate. frammento di codice Hello si presuppone che si utilizzerà un meccanismo per la persistenza toovalidate chiave di hello futuri di memorizzazione nella cache dei token da Azure AD, che può essere in un database, file di configurazione o in un' posizione.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2012
Se l'applicazione è stata creata in Visual Studio 2012, è stato probabilmente usato hello identità e tooconfigure dello strumento di accesso dell'applicazione. È inoltre probabile che si sta utilizzando hello [convalida Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx). Hello VINR è responsabile della gestione delle informazioni sui provider di identità attendibili (Azure AD) e le chiavi di hello utilizzate toovalidate token emesso da essi. Hello VINR rende facile tooautomatically aggiornamento hello informazioni sulle chiavi archiviate in un file Web. config scaricando hello più recente documento metadati federazione associato alla directory, controllando se hello non aggiornato con hello più recente documento e l'aggiornamento hello applicazione toouse hello nuova chiave in base alle esigenze.

Se è stato creato l'applicazione utilizzando uno degli esempi di codice hello o dettagliate fornite da Microsoft, la logica di rollover della chiave hello è già incluso nel progetto. Si noterà che codice hello seguente esiste già nel progetto. Se l'applicazione non dispone già di questa logica, seguire i passaggi di hello sotto tooadd e tooverify che funzioni correttamente.

1. In **Esplora**, aggiungere un riferimento toohello **System. IdentityModel** assembly per il progetto appropriato hello.
2. Aprire hello **Global.asax.cs** file e aggiungere hello seguenti direttive using:
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. Aggiungere hello seguente metodo toohello **Global.asax.cs** file:
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Richiamare hello **refreshvalidationsettings ()** metodo hello **Application_Start ()** metodo **Global.asax.cs** come illustrato:
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

Dopo aver eseguito questi passaggi, Web. config dell'applicazione verrà aggiornato con informazioni più recenti di hello dal documento di metadati di federazione hello, incluse le chiavi più recenti di hello. Questo aggiornamento si verificherà ogni volta che il pool di applicazioni viene riciclato in IIS. Per impostazione predefinita IIS è toorecycle applicazioni 29 ore.

Eseguire operazioni di hello seguenti tooverify che la logica di rollover della chiave hello sia in esecuzione.

1. Dopo aver verificato che l'applicazione utilizza codice hello sopra, aprire hello **Web. config** file e passare toohello  **<issuerNameRegistry>**  blocco, cercare in particolare hello alcune righe seguenti:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. In hello  **<add thumbprint=””>**  impostazione, modificare il valore di identificazione personale hello sostituendo ogni carattere con uno diverso. Salvare hello **Web. config** file.
3. Compilare un'applicazione hello e quindi eseguirlo. Se è possibile completare hello Accedi processo, l'applicazione aggiorna in modo corretto la chiave hello scaricando informazioni hello necessario dal documento di metadati di federazione della directory. Se si sono verificati problemi di accesso, verificare le modifiche di hello nell'applicazione siano corrette leggendo hello [tooYour aggiunta Sign-On Web dell'applicazione tramite Azure Active Directory](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) argomento oppure scaricare ed esaminare hello nell'esempio di codice seguente: [ Applicazione Cloud multi-Tenant per Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### <a name="vs2010"></a>Applicazioni Web che proteggono le risorse e sono state create con Visual Studio 2008 o 2010 o con Windows Identity Foundation (WIF) v1.0 per .NET 3.5
Se è stata compilata un'applicazione in WIF v 1.0, non vi è alcun aggiornamento tooautomatically meccanismo toouse di configurazione dell'applicazione una nuova chiave.

* *Il modo più semplice* utilizzare strumento di FedUtil hello incluso in WIF SDK, che può recuperare il documento di metadati più recente hello e aggiornare la configurazione di hello.
* Aggiornare il too.NET applicazione 4.5, che include la versione più recente di hello di WIF nello spazio dei nomi System hello. È quindi possibile utilizzare hello [convalida Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform aggiornamenti automatici della configurazione dell'applicazione hello.
* Eseguire un rollover manuale in base alle istruzioni hello alla fine di hello di questo documento di istruzioni.

Istruzioni toouse hello FedUtil tooupdate la configurazione:

1. Verificare di aver hello WIF v 1.0 SDK installato nel computer di sviluppo per Visual Studio 2008 o 2010. È possibile [scaricarlo da qui](https://www.microsoft.com/en-us/download/details.aspx?id=4451) se non è ancora installato.
2. In Visual Studio, aprire la soluzione hello, quindi fare clic sul progetto applicabile hello e selezionare **aggiornare i metadati di federazione**. Se questa opzione non è disponibile, FedUtil o hello WIF v 1.0 SDK non è stato installato.
3. Dal prompt dei comandi hello, selezionare **aggiornamento** toobegin aggiornare i metadati di federazione. Se si dispone di ambiente server di accesso toohello ospita un'applicazione hello, è possibile utilizzare facoltativamente FedUtil [dell'utilità di pianificazione aggiornamento automatico dei metadati](https://msdn.microsoft.com/library/ee517272.aspx).
4. Fare clic su **fine** toocomplete processo di aggiornamento hello.

### <a name="other"></a>Applicazioni Web / API di protezione delle risorse utilizzando qualsiasi altre librerie o implementare manualmente uno di hello protocolli supportati
Se si utilizza qualche altra libreria o implementata manualmente i protocolli supportato hello, dovrai libreria hello tooreview o l'implementazione tooensure che hello chiave viene recuperato dal documento di individuazione OpenID Connect hello o hello documento di metadati di federazione. Un modo toocheck per questo è toodo una ricerca nel codice o nel codice della libreria hello per le chiamate di un documento di individuazione OpenID tooeither hello o documento di metadati di federazione hello.

Se la chiave viene archiviato in un punto o hardcoded nell'applicazione, è possibile eseguire manualmente recuperare chiave hello e l'aggiornamento pertanto di eseguire un rollover manuale in base alle istruzioni hello alla fine di hello di questo documento di istruzioni. **Migliorare il rollover automatico toosupport di applicazione è vivamente consigliato** utilizzando uno dei hello si avvicina struttura questo interruzioni future tooavoid di articolo e overhead se Azure Active Directory aumenta la frequenza di rollover o ha un emergenza rollover fuori banda.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>Come tootest toodetermine l'applicazione, se ne risentirà
È possibile verificare se l'applicazione supporta il rollover automatico della chiave download script hello e seguendo le istruzioni di hello in [questo repository GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>Come tooperform un rollover manuale se l'applicazione non supporta il rollover automatico
Se l'applicazione **non** supporta il rollover automatico, è necessario pertanto tooestablish un processo di firma del periodicamente monitoraggi Azure AD chiavi ed esegue un aggiornamento manuale. [Questo repository GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contiene script e istruzioni su come toodo questo.

