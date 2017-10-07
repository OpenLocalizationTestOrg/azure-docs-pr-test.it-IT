---
title: aaaCreate un'applicazione .NET per Service Fabric | Documenti Microsoft
description: Scopri back-end basato sullo stato del servizio e distribuire hello applicazione tooa cluster toocreate un'applicazione con un front-end ASP.NET Core e affidabili.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Creare e distribuire un'applicazione con un servizio front-end API Web ASP.NET Core e un servizio back-end con stato
Questa è la prima di una serie di esercitazioni.  Si apprenderà come toocreate un'applicazione Azure Service Fabric con inizio un'API Web di ASP.NET Core terminare e toostore un servizio back-end basato sullo stato dei dati. Al termine, si dispone di un'applicazione voto con un front-end che salva i risultati di voto in un servizio back-end con stato cluster hello web di ASP.NET Core. Se non si desidera toomanually creare hello voto applicazione, è possibile [scaricare il codice sorgente hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) per hello completa l'applicazione e andare troppo[analizzerà hello voto applicazione di esempio](#walkthrough_anchor).

![Diagramma dell'applicazione](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Nel parte di una serie di hello, si apprenderà come:

> [!div class="checklist"]
> * Creare un servizio API Web ASP.NET Core come servizio Reliable con stato
> * Creare un servizio applicazione Web ASP.NET Core come servizio Web senza stato
> * Utilizzare hello proxy inverso toocommunicate con il servizio con stato hello

In questa serie di esercitazioni si apprenderà come:
> [!div class="checklist"]
> * Creare un'applicazione di Service Fabric .NET
> * [Distribuire hello applicazione tooa remota del cluster](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [Configurare l'integrazione continua e la distribuzione continua usando Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione:
- Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Installare Visual Studio 2017](https://www.visualstudio.com/) e installare hello **lo sviluppo di Azure** e **sviluppo web ASP.NET e** i carichi di lavoro.
- [Installare hello Service Fabric SDK](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Creare un servizio API Web ASP.NET come servizio Reliable
Innanzitutto, creare web hello front-end dell'applicazione mediante ASP.NET Core di voto hello. ASP.NET Core è un framework di sviluppo web lightweight e multipiattaforma che è possibile utilizzare l'interfaccia utente web moderna toocreate e le API web. tooget una conoscenza approfondita della modalità di integrazione ASP.NET Core con Service Fabric, è consigliabile leggere hello [ASP.NET Core in servizi di Service Fabric affidabile](service-fabric-reliable-services-communication-aspnetcore.md) articolo. Per il momento, è possibile seguire questa esercitazione tooget in tempi brevi. toolearn ulteriori informazioni su ASP.NET Core, vedere hello [documentazione principale di ASP.NET](https://docs.microsoft.com/aspnet/core/).

> [!NOTE]
> In questa esercitazione si basa sull'hello [di strumenti di ASP.NET Core per Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc). strumenti di .NET Core Hello per Visual Studio 2015 non è più corso l'aggiornamento.

1. Avviare Visual Studio come **amministratore**.

2. Creare un progetto da **File**->**Nuovo**->**Progetto**

3. In hello **nuovo progetto** finestra di dialogo, scegliere **Cloud > applicazione di Service Fabric**.

4. Nome di un'applicazione hello **voto** e premere **OK**.

   ![Finestra di dialogo Nuovo progetto in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. In hello **nuovo servizio Service Fabric** pagina, scegliere **senza stato ASP.NET Core**e il nome del servizio **VotingWeb**.
   
   ![Scelta di servizi web ASP.NET nella finestra di dialogo di hello nuovo servizio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. la pagina successiva di Hello fornisce un set di ASP.NET Core modelli di progetto. Per questa esercitazione scegliere **Applicazione Web**. 
   
   ![Scegliere un tipo di progetto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio crea un'applicazione e un progetto di servizio e li visualizza in Esplora soluzioni.

   ![Esplora soluzioni dopo la creazione dell'applicazione con il servizio API Web ASP.NET Core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>Aggiungere AngularJS toohello VotingWeb servizio
Aggiungere [AngularJS](http://angularjs.org/) servizio tooyour utilizzando hello incorporata [Bower supporto](/aspnet/core/client-side/bower). Aprire *bower.json* e aggiungere le voci appropriate per Angular e Angular-Bootstrap e quindi salvare le modifiche.

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
Quando si salvano hello *bower. JSON* angolare file viene installato del progetto *wwwroot/lib* cartella. Inoltre, viene elencato all'interno di hello *dipendenze/Bower* cartella.

### <a name="update-hello-sitejs-file"></a>File di aggiornamento hello site.js
Aprire hello *wwwroot/js/site.js* file.  Sostituire il contenuto con hello JavaScript utilizzati dalle viste Home hello:

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-hello-indexcshtml-file"></a>Aggiornare file cshtml hello
Aprire hello *Views/Home/Index.cshtml* file, il controller Home toohello specifico di hello vista.  Sostituire il contenuto con hello seguente, quindi salvare le modifiche.

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click toovote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-hello-layoutcshtml-file"></a>Aggiornare il file layout. cshtml hello
Aprire hello *Views/Shared/_Layout.cshtml* file, il layout predefinito hello per app ASP.NET hello.  Sostituire il contenuto con hello seguente, quindi salvare le modifiche.

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-hello-votingwebcs-file"></a>File di aggiornamento hello VotingWeb.cs
Aprire hello *VotingWeb.cs* file, che crea hello ASP.NET Core WebHost all'interno di hello servizio senza stato Usa server web di WebListener hello.  Aggiungere hello `using System.Net.Http;` toohello direttiva parte superiore del file hello.  Sostituire hello `CreateServiceInstanceListeners()` funzionare con i seguenti hello, quindi salvare le modifiche.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-hello-votescontrollercs-file"></a>Aggiungere file VotesController.cs hello
Aggiungere un controller che definisce le azioni di voto. Fare clic su hello **controller** cartella, quindi selezionare **Aggiungi -> Nuovo elemento -> classe**.  Nome file hello "VotesController.cs" e fare clic su **Aggiungi**.  Sostituire il contenuto del file hello con hello seguente, quindi salvare le modifiche.  Più avanti in [file di aggiornamento hello VotesController.cs](#updatevotecontroller_anchor), questo file verrà modificato tooread e scrivere dati voti dal servizio back-end hello.  Per il momento controller hello restituisce vista toohello di dati stringa statica.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-hello-application-locally"></a>Distribuire ed eseguire un'applicazione hello in locale
È ora possibile procedere ed eseguire un'applicazione hello. In Visual Studio, premere `F5` toodeploy per il debug di un'applicazione hello. `F5` ha esito negativo se in precedenza Visual Studio non è stato aperto come **amministratore**.

> [!NOTE]
> Hello prima eseguire e distribuire un'applicazione hello in locale, Visual Studio crea un cluster locale per il debug.  La creazione del cluster può richiedere del tempo. lo stato di creazione di cluster Hello viene visualizzato nella finestra di output di hello Visual Studio.

L'app Web, a questo punto, dovrebbe aver l'aspetto seguente:

![Front-end ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

toostop il debug di un'applicazione hello, tornare indietro tooVisual Studio e premere **MAIUSC + F5**.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>Aggiungere un'applicazione di servizio back-end con stato tooyour
Ora che è disponibile un servizio API Web ASP.NET in esecuzione nell'applicazione, proseguire e aggiungere toostore un servizio reliable con stato di alcuni dati nell'applicazione.

Service Fabric è tooconsistently e archiviare in modo affidabile i dati direttamente all'interno del servizio tramite raccolte affidabile. Le raccolte affidabili sono un set di classi di raccolta a elevata disponibilità e affidabile che sono familiari tooanyone che ha utilizzato c# raccolte.

In questa esercitazione si creerà un servizio che archivia un valore del contatore in una Reliable Collection.

1. In Esplora soluzioni fare doppio clic su **servizi** interno hello progetto di applicazione e scegliere **Aggiungi > nuovo servizio Service Fabric**.
   
    ![Aggiunta di una nuova applicazione esistente tooan di servizio](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. In hello **nuovo servizio Service Fabric** finestra di dialogo, scegliere **Stateful ASP.NET Core**e il nome hello servizio **VotingData** e premere **OK**.

    ![Finestra di dialogo Nuovo servizio in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    Una volta creato il progetto di servizio, l'applicazione includerà due servizi. Mentre si continua a toobuild l'applicazione, è possibile aggiungere più servizi in hello allo stesso modo. Per ogni servizio, sarà possibile eseguire in modo indipendente il controllo della versione e l'aggiornamento.

3. la pagina successiva di Hello fornisce un set di ASP.NET Core modelli di progetto. Per questa esercitazione si sceglierà **API Web**,

    ![Scegliere un tipo di progetto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio crea un progetto di servizio e lo visualizza in Esplora soluzioni.

    ![Esplora soluzioni](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Aggiungere file VoteDataController.cs hello

In hello **VotingData** progetto pulsante destro del mouse su hello **controller** cartella, quindi selezionare **Aggiungi -> Nuovo elemento -> classe**. Nome file hello "VoteDataController.cs" e fare clic su **Aggiungi**. Sostituire il contenuto del file hello con hello seguente, quindi salvare le modifiche.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-hello-services"></a>Connessione dei servizi di hello
In questo passaggio successivo verrà hello due servizi di connessione e rendere hello Web front-end dell'applicazione get e set di informazioni dal servizio back-end hello di voto.

L'infrastruttura di servizi offre la massima flessibilità nella comunicazione con Reliable Services. All'interno di una singola applicazione possono esserci servizi accessibili tramite TCP. Altri servizi potrebbero essere accessibili tramite un'API REST HTTP e altri ancora tramite Web Socket. Per informazioni sulle opzioni di hello disponibili e gli svantaggi di hello relativi, vedere [comunicazione con i servizi](service-fabric-connect-and-communicate-with-services.md).

In questa esercitazione si userà l'[API Web ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>File di aggiornamento hello VotesController.cs
In hello **VotingWeb** progetto, aprire hello *Controllers/VotesController.cs* file.  Sostituire hello `VotesController` classe contenuto definizione con seguenti hello, quindi salvare le modifiche.

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-hello-voting-sample-application"></a>Procedura dettagliata hello voto applicazione di esempio
Hello voto applicazione è costituita da due servizi:
- Il servizio front-end (VotingWeb) Web - An ASP.NET Core web front-end del servizio, che serve a pagina web hello ed espone web toocommunicate API con il servizio back-end hello.
- Il servizio back-end (VotingData)-servizio web di ASP.NET Core, che espone un voto di hello toostore API comporta un dizionario affidabile persistente su disco.

![Diagramma dell'applicazione](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Quando voto hello applicazione hello seguenti si verificano eventi:
1. JavaScript invia API web toohello richiesta di voto hello in servizio front-end web di hello come una richiesta HTTP PUT.

2. servizio front-end web di Hello Usa un proxy toolocate e inoltrare un servizio back-end toohello di richiesta HTTP PUT.

3. servizio back-end Hello accetta la richiesta in ingresso hello e archivi hello aggiornamento risultato in un dizionario affidabile, che ottiene i nodi toomultiple replicati all'interno di cluster hello e persistente su disco. Dati dell'applicazione hello tutti archiviati in cluster hello, pertanto non è necessario alcun database.

## <a name="debug-in-visual-studio"></a>Eseguire il debug in Visual Studio
Durante il debug dell'applicazione in Visual Studio, viene usato un cluster di sviluppo locale di Service Fabric. È necessario hello opzione tooadjust lo scenario di tooyour esperienza di debug. In questa applicazione, i dati vengono archiviati nel servizio back-end tramite un oggetto Reliable Dictionary. Visual Studio rimuove un'applicazione hello per impostazione predefinita, quando si arresta il debugger hello. Rimozione di un'applicazione hello comporta hello dati back-end hello tooalso servizio da rimuovere. dati di hello toopersist tra le sessioni di debug, è possibile modificare hello **modalità di Debug dell'applicazione** come proprietà nel hello **voto** progetto in Visual Studio.

toolook cosa accade nel codice hello, hello completo alla procedura seguente:
1. Aprire hello **VotesController.cs** file e impostare un punto di interruzione dell'API web hello **inserire** (metodo) (riga 47), è possibile cercare file hello in hello Esplora soluzioni in Visual Studio.

2. Aprire hello **VoteDataController.cs** file e impostare un punto di interruzione in questa web API **inserire** (metodo) (riga 50).

3. Tornare indietro del browser toohello e fare clic su un'opzione di voto oppure aggiungere una nuova opzione di voto. È stato raggiunto punto di interruzione prima hello nel controller api hello web front-end.
    
    1. Si tratta di dove hello JavaScript nel browser hello invia un controller di API web toohello richiesta nel servizio front-end hello.
    
    ![Aggiungere il servizio front-end di voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Prima di tutto è costruire hello URL toohello ReverseProxy per il servizio back-end **(1)**.
    3. Quindi inviare hello HTTP PUT richiesta toohello ReverseProxy **(2)**.
    4. Infine hello restituiamo risposta hello client toohello servizio back-end di hello **(3)**.

4. Premere **F5** toocontinue
    1. Sono ora al punto di interruzione hello in servizio back-end hello.
    
    ![Aggiungere il servizio back-end di voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. Nella prima riga di hello nel metodo hello **(1)** usiamo hello `StateManager` tooget o aggiungere un dizionario affidabile denominato `counts`.
    3. Tutte le interazioni con i valori in un oggetto Reliable Dictionary richiedono una transazione, che viene creata dall'istruzione using **(2)**.
    4. Transazione hello, è stato quindi aggiornare il valore di hello della chiave pertinenti di hello per hello voto opzione e commit hello operazione **(3)**. Dopo il commit di hello metodo viene restituito, hello dati viene aggiornati nel dizionario hello e replicati tooother nodi nel cluster hello. dati Hello sono ora archiviati in modo sicuro in cluster hello e servizio back-end hello failover dei nodi tooother, persistono dati hello disponibili.
5. Premere **F5** toocontinue

hello toostop debug sessione, premere **MAIUSC + F5**.


## <a name="next-steps"></a>Passaggi successivi
In questa parte dell'esercitazione di hello, si è appreso come:

> [!div class="checklist"]
> * Creare un servizio API Web ASP.NET Core come servizio Reliable con stato
> * Creare un servizio applicazione Web ASP.NET Core come servizio Web senza stato
> * Utilizzare hello proxy inverso toocommunicate con il servizio con stato hello

Esercitazione successiva toohello avanzate:
> [!div class="nextstepaction"]
> [Distribuire tooAzure applicazione hello](service-fabric-tutorial-deploy-app-to-party-cluster.md)
