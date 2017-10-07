---
title: aaaGet avviato con l'App per le API e ASP.NET nel servizio App | Documenti Microsoft
description: Informazioni su come toocreate, distribuire e usare un'app per le API di ASP.NET in Azure App Service, con Visual Studio 2015.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>Introduzione alle app per le API, ad ASP.NET e a Swagger in Servizio app di Azure
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

Si tratta hello prima in una serie di esercitazioni che mostrano come toouse funzionalità di Azure App Service che sono utili per lo sviluppo e l'API REST per l'hosting.  Questa esercitazione illustra il supporto per i metadati dell'API in formato Swagger.

Si apprenderà come:

* Come toocreate e distribuire [App per le API](app-service-api-apps-why-best-platform.md) nel servizio App di Azure utilizzando gli strumenti incorporati in Visual Studio 2015.
* La modalità individuazione tooautomate API tramite hello del pacchetto Swashbuckle NuGet toodynamically generare metadati Swagger API.
* Tooautomatically di metadati Swagger API toouse come generare codice client per un'app per le API.

## <a name="sample-application-overview"></a>Panoramica dell'applicazione di esempio
In questa esercitazione si usa una semplice applicazione di esempio di elenco attività. un'applicazione Hello dispone di un front-end dell'applicazione a pagina singola (SPA), un livello intermedio di ASP.NET Web API e un livello di dati di ASP.NET Web API.

![Diagramma dell'applicazione di esempio di app per le API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

Ecco una cattura di schermata di hello [AngularJS](https://angularjs.org/) front-end.

![Elenco di App per le API esempio applicazione toodo](./media/app-service-api-dotnet-get-started/todospa.png)

Hello soluzione di Visual Studio include tre progetti:

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -front-end hello: un SPA AngularJS che chiama intermedio hello.
* **ToDoListAPI** -intermedio hello: un progetto di API Web ASP.NET che chiama operazioni CRUD tooperform sugli elementi di attività di livello dati hello.
* **ToDoListDataAPI** -livello di dati hello: un progetto ASP.NET Web API che consente di eseguire operazioni CRUD sulle attività da svolgere.

architettura a tre livelli Hello è una delle molte architetture che è possibile implementare usando l'App per le API e viene usato solo per scopi dimostrativi. codice Hello in ogni livello è semplice come funzionalità di App per le API toodemonstrate possibili. ad esempio, il livello di dati hello utilizza la memoria del server invece di un database come meccanismo di persistenza.

Dopo aver completato questa esercitazione, è necessario hello due progetti di API Web di e in esecuzione nel cloud hello in App per le API di servizio App.

esercitazione successiva di Hello in serie hello distribuisce cloud toohello di hello SPA front-end.

## <a name="prerequisites"></a>Prerequisiti
* ASP.NET Web API - istruzioni delle esercitazioni hello si supponga di abbia una conoscenza di base come toowork con ASP.NET [API Web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.
* Account Azure: è possibile [aprire un account Azure gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) o [attivare i benefici della sottoscrizione di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
  
    Se si desidera tooget avviato con il servizio App di Azure prima di iscriversi per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/). In questa pagina è possibile creare immediatamente un'app iniziale temporanea nel servizio app, **senza carta di credito**e senza impegno.
* Visual Studio 2015 con hello [Azure SDK per .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK viene installato Visual Studio 2015 automaticamente se non si dispone già.
  
  * In Visual Studio fare clic su ? -> Informazioni su Microsoft Visual Studio e assicurarsi di aver installato "Strumenti del servizio app di Azure versione 2.9.1" o versioni successive.
    
    ![Versione di Strumenti del servizio app di Azure](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > A seconda di quanti le dipendenze del SDK hello già presenti nel computer, l'installazione hello SDK potrebbe richiedere molto tempo, da alcuni minuti tooa mezz'ora o più.
    > 
    > 

## <a name="download-hello-sample-application"></a>Scaricare l'applicazione di esempio hello
1. Scaricare hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.
   
    È possibile fare clic su hello **ZIP di Download** pulsante o clone repository hello sul computer locale.
2. Aprire hello ToDoList soluzione in Visual Studio 2015 o 2013.
   
   1. È necessario tootrust ciascuna soluzione.
         ![Avviso di sicurezza](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. Compilazione dei pacchetti NuGet di hello toorestore di hello soluzioni (CTRL + MAIUSC + B).
   
    Se si desidera un'applicazione hello toosee nell'operazione prima della distribuzione, è possibile eseguire in locale. Assicurarsi che ToDoListDataAPI sia il progetto di avvio e la soluzione hello esecuzione. È necessario prevedere un HTTP 403 toosee errore nel browser.

## <a name="use-swagger-api-metadata-and-ui"></a>Usare l'interfaccia utente e i metadati dell'API Swagger
Il supporto per i metadati dell'API [Swagger](http://swagger.io/) 2.0 è integrato nel servizio app di Azure. Ogni app per le API è possibile specificare un endpoint dell'URL che restituisce i metadati per hello API in formato JSON Swagger. Hello metadati restituiti da tale endpoint possono essere utilizzato il codice client toogenerate.

Un progetto ASP.NET Web API possa generare in modo dinamico i metadati Swagger utilizzando hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) pacchetto NuGet. pacchetto Swashbuckle NuGet Hello è già installato in hello ToDoListDataAPI ToDoListAPI i progetti e che è stato scaricato.

In questa sezione dell'esercitazione hello, si esamina i metadati di Swagger 2.0 hello generato e quindi si tenta una prova dell'interfaccia utente che si basa sui metadati di Swagger hello.

1. Impostare il progetto di ToDoListDataAPI hello (**non** progetto ToDoListAPI hello) come progetto di avvio hello.
   
    ![Impostare ToDoDataAPI come progetto di avvio](./media/app-service-api-dotnet-get-started/startupproject.png)
2. Premere F5 o fare clic su **Debug > Avvia debug** progetto hello toorun in modalità di debug.
   
    browser Hello viene visualizzata la pagina di errore HTTP 403 hello.
3. Nella barra degli indirizzi del browser, aggiungere `swagger/docs/v1` toohello fine riga hello e quindi premere INVIO. (hello URL `http://localhost:45914/swagger/docs/v1`.)
   
    Si tratta di hello URL predefinito dai metadati di Swagger 2.0 JSON tooreturn Swashbuckle per hello API.
   
    Se si utilizza Internet Explorer, hello chiesto toodownload un *v1.json* file.
   
    ![Scaricare i metadati JSON in Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    Se si usa Chrome, Firefox o Edge, hello JSON browser hello Visualizza nella finestra del browser hello. Diversi browser gestiscono JSON in modo diverso, e la finestra del browser potrebbe non apparire esattamente come esempio hello.
   
    ![Metadati JSON in Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    Hello esempio seguente viene mostrata hello prima sezione di metadati Swagger hello per hello API, con la definizione di hello per hello Get (metodo). Questi metadati sono quali hello unità Swagger dell'interfaccia utente che si utilizza in hello seguendo i passaggi e utilizzare in una sezione successiva di hello esercitazione tooautomatically genera il codice client.
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. Chiudere il browser hello e arrestare il debug di Visual Studio.
5. In hello ToDoListDataAPI progetto **Esplora**aprire hello *App_Start\SwaggerConfig.cs* file, quindi scorrere verso il basso tooline 174 e rimuovere il commento hello seguente codice.
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    Hello *SwaggerConfig.cs* file viene creato quando si installa il pacchetto di Swashbuckle hello in un progetto. file Hello fornisce una serie di modi tooconfigure Swashbuckle.
   
    codice Hello che è stata non commentata hello Abilita UI Swagger utilizzato in hello seguendo i passaggi. Quando si crea un progetto di API Web utilizzando il modello di progetto applicazione hello API, questo codice è commentato per impostazione predefinita come misura di sicurezza.
6. Eseguire nuovamente il progetto di hello.
7. Nella barra degli indirizzi del browser, aggiungere `swagger` toohello fine riga hello e quindi premere INVIO. (hello URL `http://localhost:45914/swagger`.)
8. Quando viene visualizzata la pagina di hello Swagger dell'interfaccia utente, fare clic su **ToDoList** metodi hello toosee disponibili.
   
    ![Metodi disponibili dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. Fare clic su hello innanzitutto **ottenere** pulsante nell'elenco di hello.
10. In hello **parametri** sezione, immettere un asterisco come valore hello hello `owner` parametro e quindi fare clic su **provarlo**.
    
    Quando si aggiunge l'autenticazione nelle esercitazioni successive, il livello intermedio hello fornirà livello di dati toohello ID utente effettivo hello. Per il momento, tutte le attività avranno asterisco come l'ID del proprietario durante l'esecuzione di un'applicazione hello senza abilitata l'autenticazione.
    
    ![Prova dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    Hello Swagger dell'interfaccia utente chiama il metodo ToDoList Get hello e visualizza il codice di risposta hello e risultati JSON.
    
    ![Risultati della prova dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. Fare clic su **Post**e quindi fare clic sulla casella hello in **lo Schema del modello**.
    
    Fare clic su hello modello schema prefills hello casella di input in cui è possibile specificare il valore di parametro hello per hello metodo Post. (Se il problema persiste in Internet Explorer, utilizzare un browser diverso o immettere manualmente il valore di parametro hello nel passaggio successivo hello.)  
    
    ![Post della prova dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/post.png)
12. Ciao modifica JSON hello `todo` un parametro di input in modo che risulti simile al seguente esempio hello o di sostituire il testo di descrizione:
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. Fare clic su **Try it out**.
    
    Hello ToDoList API restituisce un codice di risposta HTTP 204 che indica l'esito positivo.
14. Fare clic su hello innanzitutto **ottenere** pulsante e quindi fare clic su hello in questa sezione della pagina hello **provarlo** pulsante.
    
    risposta al metodo Get Hello include ora il nuovo elemento di toodo hello.
15. Facoltativo: Provare inoltre Put, Delete, hello e ottenere dai metodi di ID.
16. Chiudere il browser hello e arrestare il debug di Visual Studio.

Swashbuckle funziona con qualsiasi progetto API Web ASP.NET. Se si desidera tooadd Swagger metadati generazione tooan esistente, è sufficiente installare il pacchetto di Swashbuckle hello.

> [!NOTE]
> I metadati di Swagger includono un ID univoco per ogni operazione API. Per impostazione predefinita, Swashbuckle può generare ID operazione di Swagger duplicati per i metodi del controller dell'API Web. Ciò si verifica se il controller presenta metodi di overload HTTP, ad esempio `Get()` e `Get(id)`. Per informazioni su come toohandle overload, vedere [definizioni generato personalizzare Swashbuckle API](app-service-api-dotnet-swashbuckle-customize.md). Se si crea un progetto di API Web in Visual Studio usando il modello di Azure API App hello, che genera gli ID di operazione univoco viene aggiunto codice automaticamente toohello *SwaggerConfig.cs* file.  
> 
> 

## <a id="createapiapp"></a>Creare un'app per le API in Azure e distribuire codice tooit
In questa sezione, utilizzare gli strumenti di Azure che sono integrati in Visual Studio hello **pubblica sul Web** guidata toocreate una nuova API app in Azure. Quindi si distribuisce hello ToDoListDataAPI progetto toohello nuova API app e chiamare l'API di hello eseguendo hello Swagger dell'interfaccia utente.

1. In **Esplora**, fare clic sul progetto ToDoListDataAPI hello e quindi fare clic su **pubblica**.
   
    ![Fare clic su Pubblica in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. In hello **profilo** passaggio di hello **pubblica sul Web** procedura guidata, fare clic su **servizio App di Microsoft Azure**.
   
   ![Fare clic su Servizio app di Azure in Pubblica sul Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. Accedi a tooyour account Azure, se non è già stato fatto, o aggiornare le credenziali se si scadute.
4. In hello la finestra di dialogo di servizio App, scegliere hello Azure **sottoscrizione** toouse desiderato e quindi fare clic su **New**.
   
    ![Fare clic su Nuovo nella finestra di dialogo Servizio app](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    Hello **Hosting** scheda di hello **Crea servizio App** viene visualizzata la finestra di dialogo.
   
    Poiché si distribuisce un progetto di API Web che ha installato Swashbuckle, Visual Studio si presuppone che un'App per le API toocreate. In questo caso viene hello **API App Name** title e da hello delle tabelle dei fatti che hello **Modifica tipo** riepilogo è stato impostato troppo**App per le API**.
   
    ![Tipo di app nella finestra di dialogo Servizio app](./media/app-service-api-dotnet-get-started/apptype.png)
5. Immettere un **API App Name** che sia univoco in hello *azurewebsites.net* dominio. È possibile accettare nome predefinito hello che si propone di Visual Studio.
   
    Se si immette un nome di un altro utente ha già in uso, viene visualizzato un diritto toohello punto esclamativo rosso.
   
    Hello URL dell'app hello API sarà `{API app name}.azurewebsites.net`.
6. In hello **gruppo di risorse** fare clic su elenco a discesa **New**, quindi immettere "ToDoListGroup" o un altro nome se si preferisce.
   
    Un gruppo di risorse è una raccolta di risorse di Azure, ad esempio app per le api, database, VM e così via.    Per questa esercitazione, è migliore toocreate un nuovo gruppo di risorse perché che rende facile toodelete in un unico passaggio, che tutte le risorse di Azure creato per l'esercitazione hello di hello.
   
    Questa casella consente di selezionare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) esistente o crearne uno nuovo digitando un nome diverso da qualsiasi gruppo di risorse esistente nella sottoscrizione.
7. Fare clic su hello **New** pulsante Avanti toohello **piano di servizio App** elenco a discesa.
   
    cattura di schermata Hello Mostra i valori di esempio per **API App Name**, **sottoscrizione**, e **gruppo di risorse** -i valori saranno diversi.
   
    ![Finestra di dialogo Crea servizio app](./media/app-service-api-dotnet-get-started/createas.png)
   
    In hello alla procedura seguente creare un piano di servizio App per il nuovo gruppo di risorse hello. Un piano di servizio App specifica le risorse di calcolo hello utilizzabile con app per le API. Ad esempio, se si sceglie di livello gratuito hello, app per le API viene eseguito in macchine virtuali condivisione, mentre per alcuni livelli a pagamento è in esecuzione nelle macchine virtuali dedicate. Per altre informazioni sui piani di servizio app, vedere [Panoramica approfondita dei piani del servizio app di Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
8. In hello **configurare il piano di servizio App** finestra di dialogo, immettere "ToDoListPlan" o un altro nome se si preferisce.
9. In hello **percorso** elenco a discesa scegliere percorso hello tooyou più vicino.
   
    Questa impostazione specifica il data center di Azure in cui verrà eseguita l'app. Scegliere un percorso chiudere tooyou toominimize [latenza](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).
10. In hello **dimensioni** fare clic su elenco a discesa **libero**.
    
    Per questa esercitazione, hello disponibile a livello di prezzo fornisca prestazioni insufficienti.
11. In hello **configurare il piano di servizio App** finestra di dialogo, fare clic su **OK**.
    
    ![Fare clic su OK in Configura piano di servizio app](./media/app-service-api-dotnet-get-started/configasp.png)
12. In hello **Crea servizio App** la finestra di dialogo, fare clic su **crea**.
    
    ![Fare clic su Crea nella finestra di dialogo Crea servizio app](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Visual Studio crea app hello per le API e un profilo di pubblicazione che dispone di tutte le impostazioni di hello necessario per l'applicazione hello API. Apre hello **pubblica sul Web** guidata, si userà progetto hello toodeploy.
    
    Hello **pubblica sul Web** guidato su hello **connessione** scheda (mostrata sotto).
    
    In hello **connessione** scheda hello **Server** e **nome sito** impostazioni punto tooyour API app. Hello **nome utente** e **Password** sono le credenziali di distribuzione Azure crea automaticamente. Dopo la distribuzione, Visual Studio apre un browser toohello **URL di destinazione** (che è l'unico scopo di hello per **URL di destinazione**).  
13. Fare clic su **Avanti**.
    
    ![Fare clic su Avanti nella scheda Connessione di Pubblica sito Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    scheda successiva Hello è hello **impostazioni** scheda (mostrata sotto). Qui è possibile modificare hello compilazione configurazione scheda toodeploy una build di debug per [il debug remoto](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug). Hello scheda offre inoltre diversi **Opzioni pubblicazione File**:
    
    * Rimuovi i file aggiuntivi nella destinazione
    * Precompila durante la pubblicazione
    * Escludi file dalla cartella App_Data hello
    
    Per questa esercitazione non ne è necessaria nessuna. Per una descrizione dettagliata del funzionamento di queste opzioni, vedere [Procedura: Distribuire un progetto di applicazione Web tramite la pubblicazione con un clic in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).
14. Fare clic su **Avanti**.
    
    ![Fare clic su Avanti nella scheda Impostazioni di Pubblica sito Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    Di seguito è riportato hello **anteprima** scheda (mostrata sotto), che consente un'opportunità toosee quali file verranno copiati dal progetto toohello API app toobe. Quando si distribuisce un progetto di app tooan API che è già stato distribuito tooearlier, vengono copiati solo i file modificati. Se si desidera un elenco di ciò che verrà copiato toosee, è possibile fare clic su hello **avviare Anteprima** pulsante.
15. Fare clic su **Pubblica**.
    
    ![Fare clic su Pubblica nella scheda Anteprima di Pubblica sito Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    Visual Studio distribuisce hello ToDoListDataAPI progetto toohello nuova app per le API. Hello **Output** finestra registri di distribuzione ha esito positivo e viene visualizzata una pagina "è stata creata" in un URL di toohello finestra aperta del browser di applicazione hello API.
    
    ![Finestra di output che segnala che la distribuzione è completata](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Pagina che segnala che la creazione dell'app per le API è completata](./media/app-service-api-dotnet-get-started/appcreated.png)
16. Aggiungere "swagger" toohello URL nella barra degli indirizzi del browser hello e quindi premere INVIO. (hello URL `http://{apiappname}.azurewebsites.net/swagger`.)
    
    browser Hello Visualizza hello stesso Swagger dell'interfaccia utente che è stato illustrato in precedenza, ma ora è in esecuzione nel cloud hello. Provare hello metodo Get, e viene visualizzato che hai toohello indietro predefinito 2 attività da svolgere. modifiche di Hello apportate in precedenza sono state salvate in memoria nel computer locale hello.
17. Aprire hello [portale di Azure](https://portal.azure.com/).
    
    Hello portale di Azure è un'interfaccia web per la gestione delle risorse di Azure, ad esempio di App per le API.
18. Fare clic su **Altri servizi > Servizi app**.
    
    ![Selezionare Servizi app](./media/app-service-api-dotnet-get-started/browseas.png)
19. In hello **servizi App** pannello, trovare e fare clic su nuova app per le API. (In hello portale di Azure, sono detti finestre aperte destra toohello *pannelli*.)
    
    ![Pannello Servizi app](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    Vengono aperti due pannelli, Uno è un lungo elenco di impostazioni che è possibile visualizzare e modificare una panoramica delle app per le API hello dispone di un pannello.
20. In hello **impostazioni** blade, hello trova **API** sezione e fare clic su **di definizione dell'API**.
    
    ![Definizione dell'API nel pannello Impostazioni](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    Hello **di definizione dell'API** pannello consente di specificare l'URL di hello che restituisce i metadati di Swagger 2.0 in formato JSON. Quando Visual Studio crea applicazione hello API, imposta il valore predefinito toohello di hello API definizione URL di base Swashbuckle metadati generati che illustrato in precedenza, ovvero app hello API URL più `/swagger/docs/v1`.
    
    ![URL di definizione dell'API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    Quando si seleziona un codice client dell'API app toogenerate per tale, Visual Studio recupera i metadati di hello dal seguente URL.

## <a id="codegen"></a>Generare codice client per il livello di dati hello
Uno dei vantaggi di hello dell'integrazione di Swagger in App per le API di Azure è la generazione automatica di codice. Classi client generate rendono più semplice toowrite il codice che chiama un'API app.

progetto ToDoListAPI Hello dispone già di hello generato il codice client, ma in hello alla procedura seguente viene eliminato e rigenerarlo toosee come la generazione di codice hello toodo.

1. In Visual Studio **Esplora**, hello ToDoListAPI project, eliminare hello *ToDoListDataAPI* cartella. **Attenzione: Eliminare solo cartelle di hello, non il progetto di ToDoListDataAPI hello.**
   
    ![Eliminare il codice client generato](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    Questa cartella è stata creata con processo di generazione di codice hello è quasi toogo tramite.
2. Fare clic sul progetto ToDoListAPI hello e quindi fare clic su **Aggiungi > Client dell'API REST**.
   
    ![Aggiungere il client API REST in Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. In hello **aggiungere Client dell'API REST** nella finestra di dialogo fare clic su **URL Swagger**, quindi fare clic su **selezionare Asset Azure**.
   
    ![Seleziona asset di Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. In hello **servizio App** nella finestra di dialogo espandere il gruppo di risorse hello in uso per questa esercitazione selezionare app per le API e quindi fare clic su **OK**.
   
    ![Selezionare l'app per le API per la generazione di codice](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    Si noti che quando si torna toohello **aggiungere Client dell'API REST** finestra di dialogo, la casella di testo hello è stato compilato con definizione hello API valore di URL che è stato illustrato in precedenza nel portale di hello.
   
    ![URL di definizione dell'API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > I metadati di tooget un modo alternativo per la generazione di codice sono tooenter hello URL direttamente anziché passare attraverso una finestra di dialogo Sfoglia hello. O se si desidera il codice client toogenerate prima di distribuire tooAzure, è possibile eseguire il progetto API Web hello localmente, Vai a URL toohello che fornisce file Swagger JSON hello, salvare il file hello, e utilizzare hello **selezionare un file di metadati Swagger esistente**opzione.
   > 
   > 
5. In hello **aggiungere Client dell'API REST** la finestra di dialogo, fare clic su **OK**.
   
    Visual Studio crea una cartella denominata dopo l'applicazione hello API e genera classi del client.
   
    ![File di codice per il client generato](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. Nel progetto ToDoListAPI hello aprire *Controllers\ToDoListController.cs* codice hello toosee riga 40 che chiama l'API di hello utilizzando client hello generato.
   
    Hello frammento di codice seguente viene illustrato come codice hello crea un'istanza di oggetto client hello e chiamate hello metodo Get.
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    parametro del costruttore Hello Ottiene hello URL dell'endpoint da hello `toDoListDataAPIURL` impostazione dell'app. Nel file Web. config hello, tale valore è toohello set IIS Express URL locale di hello API progetto in modo che è possibile eseguire un'applicazione hello in locale. Se si omette un parametro di costruttore hello, endpoint predefinito hello è hello URL che è stato generato codice hello.
7. Classe del client verrà generata con un nome diverso in base al nome di app API; modificare il codice hello in *Controllers\ToDoListController.cs* in modo che hello nome del tipo corrisponde a ciò che è stato generato nel progetto. Se, ad esempio, si è assegnato all'app per le API il nome ToDoListDataAPI071316, si sostituirà questo codice:
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis:

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>Creare un livello intermedio API app toohost hello
In precedenza si [hello dati livello API app creata e distribuita codice tooit](#createapiapp).  Ora è seguire hello stessa procedura per l'applicazione di livello intermedio API hello.

1. In **Esplora**, livello intermedio rapida hello ToDoListAPI progetto (non hello livello dati ToDoListDataAPI) e quindi fare clic su **pubblica**.
   
    ![Fare clic su Pubblica in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. In hello **profilo** scheda di hello **pubblica sul Web** procedura guidata, fare clic su **servizio App di Microsoft Azure**.
3. In hello **servizio App** la finestra di dialogo, fare clic su **New**.
4. In hello **Hosting** scheda di hello **Crea servizio App** finestra di dialogo casella, accettare l'impostazione predefinita di hello **API App Name** o immettere un nome univoco nel hello  *azurewebsites.NET* dominio.
5. Scegliere hello Azure **sottoscrizione** è stato utilizzato.
6. In hello **gruppo di risorse** elenco a discesa, scegliere hello stesso gruppo di risorse creato in precedenza.
7. In hello **piano di servizio App** elenco a discesa, scegliere hello stesso piano creato in precedenza. Verrà aperta toothat valore.
8. Fare clic su **Crea**.
   
    Visual Studio crea hello API app, crea un profilo di pubblicazione per tale e Visualizza hello **connessione** passaggio di hello **pubblica sul Web** procedura guidata.
9. In hello **connessione** passaggio di hello **pubblica sul Web** procedura guidata, fare clic su **pubblica**.
   
   Visual Studio distribuisce hello ToDoListAPI progetto toohello nuova app per le API e apre un browser toohello URL app hello per le API. verrà visualizzata la pagina Hello "completata".

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>Configurare il livello dati hello di hello intermedio toocall
Se è stato chiamato app API di livello intermedio hello ora, cercherà di livello dati di hello toocall utilizzando URL localhost hello che è ancora in Web. config hello. In questa sezione è immettere hello dati livello API app URL in un'impostazione di ambiente app hello per le API livello intermedio. Quando hello codice nell'app di API di livello intermedio hello recupera impostazione URL di livello dati hello, impostazione di ambiente hello sostituiranno novità nel file Web. config hello.

1. Passare toohello [portale di Azure](https://portal.azure.com/), quindi passare toohello **App per le API** pannello per l'applicazione hello API creata dal progetto di toohost hello TodoListAPI (intermedio).
2. Nell'API dell'applicazione di hello **impostazioni** pannello, fare clic su **le impostazioni dell'applicazione**.
3. Nell'API dell'applicazione di hello **le impostazioni dell'applicazione** pannello, scorrere verso il basso toohello **le impostazioni dell'App** sezione e aggiungere il seguente hello chiave e il valore. il valore di Hello sarà hello URL dell'API prima hello App pubblicata in questa esercitazione.
   
   | **Chiave** | toDoListDataAPIURL |
   | --- | --- |
   | **Valore** |https://{nome dell'app per le API di livello dati}.azurewebsites.net |
   | **Esempio** |https://todolistdataapi.azurewebsites.net |
4. Fare clic su **Save**.
   
    ![Fare clic su Salva per le impostazioni dell'app](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    Quando l'esecuzione del codice hello in Azure, questo valore sostituirà ora hello localhost URL nel file Web. config hello.

## <a name="test"></a>Test
1. In una finestra del browser, passare URL toohello di livello intermedio nuova app per le API appena creata per ToDoListAPI hello. È possibile ottenere sono facendo hello URL nel pannello principale di hello API dell'app nel portale di hello.
2. Aggiungere "swagger" toohello URL nella barra degli indirizzi del browser hello e quindi premere INVIO. (hello URL `http://{apiappname}.azurewebsites.net/swagger`.)
   
    browser viene visualizzata Hello hello stesso Swagger dell'interfaccia utente che illustrato in precedenza per ToDoListDataAPI, ma ora `owner` non è un campo obbligatorio per l'operazione Get hello, perché l'applicazione di livello intermedio API hello invia tale valore toohello dati livello app per le API per l'utente. (Quando hello esercitazioni di autenticazione, livello intermedio hello invierà ID utente effettivo per hello `owner` parametro; per questo punto è a livello di codice un asterisco.)
3. Provare hello metodo Get e hello altri toovalidate metodi che hello app API di livello intermedio è esito positivo della chiamata hello dati livello app per le API.
   
    ![Metodo Get dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>Risoluzione dei problemi
In caso di problemi nel corso dell'esercitazione, ecco alcune idee per risolverli:

* Assicurarsi che si usi l'ultima versione di hello di hello [Azure SDK per .NET](http://go.microsoft.com/fwlink/?linkid=518003).
* Due hello nomi di progetto sono simili (ToDoListAPI, ToDoListDataAPI). Se il documento non è quello come descritto nelle istruzioni di hello quando si lavora con un progetto, verificare che hello corretto progetto è stato aperto.
* Se è attiva in una rete aziendale e si sta tentando di toodeploy tooAzure servizio App attraverso un firewall, assicurarsi che le porte 443 e 8172 siano aperte per distribuzione Web. Se non è possibile aprire tali porte, si possono usare altri metodi di distribuzione.  Vedere [distribuire il servizio App di tooAzure app](../app-service-web/web-sites-deploy.md).
* Errori di "nomi di route devono essere univoci", è possibile ottenere questi se si distribuire accidentalmente hello progetto errato tooan API app e distribuirla in un secondo momento una tooit corretta hello. toocorrect, ridistribuire hello progetto corretto toohello API app e su hello **impostazioni** scheda di hello **pubblica sul Web** procedura guidata seleziona **Rimuovi file aggiuntivi nella destinazione**.

Dopo aver app per le API di ASP.NET in esecuzione in Azure App Service, è consigliabile toolearn ulteriori informazioni sulle funzionalità di Visual Studio che semplificano la risoluzione dei problemi. Per informazioni sulla registrazione, il debug remoto e altro ancora, vedere [Risoluzione dei problemi di un'app Web nel servizio app di Azure tramite Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Passaggi successivi
È stato illustrato come generare codice client per App per le API toodeploy API Web progetti tooAPI App esistenti e utilizzare App per le API da client .NET. Hello successivo di questa serie vengono descritte le modalità troppo[usare App tooconsume API CORS da client JavaScript](app-service-api-cors-consume-javascript.md).

Per ulteriori informazioni sulla generazione del codice client, vedere hello [Azure/AutoRest](https://github.com/azure/autorest) repository in GitHub.com. Per informazioni sui problemi utilizzando client hello generato, aprire un [problema nel repository AutoRest hello](https://github.com/azure/autorest/issues).

Se si desidera toocreate nuovi progetti API app da zero, utilizzare hello **Azure API App** modello.

![Modello di app per le API in Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

Hello **Azure API App** modello di progetto è hello equivalente toochoosing **vuoto** ASP.NET 4.5.2 modello, fare clic sul supporto di API Web tooadd di hello casella di controllo e l'installazione del pacchetto Swashbuckle NuGet hello. Inoltre, modello hello viene alcuni Swashbuckle configurazione codice progettato tooprevent hello creato duplicati Swagger operazione ID. Dopo aver creato un progetto di App per le API, è possibile distribuirlo hello app tooan API allo stesso modo è stato illustrato in questa esercitazione.

