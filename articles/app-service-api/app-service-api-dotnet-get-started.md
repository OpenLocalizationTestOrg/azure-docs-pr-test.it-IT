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
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="5d954-103">Introduzione alle app per le API, ad ASP.NET e a Swagger in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="5d954-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="5d954-104">Si tratta hello prima in una serie di esercitazioni che mostrano come toouse funzionalità di Azure App Service che sono utili per lo sviluppo e l'API REST per l'hosting.</span><span class="sxs-lookup"><span data-stu-id="5d954-104">This is hello first in a series of tutorials that show how toouse features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="5d954-105">Questa esercitazione illustra il supporto per i metadati dell'API in formato Swagger.</span><span class="sxs-lookup"><span data-stu-id="5d954-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="5d954-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="5d954-106">You'll learn:</span></span>

* <span data-ttu-id="5d954-107">Come toocreate e distribuire [App per le API](app-service-api-apps-why-best-platform.md) nel servizio App di Azure utilizzando gli strumenti incorporati in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5d954-107">How toocreate and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="5d954-108">La modalità individuazione tooautomate API tramite hello del pacchetto Swashbuckle NuGet toodynamically generare metadati Swagger API.</span><span class="sxs-lookup"><span data-stu-id="5d954-108">How tooautomate API discovery by using hello Swashbuckle NuGet package toodynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="5d954-109">Tooautomatically di metadati Swagger API toouse come generare codice client per un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="5d954-109">How toouse Swagger API metadata tooautomatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="5d954-110">Panoramica dell'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="5d954-110">Sample application overview</span></span>
<span data-ttu-id="5d954-111">In questa esercitazione si usa una semplice applicazione di esempio di elenco attività.</span><span class="sxs-lookup"><span data-stu-id="5d954-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="5d954-112">un'applicazione Hello dispone di un front-end dell'applicazione a pagina singola (SPA), un livello intermedio di ASP.NET Web API e un livello di dati di ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="5d954-112">hello application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Diagramma dell'applicazione di esempio di app per le API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="5d954-114">Ecco una cattura di schermata di hello [AngularJS](https://angularjs.org/) front-end.</span><span class="sxs-lookup"><span data-stu-id="5d954-114">Here's a screen shot of hello [AngularJS](https://angularjs.org/) front end.</span></span>

![Elenco di App per le API esempio applicazione toodo](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="5d954-116">Hello soluzione di Visual Studio include tre progetti:</span><span class="sxs-lookup"><span data-stu-id="5d954-116">hello Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="5d954-117">**ToDoListAngular** -front-end hello: un SPA AngularJS che chiama intermedio hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-117">**ToDoListAngular** - hello front end: an AngularJS SPA that calls hello middle tier.</span></span>
* <span data-ttu-id="5d954-118">**ToDoListAPI** -intermedio hello: un progetto di API Web ASP.NET che chiama operazioni CRUD tooperform sugli elementi di attività di livello dati hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-118">**ToDoListAPI** - hello middle tier: an ASP.NET Web API project that calls hello data tier tooperform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="5d954-119">**ToDoListDataAPI** -livello di dati hello: un progetto ASP.NET Web API che consente di eseguire operazioni CRUD sulle attività da svolgere.</span><span class="sxs-lookup"><span data-stu-id="5d954-119">**ToDoListDataAPI** - hello data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="5d954-120">architettura a tre livelli Hello è una delle molte architetture che è possibile implementare usando l'App per le API e viene usato solo per scopi dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="5d954-120">hello three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="5d954-121">codice Hello in ogni livello è semplice come funzionalità di App per le API toodemonstrate possibili. ad esempio, il livello di dati hello utilizza la memoria del server invece di un database come meccanismo di persistenza.</span><span class="sxs-lookup"><span data-stu-id="5d954-121">hello code in each tier is as simple as possible toodemonstrate API Apps features; for example, hello data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="5d954-122">Dopo aver completato questa esercitazione, è necessario hello due progetti di API Web di e in esecuzione nel cloud hello in App per le API di servizio App.</span><span class="sxs-lookup"><span data-stu-id="5d954-122">On completing this tutorial, you'll have hello two Web API projects up and running in hello cloud in App Service API apps.</span></span>

<span data-ttu-id="5d954-123">esercitazione successiva di Hello in serie hello distribuisce cloud toohello di hello SPA front-end.</span><span class="sxs-lookup"><span data-stu-id="5d954-123">hello next tutorial in hello series deploys hello SPA front end toohello cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d954-124">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5d954-124">Prerequisites</span></span>
* <span data-ttu-id="5d954-125">ASP.NET Web API - istruzioni delle esercitazioni hello si supponga di abbia una conoscenza di base come toowork con ASP.NET [API Web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d954-125">ASP.NET Web API - hello tutorial instructions assume you have a basic knowledge of how toowork with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="5d954-126">Account Azure: è possibile [aprire un account Azure gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) o [attivare i benefici della sottoscrizione di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="5d954-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="5d954-127">Se si desidera tooget avviato con il servizio App di Azure prima di iscriversi per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="5d954-127">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="5d954-128">In questa pagina è possibile creare immediatamente un'app iniziale temporanea nel servizio app, **senza carta di credito**e senza impegno.</span><span class="sxs-lookup"><span data-stu-id="5d954-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="5d954-129">Visual Studio 2015 con hello [Azure SDK per .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK viene installato Visual Studio 2015 automaticamente se non si dispone già.</span><span class="sxs-lookup"><span data-stu-id="5d954-129">Visual Studio 2015 with hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - hello SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="5d954-130">In Visual Studio fare clic su ? -> Informazioni su Microsoft Visual Studio e assicurarsi di aver installato "Strumenti del servizio app di Azure versione 2.9.1" o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="5d954-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Versione di Strumenti del servizio app di Azure](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="5d954-132">A seconda di quanti le dipendenze del SDK hello già presenti nel computer, l'installazione hello SDK potrebbe richiedere molto tempo, da alcuni minuti tooa mezz'ora o più.</span><span class="sxs-lookup"><span data-stu-id="5d954-132">Depending on how many of hello SDK dependencies you already have on your machine, installing hello SDK could take a long time, from several minutes tooa half hour or more.</span></span>
    > 
    > 

## <a name="download-hello-sample-application"></a><span data-ttu-id="5d954-133">Scaricare l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="5d954-133">Download hello sample application</span></span>
1. <span data-ttu-id="5d954-134">Scaricare hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span><span class="sxs-lookup"><span data-stu-id="5d954-134">Download hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="5d954-135">È possibile fare clic su hello **ZIP di Download** pulsante o clone repository hello sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="5d954-135">You can click hello **Download ZIP** button or clone hello repository on your local machine.</span></span>
2. <span data-ttu-id="5d954-136">Aprire hello ToDoList soluzione in Visual Studio 2015 o 2013.</span><span class="sxs-lookup"><span data-stu-id="5d954-136">Open hello ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="5d954-137">È necessario tootrust ciascuna soluzione.</span><span class="sxs-lookup"><span data-stu-id="5d954-137">You will need tootrust each solution.</span></span>
         <span data-ttu-id="5d954-138">![Avviso di sicurezza](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="5d954-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="5d954-139">Compilazione dei pacchetti NuGet di hello toorestore di hello soluzioni (CTRL + MAIUSC + B).</span><span class="sxs-lookup"><span data-stu-id="5d954-139">Build hello solution (CTRL + SHIFT + B)  toorestore hello NuGet packages.</span></span>
   
    <span data-ttu-id="5d954-140">Se si desidera un'applicazione hello toosee nell'operazione prima della distribuzione, è possibile eseguire in locale.</span><span class="sxs-lookup"><span data-stu-id="5d954-140">If you want toosee hello application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="5d954-141">Assicurarsi che ToDoListDataAPI sia il progetto di avvio e la soluzione hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5d954-141">Make sure that ToDoListDataAPI is your startup project and run hello solution.</span></span> <span data-ttu-id="5d954-142">È necessario prevedere un HTTP 403 toosee errore nel browser.</span><span class="sxs-lookup"><span data-stu-id="5d954-142">You should expect toosee a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="5d954-143">Usare l'interfaccia utente e i metadati dell'API Swagger</span><span class="sxs-lookup"><span data-stu-id="5d954-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="5d954-144">Il supporto per i metadati dell'API [Swagger](http://swagger.io/) 2.0 è integrato nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d954-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="5d954-145">Ogni app per le API è possibile specificare un endpoint dell'URL che restituisce i metadati per hello API in formato JSON Swagger.</span><span class="sxs-lookup"><span data-stu-id="5d954-145">Each API app can specify a URL endpoint that returns metadata for hello API in Swagger JSON format.</span></span> <span data-ttu-id="5d954-146">Hello metadati restituiti da tale endpoint possono essere utilizzato il codice client toogenerate.</span><span class="sxs-lookup"><span data-stu-id="5d954-146">hello metadata returned from that endpoint can be used toogenerate client code.</span></span>

<span data-ttu-id="5d954-147">Un progetto ASP.NET Web API possa generare in modo dinamico i metadati Swagger utilizzando hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="5d954-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="5d954-148">pacchetto Swashbuckle NuGet Hello è già installato in hello ToDoListDataAPI ToDoListAPI i progetti e che è stato scaricato.</span><span class="sxs-lookup"><span data-stu-id="5d954-148">hello Swashbuckle NuGet package is already installed in hello ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="5d954-149">In questa sezione dell'esercitazione hello, si esamina i metadati di Swagger 2.0 hello generato e quindi si tenta una prova dell'interfaccia utente che si basa sui metadati di Swagger hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-149">In this section of hello tutorial, you look at hello generated Swagger 2.0 metadata, and then you try out a test UI that is based on hello Swagger metadata.</span></span>

1. <span data-ttu-id="5d954-150">Impostare il progetto di ToDoListDataAPI hello (**non** progetto ToDoListAPI hello) come progetto di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-150">Set hello ToDoListDataAPI project (**not** hello ToDoListAPI project) as hello startup project.</span></span>
   
    ![Impostare ToDoDataAPI come progetto di avvio](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="5d954-152">Premere F5 o fare clic su **Debug > Avvia debug** progetto hello toorun in modalità di debug.</span><span class="sxs-lookup"><span data-stu-id="5d954-152">Press F5 or click **Debug > Start Debugging** toorun hello project in debug mode.</span></span>
   
    <span data-ttu-id="5d954-153">browser Hello viene visualizzata la pagina di errore HTTP 403 hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-153">hello browser opens and shows hello HTTP 403 error page.</span></span>
3. <span data-ttu-id="5d954-154">Nella barra degli indirizzi del browser, aggiungere `swagger/docs/v1` toohello fine riga hello e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="5d954-154">In your browser address bar, add `swagger/docs/v1` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="5d954-155">(hello URL `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="5d954-155">(hello URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="5d954-156">Si tratta di hello URL predefinito dai metadati di Swagger 2.0 JSON tooreturn Swashbuckle per hello API.</span><span class="sxs-lookup"><span data-stu-id="5d954-156">This is hello default URL used by Swashbuckle tooreturn Swagger 2.0 JSON metadata for hello API.</span></span>
   
    <span data-ttu-id="5d954-157">Se si utilizza Internet Explorer, hello chiesto toodownload un *v1.json* file.</span><span class="sxs-lookup"><span data-stu-id="5d954-157">If you're using Internet Explorer, hello browser prompts you toodownload a *v1.json* file.</span></span>
   
    ![Scaricare i metadati JSON in Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="5d954-159">Se si usa Chrome, Firefox o Edge, hello JSON browser hello Visualizza nella finestra del browser hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-159">If you're using Chrome, Firefox, or Edge, hello browser displays hello JSON in hello browser window.</span></span> <span data-ttu-id="5d954-160">Diversi browser gestiscono JSON in modo diverso, e la finestra del browser potrebbe non apparire esattamente come esempio hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-160">Different browsers handle JSON differently, and your browser window may not look exactly like hello example.</span></span>
   
    ![Metadati JSON in Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="5d954-162">Hello esempio seguente viene mostrata hello prima sezione di metadati Swagger hello per hello API, con la definizione di hello per hello Get (metodo).</span><span class="sxs-lookup"><span data-stu-id="5d954-162">hello following sample shows hello first section of hello Swagger metadata for hello API, with hello definition for hello Get method.</span></span> <span data-ttu-id="5d954-163">Questi metadati sono quali hello unità Swagger dell'interfaccia utente che si utilizza in hello seguendo i passaggi e utilizzare in una sezione successiva di hello esercitazione tooautomatically genera il codice client.</span><span class="sxs-lookup"><span data-stu-id="5d954-163">This metadata is what drives hello Swagger UI that you use in hello following steps, and you use it in a later section of hello tutorial tooautomatically generate client code.</span></span>
   
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
4. <span data-ttu-id="5d954-164">Chiudere il browser hello e arrestare il debug di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d954-164">Close hello browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="5d954-165">In hello ToDoListDataAPI progetto **Esplora**aprire hello *App_Start\SwaggerConfig.cs* file, quindi scorrere verso il basso tooline 174 e rimuovere il commento hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="5d954-165">In hello ToDoListDataAPI project in **Solution Explorer**, open hello *App_Start\SwaggerConfig.cs* file, then scroll down tooline 174 and uncomment hello following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="5d954-166">Hello *SwaggerConfig.cs* file viene creato quando si installa il pacchetto di Swashbuckle hello in un progetto.</span><span class="sxs-lookup"><span data-stu-id="5d954-166">hello *SwaggerConfig.cs* file is created when you install hello Swashbuckle package in a project.</span></span> <span data-ttu-id="5d954-167">file Hello fornisce una serie di modi tooconfigure Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="5d954-167">hello file provides a number of ways tooconfigure Swashbuckle.</span></span>
   
    <span data-ttu-id="5d954-168">codice Hello che è stata non commentata hello Abilita UI Swagger utilizzato in hello seguendo i passaggi.</span><span class="sxs-lookup"><span data-stu-id="5d954-168">hello code you've uncommented enables hello Swagger UI that you use in hello following steps.</span></span> <span data-ttu-id="5d954-169">Quando si crea un progetto di API Web utilizzando il modello di progetto applicazione hello API, questo codice è commentato per impostazione predefinita come misura di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5d954-169">When you create a Web API project by using hello API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="5d954-170">Eseguire nuovamente il progetto di hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-170">Run hello project again.</span></span>
7. <span data-ttu-id="5d954-171">Nella barra degli indirizzi del browser, aggiungere `swagger` toohello fine riga hello e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="5d954-171">In your browser address bar, add `swagger` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="5d954-172">(hello URL `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="5d954-172">(hello URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="5d954-173">Quando viene visualizzata la pagina di hello Swagger dell'interfaccia utente, fare clic su **ToDoList** metodi hello toosee disponibili.</span><span class="sxs-lookup"><span data-stu-id="5d954-173">When hello Swagger UI page appears, click **ToDoList** toosee hello methods available.</span></span>
   
    ![Metodi disponibili dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="5d954-175">Fare clic su hello innanzitutto **ottenere** pulsante nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-175">Click hello first **Get** button in hello list.</span></span>
10. <span data-ttu-id="5d954-176">In hello **parametri** sezione, immettere un asterisco come valore hello hello `owner` parametro e quindi fare clic su **provarlo**.</span><span class="sxs-lookup"><span data-stu-id="5d954-176">In hello **Parameters** section, enter an asterisk as hello value of hello `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="5d954-177">Quando si aggiunge l'autenticazione nelle esercitazioni successive, il livello intermedio hello fornirà livello di dati toohello ID utente effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-177">When you add authentication in later tutorials, hello middle tier will provide hello actual user ID toohello data tier.</span></span> <span data-ttu-id="5d954-178">Per il momento, tutte le attività avranno asterisco come l'ID del proprietario durante l'esecuzione di un'applicazione hello senza abilitata l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="5d954-178">For now, all tasks will have asterisk as their owner ID while hello application runs without authentication enabled.</span></span>
    
    ![Prova dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="5d954-180">Hello Swagger dell'interfaccia utente chiama il metodo ToDoList Get hello e visualizza il codice di risposta hello e risultati JSON.</span><span class="sxs-lookup"><span data-stu-id="5d954-180">hello Swagger UI calls hello ToDoList Get method and displays hello response code and JSON results.</span></span>
    
    ![Risultati della prova dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="5d954-182">Fare clic su **Post**e quindi fare clic sulla casella hello in **lo Schema del modello**.</span><span class="sxs-lookup"><span data-stu-id="5d954-182">Click **Post**, and then click hello box under **Model Schema**.</span></span>
    
    <span data-ttu-id="5d954-183">Fare clic su hello modello schema prefills hello casella di input in cui è possibile specificare il valore di parametro hello per hello metodo Post.</span><span class="sxs-lookup"><span data-stu-id="5d954-183">Clicking hello model schema prefills hello input box where you can specify hello parameter value for hello Post method.</span></span> <span data-ttu-id="5d954-184">(Se il problema persiste in Internet Explorer, utilizzare un browser diverso o immettere manualmente il valore di parametro hello nel passaggio successivo hello.)</span><span class="sxs-lookup"><span data-stu-id="5d954-184">(If this doesn't work in Internet Explorer, use a different browser or enter hello parameter value manually in hello next step.)</span></span>  
    
    ![Post della prova dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="5d954-186">Ciao modifica JSON hello `todo` un parametro di input in modo che risulti simile al seguente esempio hello o di sostituire il testo di descrizione:</span><span class="sxs-lookup"><span data-stu-id="5d954-186">Change hello JSON in hello `todo` parameter input box so that it looks like hello following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="5d954-187">Fare clic su **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="5d954-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="5d954-188">Hello ToDoList API restituisce un codice di risposta HTTP 204 che indica l'esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5d954-188">hello ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="5d954-189">Fare clic su hello innanzitutto **ottenere** pulsante e quindi fare clic su hello in questa sezione della pagina hello **provarlo** pulsante.</span><span class="sxs-lookup"><span data-stu-id="5d954-189">Click hello first **Get** button, and then in that section of hello page click hello **Try it out** button.</span></span>
    
    <span data-ttu-id="5d954-190">risposta al metodo Get Hello include ora il nuovo elemento di toodo hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-190">hello Get method response now includes hello new toodo item.</span></span>
15. <span data-ttu-id="5d954-191">Facoltativo: Provare inoltre Put, Delete, hello e ottenere dai metodi di ID.</span><span class="sxs-lookup"><span data-stu-id="5d954-191">Optional: Try also hello Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="5d954-192">Chiudere il browser hello e arrestare il debug di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d954-192">Close hello browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="5d954-193">Swashbuckle funziona con qualsiasi progetto API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5d954-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="5d954-194">Se si desidera tooadd Swagger metadati generazione tooan esistente, è sufficiente installare il pacchetto di Swashbuckle hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-194">If you want tooadd Swagger metadata generation tooan existing project, just install hello Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="5d954-195">I metadati di Swagger includono un ID univoco per ogni operazione API.</span><span class="sxs-lookup"><span data-stu-id="5d954-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="5d954-196">Per impostazione predefinita, Swashbuckle può generare ID operazione di Swagger duplicati per i metodi del controller dell'API Web.</span><span class="sxs-lookup"><span data-stu-id="5d954-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="5d954-197">Ciò si verifica se il controller presenta metodi di overload HTTP, ad esempio `Get()` e `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="5d954-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="5d954-198">Per informazioni su come toohandle overload, vedere [definizioni generato personalizzare Swashbuckle API](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="5d954-198">For information about how toohandle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="5d954-199">Se si crea un progetto di API Web in Visual Studio usando il modello di Azure API App hello, che genera gli ID di operazione univoco viene aggiunto codice automaticamente toohello *SwaggerConfig.cs* file.</span><span class="sxs-lookup"><span data-stu-id="5d954-199">If you create a Web API project in Visual Studio by using hello Azure API App template, code that generates unique operation IDs is automatically added toohello *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="5d954-200"><a id="createapiapp"></a>Creare un'app per le API in Azure e distribuire codice tooit</span><span class="sxs-lookup"><span data-stu-id="5d954-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code tooit</span></span>
<span data-ttu-id="5d954-201">In questa sezione, utilizzare gli strumenti di Azure che sono integrati in Visual Studio hello **pubblica sul Web** guidata toocreate una nuova API app in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d954-201">In this section, you use Azure tools that are integrated into hello Visual Studio **Publish Web** wizard toocreate a new API app in Azure.</span></span> <span data-ttu-id="5d954-202">Quindi si distribuisce hello ToDoListDataAPI progetto toohello nuova API app e chiamare l'API di hello eseguendo hello Swagger dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="5d954-202">Then you deploy hello ToDoListDataAPI project toohello new API app and call hello API by running hello Swagger UI.</span></span>

1. <span data-ttu-id="5d954-203">In **Esplora**, fare clic sul progetto ToDoListDataAPI hello e quindi fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="5d954-203">In **Solution Explorer**, right-click hello ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Fare clic su Pubblica in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="5d954-205">In hello **profilo** passaggio di hello **pubblica sul Web** procedura guidata, fare clic su **servizio App di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="5d954-205">In hello **Profile** step of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Fare clic su Servizio app di Azure in Pubblica sul Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="5d954-207">Accedi a tooyour account Azure, se non è già stato fatto, o aggiornare le credenziali se si scadute.</span><span class="sxs-lookup"><span data-stu-id="5d954-207">Sign in tooyour Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="5d954-208">In hello la finestra di dialogo di servizio App, scegliere hello Azure **sottoscrizione** toouse desiderato e quindi fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="5d954-208">In hello App Service dialog box, choose hello Azure **Subscription** you want toouse, and then click **New**.</span></span>
   
    ![Fare clic su Nuovo nella finestra di dialogo Servizio app](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="5d954-210">Hello **Hosting** scheda di hello **Crea servizio App** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5d954-210">hello **Hosting** tab of hello **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="5d954-211">Poiché si distribuisce un progetto di API Web che ha installato Swashbuckle, Visual Studio si presuppone che un'App per le API toocreate.</span><span class="sxs-lookup"><span data-stu-id="5d954-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want toocreate an API App.</span></span> <span data-ttu-id="5d954-212">In questo caso viene hello **API App Name** title e da hello delle tabelle dei fatti che hello **Modifica tipo** riepilogo è stato impostato troppo**App per le API**.</span><span class="sxs-lookup"><span data-stu-id="5d954-212">This is indicated by hello **API App Name** title and by hello fact that hello **Change Type** drop-down list is set too**API App**.</span></span>
   
    ![Tipo di app nella finestra di dialogo Servizio app](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="5d954-214">Immettere un **API App Name** che sia univoco in hello *azurewebsites.net* dominio.</span><span class="sxs-lookup"><span data-stu-id="5d954-214">Enter an **API App Name** that is unique in hello *azurewebsites.net* domain.</span></span> <span data-ttu-id="5d954-215">È possibile accettare nome predefinito hello che si propone di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d954-215">You can accept hello default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="5d954-216">Se si immette un nome di un altro utente ha già in uso, viene visualizzato un diritto toohello punto esclamativo rosso.</span><span class="sxs-lookup"><span data-stu-id="5d954-216">If you enter a name that someone else has already used, you see a red exclamation mark toohello right.</span></span>
   
    <span data-ttu-id="5d954-217">Hello URL dell'app hello API sarà `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5d954-217">hello URL of hello API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="5d954-218">In hello **gruppo di risorse** fare clic su elenco a discesa **New**, quindi immettere "ToDoListGroup" o un altro nome se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="5d954-218">In hello **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="5d954-219">Un gruppo di risorse è una raccolta di risorse di Azure, ad esempio app per le api, database, VM e così via.</span><span class="sxs-lookup"><span data-stu-id="5d954-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="5d954-220">Per questa esercitazione, è migliore toocreate un nuovo gruppo di risorse perché che rende facile toodelete in un unico passaggio, che tutte le risorse di Azure creato per l'esercitazione hello di hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-220">For this tutorial, it's best toocreate a new resource group because that makes it easy toodelete in one step all hello Azure resources that you create for hello tutorial.</span></span>
   
    <span data-ttu-id="5d954-221">Questa casella consente di selezionare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) esistente o crearne uno nuovo digitando un nome diverso da qualsiasi gruppo di risorse esistente nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5d954-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="5d954-222">Fare clic su hello **New** pulsante Avanti toohello **piano di servizio App** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="5d954-222">Click hello **New** button next toohello **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="5d954-223">cattura di schermata Hello Mostra i valori di esempio per **API App Name**, **sottoscrizione**, e **gruppo di risorse** -i valori saranno diversi.</span><span class="sxs-lookup"><span data-stu-id="5d954-223">hello screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Finestra di dialogo Crea servizio app](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="5d954-225">In hello alla procedura seguente creare un piano di servizio App per il nuovo gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-225">In hello following steps you create an App Service plan for hello new resource group.</span></span> <span data-ttu-id="5d954-226">Un piano di servizio App specifica le risorse di calcolo hello utilizzabile con app per le API.</span><span class="sxs-lookup"><span data-stu-id="5d954-226">An App Service plan specifies hello compute resources that your API app runs on.</span></span> <span data-ttu-id="5d954-227">Ad esempio, se si sceglie di livello gratuito hello, app per le API viene eseguito in macchine virtuali condivisione, mentre per alcuni livelli a pagamento è in esecuzione nelle macchine virtuali dedicate.</span><span class="sxs-lookup"><span data-stu-id="5d954-227">For example, if you choose hello free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="5d954-228">Per altre informazioni sui piani di servizio app, vedere [Panoramica approfondita dei piani del servizio app di Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d954-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="5d954-229">In hello **configurare il piano di servizio App** finestra di dialogo, immettere "ToDoListPlan" o un altro nome se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="5d954-229">In hello **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="5d954-230">In hello **percorso** elenco a discesa scegliere percorso hello tooyou più vicino.</span><span class="sxs-lookup"><span data-stu-id="5d954-230">In hello **Location** drop-down list, choose hello location that is closest tooyou.</span></span>
   
    <span data-ttu-id="5d954-231">Questa impostazione specifica il data center di Azure in cui verrà eseguita l'app.</span><span class="sxs-lookup"><span data-stu-id="5d954-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="5d954-232">Scegliere un percorso chiudere tooyou toominimize [latenza](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="5d954-232">Choose a location close tooyou toominimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="5d954-233">In hello **dimensioni** fare clic su elenco a discesa **libero**.</span><span class="sxs-lookup"><span data-stu-id="5d954-233">In hello **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="5d954-234">Per questa esercitazione, hello disponibile a livello di prezzo fornisca prestazioni insufficienti.</span><span class="sxs-lookup"><span data-stu-id="5d954-234">For this tutorial, hello free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="5d954-235">In hello **configurare il piano di servizio App** finestra di dialogo, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d954-235">In hello **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Fare clic su OK in Configura piano di servizio app](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="5d954-237">In hello **Crea servizio App** la finestra di dialogo, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="5d954-237">In hello **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Fare clic su Crea nella finestra di dialogo Crea servizio app](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="5d954-239">Visual Studio crea app hello per le API e un profilo di pubblicazione che dispone di tutte le impostazioni di hello necessario per l'applicazione hello API.</span><span class="sxs-lookup"><span data-stu-id="5d954-239">Visual Studio creates hello API app and a publish profile that has all of hello required settings for hello API app.</span></span> <span data-ttu-id="5d954-240">Apre hello **pubblica sul Web** guidata, si userà progetto hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="5d954-240">Then it opens hello **Publish Web** wizard, which you'll use toodeploy hello project.</span></span>
    
    <span data-ttu-id="5d954-241">Hello **pubblica sul Web** guidato su hello **connessione** scheda (mostrata sotto).</span><span class="sxs-lookup"><span data-stu-id="5d954-241">hello **Publish Web** wizard opens on hello **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="5d954-242">In hello **connessione** scheda hello **Server** e **nome sito** impostazioni punto tooyour API app.</span><span class="sxs-lookup"><span data-stu-id="5d954-242">On hello **Connection** tab, hello **Server** and **Site name** settings point tooyour API app.</span></span> <span data-ttu-id="5d954-243">Hello **nome utente** e **Password** sono le credenziali di distribuzione Azure crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5d954-243">hello **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="5d954-244">Dopo la distribuzione, Visual Studio apre un browser toohello **URL di destinazione** (che è l'unico scopo di hello per **URL di destinazione**).</span><span class="sxs-lookup"><span data-stu-id="5d954-244">After deployment, Visual Studio opens a browser toohello **Destination URL** (that's hello only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="5d954-245">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5d954-245">Click **Next**.</span></span>
    
    ![Fare clic su Avanti nella scheda Connessione di Pubblica sito Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="5d954-247">scheda successiva Hello è hello **impostazioni** scheda (mostrata sotto).</span><span class="sxs-lookup"><span data-stu-id="5d954-247">hello next tab is hello **Settings** tab (shown below).</span></span> <span data-ttu-id="5d954-248">Qui è possibile modificare hello compilazione configurazione scheda toodeploy una build di debug per [il debug remoto](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="5d954-248">Here you can change hello build configuration tab toodeploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="5d954-249">Hello scheda offre inoltre diversi **Opzioni pubblicazione File**:</span><span class="sxs-lookup"><span data-stu-id="5d954-249">hello tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="5d954-250">Rimuovi i file aggiuntivi nella destinazione</span><span class="sxs-lookup"><span data-stu-id="5d954-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="5d954-251">Precompila durante la pubblicazione</span><span class="sxs-lookup"><span data-stu-id="5d954-251">Precompile during publishing</span></span>
    * <span data-ttu-id="5d954-252">Escludi file dalla cartella App_Data hello</span><span class="sxs-lookup"><span data-stu-id="5d954-252">Exclude files from hello App_Data folder</span></span>
    
    <span data-ttu-id="5d954-253">Per questa esercitazione non ne è necessaria nessuna.</span><span class="sxs-lookup"><span data-stu-id="5d954-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="5d954-254">Per una descrizione dettagliata del funzionamento di queste opzioni, vedere [Procedura: Distribuire un progetto di applicazione Web tramite la pubblicazione con un clic in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d954-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="5d954-255">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5d954-255">Click **Next**.</span></span>
    
    ![Fare clic su Avanti nella scheda Impostazioni di Pubblica sito Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="5d954-257">Di seguito è riportato hello **anteprima** scheda (mostrata sotto), che consente un'opportunità toosee quali file verranno copiati dal progetto toohello API app toobe.</span><span class="sxs-lookup"><span data-stu-id="5d954-257">Next is hello **Preview** tab (shown below), which gives you an opportunity toosee what files are going toobe copied from your project toohello API app.</span></span> <span data-ttu-id="5d954-258">Quando si distribuisce un progetto di app tooan API che è già stato distribuito tooearlier, vengono copiati solo i file modificati.</span><span class="sxs-lookup"><span data-stu-id="5d954-258">When you're deploying a project tooan API app that you already deployed tooearlier, only changed files are copied.</span></span> <span data-ttu-id="5d954-259">Se si desidera un elenco di ciò che verrà copiato toosee, è possibile fare clic su hello **avviare Anteprima** pulsante.</span><span class="sxs-lookup"><span data-stu-id="5d954-259">If you want toosee a list of what will be copied, you can click hello **Start Preview** button.</span></span>
15. <span data-ttu-id="5d954-260">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="5d954-260">Click **Publish**.</span></span>
    
    ![Fare clic su Pubblica nella scheda Anteprima di Pubblica sito Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="5d954-262">Visual Studio distribuisce hello ToDoListDataAPI progetto toohello nuova app per le API.</span><span class="sxs-lookup"><span data-stu-id="5d954-262">Visual Studio deploys hello ToDoListDataAPI project toohello new API app.</span></span> <span data-ttu-id="5d954-263">Hello **Output** finestra registri di distribuzione ha esito positivo e viene visualizzata una pagina "è stata creata" in un URL di toohello finestra aperta del browser di applicazione hello API.</span><span class="sxs-lookup"><span data-stu-id="5d954-263">hello **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened toohello URL of hello API app.</span></span>
    
    ![Finestra di output che segnala che la distribuzione è completata](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Pagina che segnala che la creazione dell'app per le API è completata](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="5d954-266">Aggiungere "swagger" toohello URL nella barra degli indirizzi del browser hello e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="5d954-266">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="5d954-267">(hello URL `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="5d954-267">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="5d954-268">browser Hello Visualizza hello stesso Swagger dell'interfaccia utente che è stato illustrato in precedenza, ma ora è in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-268">hello browser displays hello same Swagger UI that you saw earlier, but now it's running in hello cloud.</span></span> <span data-ttu-id="5d954-269">Provare hello metodo Get, e viene visualizzato che hai toohello indietro predefinito 2 attività da svolgere.</span><span class="sxs-lookup"><span data-stu-id="5d954-269">Try out hello Get method, and you see that you're back toohello default 2 to-do items.</span></span> <span data-ttu-id="5d954-270">modifiche di Hello apportate in precedenza sono state salvate in memoria nel computer locale hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-270">hello changes you made earlier were saved in memory in hello local machine.</span></span>
17. <span data-ttu-id="5d954-271">Aprire hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5d954-271">Open hello [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="5d954-272">Hello portale di Azure è un'interfaccia web per la gestione delle risorse di Azure, ad esempio di App per le API.</span><span class="sxs-lookup"><span data-stu-id="5d954-272">hello Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="5d954-273">Fare clic su **Altri servizi > Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="5d954-273">Click **More Services > App Services**.</span></span>
    
    ![Selezionare Servizi app](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="5d954-275">In hello **servizi App** pannello, trovare e fare clic su nuova app per le API.</span><span class="sxs-lookup"><span data-stu-id="5d954-275">In hello **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="5d954-276">(In hello portale di Azure, sono detti finestre aperte destra toohello *pannelli*.)</span><span class="sxs-lookup"><span data-stu-id="5d954-276">(In hello Azure portal, windows that open toohello right are called *blades*.)</span></span>
    
    ![Pannello Servizi app](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="5d954-278">Vengono aperti due pannelli,</span><span class="sxs-lookup"><span data-stu-id="5d954-278">Two blades open.</span></span> <span data-ttu-id="5d954-279">Uno è un lungo elenco di impostazioni che è possibile visualizzare e modificare una panoramica delle app per le API hello dispone di un pannello.</span><span class="sxs-lookup"><span data-stu-id="5d954-279">One blade has an overview of hello API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="5d954-280">In hello **impostazioni** blade, hello trova **API** sezione e fare clic su **di definizione dell'API**.</span><span class="sxs-lookup"><span data-stu-id="5d954-280">In hello **Settings** blade, find hello **API** section and click **API Definition**.</span></span>
    
    ![Definizione dell'API nel pannello Impostazioni](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="5d954-282">Hello **di definizione dell'API** pannello consente di specificare l'URL di hello che restituisce i metadati di Swagger 2.0 in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="5d954-282">hello **API Definition** blade lets you specify hello URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="5d954-283">Quando Visual Studio crea applicazione hello API, imposta il valore predefinito toohello di hello API definizione URL di base Swashbuckle metadati generati che illustrato in precedenza, ovvero app hello API URL più `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="5d954-283">When Visual Studio creates hello API app, it sets hello API definition URL toohello default value for Swashbuckle-generated metadata that you saw earlier, which is hello API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL di definizione dell'API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="5d954-285">Quando si seleziona un codice client dell'API app toogenerate per tale, Visual Studio recupera i metadati di hello dal seguente URL.</span><span class="sxs-lookup"><span data-stu-id="5d954-285">When you select an API app toogenerate client code for it, Visual Studio retrieves hello metadata from this URL.</span></span>

## <span data-ttu-id="5d954-286"><a id="codegen"></a>Generare codice client per il livello di dati hello</span><span class="sxs-lookup"><span data-stu-id="5d954-286"><a id="codegen"></a> Generate client code for hello data tier</span></span>
<span data-ttu-id="5d954-287">Uno dei vantaggi di hello dell'integrazione di Swagger in App per le API di Azure è la generazione automatica di codice.</span><span class="sxs-lookup"><span data-stu-id="5d954-287">One of hello advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="5d954-288">Classi client generate rendono più semplice toowrite il codice che chiama un'API app.</span><span class="sxs-lookup"><span data-stu-id="5d954-288">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="5d954-289">progetto ToDoListAPI Hello dispone già di hello generato il codice client, ma in hello alla procedura seguente viene eliminato e rigenerarlo toosee come la generazione di codice hello toodo.</span><span class="sxs-lookup"><span data-stu-id="5d954-289">hello ToDoListAPI project already has hello generated client code, but in hello following steps you'll delete it and regenerate it toosee how toodo hello code generation.</span></span>

1. <span data-ttu-id="5d954-290">In Visual Studio **Esplora**, hello ToDoListAPI project, eliminare hello *ToDoListDataAPI* cartella.</span><span class="sxs-lookup"><span data-stu-id="5d954-290">In Visual Studio **Solution Explorer**, in hello ToDoListAPI project, delete hello *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="5d954-291">**Attenzione: Eliminare solo cartelle di hello, non il progetto di ToDoListDataAPI hello.**</span><span class="sxs-lookup"><span data-stu-id="5d954-291">**Caution: Delete only hello folder, not hello ToDoListDataAPI project.**</span></span>
   
    ![Eliminare il codice client generato](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="5d954-293">Questa cartella è stata creata con processo di generazione di codice hello è quasi toogo tramite.</span><span class="sxs-lookup"><span data-stu-id="5d954-293">This folder was created by using hello code generation process that you're about toogo through.</span></span>
2. <span data-ttu-id="5d954-294">Fare clic sul progetto ToDoListAPI hello e quindi fare clic su **Aggiungi > Client dell'API REST**.</span><span class="sxs-lookup"><span data-stu-id="5d954-294">Right-click hello ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Aggiungere il client API REST in Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="5d954-296">In hello **aggiungere Client dell'API REST** nella finestra di dialogo fare clic su **URL Swagger**, quindi fare clic su **selezionare Asset Azure**.</span><span class="sxs-lookup"><span data-stu-id="5d954-296">In hello **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Seleziona asset di Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="5d954-298">In hello **servizio App** nella finestra di dialogo espandere il gruppo di risorse hello in uso per questa esercitazione selezionare app per le API e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d954-298">In hello **App Service** dialog box, expand hello resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Selezionare l'app per le API per la generazione di codice](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="5d954-300">Si noti che quando si torna toohello **aggiungere Client dell'API REST** finestra di dialogo, la casella di testo hello è stato compilato con definizione hello API valore di URL che è stato illustrato in precedenza nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-300">Notice that when you return toohello **Add REST API Client** dialog, hello text box has been filled in with hello API definition URL value that you saw earlier in hello portal.</span></span>
   
    ![URL di definizione dell'API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="5d954-302">I metadati di tooget un modo alternativo per la generazione di codice sono tooenter hello URL direttamente anziché passare attraverso una finestra di dialogo Sfoglia hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-302">An alternative way tooget metadata for code generation is tooenter hello URL directly instead of going through hello browse dialog.</span></span> <span data-ttu-id="5d954-303">O se si desidera il codice client toogenerate prima di distribuire tooAzure, è possibile eseguire il progetto API Web hello localmente, Vai a URL toohello che fornisce file Swagger JSON hello, salvare il file hello, e utilizzare hello **selezionare un file di metadati Swagger esistente**opzione.</span><span class="sxs-lookup"><span data-stu-id="5d954-303">Or if you want toogenerate client code before deploying tooAzure, you could run hello Web API project locally, go toohello URL that provides hello Swagger JSON file, save hello file, and use hello **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="5d954-304">In hello **aggiungere Client dell'API REST** la finestra di dialogo, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d954-304">In hello **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="5d954-305">Visual Studio crea una cartella denominata dopo l'applicazione hello API e genera classi del client.</span><span class="sxs-lookup"><span data-stu-id="5d954-305">Visual Studio creates a folder named after hello API app and generates client classes.</span></span>
   
    ![File di codice per il client generato](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="5d954-307">Nel progetto ToDoListAPI hello aprire *Controllers\ToDoListController.cs* codice hello toosee riga 40 che chiama l'API di hello utilizzando client hello generato.</span><span class="sxs-lookup"><span data-stu-id="5d954-307">In hello ToDoListAPI project, open *Controllers\ToDoListController.cs* toosee hello code at line 40  that calls hello API by using hello generated client.</span></span>
   
    <span data-ttu-id="5d954-308">Hello frammento di codice seguente viene illustrato come codice hello crea un'istanza di oggetto client hello e chiamate hello metodo Get.</span><span class="sxs-lookup"><span data-stu-id="5d954-308">hello following snippet shows how hello code instantiates hello client object and calls hello Get method.</span></span>
   
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
   
    <span data-ttu-id="5d954-309">parametro del costruttore Hello Ottiene hello URL dell'endpoint da hello `toDoListDataAPIURL` impostazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="5d954-309">hello constructor parameter gets hello endpoint URL from  hello `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="5d954-310">Nel file Web. config hello, tale valore è toohello set IIS Express URL locale di hello API progetto in modo che è possibile eseguire un'applicazione hello in locale.</span><span class="sxs-lookup"><span data-stu-id="5d954-310">In hello Web.config file, that value is set toohello local IIS Express URL of hello API project so that you can run hello application locally.</span></span> <span data-ttu-id="5d954-311">Se si omette un parametro di costruttore hello, endpoint predefinito hello è hello URL che è stato generato codice hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-311">If you omit hello constructor parameter, hello default endpoint is hello URL that you generated hello code from.</span></span>
7. <span data-ttu-id="5d954-312">Classe del client verrà generata con un nome diverso in base al nome di app API; modificare il codice hello in *Controllers\ToDoListController.cs* in modo che hello nome del tipo corrisponde a ciò che è stato generato nel progetto.</span><span class="sxs-lookup"><span data-stu-id="5d954-312">Your client class will be generated with a different name based on your API app name; change hello code in *Controllers\ToDoListController.cs* so that hello type name matches what was generated in your project.</span></span> <span data-ttu-id="5d954-313">Se, ad esempio, si è assegnato all'app per le API il nome ToDoListDataAPI071316, si sostituirà questo codice:</span><span class="sxs-lookup"><span data-stu-id="5d954-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="5d954-314">toothis:</span><span class="sxs-lookup"><span data-stu-id="5d954-314">toothis:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a><span data-ttu-id="5d954-315">Creare un livello intermedio API app toohost hello</span><span class="sxs-lookup"><span data-stu-id="5d954-315">Create an API app toohost hello middle tier</span></span>
<span data-ttu-id="5d954-316">In precedenza si [hello dati livello API app creata e distribuita codice tooit](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="5d954-316">Earlier you [created hello data tier API app and deployed code tooit](#createapiapp).</span></span>  <span data-ttu-id="5d954-317">Ora è seguire hello stessa procedura per l'applicazione di livello intermedio API hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-317">Now you follow hello same procedure for hello middle tier API app.</span></span>

1. <span data-ttu-id="5d954-318">In **Esplora**, livello intermedio rapida hello ToDoListAPI progetto (non hello livello dati ToDoListDataAPI) e quindi fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="5d954-318">In **Solution Explorer**, right-click hello middle tier ToDoListAPI  project (not hello data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Fare clic su Pubblica in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="5d954-320">In hello **profilo** scheda di hello **pubblica sul Web** procedura guidata, fare clic su **servizio App di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="5d954-320">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="5d954-321">In hello **servizio App** la finestra di dialogo, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="5d954-321">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="5d954-322">In hello **Hosting** scheda di hello **Crea servizio App** finestra di dialogo casella, accettare l'impostazione predefinita di hello **API App Name** o immettere un nome univoco nel hello  *azurewebsites.NET* dominio.</span><span class="sxs-lookup"><span data-stu-id="5d954-322">In hello **Hosting** tab of hello **Create App Service** dialog box, accept hello default **API App Name** or enter a name that is unique in hello *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="5d954-323">Scegliere hello Azure **sottoscrizione** è stato utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5d954-323">Choose hello Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="5d954-324">In hello **gruppo di risorse** elenco a discesa, scegliere hello stesso gruppo di risorse creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5d954-324">In hello **Resource Group** drop-down, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="5d954-325">In hello **piano di servizio App** elenco a discesa, scegliere hello stesso piano creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5d954-325">In hello **App Service Plan** drop-down, choose hello same plan you created earlier.</span></span> <span data-ttu-id="5d954-326">Verrà aperta toothat valore.</span><span class="sxs-lookup"><span data-stu-id="5d954-326">It will default toothat value.</span></span>
8. <span data-ttu-id="5d954-327">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5d954-327">Click **Create**.</span></span>
   
    <span data-ttu-id="5d954-328">Visual Studio crea hello API app, crea un profilo di pubblicazione per tale e Visualizza hello **connessione** passaggio di hello **pubblica sul Web** procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="5d954-328">Visual Studio creates hello API app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
9. <span data-ttu-id="5d954-329">In hello **connessione** passaggio di hello **pubblica sul Web** procedura guidata, fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="5d954-329">In hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="5d954-330">Visual Studio distribuisce hello ToDoListAPI progetto toohello nuova app per le API e apre un browser toohello URL app hello per le API.</span><span class="sxs-lookup"><span data-stu-id="5d954-330">Visual Studio deploys hello ToDoListAPI project toohello new API app and opens a browser toohello URL of hello API app.</span></span> <span data-ttu-id="5d954-331">verrà visualizzata la pagina Hello "completata".</span><span class="sxs-lookup"><span data-stu-id="5d954-331">hello "successfully created" page appears.</span></span>

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a><span data-ttu-id="5d954-332">Configurare il livello dati hello di hello intermedio toocall</span><span class="sxs-lookup"><span data-stu-id="5d954-332">Configure hello middle tier toocall hello data tier</span></span>
<span data-ttu-id="5d954-333">Se è stato chiamato app API di livello intermedio hello ora, cercherà di livello dati di hello toocall utilizzando URL localhost hello che è ancora in Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-333">If you called hello middle tier API app now, it would try toocall hello data tier using hello localhost URL that is still in hello Web.config file.</span></span> <span data-ttu-id="5d954-334">In questa sezione è immettere hello dati livello API app URL in un'impostazione di ambiente app hello per le API livello intermedio.</span><span class="sxs-lookup"><span data-stu-id="5d954-334">In this section you enter hello data tier API app URL into an environment setting in hello middle tier API app.</span></span> <span data-ttu-id="5d954-335">Quando hello codice nell'app di API di livello intermedio hello recupera impostazione URL di livello dati hello, impostazione di ambiente hello sostituiranno novità nel file Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-335">When hello code in hello middle tier API app retrieves hello data tier URL setting, hello environment setting will override what's in hello Web.config file.</span></span>

1. <span data-ttu-id="5d954-336">Passare toohello [portale di Azure](https://portal.azure.com/), quindi passare toohello **App per le API** pannello per l'applicazione hello API creata dal progetto di toohost hello TodoListAPI (intermedio).</span><span class="sxs-lookup"><span data-stu-id="5d954-336">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **API App** blade for hello API app that you created toohost hello TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="5d954-337">Nell'API dell'applicazione di hello **impostazioni** pannello, fare clic su **le impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="5d954-337">In hello API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="5d954-338">Nell'API dell'applicazione di hello **le impostazioni dell'applicazione** pannello, scorrere verso il basso toohello **le impostazioni dell'App** sezione e aggiungere il seguente hello chiave e il valore.</span><span class="sxs-lookup"><span data-stu-id="5d954-338">In hello API App's **Application Settings** blade, scroll down toohello **App settings** section and add hello following key and value.</span></span> <span data-ttu-id="5d954-339">il valore di Hello sarà hello URL dell'API prima hello App pubblicata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5d954-339">hello value will be hello URL of hello first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="5d954-340">**Chiave**</span><span class="sxs-lookup"><span data-stu-id="5d954-340">**Key**</span></span> | <span data-ttu-id="5d954-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="5d954-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="5d954-342">**Valore**</span><span class="sxs-lookup"><span data-stu-id="5d954-342">**Value**</span></span> |<span data-ttu-id="5d954-343">https://{nome dell'app per le API di livello dati}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="5d954-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="5d954-344">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="5d954-344">**Example**</span></span> |<span data-ttu-id="5d954-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="5d954-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="5d954-346">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="5d954-346">Click **Save**.</span></span>
   
    ![Fare clic su Salva per le impostazioni dell'app](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="5d954-348">Quando l'esecuzione del codice hello in Azure, questo valore sostituirà ora hello localhost URL nel file Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-348">When hello code runs in Azure, this value will now override hello localhost URL that is in hello Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="5d954-349">Test</span><span class="sxs-lookup"><span data-stu-id="5d954-349">Test</span></span>
1. <span data-ttu-id="5d954-350">In una finestra del browser, passare URL toohello di livello intermedio nuova app per le API appena creata per ToDoListAPI hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-350">In a browser window, browse toohello URL of hello new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="5d954-351">È possibile ottenere sono facendo hello URL nel pannello principale di hello API dell'app nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-351">You can get there by clicking hello URL in hello API app's main blade in hello portal.</span></span>
2. <span data-ttu-id="5d954-352">Aggiungere "swagger" toohello URL nella barra degli indirizzi del browser hello e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="5d954-352">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="5d954-353">(hello URL `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="5d954-353">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="5d954-354">browser viene visualizzata Hello hello stesso Swagger dell'interfaccia utente che illustrato in precedenza per ToDoListDataAPI, ma ora `owner` non è un campo obbligatorio per l'operazione Get hello, perché l'applicazione di livello intermedio API hello invia tale valore toohello dati livello app per le API per l'utente.</span><span class="sxs-lookup"><span data-stu-id="5d954-354">hello browser displays hello same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for hello Get operation, because hello middle tier API app is sending that value toohello data tier API app for you.</span></span> <span data-ttu-id="5d954-355">(Quando hello esercitazioni di autenticazione, livello intermedio hello invierà ID utente effettivo per hello `owner` parametro; per questo punto è a livello di codice un asterisco.)</span><span class="sxs-lookup"><span data-stu-id="5d954-355">(When you do hello authentication tutorials, hello middle tier will send actual user IDs for hello `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="5d954-356">Provare hello metodo Get e hello altri toovalidate metodi che hello app API di livello intermedio è esito positivo della chiamata hello dati livello app per le API.</span><span class="sxs-lookup"><span data-stu-id="5d954-356">Try out hello Get method and hello other methods toovalidate that hello middle tier API app is successfully calling hello data tier API app.</span></span>
   
    ![Metodo Get dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="5d954-358">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="5d954-358">Troubleshooting</span></span>
<span data-ttu-id="5d954-359">In caso di problemi nel corso dell'esercitazione, ecco alcune idee per risolverli:</span><span class="sxs-lookup"><span data-stu-id="5d954-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="5d954-360">Assicurarsi che si usi l'ultima versione di hello di hello [Azure SDK per .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="5d954-360">Make sure that you're using hello latest version of hello [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="5d954-361">Due hello nomi di progetto sono simili (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="5d954-361">Two of hello project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="5d954-362">Se il documento non è quello come descritto nelle istruzioni di hello quando si lavora con un progetto, verificare che hello corretto progetto è stato aperto.</span><span class="sxs-lookup"><span data-stu-id="5d954-362">If things don't look as described in hello instructions when you are working with a project, make sure you have opened hello correct project.</span></span>
* <span data-ttu-id="5d954-363">Se è attiva in una rete aziendale e si sta tentando di toodeploy tooAzure servizio App attraverso un firewall, assicurarsi che le porte 443 e 8172 siano aperte per distribuzione Web.</span><span class="sxs-lookup"><span data-stu-id="5d954-363">If you're on a corporate network and are trying toodeploy tooAzure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="5d954-364">Se non è possibile aprire tali porte, si possono usare altri metodi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5d954-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="5d954-365">Vedere [distribuire il servizio App di tooAzure app](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5d954-365">See [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="5d954-366">Errori di "nomi di route devono essere univoci", è possibile ottenere questi se si distribuire accidentalmente hello progetto errato tooan API app e distribuirla in un secondo momento una tooit corretta hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-366">"Route names must be unique" errors -- you could get these if you accidentally deploy hello wrong project tooan API app and then later deploy hello correct one tooit.</span></span> <span data-ttu-id="5d954-367">toocorrect, ridistribuire hello progetto corretto toohello API app e su hello **impostazioni** scheda di hello **pubblica sul Web** procedura guidata seleziona **Rimuovi file aggiuntivi nella destinazione**.</span><span class="sxs-lookup"><span data-stu-id="5d954-367">toocorrect this, redeploy hello correct project toohello API app, and on hello **Settings** tab of hello **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="5d954-368">Dopo aver app per le API di ASP.NET in esecuzione in Azure App Service, è consigliabile toolearn ulteriori informazioni sulle funzionalità di Visual Studio che semplificano la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="5d954-368">After you have your ASP.NET API app running in Azure App Service, you may want toolearn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="5d954-369">Per informazioni sulla registrazione, il debug remoto e altro ancora, vedere [Risoluzione dei problemi di un'app Web nel servizio app di Azure tramite Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="5d954-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d954-370">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d954-370">Next steps</span></span>
<span data-ttu-id="5d954-371">È stato illustrato come generare codice client per App per le API toodeploy API Web progetti tooAPI App esistenti e utilizzare App per le API da client .NET.</span><span class="sxs-lookup"><span data-stu-id="5d954-371">You've seen how toodeploy existing Web API projects tooAPI apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="5d954-372">Hello successivo di questa serie vengono descritte le modalità troppo[usare App tooconsume API CORS da client JavaScript](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="5d954-372">hello next tutorial in this series shows how too[use CORS tooconsume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="5d954-373">Per ulteriori informazioni sulla generazione del codice client, vedere hello [Azure/AutoRest](https://github.com/azure/autorest) repository in GitHub.com. Per informazioni sui problemi utilizzando client hello generato, aprire un [problema nel repository AutoRest hello](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="5d954-373">For more information about client code generation, see hello [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com. For help with problems using hello generated client, open an [issue in hello AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="5d954-374">Se si desidera toocreate nuovi progetti API app da zero, utilizzare hello **Azure API App** modello.</span><span class="sxs-lookup"><span data-stu-id="5d954-374">If you want toocreate new API app projects from scratch, use hello **Azure API App** template.</span></span>

![Modello di app per le API in Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="5d954-376">Hello **Azure API App** modello di progetto è hello equivalente toochoosing **vuoto** ASP.NET 4.5.2 modello, fare clic sul supporto di API Web tooadd di hello casella di controllo e l'installazione del pacchetto Swashbuckle NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="5d954-376">hello **Azure API App** project template is equivalent toochoosing hello **Empty** ASP.NET 4.5.2 template, clicking hello check box tooadd Web API support, and installing hello Swashbuckle NuGet package.</span></span> <span data-ttu-id="5d954-377">Inoltre, modello hello viene alcuni Swashbuckle configurazione codice progettato tooprevent hello creato duplicati Swagger operazione ID.</span><span class="sxs-lookup"><span data-stu-id="5d954-377">In addition, hello template adds some Swashbuckle configuration code designed tooprevent hello creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="5d954-378">Dopo aver creato un progetto di App per le API, è possibile distribuirlo hello app tooan API allo stesso modo è stato illustrato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5d954-378">Once you've created an API App project, you can deploy it tooan API app hello same way you saw in this tutorial.</span></span>

