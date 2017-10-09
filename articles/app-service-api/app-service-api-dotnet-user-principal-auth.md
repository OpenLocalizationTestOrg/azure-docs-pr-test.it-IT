---
title: autenticazione aaaUser per App per le API in Azure App Service | Documenti Microsoft
description: Informazioni su come un'app per le API nel servizio App di Azure, consentendo di tooprotect tooauthenticated solo utenti di accesso.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Autenticazione utente per le app per le API nel servizio app di Azure
## <a name="overview"></a>Panoramica
Questo articolo illustra come può essere chiamato tooprotect un'app per le API di Azure in modo che solo gli utenti autenticati. Hello articolo si presuppone di avere letto hello [panoramica dell'autenticazione del servizio App di Azure](../app-service/app-service-authentication-overview.md).

Si apprenderà come:

* Come tooconfigure un provider di autenticazione, con i dettagli per Azure Active Directory (Azure AD).
* Come tooconsume un'app di API protetta utilizzando hello [Active Directory Authentication Library (ADAL) per JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

Hello articolo sono contenute due sezioni:

* Hello [come l'autenticazione utente tooconfigure in Azure App Service](#authconfig) sezione viene illustrato in generale come tooconfigure l'autenticazione utente per qualsiasi app per le API e si applica equamente tooall Framework supportato dal servizio App, tra cui .NET, Node.js e Java.
* A partire da hello [continuare esercitazioni di App per le API .NET hello](#tutorialstart) sezione, hello Guide articolo tramite la configurazione di un'applicazione di esempio con .NET eseguire il fine e un front-end di AngularJS in modo che utilizzi Azure Active Directory per utente autenticazione. 

## <a id="authconfig"></a>Come l'autenticazione utente tooconfigure in Azure App Service
In questa sezione fornisce istruzioni generali valide tooany API app. Per passaggi specifici toohello tooDo applicazione di esempio elenco .NET, andare troppo[continuare esercitazioni su Guida introduttiva di .NET hello](#tutorialstart).

1. In hello [portale di Azure](https://portal.azure.com/), passare toohello **impostazioni** pannello App hello API che si desidera tooprotect, hello trova **funzionalità** sezione e quindi fare clic su  **Autenticazione / autorizzazione**.
   
    ![Autenticazione/Autorizzazione del portale di Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. In hello **autenticazione / autorizzazione** pannello, fare clic su **su**.
3. Selezionare una delle opzioni di hello hello **tootake azione quando la richiesta non è autenticata** elenco a discesa.
   
   * Se si desidera solo chiamate autenticate tooreach app per le API, scegliere una delle hello **Log con...**  opzioni. Questa opzione consente di tooprotect hello API app senza scrivere codice che viene eseguito in essa contenuti.
   * Se si desidera tooreach tutte le chiamate API app, scegliere **Consenti richiesta (alcuna azione)**. È possibile utilizzare questa opzione toodirect non autenticati chiamanti tooa scelta dei provider di autenticazione. Con questa opzione si dispone dell'autorizzazione di toohandle di toowrite codice.
     
     Per altre informazioni, vedere [Autenticazione e autorizzazione per app per le API nel servizio app di Azure](app-service-api-authentication.md#multiple-protection-options).
4. Selezionare uno o più di hello **provider di autenticazione**.
   
    immagine di Hello Mostra le scelte che richiedono tutti i chiamanti toobe autenticato da Azure AD.
   
    ![Pannello Autenticazione/Autorizzazione del portale di Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Quando si sceglie un provider di autenticazione, portale hello viene visualizzato un pannello di configurazione per il provider. 
   
    Per istruzioni dettagliate che illustrano come tooconfigure hello pannelli di configurazione del provider di autenticazione, vedere [come tooconfigure l'accesso di Azure Active Directory di servizio App applicazione toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (collegamento di hello viene tooan articolo su Azure AD, ma articolo hello stesso contiene schede che collegano tooarticles per hello altri provider di autenticazione).
5. Al pannello di configurazione del provider di autenticazione hello termine, fare clic su **OK**.
6. In hello **autenticazione / autorizzazione** pannello, fare clic su **salvare**.

Quando questa operazione viene eseguita, servizio App autentica tutte le chiamate API prima che raggiungano app hello per le API. lavoro di servizi di autenticazione Hello hello uguale per tutte le lingue supportate dal servizio App, inclusi .NET, Node.js e Java di. 

toomake autenticato chiamate API, chiamante hello include i token di connessione del provider di autenticazione hello OAuth 2.0 nell'intestazione di autorizzazione hello di richieste HTTP. token Hello possono essere acquisite tramite il SDK del provider di autenticazione hello.

## <a id="tutorialstart"></a>Esercitazioni di App per le API .NET hello continuare
Se si segue esercitazioni di Node.js o Java hello per le app di API, ignorare l'articolo successivo toohello, [l'autenticazione dell'entità servizio per App per le API](app-service-api-dotnet-service-principal-auth.md). 

Se si segue serie di esercitazioni hello .NET per App per le API e applicazione di esempio hello hanno già distribuito come indicato in hello [prima](app-service-api-dotnet-get-started.md) e [secondo](app-service-api-cors-consume-javascript.md) esercitazioni, ignorare toohello [impostare l'autenticazione in Azure AD e di servizio App](#azureauth) sezione.

Se si desidera toofollow questa esercitazione senza passare attraverso le esercitazioni di prima e seconda hello, hello seguendo i passaggi che illustrano la modalità di avvio tooget tramite un'applicazione di esempio hello toodeploy processo automatico.

> [!NOTE]
> Hello segue iniziare toohello punto di partenza stesso come se si hello prime due esercitazioni, con una sola eccezione: Visual Studio non sapranno già quali app web o app per le API che ogni progetto viene distribuito a. Pertanto, non sarà possibile le istruzioni esatte in questa esercitazione viene illustrato come destinazioni di destra toohello toodeploy. Se non si ha familiarità con pensare a come passaggi di distribuzione hello toodo autonomamente, è preferibile toofollow hello esercitazione serie hello [prima esercitazione](app-service-api-dotnet-get-started.md) di toostart con questo automatizzato il processo di distribuzione.
> 
> 

1. Assicurarsi di disporre di tutti i prerequisiti di hello elencati in hello [prima esercitazione](app-service-api-dotnet-get-started.md). In aggiunta toohello prerequisiti elencati queste esercitazioni autenticazione presuppongono che si ha familiarità con App del servizio web App e App in Visual Studio per le API e hello portale di Azure.
2. Fare clic su hello **distribuire tooAzure** pulsante hello [file Leggimi di tooDo elenco esempio repository](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) toodeploy hello API App e hello web app. Prendere nota del gruppo di risorse di Azure hello che viene creato, come è possibile usare questo toolook successive di app web e i nomi delle app di API.
3. Download o hello clone [repository di esempio elenco tooDo](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) codice hello tooget che verranno utilizzate in locale in Visual Studio.

## <a id="azureauth"></a> Configurare l'autenticazione nel servizio app e in Azure AD
È ora disponibile un'applicazione hello in esecuzione in Azure App Service senza richiedere che gli utenti autenticati. In questa sezione è aggiungere l'autenticazione in questo modo hello seguenti attività:

* Configurare l'autenticazione di Azure Active Directory (Azure AD) toorequire di servizio App per chiamare l'applicazione di livello intermedio API hello.
* Creare un'applicazione Azure AD.
* Configurare il token di connessione hello hello Azure AD applicazione toosend dopo front-end di accesso toohello AngularJS. 

Se si verificano problemi durante le direzioni dell'esercitazione di hello seguenti, vedere hello [Troubleshooting](#troubleshooting) sezione alla fine di hello dell'esercitazione hello. 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>Configurare l'autenticazione per il livello intermedio di hello app per le API
1. In hello [portale di Azure](https://portal.azure.com/), passare toohello **impostazioni** pannello dell'applicazione hello API che è stato creato per il progetto ToDoListAPI hello, trovare hello **funzionalità** sezione e quindi Fare clic su **autenticazione / autorizzazione**.
   
    ![Autenticazione/Autorizzazione del portale di Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. In hello **autenticazione / autorizzazione** pannello, fare clic su **su**.
3. In hello **tootake azione quando la richiesta non è autenticata** elenco a discesa, seleziona **Accedi con Azure Active Directory**.
   
    Questa opzione garantisce che nessuna richiesta unauathenticated raggiungerà app hello per le API. 
4. In **Provider di autenticazione** fare clic su **Azure Active Directory**.
   
    ![Pannello Autenticazione/Autorizzazione del portale di Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. In hello **impostazioni di Azure Active Directory** pannello, fare clic su **Express**
   
    ![Opzione Rapida di Autenticazione/Autorizzazione del portale di Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Con hello **Express** opzione servizio App può creare automaticamente un'applicazione Azure AD in Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Non è necessario toocreate un tenant, perché ogni account di Azure dispone automaticamente di uno.
6. In **modalità di gestione**, fare clic su **Crea nuova App AD** se non è già selezionata e osservare il valore hello in hello **creare App** casella di testo; è possibile cercare questo AAD applicazione hello portale di Azure classico in un secondo momento.
   
    ![Impostazioni di Azure AD del portale di Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure crea automaticamente un'applicazione Azure AD con hello nome indicato nel tenant di Azure AD. Per impostazione predefinita, viene denominato hello applicazione AD Azure stesso hello come applicazione hello API. Se si preferisce, è possibile immettere un nome diverso.
7. Fare clic su **OK**.
8. In hello **autenticazione / autorizzazione** pannello, fare clic su **salvare**.
   
    ![Fare clic su Salva.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Ora solo gli utenti nel tenant di Azure AD possono chiamare app hello per le API.

### <a name="optional-test-hello-api-app"></a>Facoltativo: Testare l'applicazione hello API
1. In un browser andare toohello URL dell'app hello API: in hello **app per le API** pannello in hello portale di Azure, fare clic su collegamento hello in **URL**.  
   
    Si è reindirizzato tooa schermata di accesso perché le richieste non autenticate non sono consentite tooreach hello API app.
   
    Se il browser passa pagina toohello "completata", il browser hello potrebbe già essere registrato, in tal caso, aprire una finestra InPrivate o Incognito e passare l'URL dell'app toohello API.
2. Accedere con le credenziali per un utente incluso nel tenant di Azure AD.
   
    Quando si accede, hello "completata" pagina viene visualizzata nel browser hello.
3. Browser hello Chiudi.

### <a name="configure-hello-azure-ad-application"></a>Configurare un'applicazione hello Azure AD
Quando è stata configurata l'autenticazione di Azure AD, il servizio app ha creato automaticamente un'applicazione Azure AD. Per impostazione predefinita un'applicazione hello nuovo Azure AD è stato configurato tooprovide hello connessione toohello token API URL dell'app. In questa sezione configurare hello Azure AD tooprovide hello connessione toohello token AngularJS front-end dell'applicazione anziché direttamente toohello intermedio API app. front-end di Hello AngularJS invierà hello toohello token API app durante la chiamata di app per le API hello.

> [!NOTE]
> processo di hello tookeep più semplice possibile, questa esercitazione viene utilizzato un singolo Azure AD applicazione per front-end hello e applicazione di livello intermedio API hello. Un'altra opzione è toouse due applicazioni di Azure AD. In questo caso sarebbe necessario di toogive hello front-end Azure AD applicazione autorizzazione toocall hello di Azure AD applicazione di livello intermedio. Questo approccio con più applicazione fornisce un controllo più granulare livello tooeach autorizzazioni.
> 
> 

1. In hello [portale di Azure classico](https://manage.windowsazure.com/), andare troppo**Azure Active Directory**.
   
   È necessario portale classico di hello toouse poiché alcune impostazioni di Azure Active Directory che è necessario accedere tooare non è ancora disponibile nel portale di Azure corrente hello.
2. In hello **Directory** scheda, fare clic su tenant di AAD.
   
   ![Azure AD nel portale classico](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Fare clic su **applicazioni > applicazioni proprietà dell'azienda**, quindi fare clic su hello segno di spunta.
   
   Potrebbe anche essere toorefresh hello pagina toosee hello nuova applicazione.
4. Nell'elenco di hello delle applicazioni, fare clic su nome hello di hello Azure creata automaticamente quando è abilitata l'autenticazione per l'app dell'API.
   
   ![Scheda Applicazioni Azure AD](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Fare clic su **Configure**.
   
   ![Scheda Configura di Azure AD](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Impostare **Sign-on URL** toohello URL per l'app web di AngularJS, nessuna barra finale.
   
   Immettere ad esempio https://todolistangular.azurewebsites.net
   
   ![URL di accesso](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Impostare **URL di risposta** toohello URL per l'app web, nessuna barra finale.
   
   Immettere ad esempio https://todolistsangular.azurewebsites.net
8. Fare clic su **Save**.
   
   ![URL di risposta](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. Nella parte inferiore di hello della pagina hello, fare clic su **Gestisci manifesto > Download manifesto**.
   
   ![Scaricare il manifesto](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Scaricare hello tooa percorso in cui è possibile modificarlo.
11. Nel file manifesto hello scaricato, cercare hello `oauth2AllowImplicitFlow` proprietà. Modificare il valore di hello di questa proprietà da `false` troppo`true`e quindi salvare il file hello.
    
    Questa impostazione è necessaria per l'accesso da un'applicazione a singola pagina JavaScript In questo modo hello Oauth 2.0 connessione toobe token restituito nel frammento di URL hello.
12. Fare clic su **Gestisci manifesto > caricamento manifesto**e caricare file hello aggiornato nel precedente passaggio hello.
    
    ![Caricare il manifesto](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Hello copia **ID Client** valore e salvarlo in un punto è possibile ottenere dalla in un secondo momento.

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>Configurare l'autenticazione di hello ToDoListAngular progetto toouse
In questa sezione si modificare front-end di hello AngularJS in modo che utilizzi Active Directory Authentication Library (ADAL) per JS tooacquire un token di connessione per hello effettuato l'accesso utente da Azure AD. codice Hello includerà token hello in richieste HTTP inviate toohello di livello intermedio, come illustrato nel seguente diagramma hello. 

![Diagramma di autenticazione utente](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Rendere hello seguente toofiles modifiche nel progetto ToDoListAngular hello.

1. Aprire hello *cshtml* file.
2. Rimuovere il commento righe hello che fanno riferimento a hello Active Directory Authentication Library (ADAL) per gli script JS.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Aprire hello *app/scripts/app.js* file.
4. Commento blocco hello di codice contrassegnata per "senza l'autenticazione" e rimuovere il commento blocco hello di codice contrassegnato per "con l'autenticazione".
   
    Questa modifica fa riferimento a provider di autenticazione ADAL JS hello e fornisce tooit valori di configurazione. In hello alla procedura seguente impostare i valori di configurazione hello per le app per le API e l'applicazione Azure AD.
5. Nel codice hello che imposta hello `endpoints` hello variabile, impostare l'URL dell'API toohello URL dell'API hello app creata per il progetto ToDoListAPI hello e impostare hello Azure AD ID toohello ID client applicazione copiata dal portale di Azure classico hello.
   
    codice Hello è ora simile toohello esempio seguente.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. In hello chiamare troppo`adalProvider.init`, impostare `tenant` nome tenant tooyour e `clientId` toosame valore utilizzato nel passaggio precedente hello.
   
    codice Hello è ora simile toohello esempio seguente.
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    Queste modifiche sono state troppo`app.js` specificare codice chiamante hello e hello chiamata API sono in un'applicazione hello stesso Azure Active Directory.
7. Aprire hello *app/scripts/homeCtrl.js* file.
8. Commento blocco hello di codice contrassegnata per "senza l'autenticazione" e rimuovere il commento blocco hello di codice contrassegnato per "con l'autenticazione".
9. Aprire hello *app/scripts/indexCtrl.js* file.
10. Commento blocco hello di codice contrassegnata per "senza l'autenticazione" e rimuovere il commento blocco hello di codice contrassegnato per "con l'autenticazione".

### <a name="deploy-hello-todolistangular-project-tooazure"></a>Distribuire hello ToDoListAngular progetto tooAzure
1. In **Esplora**, fare clic sul progetto ToDoListAngular hello e quindi fare clic su **pubblica**.
2. Fare clic su **Pubblica**.
   
    Visual Studio distribuisce il progetto hello e apre l'URL di base dell'app di web toohello browser. Verranno visualizzati una pagina di 403 errore, che è norma per un tentativo di toogo tooa API Web URL di base da un browser.
   
    È comunque necessario toomake un livello intermedio app per le API toohello di modifica prima di poter testare un'applicazione hello.
3. Browser hello Chiudi.

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>Configurare l'autenticazione di hello ToDoListAPI progetto toouse
Attualmente hello Invia progetto ToDoListAPI "*" come hello `owner` tooToDoListDataAPI valore. In questa sezione si modificare hello codice toosend hello ID dell'utente connesso di hello.

Rendere hello dopo le modifiche nel progetto ToDoListAPI hello.

1. Aprire hello *Controllers/ToDoListController.cs* file e rimuovere il commento riga hello in ogni metodo di azione che imposta `owner` toohello Azure AD `NameIdentifier` il valore dell'attestazione. ad esempio:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Importante**: non rimuovere il commento di codice in hello `ToDoListDataAPI` metodo; operazione dovrà essere effettuata in un secondo momento per l'esercitazione di autenticazione dell'entità servizio hello.

### <a name="deploy-hello-todolistapi-project-tooazure"></a>Distribuire hello ToDoListAPI progetto tooAzure
1. In **Esplora**, fare clic sul progetto ToDoListAPI hello e quindi fare clic su **pubblica**.
2. Fare clic su **Pubblica**.
   
    Visual Studio distribuisce il progetto hello e apre URL di base di un browser toohello app per le API.
3. Browser hello Chiudi.

### <a name="test-hello-application"></a>Testare l'applicazione hello
1. Vai a URL toohello dell'app web hello, **mediante HTTPS, non HTTP**.
2. Fare clic su hello **tooDo elenco** scheda.
   
    Si è richiesta toolog in.
3. Accedere con credenziali hello di un utente nel tenant di AAD.
4. Hello **tooDo elenco** verrà visualizzata la pagina.
   
   ![pagina di elenco tooDo](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Non vengono visualizzate attività perché fino a questo momento erano tutte per owner "*". Livello intermedio hello richiede ora gli elementi per l'utente connesso hello e non sono ancora stati creati.
5. Aggiungere nuovo tooverify gli elementi di attività che sia in esecuzione un'applicazione hello.
6. In un'altra finestra del browser toohello URL Swagger di interfaccia utente per app per le API di ToDoListDataAPI hello, fare clic su **ToDoList > ottenere**. Immettere un asterisco per hello `owner` parametro e quindi fare clic su **provarlo**.
   
   risposta Hello indica che gli elementi di attività nuova hello hanno ID utente hello Azure AD effettivo nella proprietà proprietario hello.
   
   ![ID proprietario nella risposta JSON](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>Compilazione di progetti hello da zero
progetti API Web Hello due sono stati creati tramite hello **Azure API App** progetto di modello e sostituendo i controller di valori predefinito hello con un controller elenco attività. 

Per informazioni sulla creazione di un'applicazione a pagina singola AngularJS troppo con un back-end Web API 2, vedere [mani nel Lab: creare un'applicazione a pagina singola (SPA) con ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Per informazioni su come tooadd il codice di autenticazione di Azure AD, vedere hello seguenti risorse:

* [Protezione di app AngularJS a singola pagina con Azure AD](../active-directory/active-directory-devquickstarts-angular.md).
* [Introduzione ad ADAL JS v1](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Risoluzione dei problemi
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Assicurarsi di non confondere ToDoListAPI (livello intermedio) e ToDoListDataAPI (livello dati). Ad esempio, verificare di aver aggiunto l'autenticazione toohello intermedio app per le API, non il livello di dati hello. 
* Assicurarsi che l'URL di app AngularJS origine codice riferimenti hello intermedio API hello (ToDoListAPI, non ToDoListDataAPI) e hello corretti ID client di Azure AD. 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato descritto come toouse l'autenticazione del servizio App per un'app per le API e come toocall hello app per le API tramite hello libreria ADAL JS. Nella prossima esercitazione hello si apprenderà come troppo[app tooyour API di accesso sicuro per gli scenari servizio-servizio](app-service-api-dotnet-service-principal-auth.md).

