---
title: Uso di System for Cross-Domain Identity Management per abilitare il provisioning automatico di utenti e gruppi da Azure Active Directory ad applicazioni | Microsoft Docs
description: "Azure Active Directory può effettuare automaticamente il provisioning di utenti e gruppi in qualsiasi applicazione o archivio identità gestito da un servizio Web con interfaccia definita nella specifica del protocollo SCIM"
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
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a>Uso di System for Cross-Domain Identity Management per abilitare il provisioning automatico di utenti e gruppi da Azure Active Directory ad applicazioni

## <a name="overview"></a>Panoramica
Azure Active Directory (Azure AD) può effettuare automaticamente il provisioning di utenti e gruppi in qualsiasi applicazione o archivio identità gestito da un servizio Web con interfaccia definita nella [specifica del protocollo System for Cross-Domain Identity Management (SCIM) 2.0](https://tools.ietf.org/html/draft-ietf-scim-api-19). Azure Active Directory può inviare richieste per creare, modificare o eliminare utenti e gruppi assegnati al servizio Web, che converte quindi le richieste in operazioni sull'archivio identità di destinazione. 

> [!IMPORTANT]
> Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo. 



![][0]
*Figura 1: Provisioning da Azure Active Directory a un archivio identità tramite un servizio Web*

Questa funzione può essere usata insieme alla funzionalità "bring your own app" in Azure AD per abilitare l'accesso Single Sign-On e il provisioning utenti automatico in applicazioni che offrono o sono gestite da un servizio Web SCIM.

Esistono due casi in cui SCIM viene usato in Azure Active Directory:

* **Provisioning di utenti e gruppi in applicazioni che supportano SCIM**: le applicazioni che supportano SCIM 2.0 e usano token di connessione OAuth per l'autenticazione possono essere usate con Azure AD senza interventi di configurazione.
* **Compilazione di una soluzione di provisioning per le applicazioni che supportano il provisioning basato su altre API**: in caso di applicazioni non SCIM, è possibile creare un endpoint SCIM da convertire tra l'endpoint SCIM di Azure AD e qualsiasi API supportata dall'applicazione per il provisioning utente. Per facilitare lo sviluppo di un endpoint SCIM, vengono fornite librerie CLI (Common Language Infrastructure) ed esempi di codice che illustrano come creare un endpoint SCIM e convertire messaggi SCIM.  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a>Provisioning di utenti e gruppi in applicazioni che supportano SCIM
Azure AD può essere configurato in modo da effettuare automaticamente il provisioning di determinati utenti e gruppi in applicazioni che implementano un servizio Web [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) e accettano token di connessione OAuth per l'autenticazione. Nell'ambito della specifica SCIM 2.0, le applicazioni devono soddisfare i requisiti seguenti:

* Supportare la creazione di utenti e/o gruppi, come indicato nella sezione 3.3 del protocollo SCIM.  
* Supportare la modifica di utenti e/o gruppi con richieste patch, come indicato nella sezione 3.5.2 del protocollo SCIM.  
* Supportare il recupero di una risorsa nota, come indicato nella sezione 3.4.1 del protocollo SCIM.  
* Supportare l'interrogazione di utenti e/o gruppi, come indicato nella sezione 3.4.2 del protocollo SCIM.  Per impostazione predefinita, gli utenti vengono interrogati da externalId e i gruppi da displayName.  
* Supportare l'interrogazione di utenti in base all'ID o al responsabile, come indicato nella sezione 3.4.2 del protocollo SCIM.  
* Supportare l'interrogazione di gruppi in base all'ID o ai membri, come indicato nella sezione 3.4.2 del protocollo SCIM.  
* Accettare token di connessione OAuth per l'autorizzazione, come indicato nella sezione 2.1 del protocollo SCIM.

Verificare la conformità ai requisiti sopra riportati con il provider dell'applicazione o consultando la documentazione fornita dal provider.

### <a name="getting-started"></a>Introduzione
Le applicazioni che supportano il profilo SCIM descritto in questo articolo possono essere connesse ad Azure Active Directory usando la funzionalità "Applicazione non nella raccolta" nella raccolta di applicazioni di Azure AD. Una volta stabilita la connessione, Azure AD esegue un processo di sincronizzazione ogni 20 minuti in cui interroga l'endpoint SCIM dell'applicazione in merito agli utenti e ai gruppi assegnati e li crea o li modifica in base alle istruzioni di assegnazione.

**Per connettere un'applicazione che supporta SCIM:**

1. Accedere al [portale di Azure](https://portal.azure.com). 
2. Passare ad **Azure Active Directory > Applicazioni aziendali e selezionare **Nuova applicazione > Tutte > Applicazione non nella raccolta**.
3. Immettere un nome per l'applicazione e fare clic sull'icona **Aggiungi** per creare un oggetto app.
    
  ![][1]
  *Figura 2: Raccolta di applicazioni di Azure AD*
    
4. Nella schermata risultante selezionare la scheda **Provisioning** nella colonna sinistra.
5. Nel menu **Modalità di provisioning** selezionare **Automatica**.
    
  ![][2]
  *Figura 3: Configurazione del provisioning nel portale di Azure*
    
6. Nel campo **URL tenant** immettere l'URL dell'endpoint SCIM dell'applicazione. Esempio: https://api.contoso.com/scim/v2/
7. Se l'endpoint SCIM richiede un token di connessione OAuth da un'autorità di certificazione diversa da Azure AD, copiare il token di connessione OAuth nel campo **Token segreto** facoltativo. Se questo campo viene lasciato vuoto, AD Azure include in ogni richiesta un token di connessione OAuth emesso da Azure AD. Le app che usano Azure AD come provider di identità possono convalidare il token rilasciato da Azure AD.
8. Fare clic sul pulsante **Test connessione** per fare in modo che Azure Active Directory provi a connettersi all'endpoint SCIM. Se i tentativi hanno esito negativo, verranno visualizzate informazioni sul tipo di errore.  
9. Se i tentativi di connessione all'applicazione hanno esito positivo, fare clic su **Salva** per salvare le credenziali di amministratore.
10. Nella sezione **Mapping** sono disponibili due set selezionabili di mapping degli attributi: uno per gli oggetti utente e uno per gli oggetti gruppo. Selezionare ognuno dei due set per esaminare gli attributi sincronizzati da Active Directory di Azure con l'app. Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli utenti e i gruppi nell'app per le operazioni di aggiornamento. Selezionare il pulsante Salva per eseguire il commit delle modifiche.

    >[!NOTE]
    >Facoltativamente, è possibile disattivare la sincronizzazione degli oggetti gruppo disabilitando il mapping relativo ai gruppi. 

11. In **Impostazioni**, il campo **Ambito** definisce gli utenti e/o i gruppi che devono essere sincronizzati. Se si seleziona "Sync only assigned users and groups" ("Sincronizza solo utenti e gruppi assegnati") (scelta consigliata), verranno sincronizzati solo gli utenti e i gruppi assegnati nella scheda **Utenti e gruppi**.
12. Al termine della configurazione, impostare lo **Stato del provisioning** su **Sì**.
13. Fare clic su **Salva** per avviare il servizio di provisioning di Azure AD. 
14. Se si sceglie di sincronizzare solo gli utenti e i gruppi assegnati (scelta consigliata), assicurarsi di selezionare la scheda **Utenti e gruppi** e di assegnare gli utenti e/o i gruppi che si vuole sincronizzare.

Dopo aver avviato la sincronizzazione iniziale, è possibile usare la scheda **Log di controllo** per monitorare lo stato di avanzamento, che mostra tutte le azioni eseguite dal servizio di provisioning sull'app. Per altre informazioni sulla lettura dei log di provisioning di Azure AD, vedere l'esercitazione relativa alla [creazione di report sul provisioning automatico degli account utente](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

>[!NOTE]
>La sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>Creazione di una soluzione di provisioning personale per qualsiasi applicazione
Creando un servizio Web SCIM in grado di interagire con Azure Active Directory, è possibile abilitare l'accesso Single Sign-On e il provisioning utente automatico per qualsiasi applicazione che offra un'API di provisioning utente REST o SOAP.

Il servizio funziona nel modo seguente:

1. Azure AD fornisce una libreria Common Language Infrastructure denominata [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/). Gli integratori di sistemi e gli sviluppatori possono usare questa libreria per creare e distribuire un endpoint di servizio Web basato su SCIM in grado di connettere Azure AD all'archivio identità di qualsiasi applicazione.
2. I mapping vengono implementati nel servizio Web per il mapping dello schema utente standardizzato allo schema utente e al protocollo richiesto dall'applicazione.
3. L'URL dell'endpoint viene registrato in Azure AD come parte di un'applicazione personalizzata nella raccolta di applicazioni.
4. Gli utenti e i gruppi vengono assegnati a questa applicazione in Azure AD. In fase di assegnazione, vengono inseriti in una coda per la sincronizzazione con l'applicazione di destinazione. Il processo di sincronizzazione che gestisce la coda viene eseguito ogni 20 minuti.

### <a name="code-samples"></a>Esempi di codice
Per semplificare il processo, viene fornito un set di [esempi di codice](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) che creano un endpoint di servizio Web SCIM e illustrano il provisioning automatico. Un esempio è relativo a un provider che gestisce un file con righe di valori delimitati da virgole che rappresentano utenti e gruppi.  L'altro esempio è relativo a un provider che agisce sul servizio Amazon Web Services Identity e Access Management.  

**Prerequisiti**

* Visual Studio 2013 o versioni successive
* [Azure SDK per .NET](https://azure.microsoft.com/downloads/)
* Computer Windows che supporta ASP.NET Framework 4.5 da usare come endpoint SCIM. Questo computer deve essere accessibile dal cloud.
* [Una sottoscrizione di Azure con una versione di prova o concessa in licenza di Azure AD Premium](https://azure.microsoft.com/services/active-directory/)
* L'esempio relativo ad Amazon AWS richiede librerie di [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html). Per altre informazioni, vedere il file README incluso nell'esempio.

### <a name="getting-started"></a>Introduzione
Il modo più semplice per implementare un endpoint SCIM in grado di accettare richieste di provisioning da Azure AD consiste nel compilare e distribuire l'esempio di codice che fornisce come output gli utenti con provisioning in un file CSV (Comma-Separated Value).

**Per creare un endpoint SCIM di esempio:**

1. Scaricare il pacchetto dell'esempio di codice da [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Decomprimere il pacchetto e salvarlo nel computer Windows in un percorso analogo a C:\AzureAD-BYOA-Provisioning-Samples\.
3. In questa cartella avviare la soluzione FileProvisioningAgent in Visual Studio.
4. Selezionare **Strumenti > Library Package Manager (Gestione pacchetti libreria) > Console di Gestione pacchetti** ed eseguire i comandi seguenti per il progetto FileProvisioningAgent per risolvere i riferimenti alla soluzione:
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Compilare il progetto FileProvisioningAgent.
6. Avviare l'applicazione prompt dei comandi in Windows come amministratore e usare il comando **cd** per passare alla cartella **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug**.
7. Eseguire il comando seguente, sostituendo <ip-address> con l'indirizzo IP o il nome di dominio del computer Windows:
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. In Windows, in **Impostazioni di Windows > Rete e Internet**, selezionare **Windows Firewall > Impostazioni avanzate** e quindi creare una **Nuova regola connessioni in entrata** che consente l'accesso in ingresso alla porta 9000.
9. Se il computer Windows si trova dietro un router, è necessario configurare il router in modo che esegua NAT (Network Access Translation) tra la rispettiva porta 9000 esposta a Internet e la porta 9000 nel computer Windows. Questo è necessario per consentire ad Azure AD di accedere a questo endpoint sul cloud.

**Per registrare l'endpoint SCIM di esempio in Azure AD:**

1. Accedere al [portale di Azure](https://portal.azure.com). 
2. Passare ad **Azure Active Directory > Applicazioni aziendali e selezionare **Nuova applicazione > Tutte > Applicazione non nella raccolta**.
3. Immettere un nome per l'applicazione e fare clic sull'icona **Aggiungi** per creare un oggetto app. L'oggetto applicazione creato deve rappresentare l'app di destinazione in cui verrà effettuato il provisioning e per cui verrà implementato l'accesso Single Sign-On, non solo l'endpoint SCIM.
4. Nella schermata risultante selezionare la scheda **Provisioning** nella colonna sinistra.
5. Nel menu **Modalità di provisioning** selezionare **Automatica**.
    
  ![][2]
  *Figura 4: Configurazione del provisioning nel portale di Azure*
    
6. Nel campo **URL tenant** immettere l'URL esposto a Internet e la porta dell'endpoint SCIM. Questi valori saranno simili a http://testmachine.contoso.com:9000 o http://<indirizzo-IP>:9000/, dove <indirizzo-IP> è l'indirizzo IP esposto a Internet.  
7. Se l'endpoint SCIM richiede un token di connessione OAuth da un'autorità di certificazione diversa da Azure AD, copiare il token di connessione OAuth nel campo **Token segreto** facoltativo. Se questo campo viene lasciato vuoto, AD Azure includerà in ogni richiesta un token di connessione OAuth emesso da Azure AD. Le app che usano Azure AD come provider di identità possono convalidare il token rilasciato da Azure AD.
8. Fare clic sul pulsante **Test connessione** per fare in modo che Azure Active Directory provi a connettersi all'endpoint SCIM. Se i tentativi hanno esito negativo, verranno visualizzate informazioni sul tipo di errore.  
9. Se i tentativi di connessione all'applicazione hanno esito positivo, fare clic su **Salva** per salvare le credenziali di amministratore.
10. Nella sezione **Mapping** sono disponibili due set selezionabili di mapping degli attributi: uno per gli oggetti utente e uno per gli oggetti gruppo. Selezionare ognuno dei due set per esaminare gli attributi sincronizzati da Active Directory di Azure con l'app. Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli utenti e i gruppi nell'app per le operazioni di aggiornamento. Selezionare il pulsante Salva per eseguire il commit delle modifiche.
11. In **Impostazioni**, il campo **Ambito** definisce gli utenti e/o i gruppi che devono essere sincronizzati. Se si seleziona "Sync only assigned users and groups" ("Sincronizza solo utenti e gruppi assegnati") (scelta consigliata), verranno sincronizzati solo gli utenti e i gruppi assegnati nella scheda **Utenti e gruppi**.
12. Al termine della configurazione, impostare lo **Stato del provisioning** su **Sì**.
13. Fare clic su **Salva** per avviare il servizio di provisioning di Azure AD. 
14. Se si sceglie di sincronizzare solo gli utenti e i gruppi assegnati (scelta consigliata), assicurarsi di selezionare la scheda **Utenti e gruppi** e di assegnare gli utenti e/o i gruppi che si vuole sincronizzare.

Dopo aver avviato la sincronizzazione iniziale, è possibile usare la scheda **Log di controllo** per monitorare lo stato di avanzamento, che mostra tutte le azioni eseguite dal servizio di provisioning sull'app. Per altre informazioni sulla lettura dei log di provisioning di Azure AD, vedere l'esercitazione relativa alla [creazione di report sul provisioning automatico degli account utente](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

Il passaggio finale della verifica dell'esempio consiste nell'aprire il file TargetFile.csv nella cartella \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug del computer Windows. Dopo l'esecuzione del processo di provisioning, questo file include i dettagli di tutti gli utenti e gruppi assegnati e sottoposti a provisioning.

### <a name="development-libraries"></a>Librerie di sviluppo
Per sviluppare un servizio Web personalizzato conforme alla specifica SCIM, è necessario prima di tutto acquisire familiarità con le librerie Microsoft seguenti per accelerare il processo di sviluppo: 

1. Le librerie CLI (Common Language Infrastructure) vengono messe a disposizione per essere usate con linguaggi basati su questa infrastruttura, ad esempio C#. Una di queste librerie, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), dichiara un'interfaccia, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, illustrata nella figura seguente. Uno sviluppatore che usa le librerie implementerà questa interfaccia con una classe a cui è possibile fare riferimento, in modo generico, come provider. Le librerie consentono agli sviluppatori di distribuire un servizio Web conforme alla specifica SCIM, che può essere ospitato sia in Internet Information Services sia in qualsiasi assembly Common Language Infrastructure eseguibile. La richiesta viene convertita in chiamate ai metodi del provider, che saranno programmate dallo sviluppatore per agire su un archivio identità.
  
  ![][3]
  
2. I [gestori di ExpressRoute](http://expressjs.com/guide/routing.html) sono disponibili per l'analisi di oggetti richiesta node.js che rappresentano chiamate, in base alla definizione della specifica SCIM, effettuate a un servizio Web node.js.   

### <a name="building-a-custom-scim-endpoint"></a>Creazione di un endpoint SCIM personalizzato
Usando le librerie CLI, gli sviluppatori possono ospitare i servizi in un assembly Common Language Infrastructure eseguibile o in Internet Information Services. Ecco un codice di esempio per l'hosting di un servizio in un assembly eseguibile all'indirizzo http://localhost:9000: 

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

Questo servizio deve avere un indirizzo HTTP e un certificato di autenticazione server la cui autorità di certificazione radice è una delle seguenti: 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Go Daddy
* Verisign
* WoSign

Un certificato di autenticazione server può essere associato a una porta su un host Windows usando l'utilità shell di rete: 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

Il valore fornito per l'argomento certhash è l'identificazione personale del certificato, mentre il valore specificato per l'argomento appid è un identificatore univoco globale arbitrario.  

Per ospitare il servizio in Internet Information Services, uno sviluppatore deve creare un assembly della libreria di codice CLA con una classe denominata Startup nello spazio dei nomi predefinito dell'assembly.  Ecco un esempio di questa classe: 

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
Le richieste da Azure Active Directory includono un token di connessione OAuth 2.0.   Qualsiasi servizio che riceve la richiesta deve autenticare l'emittente come Azure Active Directory per conto del tenant Azure Active Directory previsto, per l'accesso al servizio Web Graph di Azure Active Directory.  Nel token l'emittente viene identificato da un'attestazione iss, ad esempio, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".  In questo esempio, l'indirizzo di base del valore dell'attestazione, https://sts.windows.net, identifica Azure Active Directory come autorità di certificazione, mentre il segmento dell'indirizzo relativo, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, è un identificatore univoco del tenant di Azure Active Directory per conto del quale è stato emesso il token.  Se il token è stato emesso per l'accesso al servizio Web Graph di Azure Active Directory, l'identificatore di quel servizio, 00000002-0000-0000-c000-000000000000, deve essere incluso nel valore dell'attestazione aud del token.  

Gli sviluppatori che usano le librerie CLA fornite da Microsoft per la creazione di un servizio SCIM possono autenticare le richieste da Azure Active Directory mediante il pacchetto Microsoft.Owin.Security.ActiveDirectory seguendo questa procedura: 

1. In un provider implementare la proprietà Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior facendo in modo che restituisca un metodo da chiamare ogni volta che viene avviato il servizio: 

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

2. Aggiungere il codice seguente al metodo, in modo che qualsiasi richiesta a uno degli endpoint del servizio venga autenticata come se includesse un token emesso da Azure Active Directory per conto di un tenant specifico, per l'accesso al servizio Web Graph di Azure AD: 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>Schema di utenti e gruppi
Azure Active Directory può effettuare il provisioning di due tipi di risorse nei servizi Web SCIM,  ovvero utenti e gruppi.  

Le risorse utente sono rilevate dall'identificatore dello schema, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, incluso in questa specifica del protocollo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.  Il mapping predefinito degli attributi degli utenti in Azure Active Directory agli attributi delle risorse urn:ietf:params:scim:schemas:extension:enterprise:2.0:User è disponibile nella tabella 1 seguente.  

Le risorse gruppo sono identificate dall'identificatore dello schema, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  La tabella 2 seguente illustra il mapping predefinito degli attributi di gruppi di Azure Active Directory agli attributi delle risorse http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  

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
La figura seguente illustra i messaggi che Azure Active Directory invia al servizio SCIM per gestire il ciclo di vita di un utente in un altro archivio identità. Il diagramma illustra anche il modo in cui un servizio SCIM implementato mediante le librerie CLI fornite da Microsoft per la creazione di questi servizi converte queste richieste in chiamate ai metodi di un provider.  

![][4]
*Figura 5: Sequenza di provisioning e deprovisioning utenti*

1. Azure Active Directory esegue query nel servizio per trovare un utente con valore dell'attributo externalId corrispondente al valore dell'attributo mailNickname di un utente in Azure AD. La query viene espressa come richiesta HTTP (Hypertext Transfer Protocol) analoga a quella dell'esempio, dove jyoung è un esempio di mailNickname di un utente in Azure Active Directory: 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Se il servizio è stato creato mediante le librerie Common Language Infrastructure fornite da Microsoft per implementare i servizi SCIM, la richiesta viene convertita in una chiamata al metodo Query del provider del servizio.  Ecco la firma del metodo: 
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
  Ecco la definizione dell'interfaccia Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters: 
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
  Nell'esempio seguente di una query per un utente con un determinato valore per l'attributo externalId, i valori degli argomenti passati al metodo Query sono: 
  * parameters.AlternateFilters.Count: 1
  * parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"
  * parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"] 

2. Se la risposta a una query sul servizio Web per cercare un utente con valore dell'attributo externalId corrispondente al valore dell'attributo mailNickname di un utente non restituisce alcun utente, Azure Active Directory richiede che il servizio effettui il provisioning di un utente corrispondente a quello in Azure Active Directory.  Ecco un esempio di questa richiesta: 
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
  Le librerie Common Language Infrastructure fornite da Microsoft per implementare servizi SCIM convertiranno tale richiesta in una chiamata al metodo Create del provider del servizio.  Il metodo Create ha la firma seguente: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  In una richiesta di provisioning di un utente, il valore dell'argomento resource è un'istanza della classe Microsoft.SystemForCrossDomainIdentityManagement. Core2EnterpriseUser, definita nella libreria Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  Se la richiesta di provisioning dell'utente ha esito positivo, si prevede che l'implementazione del metodo restituisca un'istanza di Microsoft.SystemForCrossDomainIdentityManagement. Core2EnterpriseUser, con il valore della proprietà Identifier impostato sull'identificatore univoco dell'utente appena sottoposto a provisioning.  

3. Per aggiornare un utente la cui esistenza è nota in un archivio identità gestito da SCIM, Azure Active Directory richiede al servizio lo stato corrente dell'utente con una richiesta simile alla seguente: 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  In un servizio creato mediante le librerie Common Language Infrastructure fornite da Microsoft per implementare i servizi SCIM, la richiesta viene convertita in una chiamata al metodo Retrieve del provider del servizio.  Ecco la firma del metodo Retrieve: 
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
  Nell'esempio di una richiesta per recuperare lo stato corrente di un utente, i valori delle proprietà dell'oggetto fornito come valore dell'argomento parameters sono analoghi ai seguenti: 
  
  * Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. Se è necessario aggiornare un attributo reference, Azure Active Directory esegue query sul servizio per determinare se il valore corrente dell'attributo reference nell'archivio identità gestito dal servizio corrisponde già al valore dell'attributo in Azure Active Directory. Per gli utenti, l'unico attributo il cui valore corrente viene sottoposto a query con questa modalità è l'attributo manager. Ecco un esempio di una richiesta per determinare se l'attributo manager di un oggetto utente specifico ha attualmente un determinato valore: 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  Il valore del parametro attributes della query, id, indica che se esiste un oggetto utente che soddisfa l'espressione fornita come valore del parametro filter della query, il servizio dovrà rispondere con una risorsa urn:ietf:params:scim:schemas:core:2.0:User o urn:ietf:params:scim:schemas:extension:enterprise:2.0:User che include solo il valore dell'attributo id della risorsa.  Il valore dell'attributo **id** è noto al richiedente, poiché è incluso nel valore del parametro filter della query. Il valore viene chiesto per potere richiedere una rappresentazione minima di una risorsa che soddisfa l'espressione di filtro come indicazione dell'eventuale esistenza di questo oggetto.   

  Se il servizio è stato creato mediante le librerie Common Language Infrastructure fornite da Microsoft per implementare i servizi SCIM, la richiesta viene convertita in una chiamata al metodo Query del provider del servizio. Il valore delle proprietà dell'oggetto fornito come valore dell'argomento parameters è analogo al seguente: 
  
  * parameters.AlternateFilters.Count: 2
  * parameters.AlternateFilters.ElementAt(x).AttributePath: "id"
  * parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"
  * parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * parameters.RequestedAttributePaths.ElementAt(0): "id"
  * parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

  Il valore dell'indice x può essere 0 e il valore dell'indice y può essere 1 oppure il valore di x può essere 1 e il valore di y può essere 0, in base all'ordine delle espressioni del parametro filter della query.   

5. Ecco un esempio di una richiesta di Azure Active Directory a un servizio SCIM per l'aggiornamento di un utente: 
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
  Le librerie Microsoft Common Language Infrastructure per implementare servizi SCIM convertiranno la richiesta in una chiamata al metodo Update del provider del servizio. Questa è la firma del metodo Update: 
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
    Nell'esempio di una richiesta per l'aggiornamento di un utente, i valori delle proprietà dell'oggetto fornito come valore dell'argomento patch sono analoghi ai seguenti: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest as PatchRequest2).Operations.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646

6. Per effettuare il deprovisioning di un utente da un archivio identità gestito da un servizio SCIM, Azure Active Directory invia una richiesta simile alla seguente: 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Se il servizio è stato creato mediante le librerie Common Language Infrastructure fornite da Microsoft per implementare i servizi SCIM, la richiesta viene convertita in una chiamata al metodo Delete del provider del servizio.   Il metodo ha la firma seguente: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  Nell'esempio di una richiesta per il deprovisioning di un utente, i valori delle proprietà dell'oggetto fornito come valore dell'argomento resourceIdentifier sono analoghi ai seguenti: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>Provisioning e deprovisioning gruppi
La figura seguente illustra i messaggi che Azure AD invia al servizio SCIM per gestire il ciclo di vita di un gruppo in un altro archivio identità.  Questi messaggi si differenziano dai messaggi relativi agli utenti in tre modi: 

* Lo schema di una risorsa gruppo viene identificato come http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  
* Le richieste per il recupero di gruppi stipulano che l'attributo members deve essere escluso da qualsiasi risorsa fornita in risposta alla richiesta.  
* Le richieste per determinare se un attributo reference ha un determinato valore sono richieste relative all'attributo members.  

![][5]
*Figura 6: Sequenza di provisioning e deprovisioning gruppi*

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Automatizzare il provisioning e il deprovisioning utenti in app SaaS](active-directory-saas-app-provisioning.md)
* [Personalizzazione dei mapping degli attributi per il Provisioning dell’utente](active-directory-saas-customizing-attribute-mappings.md)
* [Scrittura di espressioni per i mapping degli attributi](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Ambito dei filtri per il Provisioning utente](active-directory-saas-scoping-filters.md)
* [Notifiche relative al provisioning dell'account](active-directory-saas-account-provisioning-notifications.md)
* [Elenco di esercitazioni pratiche sulla procedura di integrazione delle applicazioni SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
