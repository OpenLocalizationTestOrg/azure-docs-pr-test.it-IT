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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="63755-103">Creare e distribuire un'applicazione con un servizio front-end API Web ASP.NET Core e un servizio back-end con stato</span><span class="sxs-lookup"><span data-stu-id="63755-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="63755-104">Questa è la prima di una serie di esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="63755-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="63755-105">Si apprenderà come toocreate un'applicazione Azure Service Fabric con inizio un'API Web di ASP.NET Core terminare e toostore un servizio back-end basato sullo stato dei dati.</span><span class="sxs-lookup"><span data-stu-id="63755-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="63755-106">Al termine, si dispone di un'applicazione voto con un front-end che salva i risultati di voto in un servizio back-end con stato cluster hello web di ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="63755-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="63755-107">Se non si desidera toomanually creare hello voto applicazione, è possibile [scaricare il codice sorgente hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) per hello completa l'applicazione e andare troppo[analizzerà hello voto applicazione di esempio](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="63755-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![Diagramma dell'applicazione](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="63755-109">Nel parte di una serie di hello, si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="63755-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="63755-110">Creare un servizio API Web ASP.NET Core come servizio Reliable con stato</span><span class="sxs-lookup"><span data-stu-id="63755-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="63755-111">Creare un servizio applicazione Web ASP.NET Core come servizio Web senza stato</span><span class="sxs-lookup"><span data-stu-id="63755-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="63755-112">Utilizzare hello proxy inverso toocommunicate con il servizio con stato hello</span><span class="sxs-lookup"><span data-stu-id="63755-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="63755-113">In questa serie di esercitazioni si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="63755-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="63755-114">Creare un'applicazione di Service Fabric .NET</span><span class="sxs-lookup"><span data-stu-id="63755-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="63755-115">Distribuire hello applicazione tooa remota del cluster</span><span class="sxs-lookup"><span data-stu-id="63755-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="63755-116">Configurare l'integrazione continua e la distribuzione continua usando Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="63755-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="63755-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="63755-117">Prerequisites</span></span>
<span data-ttu-id="63755-118">Prima di iniziare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="63755-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="63755-119">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="63755-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="63755-120">[Installare Visual Studio 2017](https://www.visualstudio.com/) e installare hello **lo sviluppo di Azure** e **sviluppo web ASP.NET e** i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="63755-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="63755-121">Installare hello Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="63755-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="63755-122">Creare un servizio API Web ASP.NET come servizio Reliable</span><span class="sxs-lookup"><span data-stu-id="63755-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="63755-123">Innanzitutto, creare web hello front-end dell'applicazione mediante ASP.NET Core di voto hello.</span><span class="sxs-lookup"><span data-stu-id="63755-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="63755-124">ASP.NET Core è un framework di sviluppo web lightweight e multipiattaforma che è possibile utilizzare l'interfaccia utente web moderna toocreate e le API web.</span><span class="sxs-lookup"><span data-stu-id="63755-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="63755-125">tooget una conoscenza approfondita della modalità di integrazione ASP.NET Core con Service Fabric, è consigliabile leggere hello [ASP.NET Core in servizi di Service Fabric affidabile](service-fabric-reliable-services-communication-aspnetcore.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="63755-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="63755-126">Per il momento, è possibile seguire questa esercitazione tooget in tempi brevi.</span><span class="sxs-lookup"><span data-stu-id="63755-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="63755-127">toolearn ulteriori informazioni su ASP.NET Core, vedere hello [documentazione principale di ASP.NET](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="63755-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="63755-128">In questa esercitazione si basa sull'hello [di strumenti di ASP.NET Core per Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="63755-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="63755-129">strumenti di .NET Core Hello per Visual Studio 2015 non è più corso l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="63755-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="63755-130">Avviare Visual Studio come **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="63755-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="63755-131">Creare un progetto da **File**->**Nuovo**->**Progetto**</span><span class="sxs-lookup"><span data-stu-id="63755-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="63755-132">In hello **nuovo progetto** finestra di dialogo, scegliere **Cloud > applicazione di Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="63755-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="63755-133">Nome di un'applicazione hello **voto** e premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="63755-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Finestra di dialogo Nuovo progetto in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="63755-135">In hello **nuovo servizio Service Fabric** pagina, scegliere **senza stato ASP.NET Core**e il nome del servizio **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="63755-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Scelta di servizi web ASP.NET nella finestra di dialogo di hello nuovo servizio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="63755-137">la pagina successiva di Hello fornisce un set di ASP.NET Core modelli di progetto.</span><span class="sxs-lookup"><span data-stu-id="63755-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="63755-138">Per questa esercitazione scegliere **Applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="63755-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![Scegliere un tipo di progetto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="63755-140">Visual Studio crea un'applicazione e un progetto di servizio e li visualizza in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="63755-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Esplora soluzioni dopo la creazione dell'applicazione con il servizio API Web ASP.NET Core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="63755-142">Aggiungere AngularJS toohello VotingWeb servizio</span><span class="sxs-lookup"><span data-stu-id="63755-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="63755-143">Aggiungere [AngularJS](http://angularjs.org/) servizio tooyour utilizzando hello incorporata [Bower supporto](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="63755-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="63755-144">Aprire *bower.json* e aggiungere le voci appropriate per Angular e Angular-Bootstrap e quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="63755-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

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
<span data-ttu-id="63755-145">Quando si salvano hello *bower. JSON* angolare file viene installato del progetto *wwwroot/lib* cartella.</span><span class="sxs-lookup"><span data-stu-id="63755-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="63755-146">Inoltre, viene elencato all'interno di hello *dipendenze/Bower* cartella.</span><span class="sxs-lookup"><span data-stu-id="63755-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="63755-147">File di aggiornamento hello site.js</span><span class="sxs-lookup"><span data-stu-id="63755-147">Update hello site.js file</span></span>
<span data-ttu-id="63755-148">Aprire hello *wwwroot/js/site.js* file.</span><span class="sxs-lookup"><span data-stu-id="63755-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="63755-149">Sostituire il contenuto con hello JavaScript utilizzati dalle viste Home hello:</span><span class="sxs-lookup"><span data-stu-id="63755-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

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

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="63755-150">Aggiornare file cshtml hello</span><span class="sxs-lookup"><span data-stu-id="63755-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="63755-151">Aprire hello *Views/Home/Index.cshtml* file, il controller Home toohello specifico di hello vista.</span><span class="sxs-lookup"><span data-stu-id="63755-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="63755-152">Sostituire il contenuto con hello seguente, quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="63755-152">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="63755-153">Aggiornare il file layout. cshtml hello</span><span class="sxs-lookup"><span data-stu-id="63755-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="63755-154">Aprire hello *Views/Shared/_Layout.cshtml* file, il layout predefinito hello per app ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="63755-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="63755-155">Sostituire il contenuto con hello seguente, quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="63755-155">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="63755-156">File di aggiornamento hello VotingWeb.cs</span><span class="sxs-lookup"><span data-stu-id="63755-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="63755-157">Aprire hello *VotingWeb.cs* file, che crea hello ASP.NET Core WebHost all'interno di hello servizio senza stato Usa server web di WebListener hello.</span><span class="sxs-lookup"><span data-stu-id="63755-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="63755-158">Aggiungere hello `using System.Net.Http;` toohello direttiva parte superiore del file hello.</span><span class="sxs-lookup"><span data-stu-id="63755-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="63755-159">Sostituire hello `CreateServiceInstanceListeners()` funzionare con i seguenti hello, quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="63755-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

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

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="63755-160">Aggiungere file VotesController.cs hello</span><span class="sxs-lookup"><span data-stu-id="63755-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="63755-161">Aggiungere un controller che definisce le azioni di voto.</span><span class="sxs-lookup"><span data-stu-id="63755-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="63755-162">Fare clic su hello **controller** cartella, quindi selezionare **Aggiungi -> Nuovo elemento -> classe**.</span><span class="sxs-lookup"><span data-stu-id="63755-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="63755-163">Nome file hello "VotesController.cs" e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="63755-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="63755-164">Sostituire il contenuto del file hello con hello seguente, quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="63755-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="63755-165">Più avanti in [file di aggiornamento hello VotesController.cs](#updatevotecontroller_anchor), questo file verrà modificato tooread e scrivere dati voti dal servizio back-end hello.</span><span class="sxs-lookup"><span data-stu-id="63755-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="63755-166">Per il momento controller hello restituisce vista toohello di dati stringa statica.</span><span class="sxs-lookup"><span data-stu-id="63755-166">For now, hello controller returns static string data toohello view.</span></span>

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



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="63755-167">Distribuire ed eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="63755-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="63755-168">È ora possibile procedere ed eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="63755-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="63755-169">In Visual Studio, premere `F5` toodeploy per il debug di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="63755-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="63755-170">`F5` ha esito negativo se in precedenza Visual Studio non è stato aperto come **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="63755-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="63755-171">Hello prima eseguire e distribuire un'applicazione hello in locale, Visual Studio crea un cluster locale per il debug.</span><span class="sxs-lookup"><span data-stu-id="63755-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="63755-172">La creazione del cluster può richiedere del tempo.</span><span class="sxs-lookup"><span data-stu-id="63755-172">Cluster creation may take some time.</span></span> <span data-ttu-id="63755-173">lo stato di creazione di cluster Hello viene visualizzato nella finestra di output di hello Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="63755-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="63755-174">L'app Web, a questo punto, dovrebbe aver l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="63755-174">At this point, your web app should look like this:</span></span>

![Front-end ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="63755-176">toostop il debug di un'applicazione hello, tornare indietro tooVisual Studio e premere **MAIUSC + F5**.</span><span class="sxs-lookup"><span data-stu-id="63755-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="63755-177">Aggiungere un'applicazione di servizio back-end con stato tooyour</span><span class="sxs-lookup"><span data-stu-id="63755-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="63755-178">Ora che è disponibile un servizio API Web ASP.NET in esecuzione nell'applicazione, proseguire e aggiungere toostore un servizio reliable con stato di alcuni dati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="63755-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="63755-179">Service Fabric è tooconsistently e archiviare in modo affidabile i dati direttamente all'interno del servizio tramite raccolte affidabile.</span><span class="sxs-lookup"><span data-stu-id="63755-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="63755-180">Le raccolte affidabili sono un set di classi di raccolta a elevata disponibilità e affidabile che sono familiari tooanyone che ha utilizzato c# raccolte.</span><span class="sxs-lookup"><span data-stu-id="63755-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="63755-181">In questa esercitazione si creerà un servizio che archivia un valore del contatore in una Reliable Collection.</span><span class="sxs-lookup"><span data-stu-id="63755-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="63755-182">In Esplora soluzioni fare doppio clic su **servizi** interno hello progetto di applicazione e scegliere **Aggiungi > nuovo servizio Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="63755-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Aggiunta di una nuova applicazione esistente tooan di servizio](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="63755-184">In hello **nuovo servizio Service Fabric** finestra di dialogo, scegliere **Stateful ASP.NET Core**e il nome hello servizio **VotingData** e premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="63755-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Finestra di dialogo Nuovo servizio in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="63755-186">Una volta creato il progetto di servizio, l'applicazione includerà due servizi.</span><span class="sxs-lookup"><span data-stu-id="63755-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="63755-187">Mentre si continua a toobuild l'applicazione, è possibile aggiungere più servizi in hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="63755-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="63755-188">Per ogni servizio, sarà possibile eseguire in modo indipendente il controllo della versione e l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="63755-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="63755-189">la pagina successiva di Hello fornisce un set di ASP.NET Core modelli di progetto.</span><span class="sxs-lookup"><span data-stu-id="63755-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="63755-190">Per questa esercitazione si sceglierà **API Web**,</span><span class="sxs-lookup"><span data-stu-id="63755-190">For this tutorial, choose **Web API**.</span></span>

    ![Scegliere un tipo di progetto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="63755-192">Visual Studio crea un progetto di servizio e lo visualizza in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="63755-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Esplora soluzioni](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="63755-194">Aggiungere file VoteDataController.cs hello</span><span class="sxs-lookup"><span data-stu-id="63755-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="63755-195">In hello **VotingData** progetto pulsante destro del mouse su hello **controller** cartella, quindi selezionare **Aggiungi -> Nuovo elemento -> classe**.</span><span class="sxs-lookup"><span data-stu-id="63755-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="63755-196">Nome file hello "VoteDataController.cs" e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="63755-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="63755-197">Sostituire il contenuto del file hello con hello seguente, quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="63755-197">Replace hello file contents with hello following, then save your changes.</span></span>

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


## <a name="connect-hello-services"></a><span data-ttu-id="63755-198">Connessione dei servizi di hello</span><span class="sxs-lookup"><span data-stu-id="63755-198">Connect hello services</span></span>
<span data-ttu-id="63755-199">In questo passaggio successivo verrà hello due servizi di connessione e rendere hello Web front-end dell'applicazione get e set di informazioni dal servizio back-end hello di voto.</span><span class="sxs-lookup"><span data-stu-id="63755-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="63755-200">L'infrastruttura di servizi offre la massima flessibilità nella comunicazione con Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="63755-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="63755-201">All'interno di una singola applicazione possono esserci servizi accessibili tramite TCP.</span><span class="sxs-lookup"><span data-stu-id="63755-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="63755-202">Altri servizi potrebbero essere accessibili tramite un'API REST HTTP e altri ancora tramite Web Socket.</span><span class="sxs-lookup"><span data-stu-id="63755-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="63755-203">Per informazioni sulle opzioni di hello disponibili e gli svantaggi di hello relativi, vedere [comunicazione con i servizi](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="63755-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="63755-204">In questa esercitazione si userà l'[API Web ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="63755-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="63755-205">File di aggiornamento hello VotesController.cs</span><span class="sxs-lookup"><span data-stu-id="63755-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="63755-206">In hello **VotingWeb** progetto, aprire hello *Controllers/VotesController.cs* file.</span><span class="sxs-lookup"><span data-stu-id="63755-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="63755-207">Sostituire hello `VotesController` classe contenuto definizione con seguenti hello, quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="63755-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

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

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="63755-208">Procedura dettagliata hello voto applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="63755-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="63755-209">Hello voto applicazione è costituita da due servizi:</span><span class="sxs-lookup"><span data-stu-id="63755-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="63755-210">Il servizio front-end (VotingWeb) Web - An ASP.NET Core web front-end del servizio, che serve a pagina web hello ed espone web toocommunicate API con il servizio back-end hello.</span><span class="sxs-lookup"><span data-stu-id="63755-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="63755-211">Il servizio back-end (VotingData)-servizio web di ASP.NET Core, che espone un voto di hello toostore API comporta un dizionario affidabile persistente su disco.</span><span class="sxs-lookup"><span data-stu-id="63755-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Diagramma dell'applicazione](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="63755-213">Quando voto hello applicazione hello seguenti si verificano eventi:</span><span class="sxs-lookup"><span data-stu-id="63755-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="63755-214">JavaScript invia API web toohello richiesta di voto hello in servizio front-end web di hello come una richiesta HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="63755-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="63755-215">servizio front-end web di Hello Usa un proxy toolocate e inoltrare un servizio back-end toohello di richiesta HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="63755-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="63755-216">servizio back-end Hello accetta la richiesta in ingresso hello e archivi hello aggiornamento risultato in un dizionario affidabile, che ottiene i nodi toomultiple replicati all'interno di cluster hello e persistente su disco.</span><span class="sxs-lookup"><span data-stu-id="63755-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="63755-217">Dati dell'applicazione hello tutti archiviati in cluster hello, pertanto non è necessario alcun database.</span><span class="sxs-lookup"><span data-stu-id="63755-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="63755-218">Eseguire il debug in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="63755-218">Debug in Visual Studio</span></span>
<span data-ttu-id="63755-219">Durante il debug dell'applicazione in Visual Studio, viene usato un cluster di sviluppo locale di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="63755-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="63755-220">È necessario hello opzione tooadjust lo scenario di tooyour esperienza di debug.</span><span class="sxs-lookup"><span data-stu-id="63755-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="63755-221">In questa applicazione, i dati vengono archiviati nel servizio back-end tramite un oggetto Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="63755-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="63755-222">Visual Studio rimuove un'applicazione hello per impostazione predefinita, quando si arresta il debugger hello.</span><span class="sxs-lookup"><span data-stu-id="63755-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="63755-223">Rimozione di un'applicazione hello comporta hello dati back-end hello tooalso servizio da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="63755-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="63755-224">dati di hello toopersist tra le sessioni di debug, è possibile modificare hello **modalità di Debug dell'applicazione** come proprietà nel hello **voto** progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="63755-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="63755-225">toolook cosa accade nel codice hello, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="63755-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="63755-226">Aprire hello **VotesController.cs** file e impostare un punto di interruzione dell'API web hello **inserire** (metodo) (riga 47), è possibile cercare file hello in hello Esplora soluzioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="63755-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="63755-227">Aprire hello **VoteDataController.cs** file e impostare un punto di interruzione in questa web API **inserire** (metodo) (riga 50).</span><span class="sxs-lookup"><span data-stu-id="63755-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="63755-228">Tornare indietro del browser toohello e fare clic su un'opzione di voto oppure aggiungere una nuova opzione di voto.</span><span class="sxs-lookup"><span data-stu-id="63755-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="63755-229">È stato raggiunto punto di interruzione prima hello nel controller api hello web front-end.</span><span class="sxs-lookup"><span data-stu-id="63755-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="63755-230">Si tratta di dove hello JavaScript nel browser hello invia un controller di API web toohello richiesta nel servizio front-end hello.</span><span class="sxs-lookup"><span data-stu-id="63755-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Aggiungere il servizio front-end di voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="63755-232">Prima di tutto è costruire hello URL toohello ReverseProxy per il servizio back-end **(1)**.</span><span class="sxs-lookup"><span data-stu-id="63755-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="63755-233">Quindi inviare hello HTTP PUT richiesta toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="63755-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="63755-234">Infine hello restituiamo risposta hello client toohello servizio back-end di hello **(3)**.</span><span class="sxs-lookup"><span data-stu-id="63755-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="63755-235">Premere **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="63755-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="63755-236">Sono ora al punto di interruzione hello in servizio back-end hello.</span><span class="sxs-lookup"><span data-stu-id="63755-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![Aggiungere il servizio back-end di voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="63755-238">Nella prima riga di hello nel metodo hello **(1)** usiamo hello `StateManager` tooget o aggiungere un dizionario affidabile denominato `counts`.</span><span class="sxs-lookup"><span data-stu-id="63755-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="63755-239">Tutte le interazioni con i valori in un oggetto Reliable Dictionary richiedono una transazione, che viene creata dall'istruzione using **(2)**.</span><span class="sxs-lookup"><span data-stu-id="63755-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="63755-240">Transazione hello, è stato quindi aggiornare il valore di hello della chiave pertinenti di hello per hello voto opzione e commit hello operazione **(3)**.</span><span class="sxs-lookup"><span data-stu-id="63755-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="63755-241">Dopo il commit di hello metodo viene restituito, hello dati viene aggiornati nel dizionario hello e replicati tooother nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="63755-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="63755-242">dati Hello sono ora archiviati in modo sicuro in cluster hello e servizio back-end hello failover dei nodi tooother, persistono dati hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="63755-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="63755-243">Premere **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="63755-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="63755-244">hello toostop debug sessione, premere **MAIUSC + F5**.</span><span class="sxs-lookup"><span data-stu-id="63755-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="63755-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63755-245">Next steps</span></span>
<span data-ttu-id="63755-246">In questa parte dell'esercitazione di hello, si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="63755-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="63755-247">Creare un servizio API Web ASP.NET Core come servizio Reliable con stato</span><span class="sxs-lookup"><span data-stu-id="63755-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="63755-248">Creare un servizio applicazione Web ASP.NET Core come servizio Web senza stato</span><span class="sxs-lookup"><span data-stu-id="63755-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="63755-249">Utilizzare hello proxy inverso toocommunicate con il servizio con stato hello</span><span class="sxs-lookup"><span data-stu-id="63755-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="63755-250">Esercitazione successiva toohello avanzate:</span><span class="sxs-lookup"><span data-stu-id="63755-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="63755-251">Distribuire tooAzure applicazione hello</span><span class="sxs-lookup"><span data-stu-id="63755-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
