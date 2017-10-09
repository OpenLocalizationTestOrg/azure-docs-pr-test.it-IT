---
title: un'app di Azure line-of-business con l'autenticazione di ADFS aaaCreate | Documenti Microsoft
description: "Informazioni su come un'app line-of-business nel servizio App di Azure che esegue l'autenticazione con toocreate locale servizio token di sicurezza. In questa esercitazione è destinato AD FS come hello servizio token di sicurezza locale."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>Creare un'app line-of-business in Azure con l'autenticazione di AD FS
In questo articolo illustra come applicazione toocreate un ASP.NET MVC line-of-business in [Azure App Service](../app-service/app-service-value-prop-what-is.md) tramite un locale [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) come provider di identità hello. Questo scenario è possibile utilizzare quando si desidera che le applicazioni line-of-business toocreate in Azure App Service ma l'organizzazione richiede toobe di dati di directory archiviate localmente.

> [!NOTE]
> Per una panoramica delle opzioni hello enterprise diversi autenticazione e autorizzazione per il servizio App di Azure, vedere [autentica con locale di Active Directory in Azure app](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Obiettivo di compilazione
Si creerà un'applicazione ASP.NET di base nelle App Web di servizio App di Azure con hello seguenti caratteristiche:

* Autenticazione degli utenti in ADFS
* Usa `[Authorize]` utenti tooauthorize per azioni diverse
* Configurazione statica per il debug in Visual Studio e la pubblicazione del servizio Web App tooApp (configurare una sola volta, eseguire il debug e pubblicare in qualsiasi momento)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Elementi necessari
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

È necessario hello seguenti toocomplete questa esercitazione:

* Un locale di distribuzione di ADFS (per una procedura dettagliata end-to-end di testing hello utilizzati in questa esercitazione, vedere [Lab di Test: STS autonomo con AD FS in una macchina virtuale di Azure (solo per test)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* Trust di relying party di autorizzazioni toocreate in Gestione ADFS
* Visual Studio 2013 Update 4 o versione successiva
* [Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) o versioni successive

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Usare l'applicazione di esempio per il modello line-of-business
applicazione di esempio in questa esercitazione, Hello [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), viene creato dal team di Azure Active Directory hello. Poiché ADFS supporta WS-Federation, è possibile utilizzare come le applicazioni line-of-business toocreate un modello con facilità. Dispone di hello seguenti caratteristiche:

* Usa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate con un locale di distribuzione di ADFS
* Funzionalità di accesso e di disconnessione
* Usa [italiano](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (anziché Windows Identity Foundation), che è hello future di ASP.NET e tooset molto più semplice per l'autenticazione e autorizzazione di WIF

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>Configurare l'applicazione di esempio hello
1. Clona o download soluzione di esempio hello in [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour directory locale.
   
   > [!NOTE]
   > Hello istruzioni [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) illustrano come tooset di un'applicazione hello con Azure Active Directory. Ma in questa esercitazione, impostare con AD FS, quindi seguire questa procedura hello invece.
   > 
   > 
2. Aprire la soluzione hello e quindi aprire Controllers\AccountController.cs in hello **Esplora**.
   
   Si noterà che il codice hello genera semplicemente un autenticazione challenge tooauthenticate hello utente che utilizza WS-Federation. Tutte le autenticazioni sono configurate in App_Start\Startup.Auth.cs.
3. Aprire App_Start\Startup.Auth.cs. In hello `ConfigureAuth` (metodo), riga hello Nota:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   Nell'ambiente OWIN hello questo frammento è davvero hello bare che minimo è necessario l'autenticazione WS-Federation tooconfigure. È molto più semplice e più elegante di WIF, in Web. config viene inserito con XML in tutto a posto hello. Hello solo informazioni necessarie sono hello della relying party (RP) identificatore e hello dell'URL del file di metadati del servizio ADFS. Ad esempio:
   
   * Identificatore della relying party: `https://contoso.com/MyLOBApp`
   * Indirizzo dei metadati: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. In App_Start\Startup.Auth.cs, modificare le definizioni di stringa statica che seguono hello:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. A questo punto, è possibile apportare le modifiche corrispondenti di hello in Web. config. Aprire Web. config hello e modificare hello seguendo le impostazioni dell'app:  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   Inserire i valori di chiave hello in base all'ambiente corrispondente.
6. Toomake applicazione hello che non siano presenti errori di compilazione.

È tutto. Applicazione di esempio hello è ora pronto toowork con AD FS. È comunque necessario tooconfigure un trust della relying Party con questa applicazione in ADFS in un secondo momento.

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>Distribuire tooAzure applicazione di esempio hello App del servizio Web App
In questo caso, pubblicare app web di tooa applicazione hello in App del servizio Web App mantenendo l'ambiente di debug di hello. Si noti che si userà un'applicazione hello toopublish prima che abbia un trust della relying Party con AD FS, in modo autenticazione ancora non funziona ancora. Se si effettua questa ora si possono tuttavia avere hello URL dell'app web che è possibile utilizzare trust della relying Party tooconfigure hello in un secondo momento.

1. Fare clic con il pulsante destro del mouse sul progetto e scegliere **Pubblica**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Selezionare **Servizio app di Microsoft Azure**.
3. Se è ancora stato effettuato tooAzure, fare clic su **Accedi** e utilizzare l'account Microsoft hello per toosign la sottoscrizione di Azure in.
4. Una volta effettuato l'accesso, fare clic su **New** toocreate un'app web.
5. Compilare tutti i campi obbligatori. Si sta dati locali tooon tooconnect in un secondo momento, in modo da non creare un database per questa app web.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. Fare clic su **Crea**. Una volta creato l'app web hello, finestra di dialogo Pubblica sito Web hello viene aperto.
7. In **URL di destinazione**, modificare **http** troppo**https**. Copia hello intero URL tooa editor di testo per un uso successivo. Fare quindi clic su **Pubblica**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. In Visual Studio aprire **Web.Release.config** nel progetto. Inserisci hello seguente XML in hello `<configuration>` tag e sostituire l'URL dell'app web pubblica valore chiave hello.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

Al termine, si dispone di due identificatori RP configurati nel progetto, uno per l'ambiente di debug in Visual Studio, e uno per hello pubblicato app web in Azure. Si imposterà un trust della relying Party per ognuno dei due ambienti di hello in ADFS. Durante il debug, le impostazioni dell'app hello in Web. config vengono utilizzati toomake il **Debug** delle operazioni di configurazione con AD FS. Quando viene pubblicato (per impostazione predefinita, hello **versione** è pubblicato configurazione), viene caricato un file Web. config trasformato che incorpori le modifiche dell'impostazione applicazione hello in Web.Release.config.

Se si desidera tooattach hello web pubblicata app in Azure toohello debugger (ad esempio, è necessario caricare i simboli di debug del codice nell'applicazione web pubblicata hello), è possibile creare un clone di hello configurazione per il debug di Azure per il Debug, ma con il proprio file Web. config personalizzati trasformare ( ad esempio Web.AzureDebug.config) che utilizza le impostazioni dell'applicazione hello Web.Release.config. Ciò consente una configurazione statica toomaintain tra ambienti diversi hello.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Configurare l'attendibilità della relying party nel componente di gestione di ADFS
È ora necessario un trust della relying Party in Gestione ADFS tooconfigure prima di poter utilizzare l'applicazione di esempio ed effettivamente l'autenticazione con AD FS. Sarà necessario tooset i due trust relying Party separati, uno per l'ambiente di debug e uno per l'applicazione web pubblicata.

> [!NOTE]
> Assicurarsi che si ripetuta hello seguendo i passaggi per entrambi gli ambienti.
> 
> 

1. Nel server AD FS, accedere con le credenziali che dispongono di diritti di gestione tooAD ADFS.
2. Aprire il componente di gestione di ADFS. Fare clic con il pulsante destro del mouse su **AD FS\Relazioni di attendibilità\Attendibilità componente** e selezionare **Aggiungi attendibilità componente**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. In hello **Seleziona origine dati** selezionare **immettere manualmente i dati sulla relying party di hello**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. In hello **Specifica nome visualizzato** pagina, digitare un nome visualizzato per un'applicazione hello e fare clic su **Avanti**.
5. In hello **scegliere protocollo** pagina, fare clic su **Avanti**.
6. In hello **Configura certificato** pagina, fare clic su **Avanti**.
   
   > [!NOTE]
   > Poiché dovrebbe essere già in uso HTTPS, i token crittografati sono facoltativi. Se si vuole token tooencrypt da AD FS in questa pagina, è inoltre necessario aggiungere logica di decrittografia di token nel codice. Per altre informazioni, vedere il post sulla [configurazione manuale di middleware WS-Federation OWIN e sull'accettazione di token crittografati](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Prima di passare al passaggio successivo hello, è necessario un'informazione dal progetto di Visual Studio. Nelle proprietà del progetto hello, si noti hello **URL SSL** dell'applicazione hello. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. In Gestione ADFS, in hello **Configura URL** pagina di hello **Aggiunta guidata attendibilità componente**selezionare **abilitare il supporto per hello protocollo passivo WS-Federation** e digitare hello URL SSL del progetto di Visual Studio che si è preso nota nel passaggio precedente hello. Quindi fare clic su **Next**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > URL specifica in cui il client hello toosend dopo l'autenticazione ha esito positivo. Per l'ambiente di debug hello, dovrebbe essere <code>https://localhost:&lt;port&gt;/</code>. Per l'applicazione web pubblicata hello, dovrebbe essere hello URL dell'app web.
   > 
   > 
9. In hello **Configura identificatori** pagina, verificare che il progetto URL SSL è già configurato e fare clic su **Avanti**. Fare clic su **Avanti** tutti hello fine toohello modo della procedura guidata hello con le selezioni predefinite.
   
   > [!NOTE]
   > In App_Start\Startup.Auth.cs del progetto di Visual Studio, questo identificatore viene confrontato con il valore di hello di <code>WsFederationAuthenticationOptions.Wtrealm</code> durante l'autenticazione federata. Per impostazione predefinita, l'URL dell'applicazione hello dal passaggio precedente hello viene aggiunto come un identificatore della relying Party.
   > 
   > 
10. Completata la configurazione di hello applicazione relying Party per il progetto in ADFS. Successivamente, si configura questo toosend applicazione hello attestazioni richieste dall'applicazione. Hello **Modifica regole attestazione** finestra di dialogo è aperto per impostazione predefinita per l'utente alla fine di hello della procedura guidata hello in modo che è possibile iniziare immediatamente. Consente di configurare almeno hello seguenti attestazioni (con gli schemi tra parentesi):
    
    * Nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - utilizzato da ASP.NET toohydrate `User.Identity.Name`.
    * Utente il nome dell'entità (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - utilizzato toouniquely identificare gli utenti dell'organizzazione hello.
    * Appartenenze ai ruoli (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - può essere utilizzato con `[Authorize(Roles="role1, role2,...")]` decorazione tooauthorize controller/azioni. In realtà, questo approccio potrebbe non essere hello ad alte prestazioni la maggior parte delle autorizzazioni dei ruoli. Se gli utenti AD appartengono toohundreds dei gruppi di sicurezza, diventano centinaia di attestazioni di ruolo in token SAML hello. Un approccio alternativo è toosend un solo ruolo di attestazione in modo condizionale in base hello appartenenza in un determinato gruppo. Tuttavia, ai fini della presente esercitazione si manterrà una configurazione semplice.
    * ID nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) può essere usata per la convalida antifalsificazione. Per ulteriori informazioni su come toomake funziona con anti-falsificazione convalida, vedere hello **aggiungere funzionalità line-of-business** sezione [creare un'app di Azure line-of-business con l'autenticazione di Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > Hello tipi di attestazioni è necessario tooconfigure per l'applicazione è determinata dalle esigenze dell'applicazione. Per hello l'elenco di attestazioni supportati dalle applicazioni di Azure Active Directory (ad esempio i trust di relying Party), ad esempio, vedere [supportati Token e tipi di attestazione](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. Nella finestra di dialogo Modifica regole attestazione hello, fare clic su **Aggiungi regola**.
12. Configurare le attestazioni di nome UPN e ruolo hello, come illustrato nella schermata di hello e fare clic su **fine**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    Creare quindi un nome temporaneo ID attestazione utilizzando hello passaggi illustrati in [identificatori del nome di asserzioni SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Fare nuovamente clic su **Add Rule** .
14. Selezionare **Inviare attestazioni mediante una regola personalizzata** e fare clic su **Avanti**.
15. Linguaggio di regola seguente di hello Incolla in hello **regola personalizzata** casella, una regola di hello nome **per ogni identificatore di sessione** e fare clic su **fine**.  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    La regola personalizzata sarà simile allo screenshot seguente:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. Fare nuovamente clic su **Add Rule** .
17. Selezionare **Trasformare un'attestazione in ingresso** e fare clic su **Avanti**.
18. Configurare la regola di hello, come illustrato nella schermata di hello (utilizzando il tipo di attestazione hello è stato creato in una regola personalizzata hello) e fare clic su **fine**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Per informazioni dettagliate sui passaggi di hello di attestazione ID nome temporaneo hello, vedere [identificatori del nome di asserzioni SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Fare clic su **applica** in hello **Modifica regole attestazione** finestra di dialogo. Ora dovrebbe essere simile hello seguente schermata:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Assicurarsi di ripetere questi passaggi sia per l'ambiente di debug che per l'app Web pubblicata.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Testare l'autenticazione federata per la propria applicazione
Si sono pronti tootest la logica di autenticazione dell'applicazione in ADFS. Nel mio ambiente di laboratorio di ADFS, è necessario un utente di test a cui appartiene il gruppo di test tooa in Active Directory (AD).

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

autenticazione tootest nel debugger hello, è sufficiente toodo ora è di tipo `F5`. Se si desidera tootest autenticazione nell'applicazione web pubblicata hello, passare toohello URL.

Dopo il caricamento di un'applicazione hello web, fare clic su **Accedi**. Ora è necessario ottenere un account di accesso finestra di dialogo o hello account di accesso pagina servita da AD FS, in base al metodo di autenticazione hello scelto da ADFS. Di seguito è riportato ciò che viene visualizzato in Internet Explorer 11.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

Quando si accede con un account utente nel dominio hello Active Directory di distribuzione FS hello Active Directory, si dovrebbe essere hello home page con **Hello, <User Name>!** Nell'angolo hello. Questo è quanto viene visualizzato nell'ambiente di questo esempio.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

Fino a questo punto, una volta completata hello seguenti modi:

* L'applicazione ha raggiunto ADFS e un identificatore della relying Party corrispondente si trova in hello database AD FS
* ADFS è stato autenticato un utente di Active Directory e reindirizza la home page dell'applicazione toohello
* AD FS come nome hello inviati attestazione applicazione tooyour (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name), come indicato dal fatto di hello utente hello nome viene visualizzato nell'angolo hello. 

Se l'attestazione nome hello manca, si sarebbe verificato **Hello,!**. Se si osserva Views\Shared\_LoginPartial.cshtml, trovare che utilizza `User.Identity.Name` nome utente di toodisplay hello. Come accennato in precedenza, se l'attestazione nome hello di hello autenticata utente è disponibile nel token SAML hello, ASP.NET hydrates questa proprietà con esso. toosee che Hello tutte le attestazioni inviate da AD FS, inserire un punto di interruzione in controllers\homecontroller.cs., hello metodo di azione Index. Dopo l'autenticazione utente hello, controllare hello `System.Security.Claims.Current.Claims` insieme.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Autorizzare utenti per controller o azioni specifiche
Poiché sono stati inclusi appartenenze a gruppi come le attestazioni dei ruoli nella configurazione di trust della relying Party, è possibile utilizzarli direttamente in hello `[Authorize(Roles="...")]` decorazione per controller e azioni. In un'applicazione line-of-business con modello di hello crea-lettura, aggiornamento ed eliminazione (CRUD), è possibile autorizzare tooaccess ruoli specifici di ogni azione. Per il momento, è sufficiente verrà provare questa funzionalità sul controller Home esistente hello.

1. Aprire Controllers\HomeController.cs.
2. Decorare hello `About` e `Contact` azione metodi simili toohello seguente di codice, tramite l'appartenenza ai gruppi di sicurezza dell'utente autenticato.  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    Poiché è stato aggiunto **utente Test** troppo**gruppo di Test** nel mio ambiente di laboratorio di ADFS, si utilizzerà autorizzazione tootest gruppo di Test su `About`. Per `Contact`, verificherà hello negativo maiuscole **Domain Admins**, toowhich **utente Test** non appartiene.
3. Avviare il debugger hello digitando `F5` accedere, quindi fare clic su **su**. Si dovrebbe ora essere visualizzando hello `~/About/Index` pagina correttamente, se l'utente autenticato è autorizzato per l'azione.
4. Fare clic su **contatto**, che in questo caso non è necessario autorizzare **utente Test** per azione di hello. Tuttavia, i browser hello è reindirizzato tooAD ADFS, che viene infine illustrato questo messaggio:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    Se è esaminare l'errore nel Visualizzatore eventi sul server AD FS hello, viene visualizzato questo messaggio di eccezione:  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    motivo di Hello di questo errore è che per impostazione predefinita, MVC restituisce un 401 non autorizzato quando i ruoli di un utente non autorizzati. In questo modo viene attivato un provider di identità tooyour richiesta riautenticazione (AD FS). Dal momento che hello è già autenticato, ADFS restituisce toohello stessa pagina, che quindi pubblica 401 un'altra, la creazione di un ciclo di reindirizzamento. Si eseguirà l'override di AuthorizeAttribute `HandleUnauthorizedRequest` metodo con logica semplice tooshow un elemento che ha senso anziché ciclo di reindirizzamento hello continua.
5. Creare un file nel progetto hello chiamato AuthorizeAttribute.cs e Incolla hello seguente codice al suo interno.
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    Hello di eseguire l'override di codice inviato un HTTP 403 (accesso negato) invece di HTTP 401 (non autorizzato) in casi autenticati ma non autorizzati.
6. Eseguire il debugger hello con `F5`. Facendo clic su **Contact** verrà visualizzato un messaggio di errore più informativo (anche se graficamente meno elegante):
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Pubblicare nuovamente tooAzure applicazione hello App del servizio Web App e verificare il comportamento di hello di un'applicazione hello in tempo reale.

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>La connessione dati tooon locali
Un motivo che si tooimplement l'applicazione line-of-business con AD FS invece di Azure Active Directory è problemi di conformità del mantenimento dati dell'organizzazione non locali. Ciò significa anche che l'app web in Azure deve accedere ai database locali, perché non è consentito toouse [Database SQL](/services/sql-database/) come livello dati hello per le app web.

App Web del servizio app di Azure supporta l'accesso ai database locali tramite due approcci: [connessioni ibride](../biztalk-services/integration-hybrid-connection-overview.md) e [reti virtuali](web-sites-integrate-with-vnet.md). Per altre informazioni, vedere il post relativo all' [uso dell'integrazione con una rete virtuale e delle connessioni ibride con App Web del servizio app di Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Altre risorse
* [Eseguire l'autenticazione con l'istanza locale di Active Directory nell'app Azure](web-sites-authentication-authorization.md)
* [Creare un'app line-of-business in Azure con l'autenticazione di Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md)
* [Utilizzare l'opzione di autenticazione aziendale locale (ADFS) con ASP.NET hello in Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [Eseguire la migrazione di un tooKatana VS2013 progetto Web da WIF](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Informazioni generali su Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx)
* [Specifica WS-Federation 1.1](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

