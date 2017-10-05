---
title: Creare un'applicazione .NET per Service Fabric | Microsoft Docs
description: Informazioni su come creare un'applicazione con un front-end ASP.NET Core e un servizio Reliable con stato back-end e distribuire l'applicazione in un cluster.
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
ms.openlocfilehash: ef50adf3af19bce494c3256308b443c8eaccdcea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="d2155-103">Creare e distribuire un'applicazione con un servizio front-end API Web ASP.NET Core e un servizio back-end con stato</span><span class="sxs-lookup"><span data-stu-id="d2155-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="d2155-104">Questa è la prima di una serie di esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="d2155-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="d2155-105">Illustra come creare un'applicazione di Azure Service Fabric con un front-end API Web ASP.NET Core e un servizio back-end con stato per archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="d2155-105">You will learn how to create an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service to store your data.</span></span> <span data-ttu-id="d2155-106">Al termine, sarà disponibile un'applicazione di voto con un front-end Web ASP.NET Core che salva i risultati delle votazioni in un servizio back-end con stato nel cluster.</span><span class="sxs-lookup"><span data-stu-id="d2155-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in the cluster.</span></span> <span data-ttu-id="d2155-107">Se non si vuole creare manualmente l'applicazione di voto, è possibile [scaricare il codice sorgente](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) per l'applicazione completata e passare direttamente alla [Descrizione dettagliata dell'applicazione di voto di esempio](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="d2155-107">If you don't want to manually create the voting application, you can [download the source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for the completed application and skip ahead to [Walk through the voting sample application](#walkthrough_anchor).</span></span>

![Diagramma dell'applicazione](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="d2155-109">Nella prima parte della serie si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="d2155-109">In part one of the series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d2155-110">Creare un servizio API Web ASP.NET Core come servizio Reliable con stato</span><span class="sxs-lookup"><span data-stu-id="d2155-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="d2155-111">Creare un servizio applicazione Web ASP.NET Core come servizio Web senza stato</span><span class="sxs-lookup"><span data-stu-id="d2155-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="d2155-112">Usare il proxy inverso per comunicare con il servizio con stato</span><span class="sxs-lookup"><span data-stu-id="d2155-112">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="d2155-113">In questa serie di esercitazioni si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="d2155-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d2155-114">Creare un'applicazione di Service Fabric .NET</span><span class="sxs-lookup"><span data-stu-id="d2155-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="d2155-115">Distribuire l'applicazione in un cluster remoto</span><span class="sxs-lookup"><span data-stu-id="d2155-115">Deploy the application to a remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="d2155-116">Configurare l'integrazione continua e la distribuzione continua usando Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="d2155-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="d2155-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d2155-117">Prerequisites</span></span>
<span data-ttu-id="d2155-118">Prima di iniziare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="d2155-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="d2155-119">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="d2155-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="d2155-120">[Installare Visual Studio 2017](https://www.visualstudio.com/) e installare i carichi di lavoro **Sviluppo di Azure** e **Sviluppo ASP.NET e Web**.</span><span class="sxs-lookup"><span data-stu-id="d2155-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="d2155-121">Installare Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="d2155-121">Install the Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="d2155-122">Creare un servizio API Web ASP.NET come servizio Reliable</span><span class="sxs-lookup"><span data-stu-id="d2155-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="d2155-123">Per prima cosa, creare il front-end Web dell'applicazione di voto usando ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d2155-123">First, create the web front-end of the voting application using ASP.NET Core.</span></span> <span data-ttu-id="d2155-124">ASP.NET Core è un framework di sviluppo Web multipiattaforma leggero, che consente di creare un'interfaccia utente Web e API Web moderne.</span><span class="sxs-lookup"><span data-stu-id="d2155-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> <span data-ttu-id="d2155-125">Per comprendere a fondo la modalità di integrazione di ASP.NET Core con Service Fabric, si consiglia di leggere l'articolo [ASP.NET Core in Reliable Services di Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="d2155-125">To get a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through the [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="d2155-126">Per il momento, è possibile seguire questa esercitazione per essere subito operativi.</span><span class="sxs-lookup"><span data-stu-id="d2155-126">For now, you can follow this tutorial to get started quickly.</span></span> <span data-ttu-id="d2155-127">Per altre informazioni su ASP.NET Core, vedere la [documentazione di ASP.NET Core](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="d2155-127">To learn more about ASP.NET Core, see the [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="d2155-128">L'esercitazione si basa sugli strumenti di [ASP.NET Core per Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="d2155-128">This tutorial is based on the [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="d2155-129">Gli strumenti di .NET Core per Visual Studio 2015 non saranno più oggetto di aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="d2155-129">The .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="d2155-130">Avviare Visual Studio come **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="d2155-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="d2155-131">Creare un progetto da **File**->**Nuovo**->**Progetto**</span><span class="sxs-lookup"><span data-stu-id="d2155-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="d2155-132">Nella finestra di dialogo **Nuovo progetto** scegliere **Cloud > Applicazione di Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="d2155-132">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="d2155-133">Assegnare all'applicazione il nome **Voting** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2155-133">Name the application **Voting** and press **OK**.</span></span>

   ![Finestra di dialogo Nuovo progetto in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="d2155-135">Nella pagina **Nuovo servizio Service Fabric** scegliere **ASP.NET Core senza stato** e assegnare al servizio il nome **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="d2155-135">On the **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Scelta di un servizio Web ASP.NET nella finestra di dialogo del nuovo servizio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="d2155-137">Nella pagina successiva è disponibile un set di modelli di progetto ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d2155-137">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="d2155-138">Per questa esercitazione scegliere **Applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="d2155-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![Scegliere un tipo di progetto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="d2155-140">Visual Studio crea un'applicazione e un progetto di servizio e li visualizza in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="d2155-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Esplora soluzioni dopo la creazione dell'applicazione con il servizio API Web ASP.NET Core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-to-the-votingweb-service"></a><span data-ttu-id="d2155-142">Aggiungere AngularJS al servizio VotingWeb</span><span class="sxs-lookup"><span data-stu-id="d2155-142">Add AngularJS to the VotingWeb service</span></span>
<span data-ttu-id="d2155-143">Aggiungere [AngularJS](http://angularjs.org/) al servizio usando il [supporto per Bower](/aspnet/core/client-side/bower) predefinito.</span><span class="sxs-lookup"><span data-stu-id="d2155-143">Add [AngularJS](http://angularjs.org/) to your service using the built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="d2155-144">Aprire *bower.json* e aggiungere le voci appropriate per Angular e Angular-Bootstrap e quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d2155-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

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
<span data-ttu-id="d2155-145">Durante il salvataggio del file *bower.json*, Angular viene installato nella cartella *wwwroot/lib* del progetto.</span><span class="sxs-lookup"><span data-stu-id="d2155-145">Upon saving the *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="d2155-146">Viene anche elencato nella cartella *Dependencies/Bower*.</span><span class="sxs-lookup"><span data-stu-id="d2155-146">Additionally, it is listed within the *Dependencies/Bower* folder.</span></span>

### <a name="update-the-sitejs-file"></a><span data-ttu-id="d2155-147">Aggiornare il file site.js</span><span class="sxs-lookup"><span data-stu-id="d2155-147">Update the site.js file</span></span>
<span data-ttu-id="d2155-148">Aprire il file *wwwroot/js/site.js*.</span><span class="sxs-lookup"><span data-stu-id="d2155-148">Open the *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="d2155-149">Sostituirne il contenuto con il codice JavaScript usato dalle visualizzazioni Home:</span><span class="sxs-lookup"><span data-stu-id="d2155-149">Replace its contents with the JavaScript used by the Home views:</span></span>

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

### <a name="update-the-indexcshtml-file"></a><span data-ttu-id="d2155-150">Aggiornare il file Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="d2155-150">Update the Index.cshtml file</span></span>
<span data-ttu-id="d2155-151">Aprire il file *Views/Home/Index.cshtml*, ovvero la visualizzazione specifica del controller Home.</span><span class="sxs-lookup"><span data-stu-id="d2155-151">Open the *Views/Home/Index.cshtml* file, the view specific to the Home controller.</span></span>  <span data-ttu-id="d2155-152">Sostituirne il contenuto con il codice seguente e quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d2155-152">Replace its contents with the following, then save your changes.</span></span>

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
                        Click to vote
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

### <a name="update-the-layoutcshtml-file"></a><span data-ttu-id="d2155-153">Aggiornare il file _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="d2155-153">Update the _Layout.cshtml file</span></span>
<span data-ttu-id="d2155-154">Aprire il file *Views/Shared/_Layout.cshtml*, ovvero il layout predefinito per l'app ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d2155-154">Open the *Views/Shared/_Layout.cshtml* file, the default layout for the ASP.NET app.</span></span>  <span data-ttu-id="d2155-155">Sostituirne il contenuto con il codice seguente e quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d2155-155">Replace its contents with the following, then save your changes.</span></span>

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

### <a name="update-the-votingwebcs-file"></a><span data-ttu-id="d2155-156">Aggiornare il file VotingWeb.cs</span><span class="sxs-lookup"><span data-stu-id="d2155-156">Update the VotingWeb.cs file</span></span>
<span data-ttu-id="d2155-157">Aprire il file *VotingWeb.cs*, che crea il WebHost ASP.NET Core all'interno del servizio senza stato tramite il server Web WebListener.</span><span class="sxs-lookup"><span data-stu-id="d2155-157">Open the *VotingWeb.cs* file, which creates the ASP.NET Core WebHost inside the stateless service using the WebListener web server.</span></span>  <span data-ttu-id="d2155-158">Aggiungere la direttiva `using System.Net.Http;` all'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="d2155-158">Add the `using System.Net.Http;` directive to the top of the file.</span></span>  <span data-ttu-id="d2155-159">Sostituire la funzione `CreateServiceInstanceListeners()` con il codice seguente e quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d2155-159">Replace the `CreateServiceInstanceListeners()` function with the following, then save your changes.</span></span>

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

### <a name="add-the-votescontrollercs-file"></a><span data-ttu-id="d2155-160">Aggiungere il file VotesController.cs</span><span class="sxs-lookup"><span data-stu-id="d2155-160">Add the VotesController.cs file</span></span>
<span data-ttu-id="d2155-161">Aggiungere un controller che definisce le azioni di voto.</span><span class="sxs-lookup"><span data-stu-id="d2155-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="d2155-162">Fare clic con il pulsante destro del mouse sulla cartella **Controller** e quindi selezionare **Aggiungi->Nuovo elemento->Classe**.</span><span class="sxs-lookup"><span data-stu-id="d2155-162">Right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="d2155-163">Assegnare al file il nome "VotesController.cs" e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d2155-163">Name the file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="d2155-164">Sostituire il contenuto del file con il codice seguente e quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d2155-164">Replace the file contents with the following, then save your changes.</span></span>  <span data-ttu-id="d2155-165">Nella sezione [Aggiornare il file VotesController.cs](#updatevotecontroller_anchor) disponibile più avanti, questo file verrà modificato per poter leggere e scrivere i dati di voto dal servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="d2155-165">Later, in [Update the VotesController.cs file](#updatevotecontroller_anchor), this file will be modified to read and write voting data from the back-end service.</span></span>  <span data-ttu-id="d2155-166">Per il momento, il controller restituisce nella visualizzazione i dati di una stringa statica.</span><span class="sxs-lookup"><span data-stu-id="d2155-166">For now, the controller returns static string data to the view.</span></span>

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



### <a name="deploy-and-run-the-application-locally"></a><span data-ttu-id="d2155-167">Distribuire ed eseguire l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="d2155-167">Deploy and run the application locally</span></span>
<span data-ttu-id="d2155-168">È ora possibile andare avanti con l'esercitazione ed eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2155-168">You can now go ahead and run the application.</span></span> <span data-ttu-id="d2155-169">In Visual Studio premere `F5` per distribuire l'applicazione per il debug.</span><span class="sxs-lookup"><span data-stu-id="d2155-169">In Visual Studio, press `F5` to deploy the application for debugging.</span></span> <span data-ttu-id="d2155-170">`F5` ha esito negativo se in precedenza Visual Studio non è stato aperto come **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="d2155-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="d2155-171">La prima volta che si esegue e si distribuisce l'applicazione in locale, Visual Studio crea un cluster locale per il debug.</span><span class="sxs-lookup"><span data-stu-id="d2155-171">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="d2155-172">La creazione del cluster può richiedere del tempo.</span><span class="sxs-lookup"><span data-stu-id="d2155-172">Cluster creation may take some time.</span></span> <span data-ttu-id="d2155-173">Lo stato della creazione del cluster verrà visualizzato nella finestra di output di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2155-173">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="d2155-174">L'app Web, a questo punto, dovrebbe aver l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="d2155-174">At this point, your web app should look like this:</span></span>

![Front-end ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="d2155-176">Per arrestare il debug dell'applicazione, tornare a Visual Studio e premere **MAIUSC+F5**.</span><span class="sxs-lookup"><span data-stu-id="d2155-176">To stop debugging the application, go back to Visual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-to-your-application"></a><span data-ttu-id="d2155-177">Aggiungere un servizio back-end con stato a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="d2155-177">Add a stateful back-end service to your application</span></span>
<span data-ttu-id="d2155-178">Ora che c'è un servizio API Web ASP.NET in esecuzione nell'applicazione, è possibile procedere e aggiungere un servizio Reliable con stato per archiviare alcuni dati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2155-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service to store some data in our application.</span></span>

<span data-ttu-id="d2155-179">Service Fabric consente di archiviare in modo coerente e affidabile i dati all'interno del servizio usando raccolte Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="d2155-179">Service Fabric allows you to consistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="d2155-180">Le Reliable Collection sono un set di classi di raccolte con elevati livelli di disponibilità e affidabilità che risultano familiari a chiunque abbia usato raccolte C#.</span><span class="sxs-lookup"><span data-stu-id="d2155-180">Reliable collections are a set of highly available and reliable collection classes that are familiar to anyone who has used C# collections.</span></span>

<span data-ttu-id="d2155-181">In questa esercitazione si creerà un servizio che archivia un valore del contatore in una Reliable Collection.</span><span class="sxs-lookup"><span data-stu-id="d2155-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="d2155-182">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Servizi** nel progetto dell'applicazione e scegliere **Aggiungi > Nuovo servizio Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="d2155-182">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Aggiunta di un nuovo servizio a un'applicazione esistente](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="d2155-184">Nella finestra di dialogo **Nuovo servizio Service Fabric** scegliere **ASP.NET Core con stato**, assegnare al servizio il nome **VotingData** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2155-184">In the **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name the service **VotingData** and press **OK**.</span></span>

    ![Finestra di dialogo Nuovo servizio in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="d2155-186">Una volta creato il progetto di servizio, l'applicazione includerà due servizi.</span><span class="sxs-lookup"><span data-stu-id="d2155-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="d2155-187">Man mano che si compila l'applicazione, è possibile aggiungere altri servizi nello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="d2155-187">As you continue to build your application, you can add more services in the same way.</span></span> <span data-ttu-id="d2155-188">Per ogni servizio, sarà possibile eseguire in modo indipendente il controllo della versione e l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d2155-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="d2155-189">Nella pagina successiva è disponibile un set di modelli di progetto ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d2155-189">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="d2155-190">Per questa esercitazione si sceglierà **API Web**,</span><span class="sxs-lookup"><span data-stu-id="d2155-190">For this tutorial, choose **Web API**.</span></span>

    ![Scegliere un tipo di progetto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="d2155-192">Visual Studio crea un progetto di servizio e lo visualizza in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="d2155-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Esplora soluzioni](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-the-votedatacontrollercs-file"></a><span data-ttu-id="d2155-194">Aggiungere il file VoteDataController.cs</span><span class="sxs-lookup"><span data-stu-id="d2155-194">Add the VoteDataController.cs file</span></span>

<span data-ttu-id="d2155-195">Nel progetto **VotingData** fare clic con il pulsante destro del mouse sulla cartella **Controller** e quindi selezionare **Aggiungi->Nuovo elemento->Classe**.</span><span class="sxs-lookup"><span data-stu-id="d2155-195">In the **VotingData** project right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="d2155-196">Assegnare al file il nome "VoteDataController.cs" e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d2155-196">Name the file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="d2155-197">Sostituire il contenuto del file con il codice seguente e quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d2155-197">Replace the file contents with the following, then save your changes.</span></span>

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


## <a name="connect-the-services"></a><span data-ttu-id="d2155-198">Connettere i servizi</span><span class="sxs-lookup"><span data-stu-id="d2155-198">Connect the services</span></span>
<span data-ttu-id="d2155-199">Nel passaggio successivo i due servizi verranno connessi e l'applicazione Web front-end otterrà e imposterà informazioni di voto dal servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="d2155-199">In this next step, we will connect the two services and make the front-end Web application get and set voting information from the back-end service.</span></span>

<span data-ttu-id="d2155-200">L'infrastruttura di servizi offre la massima flessibilità nella comunicazione con Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="d2155-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="d2155-201">All'interno di una singola applicazione possono esserci servizi accessibili tramite TCP.</span><span class="sxs-lookup"><span data-stu-id="d2155-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="d2155-202">Altri servizi potrebbero essere accessibili tramite un'API REST HTTP e altri ancora tramite Web Socket.</span><span class="sxs-lookup"><span data-stu-id="d2155-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="d2155-203">Per informazioni sulle opzioni disponibili e sui compromessi necessari, vedere [Comunicazione con i servizi](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="d2155-203">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="d2155-204">In questa esercitazione si userà l'[API Web ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="d2155-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-the-votescontrollercs-file"></a><span data-ttu-id="d2155-205">Aggiornare il file VotesController.cs</span><span class="sxs-lookup"><span data-stu-id="d2155-205">Update the VotesController.cs file</span></span>
<span data-ttu-id="d2155-206">Nel progetto **VotingWeb** aprire il file *Controllers/VotesController.cs*.</span><span class="sxs-lookup"><span data-stu-id="d2155-206">In the **VotingWeb** project, open the *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="d2155-207">Sostituire il contenuto della definizione di classe `VotesController` con il codice seguente e quindi salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d2155-207">Replace the `VotesController` class definition contents with the following, then save your changes.</span></span>

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

## <a name="walk-through-the-voting-sample-application"></a><span data-ttu-id="d2155-208">Descrizione dettagliata dell'applicazione di voto di esempio</span><span class="sxs-lookup"><span data-stu-id="d2155-208">Walk through the voting sample application</span></span>
<span data-ttu-id="d2155-209">L'applicazione di voto è costituita da due servizi:</span><span class="sxs-lookup"><span data-stu-id="d2155-209">The voting application consists of two services:</span></span>
- <span data-ttu-id="d2155-210">Il servizio front-end Web (VotingWeb) - Un servizio front-end Web ASP.NET Core che gestisce la pagina Web e che espone le API Web per la comunicazione con il servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="d2155-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves the web page and exposes web APIs to communicate with the backend service.</span></span>
- <span data-ttu-id="d2155-211">Il servizio back-end (VotingData) - Un servizio Web ASP.NET Core che espone un'API per l'archiviazione dei risultati delle votazioni in un oggetto Reliable Dictionary reso persistente su disco.</span><span class="sxs-lookup"><span data-stu-id="d2155-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API to store the vote results in a reliable dictionary persisted on disk.</span></span>

![Diagramma dell'applicazione](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="d2155-213">Quando l'utente vota nell'applicazione, si verificano gli eventi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2155-213">When you vote in the application the following events occur:</span></span>
1. <span data-ttu-id="d2155-214">JavaScript invia la richiesta di voto all'API Web nel servizio front-end Web come una richiesta HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="d2155-214">A JavaScript sends the vote request to the web API in the web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="d2155-215">Il servizio front-end Web usa un proxy per individuare e inoltrare una richiesta PUT HTTP al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="d2155-215">The web front-end service uses a proxy to locate and forward an HTTP PUT request to the back-end service.</span></span>

3. <span data-ttu-id="d2155-216">Il servizio back-end accetta la richiesta in ingresso e archivia il risultato aggiornato in un oggetto Reliable Dictionary, che viene replicato in più nodi all'interno del cluster e reso persistente su disco.</span><span class="sxs-lookup"><span data-stu-id="d2155-216">The back-end service takes the incoming request, and stores the updated result in a reliable dictionary, which gets replicated to multiple nodes within the cluster and persisted on disk.</span></span> <span data-ttu-id="d2155-217">Tutti i dati dell'applicazione sono archiviati nel cluster, quindi non è necessario alcun database.</span><span class="sxs-lookup"><span data-stu-id="d2155-217">All the application's data is stored in the cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="d2155-218">Eseguire il debug in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2155-218">Debug in Visual Studio</span></span>
<span data-ttu-id="d2155-219">Durante il debug dell'applicazione in Visual Studio, viene usato un cluster di sviluppo locale di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2155-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="d2155-220">È possibile modificare l'esperienza di debug in base allo specifico scenario.</span><span class="sxs-lookup"><span data-stu-id="d2155-220">You have the option to adjust your debugging experience to your scenario.</span></span> <span data-ttu-id="d2155-221">In questa applicazione, i dati vengono archiviati nel servizio back-end tramite un oggetto Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="d2155-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="d2155-222">Visual Studio rimuove l'applicazione per impostazione predefinita quando si arresta il debugger.</span><span class="sxs-lookup"><span data-stu-id="d2155-222">Visual Studio removes the application per default when you stop the debugger.</span></span> <span data-ttu-id="d2155-223">La rimozione dell'applicazione determina la rimozione anche dei dati nel servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="d2155-223">Removing the application causes the data in the back-end service to also be removed.</span></span> <span data-ttu-id="d2155-224">Per rendere persistenti i dati tra le sessioni di debug, è possibile modificare la proprietà **Modalità di debug applicazione** del progetto **Voting** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2155-224">To persist the data between debugging sessions, you can change the **Application Debug Mode** as a property on the **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="d2155-225">Per osservare che cosa avviene nel codice, completare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d2155-225">To look at what happens in the code, complete the following steps:</span></span>
1. <span data-ttu-id="d2155-226">Aprire il file **VotesController.cs** e impostare un punto di interruzione nel metodo **Put** dell'API Web (riga 47). È possibile eseguire una ricerca nel file usando Esplora soluzioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2155-226">Open the **VotesController.cs** file and set a breakpoint in the web API's **Put** method (line 47) - You can search for the file in the Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="d2155-227">Aprire il file **VoteDataController.cs** e impostare un punto di interruzione nel metodo **Put** dell'API Web (riga 50).</span><span class="sxs-lookup"><span data-stu-id="d2155-227">Open the **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="d2155-228">Tornare al browser e fare clic su un'opzione di voto oppure aggiungere una nuova opzione di voto.</span><span class="sxs-lookup"><span data-stu-id="d2155-228">Go back to the browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="d2155-229">È stato raggiunto il primo punto di interruzione nel controller API del front-end Web.</span><span class="sxs-lookup"><span data-stu-id="d2155-229">You hit the first breakpoint in the web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="d2155-230">In questa posizione, il codice JavaScript nel browser invia una richiesta al controller API Web nel servizio front-end.</span><span class="sxs-lookup"><span data-stu-id="d2155-230">This is where the JavaScript in the browser sends a request to the web API controller in the front-end service.</span></span>
    
    ![Aggiungere il servizio front-end di voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="d2155-232">Prima di tutto, costruire l'URL del proxy inverso per il servizio back-end **(1)**.</span><span class="sxs-lookup"><span data-stu-id="d2155-232">First we construct the URL to the ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="d2155-233">Inviare quindi la richiesta PUT HTTP al proxy inverso **(2)**.</span><span class="sxs-lookup"><span data-stu-id="d2155-233">Then we send the HTTP PUT Request to the ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="d2155-234">Infine, restituire la risposta dal servizio back-end al client **(3)**.</span><span class="sxs-lookup"><span data-stu-id="d2155-234">Finally the we return the response from the back-end service to the client **(3)**.</span></span>

4. <span data-ttu-id="d2155-235">Premere **F5** per continuare.</span><span class="sxs-lookup"><span data-stu-id="d2155-235">Press **F5** to continue</span></span>
    1. <span data-ttu-id="d2155-236">Ora ci troviamo al punto di interruzione nel servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="d2155-236">You are now at the break point in the back-end service.</span></span>
    
    ![Aggiungere il servizio back-end di voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="d2155-238">Nella prima riga del metodo **(1)** usiamo `StateManager` per ottenere o aggiungere un oggetto Reliable Dictionary denominato `counts`.</span><span class="sxs-lookup"><span data-stu-id="d2155-238">In the first line in the method **(1)** we are using the `StateManager` to get or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="d2155-239">Tutte le interazioni con i valori in un oggetto Reliable Dictionary richiedono una transazione, che viene creata dall'istruzione using **(2)**.</span><span class="sxs-lookup"><span data-stu-id="d2155-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="d2155-240">Nella transazione, aggiorniamo quindi il valore della chiave pertinente per l'opzione di voto e viene eseguito il commit dell'operazione **(3)**.</span><span class="sxs-lookup"><span data-stu-id="d2155-240">In the transaction, we then update the value of the relevant key for the voting option and commits the operation **(3)**.</span></span> <span data-ttu-id="d2155-241">Dopo la restituzione del metodo Commit, i dati vengono aggiornati nel dizionario e replicati negli altri nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="d2155-241">Once the commit method returns, the data is updated in the dictionary and replicated to other nodes in the cluster.</span></span> <span data-ttu-id="d2155-242">A questo punto, i dati sono archiviati in modo sicuro nel cluster e il servizio back-end può eseguire il failover in altri nodi, rendendo comunque disponibili i dati.</span><span class="sxs-lookup"><span data-stu-id="d2155-242">The data is now safely stored in the cluster, and the back-end service can fail over to other nodes, still having the data available.</span></span>
5. <span data-ttu-id="d2155-243">Premere **F5** per continuare.</span><span class="sxs-lookup"><span data-stu-id="d2155-243">Press **F5** to continue</span></span>

<span data-ttu-id="d2155-244">Per interrompere la sessione di debug, premere **MAIUSC+F5**.</span><span class="sxs-lookup"><span data-stu-id="d2155-244">To stop the debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d2155-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2155-245">Next steps</span></span>
<span data-ttu-id="d2155-246">In questa parte dell'esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="d2155-246">In this part of the tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d2155-247">Creare un servizio API Web ASP.NET Core come servizio Reliable con stato</span><span class="sxs-lookup"><span data-stu-id="d2155-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="d2155-248">Creare un servizio applicazione Web ASP.NET Core come servizio Web senza stato</span><span class="sxs-lookup"><span data-stu-id="d2155-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="d2155-249">Usare il proxy inverso per comunicare con il servizio con stato</span><span class="sxs-lookup"><span data-stu-id="d2155-249">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="d2155-250">Passare all'esercitazione successiva:</span><span class="sxs-lookup"><span data-stu-id="d2155-250">Advance to the next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d2155-251">Distribuire l'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="d2155-251">Deploy the application to Azure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)