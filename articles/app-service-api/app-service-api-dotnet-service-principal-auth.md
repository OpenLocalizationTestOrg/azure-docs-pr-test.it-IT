---
title: l'autenticazione principale per App per le API in Azure App Service aaaService | Documenti Microsoft
description: Informazioni su come app tooprotect un'API in Azure App Service per gli scenari servizio-servizio.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Autenticazione dell'entità servizio per app per le API nel servizio app di Azure
## <a name="overview"></a>Panoramica
Questo articolo viene illustrato come l'autenticazione di servizio App toouse per *interno* accedere alle App tooAPI. Uno scenario interno è in cui si dispone di un'app di API che si desidera toobe utilizzabile solo dal codice dell'applicazione. Hello consigliato tooimplement modo questo scenario nel servizio App è hello tooprotect toouse AD Azure chiamato app per le API. Chiamare app per le API hello protetto con un token di connessione che si ottiene da Azure AD, fornendo le credenziali (entità servizio) di identità dell'applicazione. Per alternative toousing Azure AD, vedere hello **authentication Service to service** sezione di hello [panoramica dell'autenticazione del servizio App di Azure](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

In questo articolo si apprenderà:

* Accesso non autenticato come toouse Azure Active Directory (Azure AD) tooprotect un'API dell'applicazione.
* Modalità app tooconsume un'API protetta da un'app per le API, app web o app per dispositivi mobili utilizzando le credenziali di identità (identità applicazione) del servizio di Azure AD. Per informazioni su come tooconsume da un'app di logica, vedere [utilizzando l'API personalizzata ospitato nel servizio App con la logica app](../logic-apps/logic-apps-custom-hosted-api.md).
* Come toomake che tale hello protetto app per le API non può essere chiamato da un browser, gli utenti collegati.
* Come si toomake che tale hello protetto app per le API possa solo essere chiamato da uno specifico dell'entità servizio di Azure AD.

Hello articolo sono contenute due sezioni:

* Hello [come tooconfigure servizio di autenticazione principale in Azure App Service](#authconfig) sezione viene illustrato in generale come autenticazione tooconfigure per qualsiasi app per le API e come tooconsume hello protetto app per le API. In questa sezione si applica equamente tooall Framework supportato dal servizio App, inclusi .NET, Node.js e Java.
* A partire da hello [continuare esercitazioni su Guida introduttiva di .NET hello](#tutorialstart) sezione hello esercitazione viene illustrato uno scenario di "accesso interno" per un'applicazione di esempio .NET in esecuzione nel servizio App di configurazione. 

## <a id="authconfig"></a>Come tooconfigure servizio di autenticazione principale in Azure App Service
In questa sezione fornisce istruzioni generali valide tooany API app. Per passaggi specifici toohello tooDo applicazione di esempio elenco .NET, andare troppo[continuare serie di esercitazioni di App per le API .NET di hello](#tutorialstart).

1. In hello [portale di Azure](https://portal.azure.com/), passare toohello **impostazioni** pannello App hello API che si desidera tooprotect e quindi trovare hello **funzionalità** sezione e fare clic su **Autenticazione / autorizzazione**.
   
    ![Autenticazione/Autorizzazione nel portale di Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. In hello **autenticazione / autorizzazione** pannello, fare clic su **su**.
3. In hello **tootake azione quando la richiesta non è autenticata** elenco a discesa, seleziona **Accedi con Azure Active Directory** .
4. In **Provider di autenticazione** fare clic su **Azure Active Directory**.
   
    ![Pannello Autenticazione/Autorizzazione nel portale di Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Configurare hello **impostazioni di Azure Active Directory** pannello toocreate una nuova versione di Azure AD applicazione o utilizzare un'applicazione Azure AD esistente se si dispone già di uno che si desidera toouse.
   
    Gli scenari interni in genere comprendono un'app per le API che chiama un'app per le API. È possibile usare applicazioni Azure AD separate per ogni app per le API o una sola applicazione Azure AD.
   
    Per istruzioni dettagliate su questo pannello, vedere [come tooconfigure l'accesso di Azure Active Directory di servizio App applicazione toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Al pannello di configurazione del provider di autenticazione hello termine, fare clic su **OK**.
7. In hello **autenticazione / autorizzazione** pannello, fare clic su **salvare**.
   
    ![Fare clic su Salva.](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Quando questa operazione viene eseguita, servizio App consente solo le richieste dai chiamanti nel tenant di Azure AD hello configurato. In app per le API hello protetto, non è necessario alcun codice di autenticazione o autorizzazione. Hello token di connessione viene passato toohello API app insieme attestazioni comunemente utilizzate nelle intestazioni HTTP, ed è possibile leggere le informazioni nel codice toovalidate che sono richieste da un chiamante specifico, ad esempio un'entità servizio.

Questa funzionalità di autenticazione funziona hello allo stesso modo per tutte le lingue che il servizio App supporta, tra cui .NET, Node.js e Java. 

#### <a name="how-tooconsume-hello-protected-api-app"></a>Modalità di protezione delle app per le API tooconsume hello
chiamante Hello è necessario fornire un token di connessione di Azure AD con le chiamate API. tooget un token di connessione utilizzando le credenziali dell'entità servizio, il chiamante di hello utilizza Active Directory Authentication Library (ADAL per [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), o [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). tooget un token, codice hello che chiama ADAL fornisce hello tooADAL le seguenti informazioni:

* nome Hello del tenant di Azure AD.
* Hello client ID e client segreto (chiave app) di app hello Azure AD associata al chiamante di hello.
* ID client Hello di applicazione di Azure AD associata hello hello protetto app per le API. (Se viene utilizzata una sola applicazione di Azure AD, questo è hello lo stesso ID client come hello uno per il chiamante di hello.)

Questi valori sono disponibili nelle pagine di hello Azure AD di hello [portale di Azure classico](https://manage.windowsazure.com/).

Dopo che sono stati acquisiti i token hello, chiamante hello sono incluse le richieste HTTP nell'intestazione di autorizzazione hello.  Servizio App convalida token hello e consente di hello tooreach le richieste di hello protetto app per le API.

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>Modalità app hello API tooprotect dall'accesso di utenti in hello stesso tenant
I token di connessione per gli utenti di hello stesso tenant sono considerati validi per hello protetto app per le API.  Se si desidera tooensure che è possibile chiamare solo un'entità di servizio app API protetta hello, aggiungere il codice in hello protetto hello di toovalidate API app seguendo le attestazioni del token hello:

* `appid`deve essere l'ID client hello di un'applicazione hello Azure AD associata al chiamante di hello. 
* `oid`(`objectidentifier`) deve essere l'ID di entità servizio hello del chiamante hello. 

Servizio App fornisce anche hello `objectidentifier` attestazione nell'intestazione X-MS-CLIENT--ID entità hello.

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>Come tooprotect hello app per le API di accesso del browser
Se si non convalida le attestazioni presenti nel codice di app per le API hello protetti e, se si utilizza un oggetto separato applicazione Azure AD per hello protetto API app, assicurarsi che tale hello URL di risposta dell'applicazione Azure AD è hello non uguali a quelli hello URL di base dell'app per le API. Se hello URL di risposta punta direttamente app per le API toohello protetto, un utente nel tenant di hello stesso Azure Active Directory potrebbe individuare app per le API toohello, accedere e chiamare correttamente hello API.

## <a id="tutorialstart"></a>Serie di esercitazioni di hello App per le API .NET di continuare
Se si segue hello Node.js o Java serie di esercitazioni per App per le API, ignorare toohello [passaggi successivi](#next-steps) sezione. 

resto Hello di questo articolo continua serie di esercitazioni di App per le API .NET di hello e si presuppone che siano state completate hello [esercitazione autenticazione utente](app-service-api-dotnet-user-principal-auth.md) e applicazione di esempio hello in esecuzione in Azure con l'autenticazione utente abilitata.

## <a name="set-up-authentication-in-azure"></a>Configurare l'autenticazione in Azure
In questa sezione Configura servizio App in modo tale hello solo HTTP richiede consente tooreach hello dati livello app per le API sono quelli in cui Azure valido hello i token di connessione Active Directory. 

Nella seguente sezione di hello, configurare hello API di livello intermedio app toosend applicazione credenziali tooAzure Active Directory, ottenere un token di connessione e inviare connessione hello toohello token dati livello API app. Questo processo è illustrato nel diagramma di hello.

![Diagramma di autenticazione del servizio](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Se si verificano problemi durante le direzioni dell'esercitazione di hello seguenti, vedere hello [Troubleshooting](#troubleshooting) sezione alla fine di hello dell'esercitazione hello. 

1. In hello [portale di Azure](https://portal.azure.com/), passare toohello **impostazioni** pannello App hello API creato per app di API hello ToDoListDataAPI (livello di dati) e quindi fare clic su **impostazioni**.
2. In hello **impostazioni** blade, hello trova **funzionalità** sezione e quindi fare clic su **autenticazione / autorizzazione**.
   
    ![Autenticazione/Autorizzazione nel portale di Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. In hello **autenticazione / autorizzazione** pannello, fare clic su **su**.
4. In hello **tootake azione quando la richiesta non è autenticata** elenco a discesa, seleziona **Accedi con Azure Active Directory**.
   
    Questo è l'impostazione di hello che causa tooensure di servizio App che ha autenticato solo app per le API hello richieste reach. Per le richieste che hanno i token di connessione valida, passa il token hello lungo toohello API app servizio App e popola le intestazioni HTTP con toomake attestazioni diffuse informazioni codice tooyour più facilmente disponibile.
5. In **Provider di autenticazione** fare clic su **Azure Active Directory**.
   
    ![Pannello Autenticazione/Autorizzazione nel portale di Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. In hello **impostazioni di Azure Active Directory** pannello, fare clic su **Express**.
   
    Con hello **Express** opzione Azure è possibile creare automaticamente un'applicazione AAD in Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Non è necessario toocreate un tenant, perché ogni account di Azure dispone automaticamente di uno.
7. In **Modalità di gestione** fare clic su **Crea nuova app AD** se questa opzione non è già selezionata.
   
    portale Hello inserisce hello **creare App** casella di input con un valore predefinito. Per impostazione predefinita, viene denominato hello applicazione AD Azure stesso hello come applicazione hello API. Se si preferisce, è possibile immettere un nome diverso.
   
    ![Impostazioni di Azure AD](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Nota**: in alternativa, è possibile usare un singola AD Azure dell'applicazione per entrambi hello app per chiamare le API e hello protetti app per le API. Se si sceglie tale alternativa, è necessario non hello **Crea nuova App AD** opzione qui perché già stato creato in precedenza nell'esercitazione di autenticazione utente hello un'applicazione Azure AD. Per questa esercitazione, si userà separare applicazioni Azure AD per la chiamata di app per le API e hello hello protetto app per le API.
8. Prendere nota del valore di hello in hello **creare App** casella di input; verrà cercato questa applicazione AAD nella hello portale di Azure classico in un secondo momento.
9. Fare clic su **OK**.
10. In hello **autenticazione / autorizzazione** pannello, fare clic su **salvare**.
    
    ![Fare clic su Salva.](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    Servizio App viene creata un'applicazione di Azure Active Directory con **Sign-on URL** e **URL di risposta** impostata automaticamente toohello URL dell'app per le API. valore di quest'ultimo Hello consente agli utenti nel toolog tenant AAD in e accesso hello API app.

### <a name="verify-that-hello-api-app-is-protected"></a>Verificare che app hello API sia protetto
1. In un browser andare toohello URL dell'app hello API: in hello **app per le API** pannello in hello portale di Azure, fare clic su collegamento hello in **URL**. 
   
    Si è reindirizzato tooa schermata di accesso perché le richieste non autenticate non sono consentite tooreach hello API app. 
   
    Se il browser passare toohello Swagger dell'interfaccia utente, il browser potrebbe già essere connessi - in questo caso, aprire una finestra InPrivate o Incognito e passare toohello URL Swagger di interfaccia utente.
2. Accedere con le credenziali di un utente che appartiene al tenant AAD.
   
   Quando si accede, hello "completata" pagina viene visualizzata nel browser hello.

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Configurare hello ToDoListAPI progetto tooacquire e inviare il token di Azure AD hello
In questa sezione hello quanto segue:

* Aggiungere codice nell'app di API di livello intermedio hello che utilizza Azure AD applicazione credenziali tooacquire un token e inviare che con HTTP richiede toohello dati livello API app.
* Ottenere le credenziali di hello che è necessario da Azure AD.
* Immettere le credenziali di hello in impostazioni di ambiente di runtime di servizio App di Azure nel livello intermedio hello app per le API. 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Configurare hello ToDoListAPI progetto tooacquire e inviare il token di Azure AD hello
Rendere hello dopo le modifiche apportate hello ToDoListAPI progetto in Visual Studio.

1. Rimuovere il commento tutto il codice hello in hello *ServicePrincipal.cs* file.
   
    Si tratta di codice hello Usa ADAL per i token di connessione .NET tooacquire hello Azure AD.  Usa diversi valori di configurazione che verrà impostata nell'ambiente di runtime Azure hello in un secondo momento. Ecco il codice hello: 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **Nota:** questo codice richiede hello ADAL per il pacchetto NuGet di .NET (ActiveDirectory), che è già installato nel progetto hello. Se si crea il progetto da zero, sarebbe necessario tooinstall questo pacchetto. Questo pacchetto non viene installato automaticamente dal modello nuovo progetto applicazione di hello API.
2. In *controller/ToDoListController*, rimuovere il commento di codice hello in hello `NewDataAPIClient` metodo che aggiunge le richieste di token tooHTTP hello nell'intestazione di autorizzazione hello.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Distribuire il progetto di ToDoListAPI hello. (Fare clic sul progetto hello, quindi fare clic su **pubblica > Pubblica**.)
   
    Visual Studio distribuisce il progetto hello e apre l'URL di base dell'app di web toohello browser. Verranno visualizzati una pagina di 403 errore, che è norma per un tentativo di toogo tooa API Web URL di base da un browser.
4. Browser hello Chiudi.

### <a name="get-azure-ad-configuration-values"></a>Ottenere i valori di configurazione di Azure AD
1. In hello [portale di Azure classico](https://manage.windowsazure.com/), andare troppo**Azure Active Directory**.
2. In hello **Directory** scheda, fare clic su tenant di AAD.
3. Fare clic su **applicazioni > applicazioni proprietà dell'azienda**, quindi fare clic su hello segno di spunta.
4. Nell'elenco di hello delle applicazioni, fare clic su nome hello di hello Azure creata automaticamente quando è abilitata l'autenticazione per app di API hello ToDoListDataAPI (livello di dati).
5. Fare clic su hello **configura** scheda.
6. Hello copia **ID Client** valore e salvare identificabile da ottenere più tardi. 
7. Nel portale di Azure classico hello tornare indietro elenco toohello di **applicazioni proprietà dell'azienda**, fare clic su un'applicazione AAD hello creato per app ToDoListAPI API di livello intermedio hello (Buongiorno uno creato nell'esercitazione precedente hello, non Hello uno creato in questa esercitazione).
8. Fare clic su hello **configura** scheda.
9. Hello copia **ID Client** valore e salvare identificabile da ottenere più tardi.
10. In **chiavi**selezionare **1 anno** da hello **Seleziona durata** elenco a discesa.
11. Fare clic su **Salva**.
    
     ![Generare una chiave dell'app](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Copia valore chiave hello e salvarlo identificabile da ottenere più tardi.
    
     ![Copiare una nuova chiave dell'app](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>Configurare le impostazioni di Azure AD nell'ambiente di runtime dell'applicazione di livello intermedio API hello
1. Passare toohello [portale di Azure](https://portal.azure.com/), quindi passare toohello **App per le API** pannello per l'applicazione hello API che ospita il progetto di TodoListAPI (intermedio) hello.
2. Fare clic su **Impostazioni > Impostazioni applicazione**.
3. In hello **impostazioni App** sezione, aggiungere chiavi e valori di hello seguenti:
   
   | **Chiave** | ida:Authority |
   | --- | --- |
   | **Valore** |https://login.microsoftonline.com/{your Azure AD tenant name} |
   | **Esempio** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Chiave** | ida:ClientId |
   | --- | --- |
   | **Valore** |ID client dell'hello chiamano l'applicazione (livello intermedio - ToDoListAPI) |
   | **Esempio** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Chiave** | ida:ClientSecret |
   | --- | --- |
   | **Valore** |Chiave dell'app di hello chiamano l'applicazione (livello intermedio - ToDoListAPI) |
   | **Esempio** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Chiave** | ida:Resource |
   | --- | --- |
   | **Valore** |ID client di chiamare l'applicazione hello (livello di dati - ToDoListDataAPI) |
   | **Esempio** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Nota**: per `ida:Resource`, assicurarsi di utilizzare una chiamata dell'applicazione hello **ID client** e non il relativo **URI ID App**.
   
    `ida:ClientId`e `ida:Resource` sono diversi valori per questa esercitazione, poiché si utilizza separano applicaations AD Azure di livello intermedio hello e il livello dati. Se si utilizza una singola applicazione di Azure AD per la chiamata di app per le API e hello hello protetto app per le API, si utilizzerebbe hello stesso valore in entrambi `ida:ClientId` e `ida:Resource`.
   
    codice Hello Usa ConfigurationManager tooget questi valori, quindi può essere archiviate nel file Web. config del progetto hello o nell'ambiente di runtime Azure hello. Mentre un'applicazione ASP.NET è in esecuzione nel servizio app di Azure, le impostazioni dell'ambiente eseguono automaticamente l'override delle impostazioni di Web.config. Le impostazioni di ambiente sono in genere un [le informazioni riservate più sicure modo toostore rispetto a file Web. config tooa](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Fare clic su **Salva**.
   
    ![Fare clic su Salva.](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>Testare l'applicazione hello
1. In un browser andare toohello URL HTTPS di hello AngularJS front-end web app.
2. Fare clic su hello **tooDo elenco** scheda e accedere con le credenziali per un utente nel tenant di Azure AD. 
3. Aggiungere attività elementi tooverify che un'applicazione hello sia in esecuzione.
   
    ![pagina di elenco tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Se un'applicazione hello non funziona come previsto, verificare le impostazioni di hello che immesso nel portale di Azure hello. Se vengono visualizzate tutte le impostazioni di hello toobe corretto, vedere hello [Troubleshooting](#troubleshooting) sezione più avanti in questa esercitazione.

## <a name="protect-hello-api-app-from-browser-access"></a>Proteggere app per le API hello dall'accesso di browser
Per questa esercitazione è stato creato un apposito applicazione Azure AD per l'applicazione hello API ToDoListDataAPI (livello di dati). Come si è visto, quando il servizio App viene creata un'applicazione di AAD, in modo che consente a URL di un utente toogo toohello app per le API in un browser e accedere in Configura applicazione AAD hello. Pertanto, è possibile che un utente finale nel tenant di Azure AD, non solo un'entità di servizio, tooaccess hello API. 

Se si desidera l'accesso al browser tooprevent senza scrivere alcun codice in hello protetti app per le API, è possibile modificare hello **URL di risposta** nell'applicazione AAD hello in modo che sia diverso da dell'applicazione hello API URL di base. 

### <a name="disable-browser-access"></a>Disabilitare l'accesso dal browser
1. In un portale classico hello **configura** per un'applicazione AAD hello che è stata creata per hello TodoListService scheda, modificare il valore di hello in hello **URL di risposta** campo in modo che sia un URL valido ma non hello API dell'applicazione URL.
2. Fare clic su **Salva**.

### <a name="verify-browser-access-no-longer-works"></a>Verificare che non sia più possibile accedere dal browser
Si è verificato in precedenza che è possibile passare l'URL dell'app toohello API da un browser mediante l'accesso con credenziali di un singolo utente. In questa sezione si verifica che non sia più possibile. 

1. In una nuova finestra del browser, passare toohello URL dell'app per le API hello.
2. Quando l'accesso richiesto toodo così.
3. Account di accesso ha esito positivo, ma provoca tooan pagina di errore.
   
    App AAD hello configurati in modo che gli utenti nel tenant AAD hello non possono accedere e accedere hello API da un browser. È comunque possibile accedere applicazione API hello utilizzando un token dell'entità servizio, è possibile verificare che l'URL dell'app web toohello e l'aggiunta di altre attività da svolgere.

## <a name="restrict-access-tooa-particular-service-principal"></a>Limitare l'accesso tooa particolare SPN
Attualmente, qualsiasi chiamante che è possibile ottenere un token per un utente o dell'entità servizio nel tenant di Azure AD può chiamare l'applicazione hello API TodoListDataAPI (livello di dati). È possibile che tale app per le API livello dati hello accetta chiamate da app per le API (intermedio) TodoListAPI hello e solo da un'entità servizio particolare solo toomake. 

È possibile aggiungere queste restrizioni aggiungendo hello toovalidate codice `appid` e `objectidentifier` attestazioni su chiamate in ingresso.

Per questa esercitazione è inserire codice hello che convalida l'ID dell'app e l'ID dell'entità servizio direttamente nelle azioni del controller.  Sono disponibili alternative toouse personalizzato `Authorize` attributo o toodo la convalida nelle sequenze di avvio (ad esempio, il middleware OWIN). Per un esempio di hello quest'ultimo, vedere [questa applicazione di esempio](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Rendere hello seguente progetto TodoListDataAPI toohello di modifiche.

1. Aprire hello *Controllers/TodoListController.cs* file.
2. Rimuovi commento hello che impostare `trustedCallerClientId` e `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Rimuovere il commento di codice hello in hello CheckCallerId metodo. Questo metodo viene chiamato all'inizio di hello di ogni metodo di azione nel controller hello. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. Ridistribuire hello ToDoListDataAPI progetto tooAzure servizio App.
5. Nel browser, URL HTTPS dell'app di toohello AngularJS front-end web, scegliere nella home page di hello hello **tooDo elenco** scheda.
   
    un'applicazione Hello non funziona perché toohello nuovamente terminare le chiamate hanno esito negativo. nuovo codice Hello controllo appid effettivo e objectidentifier ma non è ancora hello valori corretti toocheck loro base. browser Hello Console degli strumenti per sviluppatori segnala che il server hello ha restituito un errore HTTP 401.
   
    ![Errore nella console degli strumenti di sviluppo](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    In hello alla procedura seguente verranno configurati i valori previsti hello.
6. Con Azure AD PowerShell, ottenere il valore di hello del servizio hello principale per l'applicazione Azure Active Directory creata per il progetto TodoListWebApp hello hello.
   
    a. Per istruzioni su come tooinstall Azure PowerShell e connettersi tooyour sottoscrizione, vedere [tramite Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).
   
    b. tooget un elenco delle entità servizio, eseguire hello `Login-AzureRmAccount` comando e quindi hello `Get-AzureRmADServicePrincipal` comando.
   
    c. Cercare hello objectid hello dell'entità servizio dell'applicazione TodoListAPI hello e salvarlo in una posizione in cui da che è possibile copiare in un secondo momento.
7. Nel portale di Azure hello, passare toohello API app pannello app hello API che è stato distribuito il progetto ToDoListDataAPI hello per.
8. Fare clic su **Impostazioni > Impostazioni applicazione**.
9. In hello **impostazioni App** sezione, aggiungere chiavi e valori di hello seguenti:
   
   | **Chiave** | todo:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Valore** |ID entità servizio dell'applicazione chiamante |
   | **Esempio** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Chiave** | todo:TrustedCallerClientId |
   | --- | --- |
   | **Valore** |ID client dell'applicazione - copiato dall'applicazione di Azure AD TodoListAPI hello chiamante |
   | **Esempio** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Fare clic su **Save**.
    
     ![Fare clic su Salva.](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. Nel browser, restituire l'URL dell'app web toohello e nella home page di hello fare clic su hello **tooDo elenco** scheda.
    
     Questa applicazione hello ora funziona come previsto perché i valori previsti hello hello chiamante attendibile app ID e l'ID dell'entità servizio.
    
     ![pagina di elenco tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>Compilazione di progetti hello da zero
progetti API Web Hello due sono stati creati tramite hello **Azure API App** progetto di modello e sostituendo i controller di valori predefinito hello con un controller elenco attività. Per acquisire token dell'entità servizio di Azure AD nel progetto ToDoListAPI hello, hello [Active Directory Authentication Library (ADAL) per .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) il pacchetto NuGet è stato installato.

Per informazioni sulla creazione di un'applicazione a pagina singola AngularJS troppo con un back-end di API Web come ToDoListAngular, vedere [mani nel Lab: creare un'applicazione a pagina singola (SPA) con ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Per informazioni su come tooadd il codice di autenticazione di Azure AD, vedere [protezione AngularJS singola pagina le app con Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Assicurarsi di non confondere ToDoListAPI (livello intermedio) e ToDoListDataAPI (livello dati). Ad esempio, in questa esercitazione è aggiungere app authentication toohello dati livello API **ma chiave dell'applicazione hello deve provenire da applicazione AD Azure creato per l'applicazione di livello intermedio API hello hello**.

## <a name="next-steps"></a>Passaggi successivi
Si tratta di esercitazione di ultima hello in hello serie di App per le API. 

Per ulteriori informazioni su Azure Active Directory, vedere hello seguenti risorse.

* [Guida per sviluppatori Azure AD](http://aka.ms/aaddev)
* [Scenari per Azure AD](http://aka.ms/aadscenarios)
* [Esempi di Azure AD](http://aka.ms/aadsamples)
  
    Hello [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) esempio è simile toowhat viene visualizzato in questa esercitazione, ma senza utilizzare l'autenticazione del servizio App.

Per informazioni su altri modi toodeploy Visual Studio progetti tooAPI App, tramite Visual Studio o [l'automatizzazione della distribuzione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) da un [sistema di controllo di origine](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), vedere [come toodeploy un Applicazione di servizio App di Azure](../app-service-web/web-sites-deploy.md).

