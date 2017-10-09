---
title: supporto aaaCORS nel servizio App | Documenti Microsoft
description: Informazioni di supporto delle toouse CORS in Azure App Service di Azure.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a>Utilizzare un'app per le API da JavaScript tramite CORS
Servizio App offre supporto incorporato per [tra condivisione risorse origini (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), che consente di JavaScript client toomake domini chiama tooAPIs che sono ospitati in App per le API. Servizio App consente di configurare CORS accesso tooyour API senza scrivere codice nell'API.

Questo articolo contiene due sezioni:

* Hello [come tooconfigure CORS](#corsconfig) sezione viene illustrato in generale come tooconfigure CORS per qualsiasi app per le API, l'app web o app per dispositivi mobili. Si applica ugualmente tooall Framework supportati dal servizio App, inclusi .NET, Node.js e Java. 
* A partire da hello [continuare esercitazioni su Guida introduttiva di .NET hello](#tutorialstart) sezione, articolo hello è un'esercitazione che illustra il supporto CORS dalla compilazione in quanto configurato nel [hello prima App per le API esercitazione introduttiva ](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>Come tooconfigure CORS nel servizio App di Azure
È possibile configurare CORS nel portale di Azure hello o utilizzando [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) strumenti.

#### <a name="configure-cors-in-hello-azure-portal"></a>Configurare CORS in hello portale di Azure
1. In un browser andare toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **servizi App**, quindi fare clic su nome hello dell'app per le API.
   
    ![Selezionare un'app per le API nel portale](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. In hello **impostazioni** pannello visualizzato a destra toohello di hello **app per le API** blade, hello trova **API** sezione e quindi fare clic su **CORS**.
   
   ![Selezionare CORS nel pannello Impostazioni](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Nella casella di testo hello immettere hello URL o URL che si desidera tooallow JavaScript chiamate toocome da.

    Ad esempio, se è stata distribuita l'app web di JavaScript applicazione tooa denominato todolistangular, immettere "https://todolistangular.azurewebsites.net". In alternativa, è possibile immettere toospecify un asterisco (*) che vengono accettati tutti i domini di origine.


1. Fare clic su **Salva**.
   
   ![Fare clic su Salva.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Dopo aver fatto clic **salvare**, hello API app accetterà JavaScript chiamate da hello specificato l'URL.

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>Configurare CORS con gli strumenti di Gestione risorse di Azure
È anche possibile configurare CORS per un'app per le API tramite [modelli di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md) in strumenti da riga di comando, ad esempio [Azure PowerShell](/powershell/azureps-cmdlets-docs) hello e [CLI di Azure](../cli-install-nodejs.md). 

Per un esempio di un modello di gestione risorse di Azure che consente di impostare proprietà CORS hello, aprire hello [file azuredeploy.json nel repository di hello per l'applicazione di esempio dell'esercitazione](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Individuare la sezione hello del modello di hello simile al seguente esempio hello:

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>Continuare l'esercitazione Introduzione a .NET di hello
Se si segue hello Node.js o Java introduttivi serie per App per le API, è necessario completata hello recupero serie avviata. Ignorare toohello [passaggi successivi](#next-steps) sezione toofind suggerimenti per l'apprendimento ulteriormente App per le API.

è una continuazione di hello serie introduttivi .NET Hello parte restante di questo articolo e si presuppone che sia completata correttamente [prima esercitazione hello](app-service-api-dotnet-get-started.md).

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>Distribuire hello ToDoListAngular progetto tooa nuova app web
In [prima esercitazione hello](app-service-api-dotnet-get-started.md), un'applicazione di livello intermedio API e un'app di API di livello dati sono stati creati. In questa esercitazione creerai un'app web di applicazione a pagina singola (SPA) hello chiamate API di livello intermedio app. È possibile hello SPA toowork tooenable CORS nel livello intermedio hello app per le API. 

In hello [l'applicazione di esempio ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), progetto ToDoListAngular hello è un semplice client AngularJS che chiama progetto API Web ToDoListAPI di livello intermedio hello. il codice JavaScript in hello Hello *app/scripts/todoListSvc.js* file chiama API hello utilizzando provider HTTP AngularJS hello. 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>Creare una nuova app web per il progetto ToDoListAngular hello
Hello procedure toocreate una nuova app web di servizio App e distribuire un progetto tooit è toowhat simile per cui si è visto [la creazione e distribuzione di un'applicazione API nella prima esercitazione di hello in questa serie](app-service-api-dotnet-get-started.md#createapiapp). è di sola differenza è il tipo di app hello Hello **App Web** anziché **App per le API**.  Per le catture di schermata delle finestre di dialogo hello, vedere 

1. In **Esplora**, fare clic sul progetto ToDoListAngular hello e quindi fare clic su **pubblica**.
2. In hello **profilo** scheda di hello **pubblica sul Web** procedura guidata, fare clic su **servizio App di Microsoft Azure**.
3. In hello **servizio App** la finestra di dialogo, fare clic su **New**.
4. In hello **Hosting** scheda di hello **Crea servizio App** finestra di dialogo immettere un **nome dell'applicazione Web** che sia univoco in hello *azurewebsites.net* dominio. 
5. Scegliere hello Azure **sottoscrizione** desiderato toowork con.
6. In hello **gruppo di risorse** elenco a discesa scegliere hello stesso gruppo di risorse creato in precedenza.
7. In hello **piano di servizio App** elenco a discesa scegliere hello stesso piano creato in precedenza. 
8. Fare clic su **Crea**.
   
    Visual Studio crea app web hello, crea un profilo di pubblicazione per tale e Visualizza hello **connessione** passaggio di hello **pubblica sul Web** procedura guidata.
   
    Non è ancora il momento di fare clic su **Pubblica** . Nella seguente sezione di hello, configurare hello nuova app toocall hello API di livello intermedio app web è in esecuzione nel servizio App. 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>Impostare l'URL di livello intermedio hello nelle impostazioni app web
1. Passare toohello [portale di Azure](https://portal.azure.com/), quindi passare toohello **App Web** pannello per l'app web hello creata dal progetto di toohost hello TodoListAngular (front-end).
2. Fare clic su **Impostazioni > Impostazioni applicazione**.
3. In hello **impostazioni App** sezione, aggiungere il seguente hello chiave e il valore:
   
   | Chiave | Valore | Esempio |
   | --- | --- | --- |
   | toDoListAPIURL |https://{nome dell'app per le API di livello intermedio}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. Fare clic su **Salva**.
   
    Quando l'esecuzione del codice hello in Azure, questo valore esegue l'override URL localhost hello in hello *Web. config* file. 
   
    codice Hello che ottiene il valore di impostazione hello è *cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    codice Hello *todoListSvc.js* Usa impostazione hello:
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>Distribuire hello ToDoListAngular web progetto toohello nuova app web
* In Visual Studio, in hello **connessione** passaggio di hello **pubblica sul Web** procedura guidata, fare clic su **pubblica**.
  
   Visual Studio distribuisce hello ToDoListAngular progetto toohello nuova app web e apre un browser toohello URL hello web app. 

### <a name="test-hello-application-without-cors-enabled"></a>Testare l'applicazione hello senza CORS abilitato
1. Nel browser gli strumenti di sviluppo, aprire la finestra di Console hello.
2. Nella finestra del browser hello che visualizza hello UI AngularJS, fare clic su hello **tooDo elenco** collegamento.
   
    Hello codice JavaScript tenta di livello intermedio toocall hello app per le API, ma hello riesce per mancanza di front-end hello è in esecuzione in un dominio diverso hello nuovamente finale. finestra di Console degli strumenti per sviluppatori del browser Hello viene visualizzato un messaggio di errore cross-origin.
   
    ![Messaggio di errore tra le origini](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>Configurare CORS per il livello intermedio di hello app per le API
In questa sezione, configurare impostazione di CORS hello in Azure per il livello intermedio di hello app ToDoListAPI API. Questa impostazione consentirà hello intermedio app tooreceive JavaScript chiamate all'API da un'app web hello creato per il progetto ToDoListAngular hello.

1. In un browser, visitare toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **servizi App**, quindi fare clic su app hello API ToDoListAPI (intermedio).
   
    ![Selezionare un'app per le API nel portale](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. In hello **impostazioni** pannello visualizzato a destra toohello di hello **app per le API** blade, hello trova **API** sezione e quindi fare clic su **CORS**.
   
   ![Selezionare CORS nel portale](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Nella casella di testo hello, immettere l'URL hello per l'app web di hello ToDoListAngular (front-end). Ad esempio, se è stata distribuita denominato todolistangular0121 hello ToDoListAngular progetto tooa web app, consentire chiamate dall'URL hello `https://todolistangular0121.azurewebsites.net`.
   
   In alternativa, è possibile immettere toospecify un asterisco (*) che vengono accettati tutti i domini di origine.
5. Fare clic su **Salva**.
   
   ![Fare clic su Salva.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Dopo aver fatto clic **salvare**, hello API app accetterà JavaScript chiamate da hello URL specificato. In questa schermata, hello ToDoListAPI0223 API app accetterà le chiamate client JavaScript da hello ToDoListAngular web app.

### <a name="test-hello-application-with-cors-enabled"></a>Testare l'applicazione hello con CORS abilitato
* Aprire un toohello browser URL HTTPS dell'app web hello. 
  
    Questa applicazione hello ora consente di visualizzare, aggiungere, modificare ed eliminare gli elementi di attività da eseguire. 
  
    ![pagina di elenco tooDo di app di esempio](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>CORS del servizio app e CORS di API Web
In un progetto di API Web, è possibile installare hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify pacchetto NuGet i domini che verranno accettate dall'API JavaScript chiamate dal codice.

Il supporto di CORS per l'API Web è più flessibile del supporto di CORS per il servizio app. Ad esempio, nel codice è possibile specificare origini accettate diverse a seconda del metodo di azione, mentre per CORS per il servizio app si specifica un set di origini accettate per tutti i metodi di un'app per le API.

> [!NOTE]
> Non tentare toouse sia Web API CORS e la condivisione CORS di servizio App in un'applicazione API. CORS per il servizio app avrà la precedenza e CORS per l'API Web non avrà effetto. Ad esempio, se si abilita un dominio di origine nel servizio App e abilitare tutti i domini di origine nel codice API Web, Azure API app accetterà solo le chiamate da dominio hello specificato in Azure.
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>Come tooenable CORS nel codice API Web
Hello passaggi riepiloga processo hello per abilitare il supporto di Web API CORS. Per altre informazioni, vedere l'articolo relativo all' [abilitazione della condivisione di richieste tra le origini nelle API Web ASP.NET 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

1. In un progetto di API Web, installare hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) pacchetto NuGet.
2. Includere un `config.EnableCors()` riga di codice hello **registrare** metodo hello **WebApiConfig** classe, come esempio hello di esempio seguente. 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. Nel controller di Web API, aggiungere un `using` istruzione per hello `System.Web.Http.Cors` dello spazio dei nomi e aggiungere hello `EnableCors` attributo toohello controller classe o tooindividual metodi di azione. Nell'esempio seguente di hello, supporto CORS applica toohello intera controller.
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>Uso di Gestione API di Azure con le app per le API
Se si utilizza Gestione API di Azure con un'applicazione API, configurare CORS in Gestione API anziché in app per le API hello. Per ulteriori informazioni, vedere hello seguenti risorse:

* [Panoramica di Gestione API di Azure (video: la sezione su CORS inizia al minuto 12:10)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [Criteri tra domini di Gestione API](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>Risoluzione dei problemi
In caso di problemi nel corso dell'esercitazione, ecco alcune idee per risolverli.

* Assicurarsi che si usi l'ultima versione di hello di hello [Azure SDK per .NET per Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).
* Assicurarsi di avere immesso `https` in hello impostazione CORS e assicurarsi che si usi `https` toorun hello front-end web app.
* Assicurarsi di avere immesso impostazione CORS hello in app hello per le API livello intermedio, non nell'applicazione web front-end hello.
* Se si configura la condivisione CORS nel codice dell'applicazione e servizio App di Azure, si noti che impostazione CORS del servizio App hello sostituiranno qualsiasi eseguite nel codice dell'applicazione. 

toolearn sulle funzionalità di Visual Studio che semplificano la risoluzione dei problemi, vedere [app di risoluzione dei problemi di servizio App di Azure in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è visto come tooenable CORS del servizio App supportano in modo che il codice JavaScript client può chiamare un'API in un dominio diverso. altre informazioni sulle App per le API, leggere hello toolearn [tooauthentication introduzione nel servizio App](../app-service/app-service-authentication-overview.md), quindi andare toohello [l'autenticazione utente per App per le API](app-service-api-dotnet-user-principal-auth.md) esercitazione.

