---
title: "Sistema di gestione delle identità tra domini aaaUsing esegue automaticamente il provisioning utenti e gruppi da Azure Active Directory tooapplications | Documenti Microsoft"
description: "Azure Active Directory possono eseguire automaticamente il provisioning degli utenti e gruppi tooany identità o l'applicazione store di applicazioni da un servizio web con interfaccia hello definito nella specifica del protocollo SCIM hello"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>Utilizzo di sistema per il provisioning utenti tooautomatically di gestione delle identità tra domini e gruppi da Azure Active Directory tooapplications

## <a name="overview"></a>Panoramica
Azure Active Directory (Azure AD) può eseguire automaticamente il provisioning degli utenti e gruppi tooany identità o l'applicazione store di applicazioni da un servizio web con interfaccia hello definita in hello [sistema per domini Identity Management (SCIM) 2.0 Specifica del protocollo](https://tools.ietf.org/html/draft-ietf-scim-api-19). Azure Active Directory può inviare richieste toocreate, modificare o eliminare utenti e gruppi toohello web servizio assegnato. servizio web Hello può quindi tradurre le richieste di operazioni sull'archivio identità di destinazione hello. 

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. 



![][0]
*Figura 1: Provisioning dall'archivio di identità di Azure Active Directory tooan tramite un servizio web*

Questa funzionalità è utilizzabile in combinazione con funzionalità di "bring la propria app" hello in Azure AD tooenable single sign-on e provisioning per le applicazioni che forniscono o sono applicazioni da un servizio web SCIM automatica degli utenti.

Esistono due casi in cui SCIM viene usato in Azure Active Directory:

* **Provisioning utenti e gruppi tooapplications che supportano SCIM** applicazioni che supportano SCIM 2.0 e utilizzano i token di connessione OAuth per l'autenticazione funziona con Azure AD senza attività di configurazione.
* **Compilare la propria soluzione di provisioning per le applicazioni che supportano altri provisioning basato su API** per le applicazioni non SCIM, è possibile creare un tootranslate endpoint SCIM tra endpoint di Azure AD SCIM hello e supporta l'applicazione hello qualsiasi API per il provisioning dell'utente. toohelp si sviluppa un endpoint SCIM, si forniscono le librerie di Common Language Infrastructure (CLI) insieme a esempi di codice che illustrano come toodo forniscono un endpoint SCIM e convertire i messaggi SCIM.  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>Provisioning di utenti e gruppi tooapplications che supportano SCIM
Azure AD può essere configurato tooautomatically tooapplications utenti e gruppi a disposizione assegnato che implementano un [sistema per la gestione delle identità tra domini 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) servizio web e di accettare i token di connessione OAuth per l'autenticazione . All'interno della specifica di hello SCIM 2.0, le applicazioni devono soddisfare questi requisiti:

* Supporta la creazione di utenti e/o gruppi, come indicato nella sezione 3.3 di protocollo SCIM hello.  
* Supporta la modifica di utenti e/o gruppi con le richieste patch indicato nella sezione 3.5.2 di protocollo SCIM hello.  
* Supporta il recupero di una risorsa in base alle sezione 3.4.1 di hello protocollo SCIM nota.  
* Supporta l'esecuzione di query su utenti e/o gruppi, come indicato nella sezione sezione 3.4.2 di protocollo SCIM hello.  Per impostazione predefinita, gli utenti vengono interrogati da externalId e i gruppi da displayName.  
* Supporta l'esecuzione di query utente tramite ID e dal gestore indicato nella sezione sezione 3.4.2 di protocollo SCIM hello.  
* Supporta l'esecuzione di query gruppi tramite ID e dal membro indicato nella sezione sezione 3.4.2 di protocollo SCIM hello.  
* Accetta i token di connessione OAuth per l'autorizzazione in base alle sezione 2.1 del protocollo SCIM hello.

Verificare la conformità ai requisiti sopra riportati con il provider dell'applicazione o consultando la documentazione fornita dal provider.

### <a name="getting-started"></a>introduttiva
Le applicazioni che supportano il profilo SCIM hello descritto in questo articolo possono essere connesso tooAzure Active Directory utilizzando la funzionalità "non raccolta applicazione hello" nella raccolta di applicazione hello Azure AD. Una volta connessi, Azure AD viene eseguito un processo di sincronizzazione ogni 20 minuti in cui viene eseguita una query di endpoint SCIM dell'applicazione hello per assegnata utenti e gruppi e crea o li modifica in base a toohello i dettagli dell'assegnazione.

**un'applicazione che supporta SCIM tooconnect:**

1. Accedi troppo[hello Azure portal](https://portal.azure.com). 
2. Sfoglia troppo * * Azure Active Directory > applicazioni aziendali e selezionare **nuova applicazione > tutti > applicazione Non raccolta**.
3. Immettere un nome per l'applicazione e fare clic su **Aggiungi** icona toocreate un oggetto applicazione.
    
  ![][1]
  *Figura 2: Raccolta di applicazioni di Azure AD*
    
4. Nella schermata risultante hello selezionare hello **Provisioning** scheda nella colonna sinistra hello.
5. In hello **modalità di Provisioning** dal menu **automatica**.
    
  ![][2]
  *Figura 3: Configurazione del provisioning in hello portale di Azure*
    
6. In hello **URL Tenant** immettere hello URL dell'endpoint SCIM dell'applicazione hello. Esempio: https://api.contoso.com/scim/v2/
7. Se l'endpoint SCIM hello richiede un token di connessione OAuth da un'autorità di certificazione diversa da Azure AD, quindi hello copia necessari token di connessione OAuth nel hello facoltativo **segreto Token** campo. Se questo campo viene lasciato vuoto, AD Azure include in ogni richiesta un token di connessione OAuth emesso da Azure AD. Le app che usano Azure AD come provider di identità possono convalidare il token rilasciato da Azure AD.
8. Fare clic su hello **Test connessione** endpoint SCIM pulsante toohave Azure Active Directory tentativo tooconnect toohello. Se hello tentativi falliscono, informazioni sull'errore.  
9. Se un'applicazione hello tentativi tooconnect toohello esito negativo, quindi fare clic su **salvare** credenziali di amministratore toosave hello.
10. In hello **mapping** sezione, sono disponibili due set di mapping degli attributi selezionabile: uno per gli oggetti utente e uno per gli oggetti di gruppo. Selezionare ogni attributi di hello tooreview uno che vengono sincronizzati da app tooyour Azure Active Directory. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello utenti e gruppi nell'app per le operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.

    >[!NOTE]
    >È facoltativamente possibile disabilitare la sincronizzazione degli oggetti di gruppo dalla disabilitazione di hello "gruppi" mapping. 

11. In **impostazioni**, hello **ambito** campo definisce quali gruppi di utenti e o vengono sincronizzati. Selezione di "Sincronizzazione assegnata solo gli utenti e gruppi" (scelta consigliata) verranno sincronizzate solo gli utenti e gruppi assegnati in hello **utenti e gruppi** scheda.
12. Una volta completata la configurazione, modificare hello **lo stato di Provisioning** troppo**su**.
13. Fare clic su **salvare** toostart hello servizio provisioning di Azure AD. 
14. Se la sincronizzazione solo assegnati a utenti e gruppi (scelta consigliati), in certi hello tooselect **utenti e gruppi** scheda e assegnare gli utenti di hello e/o gruppi di cui si desidera toosync.

Una volta avviata la sincronizzazione iniziale di hello, è possibile utilizzare hello **log di controllo** scheda toomonitor lo stato di avanzamento, che mostra tutte le azioni eseguite da hello provisioning del servizio nella tua app. Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

>[!NOTE]
>la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>Creazione di una soluzione di provisioning personale per qualsiasi applicazione
Creando un servizio Web SCIM in grado di interagire con Azure Active Directory, è possibile abilitare l'accesso Single Sign-On e il provisioning utente automatico per qualsiasi applicazione che offra un'API di provisioning utente REST o SOAP.

Il servizio funziona nel modo seguente:

1. Azure AD fornisce una libreria Common Language Infrastructure denominata [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/). Gli sviluppatori e integratori di sistema possono utilizzare toocreate questa libreria e distribuire un endpoint del servizio web basato su SCIM in grado di connettersi archivio identità dell'applicazione di Azure AD tooany.
2. I mapping vengono implementati in hello web servizio toomap hello standardizzato schema utente di schema toohello utente e il protocollo richiesto da un'applicazione hello.
3. URL dell'endpoint Hello è registrato in Azure AD come parte di un'applicazione personalizzata nella raccolta di applicazione hello.
4. Utenti e gruppi assegnati toothis applicazione in Azure AD. Base all'assegnazione, vengono inseriti in un'applicazione di destinazione coda toohello toobe sincronizzato. il processo di sincronizzazione Hello gestione coda hello viene eseguito ogni 20 minuti.

### <a name="code-samples"></a>Esempi di codice
toomake questo processo più semplice, un set di [esempi di codice](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) sono incluse la creazione di un endpoint del servizio web SCIM e viene illustrato il provisioning automatico. Un esempio è relativo a un provider che gestisce un file con righe di valori delimitati da virgole che rappresentano utenti e gruppi.  altri Hello è di un provider che opera su servizio di Amazon Web Services Identity and Access Management hello.  

**Prerequisiti**

* Visual Studio 2013 o versioni successive
* [Azure SDK per .NET](https://azure.microsoft.com/downloads/)
* Computer Windows che supporta hello ASP.NET 4.5 framework toobe utilizzato come hello endpoint SCIM. Il computer deve essere accessibile dal cloud hello
* [Una sottoscrizione di Azure con una versione di prova o concessa in licenza di Azure AD Premium](https://azure.microsoft.com/services/active-directory/)
* esempio di Amazon AWS Hello richiede di librerie da hello [AWS Toolkit per Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html). Per ulteriori informazioni, vedere hello Leggimi file incluso in esempio hello.

### <a name="getting-started"></a>Introduzione
tooimplement modo più semplice Hello richiede un endpoint SCIM in grado di accettare il provisioning da Azure AD è toobuild e distribuire l'esempio di codice hello che restituisce hello provisioning utenti tooa valore delimitato da virgole (CSV) file.

**un endpoint di esempio SCIM toocreate:**

1. Download del pacchetto di esempio di codice hello in [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Decomprimere il pacchetto di hello e posizionarlo nel computer Windows in una posizione, ad esempio C:\AzureAD-BYOA-Provisioning-Samples\.
3. In questa cartella, avviare soluzione FileProvisioningAgent hello in Visual Studio.
4. Selezionare **strumenti > Gestione pacchetti libreria > Console di gestione pacchetti**ed eseguire i seguenti comandi per i riferimenti di soluzione hello tooresolve progetto FileProvisioningAgent hello hello:
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Compilare il progetto di FileProvisioningAgent hello.
6. Avvio dell'applicazione hello prompt dei comandi di Windows (come amministratore) e utilizzare hello **cd** comando toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** cartella.
7. Eseguire hello comando seguente, sostituendo < indirizzo ip > con nome hello IP indirizzo o il dominio del computer Windows hello:
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. In Windows in **impostazioni di Windows > rete e le impostazioni Internet**selezionare hello **Windows Firewall > Impostazioni avanzate**e creare un **regola connessioni in entrata** che Consente l'accesso in ingresso tooport 9000.
9. Se il computer di Windows hello è protetto da un router, hello router esigenze toobe configurato tooperform traduzione di accesso di rete tra la porta 9000 che viene esposto toohello internet e la porta 9000 sul computer di Windows hello. Questa operazione è necessaria per Azure AD toobe in grado di tooaccess questo endpoint nel cloud hello.

**tooregister hello SCIM endpoint di esempio in Azure AD:**

1. Accedi troppo[hello Azure portal](https://portal.azure.com). 
2. Sfoglia troppo * * Azure Active Directory > applicazioni aziendali e selezionare **nuova applicazione > tutti > applicazione Non raccolta**.
3. Immettere un nome per l'applicazione e fare clic su **Aggiungi** icona toocreate un oggetto applicazione. l'oggetto applicazione Hello creato è previsto toorepresent hello destinazione app verrebbe eseguito il provisioning dei tooand implementazione endpoint SCIM single sign-on per e non solo di hello.
4. Nella schermata risultante hello selezionare hello **Provisioning** scheda nella colonna sinistra hello.
5. In hello **modalità di Provisioning** dal menu **automatica**.
    
  ![][2]
  *Figura 4: Configurazione del provisioning in hello portale di Azure*
    
6. In hello **URL Tenant** immettere l'URL di hello esposto a internet e la porta dell'endpoint SCIM. Si tratterà di un elemento come http://testmachine.contoso.com:9000 o http://<ip-address>:9000/, dove < indirizzo ip > è hello internet esposti IP indirizzo.  
7. Se l'endpoint SCIM hello richiede un token di connessione OAuth da un'autorità di certificazione diversa da Azure AD, quindi hello copia necessari token di connessione OAuth nel hello facoltativo **segreto Token** campo. Se questo campo viene lasciato vuoto, AD Azure includerà in ogni richiesta un token di connessione OAuth emesso da Azure AD. Le app che usano Azure AD come provider di identità possono convalidare il token rilasciato da Azure AD.
8. Fare clic su hello **Test connessione** endpoint SCIM pulsante toohave Azure Active Directory tentativo tooconnect toohello. Se hello tentativi falliscono, informazioni sull'errore.  
9. Se un'applicazione hello tentativi tooconnect toohello esito negativo, quindi fare clic su **salvare** credenziali di amministratore toosave hello.
10. In hello **mapping** sezione, sono disponibili due set di mapping degli attributi selezionabile: uno per gli oggetti utente e uno per gli oggetti di gruppo. Selezionare ogni attributi di hello tooreview uno che vengono sincronizzati da app tooyour Azure Active Directory. gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello utenti e gruppi nell'app per le operazioni di aggiornamento. Selezionare hello Salva pulsante toocommit tutte le modifiche.
11. In **impostazioni**, hello **ambito** campo definisce quali gruppi di utenti e o vengono sincronizzati. Selezione di "Sincronizzazione assegnata solo gli utenti e gruppi" (scelta consigliata) verranno sincronizzate solo gli utenti e gruppi assegnati in hello **utenti e gruppi** scheda.
12. Una volta completata la configurazione, modificare hello **lo stato di Provisioning** troppo**su**.
13. Fare clic su **salvare** toostart hello servizio provisioning di Azure AD. 
14. Se la sincronizzazione solo assegnati a utenti e gruppi (scelta consigliati), in certi hello tooselect **utenti e gruppi** scheda e assegnare gli utenti di hello e/o gruppi di cui si desidera toosync.

Una volta avviata la sincronizzazione iniziale di hello, è possibile utilizzare hello **log di controllo** scheda toomonitor lo stato di avanzamento, che mostra tutte le azioni eseguite da hello provisioning del servizio nella tua app. Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

passaggio finale Hello verifica esempio hello è hello tooopen TargetFile.csv file nella cartella \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug hello sul proprio computer Windows. Una volta eseguito il processo di provisioning hello, questo file Mostra dettagli hello tutte assegnati e il provisioning di utenti e gruppi.

### <a name="development-libraries"></a>Librerie di sviluppo
toodevelop il proprio servizio web conforme alla specifica SCIM toohello, acquisire familiarità con hello seguendo le librerie fornite da Microsoft toohelp accelerare il processo di sviluppo hello: 

1. Le librerie CLI (Common Language Infrastructure) vengono messe a disposizione per essere usate con linguaggi basati su questa infrastruttura, ad esempio C#. Uno di tali raccolte, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), dichiara un'interfaccia, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, illustrata nella seguente figura hello: A gli sviluppatori che utilizzano le librerie di hello implementi tale interfaccia con una classe che può essere indicata, in modo generico, come un provider. librerie di Hello consentono hello developer toodeploy un servizio web conforme alla specifica SCIM toohello. servizio web Hello può essere sia ospitato all'interno di Internet Information Services o qualsiasi assembly di Common Language Infrastructure eseguibile. Richiesta viene tradotta in metodi del provider di chiamate toohello, che potrebbero essere programmati dai toooperate developer hello in un archivio di identità.
  
  ![][3]
  
2. [Express route gestori](http://expressjs.com/guide/routing.html) sono disponibili per l'analisi di oggetti di richiesta di Node. js che rappresentano chiamate (come definito dalla specifica SCIM hello), servizio web di tooa node.js.   

### <a name="building-a-custom-scim-endpoint"></a>Creazione di un endpoint SCIM personalizzato
Usa librerie CLI hello, gli sviluppatori che utilizzano tali librerie possono ospitare i servizi in qualsiasi assembly di Common Language Infrastructure eseguibile o in Internet Information Services. Di seguito è riportato il codice di esempio per l'hosting di un servizio all'interno di un assembly eseguibile, all'indirizzo hello http://localhost:9000/objectUri: 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

Questo servizio deve disporre di un HTTP indirizzo server di autenticazione certificato di cui hello autorità di certificazione radice è uno dei seguenti hello: 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Go Daddy
* Verisign
* WoSign

Un certificato di autenticazione server può essere associato tooa porta in un host Windows utilizzo hello utilità shell della rete: 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

In questo caso, il valore di hello fornito per l'argomento certhash hello è identificazione personale hello del certificato di hello, mentre il valore di hello fornito per l'argomento appid hello è un identificatore univoco globale arbitrario.  

servizio di hello toohost all'interno di Internet Information Services, uno sviluppatore sarebbe compilare un assembly libreria di codice CLA con una classe denominata avvio nello spazio dei nomi predefinito hello dell'assembly hello.  Ecco un esempio di questa classe: 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>Gestione dell'autenticazione dell'endpoint
Le richieste da Azure Active Directory includono un token di connessione OAuth 2.0.   Qualsiasi richiesta di servizio ricevente hello deve eseguire l'autenticazione dell'autorità di certificazione hello come Azure Active Directory per conto di tenant di Azure Active Directory hello previsto, per l'accesso toohello servizio web di Azure Active Directory Graph.  In token hello emittente hello è identificato da un'attestazione iss, ad esempio, "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".  In questo esempio, l'indirizzo di base del valore di attestazione hello, hello https://sts.windows.net, identifica Azure Active Directory come autorità di certificazione hello, mentre il segmento indirizzo relativo, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, hello è un identificatore univoco di hello Azure Active Tenant di directory per conto di quali hello token è stato rilasciato.  Se è stato rilasciato il token hello per accedere al servizio web di Azure Active Directory Graph hello, quindi identificatore hello di tale servizio, 00000002-0000-0000-c000-000000000000, devono essere valore hello aud del token hello di attestazioni.  

Gli sviluppatori che utilizzano librerie CLA hello fornite da Microsoft per la creazione di un servizio SCIM possono autenticare le richieste da Azure Active Directory tramite il pacchetto di ActiveDirectory hello attenendosi alla procedura seguente: 

1. In un provider, implementare proprietà Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior hello avendolo restituire toobe un metodo chiamato ogni volta che viene avviato il servizio hello: 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. Aggiungere hello seguente codice toothat metodo toohave tooany qualsiasi richiesta di endpoint del servizio hello autenticato come bearing un token emesso da Azure Active Directory per conto di un tenant specificato, per l'accesso toohello servizio web di Azure AD Graph: 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>Schema di utenti e gruppi
Azure Active Directory possono eseguire il provisioning di due tipi di servizi web tooSCIM di risorse.  ovvero utenti e gruppi.  

Le risorse utente sono identificate dall'identificatore di schema hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, incluso in questa specifica del protocollo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.  Nella tabella 1, il mapping predefinito Hello di attributi hello degli utenti in attributi toohello Azure Active Directory delle risorse urn: ietf:params:scim:schemas:extension:enterprise:2.0:User di seguito.  

Risorse del gruppo sono identificate dall'identificatore di schema hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  Tabella 2, di sotto, Mostra hello del mapping predefinito tra gli attributi di hello dei gruppi di attributi di Azure Active Directory toohello http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group risorse.  

### <a name="table-1-default-user-attribute-mapping"></a>Tabella 1: mapping predefinito degli attributi utente
| Utente Azure Active Directory | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |active |
| displayName |displayName |
| Facsimile-TelephoneNumber |phoneNumbers[type eq "fax"].value |
| givenName |name.givenName |
| jobTitle |title |
| mail |emails[type eq "work"].value |
| mailNickname |externalId |
| manager |manager |
| mobile |phoneNumbers[type eq "mobile"].value |
| objectId |id |
| postalCode |addresses[type eq "work"].postalCode |
| proxy-Addresses |emails[type eq "other"].Value |
| physical-Delivery-OfficeName |addresses[type eq "other"].Formatted |
| streetAddress |addresses[type eq "work"].streetAddress |
| surname |name.familyName |
| telephone-Number |phoneNumbers[type eq "work"].value |
| user-PrincipalName |userName |

### <a name="table-2-default-group-attribute-mapping"></a>Tabella 2: mapping predefinito degli attributi gruppo
| Gruppo di Azure Active Directory | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| displayName |externalId |
| mail |emails[type eq "work"].value |
| mailNickname |displayName |
| Membri di |Membri di |
| objectId |id |
| proxyAddresses |emails[type eq "other"].Value |

## <a name="user-provisioning-and-de-provisioning"></a>Provisioning e deprovisioning utenti
Hello nella seguente illustrazione mostra i messaggi hello che Azure Active Directory invia tooa SCIM servizio toomanage hello del ciclo di vita di un utente nell'archivio identità di un altro. diagramma di Hello Mostra anche come un servizio SCIM implementato utilizzando librerie CLI hello fornito da Microsoft per la creazione di che tali servizi traducono toohello chiama i metodi di un provider di tali richieste.  

![][4]
*Figura 5: Sequenza di provisioning e deprovisioning utenti*

1. Query di Active Directory di Azure hello servizio per un utente con un valore di attributo externalId corrispondente valore dell'attributo mailNickname hello di un utente in Azure AD. query Hello viene espresso come una richiesta di protocollo HTTP (Hypertext Transfer), ad esempio in questo esempio, in cui jyoung è un esempio di un mailNickname di un utente in Azure Active Directory: 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Se il servizio di hello è stato creato utilizzando le librerie di Common Language Infrastructure hello fornite da Microsoft per l'implementazione di servizi SCIM, richiesta hello viene convertito in un metodo di Query del provider del servizio hello di toohello chiamata.  Questa è hello firma del metodo: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  Di seguito è la definizione hello dell'interfaccia Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello: 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  Nel seguente esempio di una query per un utente con un valore specificato per l'attributo externalId hello di hello, i valori degli argomenti di hello passati toohello metodo di Query sono: 
  * parameters.AlternateFilters.Count: 1
  * parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"
  * parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"] 

2. Se nessun utente restituito hello risposta tooa toohello servizio web di query per un utente con un valore di attributo externalId che corrisponda al valore di attributo mailNickname hello di un utente, Azure Active Directory richiede che il provisioning del servizio hello un utente corrispondente toohello uno in Azure Active Directory.  Ecco un esempio di questa richiesta: 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  librerie di Common Language Infrastructure Hello fornite da Microsoft per l'implementazione di servizi SCIM Converte la richiesta in toohello una chiamata di metodo di creazione del provider del servizio hello.  Hello metodo Create con questa firma: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  In una richiesta tooprovision un utente, il valore di hello dell'argomento resource hello è un'istanza di hello Microsoft.SystemForCrossDomainIdentityManagement. Classe Core2EnterpriseUser definiti nella libreria Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.  Se ha esito positivo hello richiesta tooprovision hello utente, quindi hello implementazione del metodo hello è previsto tooreturn un'istanza di hello Microsoft.SystemForCrossDomainIdentityManagement. Classe Core2EnterpriseUser, con valore hello della proprietà identificatore hello imposta toohello identificatore univoco dell'utente appena sottoposti a provisioning hello.  

3. tooupdate un utente, noto in un archivio di identità tooexist applicazioni da un SCIM, Azure Active Directory viene eseguito tramite la richiesta di stato corrente di hello di tale utente dal servizio hello con una richiesta, ad esempio: 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  In un servizio compilato utilizzando le librerie di Common Language Infrastructure hello fornite da Microsoft per l'implementazione di servizi SCIM richiesta hello viene tradotta in toohello una chiamata di metodo di recupero del provider del servizio hello.  Questa è hello firma del metodo di recupero hello: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  Nell'esempio hello di uno stato corrente di hello tooretrieve richiesta di un utente, valori hello proprietà hello dell'oggetto di hello fornito come valore di hello dell'argomento parametri hello sono i seguenti: 
  
  * Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. Se un attributo di riferimento è toobe aggiornato, quindi Azure Active Directory query hello servizio toodetermine o meno hello valore corrente dell'attributo di riferimento hello nell'archivio identità hello applicazioni dal servizio hello già corrisponde hello di tale attributo in Azure Active Directory. Per gli utenti, unico attributo hello di quali hello valore corrente viene eseguita una query in questo modo è l'attributo manager hello. Ecco un esempio di una richiesta di toodetermine se l'attributo manager hello di un oggetto utente specifico dispone attualmente di un determinato valore: 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  valore di Hello hello gli attributi parametro della query, id, significa che se esiste un oggetto utente che soddisfa l'espressione hello fornita come valore di hello del parametro di query di filtro hello, il servizio hello toorespond previsto con un urn: ietf:params:scim:schemas: risorsa core: 2.0:User o urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, inclusi hello solo il valore dell'attributo id della risorsa.  valore di hello Hello **id** noto toohello richiedente. È incluso nel valore di hello del parametro di query di filtro hello; Hello richiede mira effettivamente toorequest una rappresentazione minima di una risorsa esistente che soddisfano l'espressione di filtro hello come indicazione della o meno tale oggetto.   

  Se il servizio di hello è stato creato utilizzando le librerie di Common Language Infrastructure hello fornite da Microsoft per l'implementazione di servizi SCIM, richiesta hello viene convertito in un metodo di Query del provider del servizio hello di toohello chiamata. il valore di Hello proprietà hello dell'oggetto di hello fornito come valore di hello dell'argomento parametri hello sono i seguenti: 
  
  * parameters.AlternateFilters.Count: 2
  * parameters.AlternateFilters.ElementAt(x).AttributePath: "id"
  * parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"
  * parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * parameters.RequestedAttributePaths.ElementAt(0): "id"
  * parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

  In questo caso, il valore di hello dell'indice di hello x può essere 0 e valore hello hello indice y può essere 1, o valore hello di x può essere 1 e valore hello y può essere 0, a seconda dell'ordine di hello di espressioni hello hello filtro del parametro della query.   

5. Di seguito è riportato un esempio di una richiesta da Azure Active Directory tooan SCIM servizio tooupdate un utente: 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  librerie di Microsoft Common Language Infrastructure Hello per l'implementazione di servizi SCIM converte richiesta hello in toohello una chiamata di metodo di aggiornamento del provider del servizio hello. Questa è hello firma del metodo Update hello: 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    Nell'esempio hello di tooupdate una richiesta utente oggetto hello fornito come valore di hello dell'argomento di patch hello presenta questi valori di proprietà: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest as PatchRequest2).Operations.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646

6. un utente da un archivio di identità di effettuare il provisioning di toode applicazioni da un servizio SCIM, Azure AD invia una richiesta, ad esempio: 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Se il servizio di hello è stato creato utilizzando le librerie di Common Language Infrastructure hello fornite da Microsoft per l'implementazione di servizi SCIM, richiesta hello viene convertito in un metodo di eliminazione del provider del servizio di hello di toohello chiamata.   Il metodo ha la firma seguente: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  oggetto Hello fornito come valore di hello dell'argomento resourceIdentifier hello presenta questi valori di proprietà nell'esempio hello di una richiesta toode a disposizione un utente: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>Provisioning e deprovisioning gruppi
Hello nella seguente figura mostra i messaggi hello che Azure AcD invia tooa SCIM servizio toomanage hello del ciclo di vita di un gruppo in un altro archivio identità.  Tali messaggi sono diversi dai messaggi hello riguardano toousers in tre modi: 

* schema di Hello di una risorsa del gruppo viene identificato come http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  
* Richieste tooretrieve gruppi stabiliscono tale attributo membri hello è escluso da qualsiasi risorsa fornita nella richiesta di risposta toohello toobe.  
* Se un attributo di riferimento dispone di un determinato valore sono richieste sull'attributo membri hello toodetermine di richieste.  

![][5]
*Figura 6: Sequenza di provisioning e deprovisioning gruppi*

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Automatizzare tooSaaS utente Provisioning o Deprovisioning App](active-directory-saas-app-provisioning.md)
* [Personalizzazione dei mapping degli attributi per il Provisioning dell’utente](active-directory-saas-customizing-attribute-mappings.md)
* [Scrittura di espressioni per i mapping degli attributi](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Ambito dei filtri per il Provisioning utente](active-directory-saas-scoping-filters.md)
* [Notifiche relative al provisioning dell'account](active-directory-saas-account-provisioning-notifications.md)
* [Elenco di esercitazioni sulla tooIntegrate App SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
