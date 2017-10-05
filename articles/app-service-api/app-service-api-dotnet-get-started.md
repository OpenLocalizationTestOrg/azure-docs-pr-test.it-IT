---
title: Introduzione alle app per le API e ad ASP.NET in Servizio app | Microsoft Docs
description: Informazioni su come creare un'app per le API ASP.NET nel servizio app di Azure con Visual Studio 2015.
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
ms.openlocfilehash: e8fbffde29efcdbb2f67362474061e9f6ee0d59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="9d025-103">Introduzione alle app per le API, ad ASP.NET e a Swagger in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="9d025-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="9d025-104">Questa è la prima di una serie di esercitazioni che illustrano come usare le funzionalità del servizio app di Azure utili per lo sviluppo e l'hosting di API RESTful.</span><span class="sxs-lookup"><span data-stu-id="9d025-104">This is the first in a series of tutorials that show how to use features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="9d025-105">Questa esercitazione illustra il supporto per i metadati dell'API in formato Swagger.</span><span class="sxs-lookup"><span data-stu-id="9d025-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="9d025-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="9d025-106">You'll learn:</span></span>

* <span data-ttu-id="9d025-107">Creare e distribuire [app per le API](app-service-api-apps-why-best-platform.md) in Servizio app di Azure usando gli strumenti predefiniti di Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9d025-107">How to create and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="9d025-108">Automatizzare l'individuazione di API tramite il pacchetto NuGet Swashbuckle per generare in modo dinamico i metadati dell'API Swagger.</span><span class="sxs-lookup"><span data-stu-id="9d025-108">How to automate API discovery by using the Swashbuckle NuGet package to dynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="9d025-109">Usare i metadati dell'API Swagger per generare automaticamente il codice client per un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-109">How to use Swagger API metadata to automatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="9d025-110">Panoramica dell'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="9d025-110">Sample application overview</span></span>
<span data-ttu-id="9d025-111">In questa esercitazione si usa una semplice applicazione di esempio di elenco attività.</span><span class="sxs-lookup"><span data-stu-id="9d025-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="9d025-112">L'applicazione ha un front-end costituito da un'applicazione a singola pagina, un livello intermedio con un'API Web ASP.NET e un livello dati con un'API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9d025-112">The application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Diagramma dell'applicazione di esempio di app per le API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="9d025-114">Di seguito è riportata una schermata del front-end [AngularJS](https://angularjs.org/) .</span><span class="sxs-lookup"><span data-stu-id="9d025-114">Here's a screen shot of the [AngularJS](https://angularjs.org/) front end.</span></span>

![Elenco attività dell'applicazione di esempio app per le API](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="9d025-116">La soluzione di Visual Studio contiene tre progetti:</span><span class="sxs-lookup"><span data-stu-id="9d025-116">The Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="9d025-117">**ToDoListAngular**: front-end. Un'applicazione a singola pagina AngularJS che chiama il livello intermedio.</span><span class="sxs-lookup"><span data-stu-id="9d025-117">**ToDoListAngular** - The front end: an AngularJS SPA that calls the middle tier.</span></span>
* <span data-ttu-id="9d025-118">**ToDoListAPI**: livello intermedio. Un progetto API Web ASP.NET che chiama il livello dati per eseguire operazioni CRUD sulle attività.</span><span class="sxs-lookup"><span data-stu-id="9d025-118">**ToDoListAPI** - The middle tier: an ASP.NET Web API project that calls the data tier to perform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="9d025-119">**ToDoListDataAPI**: livello dati. Un progetto API Web ASP.NET che esegue operazioni CRUD sulle attività.</span><span class="sxs-lookup"><span data-stu-id="9d025-119">**ToDoListDataAPI** - The data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="9d025-120">L'architettura a tre livelli è una delle tante che è possibile implementare usando le app per le API e viene usata qui solo a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="9d025-120">The three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="9d025-121">Il codice in ogni livello è quello più semplice possibile per illustrate le funzionalità delle app per le API. Il livello dati, ad esempio, usa la memoria del server invece di un database come meccanismo di salvataggio permanente.</span><span class="sxs-lookup"><span data-stu-id="9d025-121">The code in each tier is as simple as possible to demonstrate API Apps features; for example, the data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="9d025-122">Al termine di questa esercitazione, i due progetti di API Web saranno in esecuzione nel cloud tra le app per le API del servizio app.</span><span class="sxs-lookup"><span data-stu-id="9d025-122">On completing this tutorial, you'll have the two Web API projects up and running in the cloud in App Service API apps.</span></span>

<span data-ttu-id="9d025-123">L'esercitazione successiva della serie distribuisce il front-end dell'applicazione a singola pagina nel cloud.</span><span class="sxs-lookup"><span data-stu-id="9d025-123">The next tutorial in the series deploys the SPA front end to the cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d025-124">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9d025-124">Prerequisites</span></span>
* <span data-ttu-id="9d025-125">API Web ASP.NET: le istruzioni dell'esercitazione presuppongono che l'utente abbia una conoscenza di base dell'uso dell' [API Web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) ASP.NET in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9d025-125">ASP.NET Web API - The tutorial instructions assume you have a basic knowledge of how to work with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="9d025-126">Account Azure: è possibile [aprire un account Azure gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) o [attivare i benefici della sottoscrizione di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="9d025-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="9d025-127">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, passare alla pagina [Prova il servizio app](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="9d025-127">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="9d025-128">In questa pagina è possibile creare immediatamente un'app iniziale temporanea nel servizio app, **senza carta di credito**e senza impegno.</span><span class="sxs-lookup"><span data-stu-id="9d025-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="9d025-129">Visual Studio 2015 con [Azure SDK per .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) : l'SDK installa Visual Studio 2015 automaticamente se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="9d025-129">Visual Studio 2015 with the [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - The SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="9d025-130">In Visual Studio fare clic su ? -> Informazioni su Microsoft Visual Studio e assicurarsi di aver installato "Strumenti del servizio app di Azure versione 2.9.1" o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="9d025-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Versione di Strumenti del servizio app di Azure](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="9d025-132">In base al numero di dipendenze da SDK già presenti nel computer, l'installazione dell'SDK può richiedere tempi lunghi, da alcuni minuti ad almeno mezz'ora.</span><span class="sxs-lookup"><span data-stu-id="9d025-132">Depending on how many of the SDK dependencies you already have on your machine, installing the SDK could take a long time, from several minutes to a half hour or more.</span></span>
    > 
    > 

## <a name="download-the-sample-application"></a><span data-ttu-id="9d025-133">Scaricare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="9d025-133">Download the sample application</span></span>
1. <span data-ttu-id="9d025-134">Scaricare il repository [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) .</span><span class="sxs-lookup"><span data-stu-id="9d025-134">Download the [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="9d025-135">È possibile fare clic sul pulsante **Download ZIP** o clonare il repository nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="9d025-135">You can click the **Download ZIP** button or clone the repository on your local machine.</span></span>
2. <span data-ttu-id="9d025-136">Aprire la soluzione ToDoList in Visual Studio 2015 o 2013.</span><span class="sxs-lookup"><span data-stu-id="9d025-136">Open the ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="9d025-137">È necessario considerare attendibile ogni soluzione.</span><span class="sxs-lookup"><span data-stu-id="9d025-137">You will need to trust each solution.</span></span>
         <span data-ttu-id="9d025-138">![Avviso di sicurezza](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="9d025-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="9d025-139">Compilare la soluzione (CTRL+MAIUSC+B) per ripristinare i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="9d025-139">Build the solution (CTRL + SHIFT + B)  to restore the NuGet packages.</span></span>
   
    <span data-ttu-id="9d025-140">Per osservare l'applicazione in esecuzione prima di distribuirla, è possibile eseguirla in locale.</span><span class="sxs-lookup"><span data-stu-id="9d025-140">If you want to see the application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="9d025-141">Verificare che ToDoListDataAPI sia il progetto di avvio ed eseguire la soluzione.</span><span class="sxs-lookup"><span data-stu-id="9d025-141">Make sure that ToDoListDataAPI is your startup project and run the solution.</span></span> <span data-ttu-id="9d025-142">È probabile che nel browser venga visualizzato un errore HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="9d025-142">You should expect to see a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="9d025-143">Usare l'interfaccia utente e i metadati dell'API Swagger</span><span class="sxs-lookup"><span data-stu-id="9d025-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="9d025-144">Il supporto per i metadati dell'API [Swagger](http://swagger.io/) 2.0 è integrato nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d025-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="9d025-145">Ogni app per le API può specificare un endpoint dell'URL che restituisce i metadati per l'API in formato JSON Swagger.</span><span class="sxs-lookup"><span data-stu-id="9d025-145">Each API app can specify a URL endpoint that returns metadata for the API in Swagger JSON format.</span></span> <span data-ttu-id="9d025-146">I metadati restituiti da tale endpoint possono essere usati per generare codice client.</span><span class="sxs-lookup"><span data-stu-id="9d025-146">The metadata returned from that endpoint can be used to generate client code.</span></span>

<span data-ttu-id="9d025-147">Un progetto API Web ASP.NET può generare in modo dinamico i metadati di Swagger usando il pacchetto NuGet [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) .</span><span class="sxs-lookup"><span data-stu-id="9d025-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="9d025-148">Il pacchetto NuGet Swashbuckle è già installato in ToDoListDataAPI e nei progetto ToDoListAPI scaricati.</span><span class="sxs-lookup"><span data-stu-id="9d025-148">The Swashbuckle NuGet package is already installed in the ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="9d025-149">In questa sezione dell'esercitazione si esaminano i metadati di Swagger 2.0 generati e quindi si prova un'interfaccia utente di test basata sui metadati di Swagger.</span><span class="sxs-lookup"><span data-stu-id="9d025-149">In this section of the tutorial, you look at the generated Swagger 2.0 metadata, and then you try out a test UI that is based on the Swagger metadata.</span></span>

1. <span data-ttu-id="9d025-150">Impostare il progetto ToDoListDataAPI come progetto di avvio,**non** come progetto ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="9d025-150">Set the ToDoListDataAPI project (**not** the ToDoListAPI project) as the startup project.</span></span>
   
    ![Impostare ToDoDataAPI come progetto di avvio](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="9d025-152">Premere F5 o fare clic su **Debug > Avvia debug** per eseguire il progetto in modalità debug.</span><span class="sxs-lookup"><span data-stu-id="9d025-152">Press F5 or click **Debug > Start Debugging** to run the project in debug mode.</span></span>
   
    <span data-ttu-id="9d025-153">Verrà aperto il browser alla pagina di errore HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="9d025-153">The browser opens and shows the HTTP 403 error page.</span></span>
3. <span data-ttu-id="9d025-154">Nella barra degli indirizzi del browser aggiungere `swagger/docs/v1` alla fine della riga e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="9d025-154">In your browser address bar, add `swagger/docs/v1` to the end of the line, and then press Return.</span></span> <span data-ttu-id="9d025-155">L'URL è `http://localhost:45914/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="9d025-155">(The URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="9d025-156">Questo è l'URL predefinito usato da Swashbuckle per restituire i metadati JSON di Swagger 2.0 per l'API.</span><span class="sxs-lookup"><span data-stu-id="9d025-156">This is the default URL used by Swashbuckle to return Swagger 2.0 JSON metadata for the API.</span></span>
   
    <span data-ttu-id="9d025-157">Se si usa Internet Explorer, il browser richiede di scaricare un file *v1.json* .</span><span class="sxs-lookup"><span data-stu-id="9d025-157">If you're using Internet Explorer, the browser prompts you to download a *v1.json* file.</span></span>
   
    ![Scaricare i metadati JSON in Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="9d025-159">Se si usa Chrome, Firefox o Microsoft Edge, il browser visualizza il codice JSON nella finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="9d025-159">If you're using Chrome, Firefox, or Edge, the browser displays the JSON in the browser window.</span></span> <span data-ttu-id="9d025-160">Ogni browser gestisce JSON in modo diverso e la finestra del browser potrebbe non essere esattamente uguale a quella dell'esempio.</span><span class="sxs-lookup"><span data-stu-id="9d025-160">Different browsers handle JSON differently, and your browser window may not look exactly like the example.</span></span>
   
    ![Metadati JSON in Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="9d025-162">L'esempio seguente illustra la prima sezione dei metadati di Swagger per l'API, con la definizione per il metodo Get.</span><span class="sxs-lookup"><span data-stu-id="9d025-162">The following sample shows the first section of the Swagger metadata for the API, with the definition for the Get method.</span></span> <span data-ttu-id="9d025-163">Questi metadati sono alla base dell'interfaccia utente di Swagger che vengono usati nei passaggi seguenti e anche in una sezione successiva dell'esercitazione per generare automaticamente il codice client.</span><span class="sxs-lookup"><span data-stu-id="9d025-163">This metadata is what drives the Swagger UI that you use in the following steps, and you use it in a later section of the tutorial to automatically generate client code.</span></span>
   
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
4. <span data-ttu-id="9d025-164">Chiudere il browser e arrestare il debug di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9d025-164">Close the browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="9d025-165">Nel progetto ToDoListDataAPI in **Esplora soluzioni** aprire il file *App_Start\SwaggerConfig.cs* e quindi scorrere verso il basso fino alla riga 174 e rimuovere il commento dal codice seguente.</span><span class="sxs-lookup"><span data-stu-id="9d025-165">In the ToDoListDataAPI project in **Solution Explorer**, open the *App_Start\SwaggerConfig.cs* file, then scroll down to line 174 and uncomment the following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="9d025-166">Il file *SwaggerConfig.cs* viene creato quando si installa il pacchetto Swashbuckle in un progetto.</span><span class="sxs-lookup"><span data-stu-id="9d025-166">The *SwaggerConfig.cs* file is created when you install the Swashbuckle package in a project.</span></span> <span data-ttu-id="9d025-167">Il file fornisce una serie di modi per configurare Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="9d025-167">The file provides a number of ways to configure Swashbuckle.</span></span>
   
    <span data-ttu-id="9d025-168">Il codice in cui sono stati rimossi i commenti abilita l'interfaccia utente di Swagger che viene usata nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9d025-168">The code you've uncommented enables the Swagger UI that you use in the following steps.</span></span> <span data-ttu-id="9d025-169">Quando si crea un progetto API Web con il modello di progetto app per le API, questo codice è impostato come commento per impostazione predefinita come misura di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9d025-169">When you create a Web API project by using the API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="9d025-170">Eseguire di nuovo il progetto.</span><span class="sxs-lookup"><span data-stu-id="9d025-170">Run the project again.</span></span>
7. <span data-ttu-id="9d025-171">Nella barra degli indirizzi del browser aggiungere `swagger` alla fine della riga e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="9d025-171">In your browser address bar, add `swagger` to the end of the line, and then press Return.</span></span> <span data-ttu-id="9d025-172">L'URL è `http://localhost:45914/swagger`.</span><span class="sxs-lookup"><span data-stu-id="9d025-172">(The URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="9d025-173">Quando viene visualizzata la pagina dell'interfaccia utente di Swagger, fare clic su **ToDoList** per visualizzare i metodi disponibili.</span><span class="sxs-lookup"><span data-stu-id="9d025-173">When the Swagger UI page appears, click **ToDoList** to see the methods available.</span></span>
   
    ![Metodi disponibili dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="9d025-175">Fare clic sul primo pulsante **Get** nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="9d025-175">Click the first **Get** button in the list.</span></span>
10. <span data-ttu-id="9d025-176">Nella sezione **Parameters** immettere un asterisco come valore del parametro `owner` e quindi fare clic su **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="9d025-176">In the **Parameters** section, enter an asterisk as the value of the `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="9d025-177">Aggiungendo l'autenticazione nelle esercitazioni successive, il livello intermedio fornirà l'ID utente effettivo al livello dati.</span><span class="sxs-lookup"><span data-stu-id="9d025-177">When you add authentication in later tutorials, the middle tier will provide the actual user ID to the data tier.</span></span> <span data-ttu-id="9d025-178">Per ora, il campo del proprietario mostrerà un asterisco per tutte le attività mentre l'applicazione viene eseguita senza autenticazione abilitata.</span><span class="sxs-lookup"><span data-stu-id="9d025-178">For now, all tasks will have asterisk as their owner ID while the application runs without authentication enabled.</span></span>
    
    ![Prova dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="9d025-180">L'interfaccia utente di Swagger chiama il metodo Get ToDoList e visualizza il codice di risposta e i risultati JSON.</span><span class="sxs-lookup"><span data-stu-id="9d025-180">The Swagger UI calls the ToDoList Get method and displays the response code and JSON results.</span></span>
    
    ![Risultati della prova dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="9d025-182">Fare clic su **Post** e quindi fare clic sulla casella sotto **Model Schema**.</span><span class="sxs-lookup"><span data-stu-id="9d025-182">Click **Post**, and then click the box under **Model Schema**.</span></span>
    
    <span data-ttu-id="9d025-183">Selezionando lo schema del modello viene precompilata automaticamente la casella di input in cui è possibile specificare il valore del parametro per il metodo Post.</span><span class="sxs-lookup"><span data-stu-id="9d025-183">Clicking the model schema prefills the input box where you can specify the parameter value for the Post method.</span></span> <span data-ttu-id="9d025-184">Se questo non funziona in Internet Explorer, usare un browser diverso o immettere manualmente il valore del parametro nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="9d025-184">(If this doesn't work in Internet Explorer, use a different browser or enter the parameter value manually in the next step.)</span></span>  
    
    ![Post della prova dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="9d025-186">Modificare il codice JSON nella casella di input del parametro `todo` , in modo che appaia come l'esempio seguente, oppure sostituire con un testo descrittivo personalizzato:</span><span class="sxs-lookup"><span data-stu-id="9d025-186">Change the JSON in the `todo` parameter input box so that it looks like the following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy the dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="9d025-187">Fare clic su **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="9d025-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="9d025-188">L'API ToDoList restituisce un codice di risposta HTTP 204 che indica l'esito positivo.</span><span class="sxs-lookup"><span data-stu-id="9d025-188">The ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="9d025-189">Fare clic sul primo pulsante **Get** e quindi in quella sezione della pagina fare clic sul pulsante **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="9d025-189">Click the first **Get** button, and then in that section of the page click the **Try it out** button.</span></span>
    
    <span data-ttu-id="9d025-190">La risposta al metodo Get ora include la nuova attività.</span><span class="sxs-lookup"><span data-stu-id="9d025-190">The Get method response now includes the new to do item.</span></span>
15. <span data-ttu-id="9d025-191">Facoltativo: provare anche i metodi Put, Delete e Get by ID.</span><span class="sxs-lookup"><span data-stu-id="9d025-191">Optional: Try also the Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="9d025-192">Chiudere il browser e arrestare il debug di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9d025-192">Close the browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="9d025-193">Swashbuckle funziona con qualsiasi progetto API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9d025-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="9d025-194">Se si vuole aggiungere la generazione metadati di Swagger a un progetto esistente, è sufficiente installare il pacchetto Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="9d025-194">If you want to add Swagger metadata generation to an existing project, just install the Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="9d025-195">I metadati di Swagger includono un ID univoco per ogni operazione API.</span><span class="sxs-lookup"><span data-stu-id="9d025-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="9d025-196">Per impostazione predefinita, Swashbuckle può generare ID operazione di Swagger duplicati per i metodi del controller dell'API Web.</span><span class="sxs-lookup"><span data-stu-id="9d025-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="9d025-197">Ciò si verifica se il controller presenta metodi di overload HTTP, ad esempio `Get()` e `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="9d025-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="9d025-198">Per informazioni su come gestire gli overload, vedere [Personalizzare le definizioni delle API generate da Swashbuckle](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="9d025-198">For information about how to handle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="9d025-199">Se si crea un progetto di API Web in Visual Studio usando il modello App per le API di Azure, al file *SwaggerConfig.cs* viene aggiunto automaticamente codice che genera ID operazione univoci.</span><span class="sxs-lookup"><span data-stu-id="9d025-199">If you create a Web API project in Visual Studio by using the Azure API App template, code that generates unique operation IDs is automatically added to the *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="9d025-200"><a id="createapiapp"></a> Creare un'app per le API in Azure e distribuirvi il codice</span><span class="sxs-lookup"><span data-stu-id="9d025-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code to it</span></span>
<span data-ttu-id="9d025-201">In questa sezione si usano gli strumenti di Azure integrati nella procedura guidata **Pubblica sito Web** di Visual Studio per creare una nuova app per le API in Azure.</span><span class="sxs-lookup"><span data-stu-id="9d025-201">In this section, you use Azure tools that are integrated into the Visual Studio **Publish Web** wizard to create a new API app in Azure.</span></span> <span data-ttu-id="9d025-202">Si distribuisce quindi il progetto ToDoListDataAPI nella nuova app per le API e si chiama l'API eseguendo l'interfaccia utente di Swagger.</span><span class="sxs-lookup"><span data-stu-id="9d025-202">Then you deploy the ToDoListDataAPI project to the new API app and call the API by running the Swagger UI.</span></span>

1. <span data-ttu-id="9d025-203">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto ToDoListDataAPI e quindi scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="9d025-203">In **Solution Explorer**, right-click the ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Fare clic su Pubblica in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="9d025-205">Nel passaggio **Profilo** della procedura guidata **Pubblica sito Web** fare clic su **Servizio app di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="9d025-205">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Fare clic su Servizio app di Azure in Pubblica sul Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="9d025-207">Accedere al proprio account Azure, se non è già stato fatto, o aggiornare le credenziali se sono scadute.</span><span class="sxs-lookup"><span data-stu-id="9d025-207">Sign in to your Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="9d025-208">Nella finestra di dialogo Servizio app scegliere la **sottoscrizione** di Azure da usare e quindi fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="9d025-208">In the App Service dialog box, choose the Azure **Subscription** you want to use, and then click **New**.</span></span>
   
    ![Fare clic su Nuovo nella finestra di dialogo Servizio app](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="9d025-210">Viene visualizzata la scheda **Hosting** della finestra di dialogo **Crea servizio app**.</span><span class="sxs-lookup"><span data-stu-id="9d025-210">The **Hosting** tab of the **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="9d025-211">Poiché si sta distribuendo un progetto API Web con Swashbuckle installato, Visual Studio presuppone che si voglia creare un'app per le API</span><span class="sxs-lookup"><span data-stu-id="9d025-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want to create an API App.</span></span> <span data-ttu-id="9d025-212">come è indicato dal titolo **Nome app per le API** e dal fatto che l'elenco a discesa **Modifica tipo** è impostato su **App per le API**.</span><span class="sxs-lookup"><span data-stu-id="9d025-212">This is indicated by the **API App Name** title and by the fact that the **Change Type** drop-down list is set to **API App**.</span></span>
   
    ![Tipo di app nella finestra di dialogo Servizio app](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="9d025-214">Immettere un **Nome app per le API** che sia univoco nel dominio *azurewebsites.net* .</span><span class="sxs-lookup"><span data-stu-id="9d025-214">Enter an **API App Name** that is unique in the *azurewebsites.net* domain.</span></span> <span data-ttu-id="9d025-215">È possibile accettare il nome predefinito proposto da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9d025-215">You can accept the default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="9d025-216">Se si immette un nome già usato da qualcun altro, viene visualizzato un punto esclamativo a destra.</span><span class="sxs-lookup"><span data-stu-id="9d025-216">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span></span>
   
    <span data-ttu-id="9d025-217">L'URL dell'app per le API sarà `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="9d025-217">The URL of the API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="9d025-218">Nell'elenco a discesa **Gruppo di risorse** fare clic su **Nuovo** e quindi immettere "ToDoListGroup" o un altro nome, se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="9d025-218">In the **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="9d025-219">Un gruppo di risorse è una raccolta di risorse di Azure, ad esempio app per le api, database, VM e così via.</span><span class="sxs-lookup"><span data-stu-id="9d025-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="9d025-220">Per questa esercitazione è consigliabile creare un nuovo gruppo di risorse, per eliminare facilmente tutte le risorse di Azure create per l'esercitazione in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="9d025-220">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span></span>
   
    <span data-ttu-id="9d025-221">Questa casella consente di selezionare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) esistente o crearne uno nuovo digitando un nome diverso da qualsiasi gruppo di risorse esistente nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9d025-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="9d025-222">Fare clic sul pulsante **Nuovo** accanto all'elenco a discesa **Piano di servizio app**.</span><span class="sxs-lookup"><span data-stu-id="9d025-222">Click the **New** button next to the **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="9d025-223">Lo screenshot mostra i valori di esempio per **API App Name** (Nome app per le API), **Sottoscrizione** e **Gruppo di risorse**. I valori dell'utente saranno diversi.</span><span class="sxs-lookup"><span data-stu-id="9d025-223">The screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Finestra di dialogo Crea servizio app](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="9d025-225">Nei passaggi seguenti si crea un piano di servizio app per il nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9d025-225">In the following steps you create an App Service plan for the new resource group.</span></span> <span data-ttu-id="9d025-226">Un piano di servizio app specifica le risorse di calcolo in cui viene eseguita l'app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-226">An App Service plan specifies the compute resources that your API app runs on.</span></span> <span data-ttu-id="9d025-227">Se, ad esempio, si sceglie il livello gratuito, l'app per le API viene eseguita in VM condivise, mentre con alcuni livelli a pagamento viene eseguita in VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="9d025-227">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="9d025-228">Per altre informazioni sui piani di servizio app, vedere [Panoramica approfondita dei piani del servizio app di Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d025-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="9d025-229">Nella finestra di dialogo **Configura piano di servizio app** immettere "ToDoListPlan" o un altro nome, se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="9d025-229">In the **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="9d025-230">Nell'elenco a discesa **Località** scegliere la località più vicina.</span><span class="sxs-lookup"><span data-stu-id="9d025-230">In the **Location** drop-down list, choose the location that is closest to you.</span></span>
   
    <span data-ttu-id="9d025-231">Questa impostazione specifica il data center di Azure in cui verrà eseguita l'app.</span><span class="sxs-lookup"><span data-stu-id="9d025-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="9d025-232">Scegliere una località vicina per ridurre al minimo la [latenza](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="9d025-232">Choose a location close to you to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="9d025-233">Nell'elenco a discesa **Dimensioni** fare clic su **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="9d025-233">In the **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="9d025-234">Per questa esercitazione il piano tariffario Gratuito fornirà prestazioni sufficienti.</span><span class="sxs-lookup"><span data-stu-id="9d025-234">For this tutorial, the free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="9d025-235">Nella finestra di dialogo **Configura piano di servizio app** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d025-235">In the **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Fare clic su OK in Configura piano di servizio app](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="9d025-237">Nella finestra di dialogo **Crea servizio App** fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9d025-237">In the **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Fare clic su Crea nella finestra di dialogo Crea servizio app](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="9d025-239">Visual Studio crea l'app per le API e un profilo di pubblicazione che include tutte le impostazioni necessarie per l'app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-239">Visual Studio creates the API app and a publish profile that has all of the required settings for the API app.</span></span> <span data-ttu-id="9d025-240">Apre quindi la procedura guidata **Pubblica sito Web** che si userà per distribuire il progetto.</span><span class="sxs-lookup"><span data-stu-id="9d025-240">Then it opens the **Publish Web** wizard, which you'll use to deploy the project.</span></span>
    
    <span data-ttu-id="9d025-241">All'apertura della procedura guidata **Pubblica sito Web** viene visualizzata la scheda **Connessione**, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9d025-241">The **Publish Web** wizard opens on the **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="9d025-242">Nella scheda **Connessione** le impostazioni per **Server** e **Nome sito** fanno riferimento all'app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-242">On the **Connection** tab, the **Server** and **Site name** settings point to your API app.</span></span> <span data-ttu-id="9d025-243">I valori di **Nome utente** e **Password** sono credenziali di distribuzione create automaticamente da Azure.</span><span class="sxs-lookup"><span data-stu-id="9d025-243">The **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="9d025-244">Al termine della distribuzione Visual Studio apre un browser all'**URL di destinazione**. Questo è il solo scopo dell'**URL di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="9d025-244">After deployment, Visual Studio opens a browser to the **Destination URL** (that's the only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="9d025-245">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d025-245">Click **Next**.</span></span>
    
    ![Fare clic su Avanti nella scheda Connessione di Pubblica sito Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="9d025-247">La scheda successiva è **Impostazioni**, illustrata di seguito,</span><span class="sxs-lookup"><span data-stu-id="9d025-247">The next tab is the **Settings** tab (shown below).</span></span> <span data-ttu-id="9d025-248">in cui è possibile modificare la configurazione della build per distribuire una build di debug per il [debug remoto](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="9d025-248">Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="9d025-249">La scheda include anche numerose **Opzioni pubblicazione file**</span><span class="sxs-lookup"><span data-stu-id="9d025-249">The tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="9d025-250">Rimuovi i file aggiuntivi nella destinazione</span><span class="sxs-lookup"><span data-stu-id="9d025-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="9d025-251">Precompila durante la pubblicazione</span><span class="sxs-lookup"><span data-stu-id="9d025-251">Precompile during publishing</span></span>
    * <span data-ttu-id="9d025-252">Escludi file dalla cartella App_Data</span><span class="sxs-lookup"><span data-stu-id="9d025-252">Exclude files from the App_Data folder</span></span>
    
    <span data-ttu-id="9d025-253">Per questa esercitazione non ne è necessaria nessuna.</span><span class="sxs-lookup"><span data-stu-id="9d025-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="9d025-254">Per una descrizione dettagliata del funzionamento di queste opzioni, vedere [Procedura: Distribuire un progetto di applicazione Web tramite la pubblicazione con un clic in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d025-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="9d025-255">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9d025-255">Click **Next**.</span></span>
    
    ![Fare clic su Avanti nella scheda Impostazioni di Pubblica sito Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="9d025-257">Si passa quindi alla scheda **Anteprima** , illustrata di seguito, che consente di visualizzare quali file verranno copiati dal progetto all'app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-257">Next is the **Preview** tab (shown below), which gives you an opportunity to see what files are going to be copied from your project to the API app.</span></span> <span data-ttu-id="9d025-258">Quando si distribuisce un progetto in un'app per le API che è già stato distribuito prima, vengono copiati solo i file modificati.</span><span class="sxs-lookup"><span data-stu-id="9d025-258">When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied.</span></span> <span data-ttu-id="9d025-259">Per visualizzare un elenco di quelli che verranno copiati, è possibile fare clic sul pulsante **Avvia anteprima** .</span><span class="sxs-lookup"><span data-stu-id="9d025-259">If you want to see a list of what will be copied, you can click the **Start Preview** button.</span></span>
15. <span data-ttu-id="9d025-260">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="9d025-260">Click **Publish**.</span></span>
    
    ![Fare clic su Pubblica nella scheda Anteprima di Pubblica sito Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="9d025-262">Visual Studio distribuisce il progetto ToDoListDataAPI nella nuova app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-262">Visual Studio deploys the ToDoListDataAPI project to the new API app.</span></span> <span data-ttu-id="9d025-263">La finestra **Output** registra la distribuzione riuscita e una pagina indicante che la creazione è avvenuta correttamente viene visualizzata in una finestra del browser aperta all'indirizzo dell'URL dell'app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-263">The **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened to the URL of the API app.</span></span>
    
    ![Finestra di output che segnala che la distribuzione è completata](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Pagina che segnala che la creazione dell'app per le API è completata](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="9d025-266">Nella barra degli indirizzi del browser aggiungere "swagger" all'URL e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="9d025-266">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="9d025-267">L'URL è `http://{apiappname}.azurewebsites.net/swagger`.</span><span class="sxs-lookup"><span data-stu-id="9d025-267">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="9d025-268">Il browser visualizza la stessa interfaccia utente di Swagger mostrata in precedenza, ma ora viene eseguita nel cloud.</span><span class="sxs-lookup"><span data-stu-id="9d025-268">The browser displays the same Swagger UI that you saw earlier, but now it's running in the cloud.</span></span> <span data-ttu-id="9d025-269">Provando a usare il metodo Get le attività predefinite tornano a essere due.</span><span class="sxs-lookup"><span data-stu-id="9d025-269">Try out the Get method, and you see that you're back to the default 2 to-do items.</span></span> <span data-ttu-id="9d025-270">Le modifiche apportate in precedenza sono state salvate in memoria nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="9d025-270">The changes you made earlier were saved in memory in the local machine.</span></span>
17. <span data-ttu-id="9d025-271">Aprire il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9d025-271">Open the [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="9d025-272">Il portale di Azure è un'interfaccia Web per la gestione delle risorse di Azure, ad esempio le app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-272">The Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="9d025-273">Fare clic su **Altri servizi > Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="9d025-273">Click **More Services > App Services**.</span></span>
    
    ![Selezionare Servizi app](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="9d025-275">Nel pannello **Servizi app** trovare la nuova app per le API e fare clic su di essa.</span><span class="sxs-lookup"><span data-stu-id="9d025-275">In the **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="9d025-276">Nel portale di Azure le finestre che si aprono sulla destra sono dette *pannelli*.</span><span class="sxs-lookup"><span data-stu-id="9d025-276">(In the Azure portal, windows that open to the right are called *blades*.)</span></span>
    
    ![Pannello Servizi app](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="9d025-278">Vengono aperti due pannelli,</span><span class="sxs-lookup"><span data-stu-id="9d025-278">Two blades open.</span></span> <span data-ttu-id="9d025-279">uno con una panoramica dell'app per le API e uno con un lungo elenco di impostazioni che è possibile visualizzare e modificare.</span><span class="sxs-lookup"><span data-stu-id="9d025-279">One blade has an overview of the API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="9d025-280">Nel pannello **Impostazioni** trovare la sezione **API** e fare clic su **Definizione API**.</span><span class="sxs-lookup"><span data-stu-id="9d025-280">In the **Settings** blade, find the **API** section and click **API Definition**.</span></span>
    
    ![Definizione dell'API nel pannello Impostazioni](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="9d025-282">Il pannello **Definizione API** consente di specificare l'URL che restituisce i metadati di Swagger 2.0 in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="9d025-282">The **API Definition** blade lets you specify the URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="9d025-283">Quando Visual Studio crea l'app per le API, imposta l'URL di definizione dell'API sul valore predefinito per i metadati generati da Swashbuckle visualizzati in precedenza, ovvero l'URL di base dell'app per le API più `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="9d025-283">When Visual Studio creates the API app, it sets the API definition URL to the default value for Swashbuckle-generated metadata that you saw earlier, which is the API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL di definizione dell'API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="9d025-285">Quando si seleziona un'app per le API per generare il relativo codice client, Visual Studio recupera i metadati dall'URL.</span><span class="sxs-lookup"><span data-stu-id="9d025-285">When you select an API app to generate client code for it, Visual Studio retrieves the metadata from this URL.</span></span>

## <span data-ttu-id="9d025-286"><a id="codegen"></a> Generare il codice client per il livello dati</span><span class="sxs-lookup"><span data-stu-id="9d025-286"><a id="codegen"></a> Generate client code for the data tier</span></span>
<span data-ttu-id="9d025-287">Uno dei vantaggi dell'integrazione di Swagger nelle app per le API di Azure è la generazione automatica del codice.</span><span class="sxs-lookup"><span data-stu-id="9d025-287">One of the advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="9d025-288">Le classi client generate semplificano la scrittura del codice che chiama un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-288">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="9d025-289">Il progetto ToDoListAPI include già il codice client generato, ma nei passaggi seguenti è necessario eliminarlo e rigenerarlo per sapere come eseguire la generazione del codice.</span><span class="sxs-lookup"><span data-stu-id="9d025-289">The ToDoListAPI project already has the generated client code, but in the following steps you'll delete it and regenerate it to see how to do the code generation.</span></span>

1. <span data-ttu-id="9d025-290">Nel progetto ToDoListAPI in **Esplora soluzioni**di Visual Studio eliminare la cartella *ToDoListDataAPI* .</span><span class="sxs-lookup"><span data-stu-id="9d025-290">In Visual Studio **Solution Explorer**, in the ToDoListAPI project, delete the *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="9d025-291">**Attenzione: eliminare solo la cartella, non il progetto ToDoListDataAPI.**</span><span class="sxs-lookup"><span data-stu-id="9d025-291">**Caution: Delete only the folder, not the ToDoListDataAPI project.**</span></span>
   
    ![Eliminare il codice client generato](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="9d025-293">Questa cartella è stata creata con il processo di generazione di codice illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9d025-293">This folder was created by using the code generation process that you're about to go through.</span></span>
2. <span data-ttu-id="9d025-294">Fare clic con il pulsante destro del mouse sul progetto ToDoListAPI e quindi scegliere **Aggiungi > Client dell'API REST**.</span><span class="sxs-lookup"><span data-stu-id="9d025-294">Right-click the ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Aggiungere il client API REST in Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="9d025-296">Nella finestra di dialogo **Aggiungi il client dell'API REST** fare clic su **URL Swagger** e quindi su **Seleziona asset di Azure**.</span><span class="sxs-lookup"><span data-stu-id="9d025-296">In the **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Seleziona asset di Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="9d025-298">Nella finestra di dialogo **Servizio app** espandere il gruppo di risorse usato per questa esercitazione, selezionare l'app per le API e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d025-298">In the **App Service** dialog box, expand the resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Selezionare l'app per le API per la generazione di codice](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="9d025-300">Quando si torna alla finestra di dialogo **Aggiungi client API REST** , la casella di testo risulta già compilata con il valore dell'URL di definizione dell'API visualizzato in precedenza nel portale.</span><span class="sxs-lookup"><span data-stu-id="9d025-300">Notice that when you return to the **Add REST API Client** dialog, the text box has been filled in with the API definition URL value that you saw earlier in the portal.</span></span>
   
    ![URL di definizione dell'API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="9d025-302">Un modo alternativo per ottenere i metadati per la generazione del codice consiste nell'immettere l'URL direttamente invece che tramite la finestra di dialogo Sfoglia.</span><span class="sxs-lookup"><span data-stu-id="9d025-302">An alternative way to get metadata for code generation is to enter the URL directly instead of going through the browse dialog.</span></span> <span data-ttu-id="9d025-303">In alternativa, per generare il codice client prima di distribuirlo in Azure, è possibile eseguire il progetto API Web in locale, andare all'URL che fornisce il file JSON per Swagger e usare l'opzione **Selezionare un file di metadati Swagger esistente** .</span><span class="sxs-lookup"><span data-stu-id="9d025-303">Or if you want to generate client code before deploying to Azure, you could run the Web API project locally, go to the URL that provides the Swagger JSON file, save the file, and use the **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="9d025-304">Nella finestra di dialogo **Aggiungi il client dell'API REST** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d025-304">In the **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="9d025-305">Visual Studio crea una cartella con il nome dell'app per le API e genera classi client.</span><span class="sxs-lookup"><span data-stu-id="9d025-305">Visual Studio creates a folder named after the API app and generates client classes.</span></span>
   
    ![File di codice per il client generato](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="9d025-307">Nel progetto ToDoListAPI aprire *Controllers\ToDoListController.cs* per visualizzare il codice nella riga 40 che chiama l'API usando il client generato.</span><span class="sxs-lookup"><span data-stu-id="9d025-307">In the ToDoListAPI project, open *Controllers\ToDoListController.cs* to see the code at line 40  that calls the API by using the generated client.</span></span>
   
    <span data-ttu-id="9d025-308">Il frammento seguente illustra come il codice crea un'istanza dell'oggetto client e chiama il metodo Get.</span><span class="sxs-lookup"><span data-stu-id="9d025-308">The following snippet shows how the code instantiates the client object and calls the Get method.</span></span>
   
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
   
    <span data-ttu-id="9d025-309">Il parametro del costruttore ottiene l'URL dell'endpoint dall'impostazione `toDoListDataAPIURL` dell'app.</span><span class="sxs-lookup"><span data-stu-id="9d025-309">The constructor parameter gets the endpoint URL from  the `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="9d025-310">Nel file Web.config questo valore è impostato sull'URL di IIS Express locale del progetto API per consentire l'esecuzione dell'applicazione in locale.</span><span class="sxs-lookup"><span data-stu-id="9d025-310">In the Web.config file, that value is set to the local IIS Express URL of the API project so that you can run the application locally.</span></span> <span data-ttu-id="9d025-311">Se si omette il parametro del costruttore, l'endpoint predefinito sarà l'URL da cui è stato generato il codice.</span><span class="sxs-lookup"><span data-stu-id="9d025-311">If you omit the constructor parameter, the default endpoint is the URL that you generated the code from.</span></span>
7. <span data-ttu-id="9d025-312">La classe del client verrà generata con un nome diverso basato sul nome dell'app per le API. Modificare il codice in *Controllers\ToDoListController.cs* in modo che il nome del tipo corrisponda a quanto generato nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9d025-312">Your client class will be generated with a different name based on your API app name; change the code in *Controllers\ToDoListController.cs* so that the type name matches what was generated in your project.</span></span> <span data-ttu-id="9d025-313">Se, ad esempio, si è assegnato all'app per le API il nome ToDoListDataAPI071316, si sostituirà questo codice:</span><span class="sxs-lookup"><span data-stu-id="9d025-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="9d025-314">con questo:</span><span class="sxs-lookup"><span data-stu-id="9d025-314">to this:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-to-host-the-middle-tier"></a><span data-ttu-id="9d025-315">Creare un'app per le API per ospitare il livello intermedio</span><span class="sxs-lookup"><span data-stu-id="9d025-315">Create an API app to host the middle tier</span></span>
<span data-ttu-id="9d025-316">Prima è stata [creata l'app per le API di livello dati in cui si è distribuito il codice](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="9d025-316">Earlier you [created the data tier API app and deployed code to it](#createapiapp).</span></span>  <span data-ttu-id="9d025-317">Ora si seguirà la stessa procedura per l'app per le API di livello intermedio.</span><span class="sxs-lookup"><span data-stu-id="9d025-317">Now you follow the same procedure for the middle tier API app.</span></span>

1. <span data-ttu-id="9d025-318">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto ToDoListAPI di livello intermedio, non su ToDoListDataAPI del livello dati, e quindi scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="9d025-318">In **Solution Explorer**, right-click the middle tier ToDoListAPI  project (not the data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Fare clic su Pubblica in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="9d025-320">Nella scheda **Profilo** della procedura guidata **Pubblica sito Web** fare clic su **Servizio app di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="9d025-320">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="9d025-321">Nella finestra di dialogo **Servizio App** fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="9d025-321">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="9d025-322">Nella scheda **Hosting** della finestra di dialogo **Crea servizio app** accettare il **API App Name** (Nome app per le API) predefinito o immettere un nome che sia univoco nel dominio *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="9d025-322">In the **Hosting** tab of the **Create App Service** dialog box, accept the default **API App Name** or enter a name that is unique in the *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="9d025-323">Scegliere la **Sottoscrizione** di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="9d025-323">Choose the Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="9d025-324">Nell'elenco a discesa **Gruppo di risorse** selezionare il nome del gruppo di risorse creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9d025-324">In the **Resource Group** drop-down, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="9d025-325">Nell'elenco a discesa **Piano di servizio app** scegliere lo stesso piano creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9d025-325">In the **App Service Plan** drop-down, choose the same plan you created earlier.</span></span> <span data-ttu-id="9d025-326">Tale valore sarà l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9d025-326">It will default to that value.</span></span>
8. <span data-ttu-id="9d025-327">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9d025-327">Click **Create**.</span></span>
   
    <span data-ttu-id="9d025-328">Visual Studio crea l'app per le API e un profilo di pubblicazione per l'app, quindi visualizza il passaggio **Connessione** della procedura guidata **Pubblica sito Web**.</span><span class="sxs-lookup"><span data-stu-id="9d025-328">Visual Studio creates the API app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
9. <span data-ttu-id="9d025-329">Nel passaggio **Connessione** della procedura guidata **Pubblica sito Web** fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="9d025-329">In the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="9d025-330">Visual Studio distribuisce il progetto ToDoListAPI nella nuova app per le API e apre una finestra del browser all'URL dell'app per le API.</span><span class="sxs-lookup"><span data-stu-id="9d025-330">Visual Studio deploys the ToDoListAPI project to the new API app and opens a browser to the URL of the API app.</span></span> <span data-ttu-id="9d025-331">Viene visualizzata una pagina che informa che l'operazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="9d025-331">The "successfully created" page appears.</span></span>

## <a name="configure-the-middle-tier-to-call-the-data-tier"></a><span data-ttu-id="9d025-332">Configurare il livello intermedio per chiamare il livello dati</span><span class="sxs-lookup"><span data-stu-id="9d025-332">Configure the middle tier to call the data tier</span></span>
<span data-ttu-id="9d025-333">Se l'app per le API di livello intermedio venisse chiamata ora, cercherebbe di chiamare il livello dati usando l'URL localhost che si trova ancora nel file Web.config.</span><span class="sxs-lookup"><span data-stu-id="9d025-333">If you called the middle tier API app now, it would try to call the data tier using the localhost URL that is still in the Web.config file.</span></span> <span data-ttu-id="9d025-334">In questa sezione si immette l'URL dell'app per le API del livello dati in un'impostazione dell'ambiente nell'app per le API del livello intermedio.</span><span class="sxs-lookup"><span data-stu-id="9d025-334">In this section you enter the data tier API app URL into an environment setting in the middle tier API app.</span></span> <span data-ttu-id="9d025-335">Quando il codice nell'app per le API del livello intermedio recupera l'impostazione dell'URL del livello dati, l'impostazione dell'ambiente esegue l'override del contenuto del file Web.config.</span><span class="sxs-lookup"><span data-stu-id="9d025-335">When the code in the middle tier API app retrieves the data tier URL setting, the environment setting will override what's in the Web.config file.</span></span>

1. <span data-ttu-id="9d025-336">Accedere al [portale di Azure](https://portal.azure.com/)e passare al pannello **App per le API** relativo all'app per le API creata per ospitare il progetto TodoListAPI (livello intermedio).</span><span class="sxs-lookup"><span data-stu-id="9d025-336">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that you created to host the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="9d025-337">Nel pannello **Impostazioni** dell'app per le API fare clic su **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="9d025-337">In the API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="9d025-338">Nel pannello **Impostazioni applicazione** dell'app per le API scorrere verso il basso fino alla sezione **Impostazioni app** e aggiungere la chiave e il valore seguenti.</span><span class="sxs-lookup"><span data-stu-id="9d025-338">In the API App's **Application Settings** blade, scroll down to the **App settings** section and add the following key and value.</span></span> <span data-ttu-id="9d025-339">Il valore sarà costituito dall'URL della prima app per le API pubblicata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9d025-339">The value will be the URL of the first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="9d025-340">**Chiave**</span><span class="sxs-lookup"><span data-stu-id="9d025-340">**Key**</span></span> | <span data-ttu-id="9d025-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="9d025-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="9d025-342">**Valore**</span><span class="sxs-lookup"><span data-stu-id="9d025-342">**Value**</span></span> |<span data-ttu-id="9d025-343">https://{nome dell'app per le API di livello dati}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="9d025-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="9d025-344">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9d025-344">**Example**</span></span> |<span data-ttu-id="9d025-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="9d025-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="9d025-346">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="9d025-346">Click **Save**.</span></span>
   
    ![Fare clic su Salva per le impostazioni dell'app](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="9d025-348">Quando il codice è in esecuzione in Azure, questo valore sostituisce l'URL localhost contenuto nel file Web.config.</span><span class="sxs-lookup"><span data-stu-id="9d025-348">When the code runs in Azure, this value will now override the localhost URL that is in the Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="9d025-349">Test</span><span class="sxs-lookup"><span data-stu-id="9d025-349">Test</span></span>
1. <span data-ttu-id="9d025-350">In una finestra del browser passare all'URL della nuova app per le API di livello intermedio appena creata per ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="9d025-350">In a browser window, browse to the URL of the new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="9d025-351">A questo scopo, fare clic sull'URL nel pannello principale dell'app per le API nel portale.</span><span class="sxs-lookup"><span data-stu-id="9d025-351">You can get there by clicking the URL in the API app's main blade in the portal.</span></span>
2. <span data-ttu-id="9d025-352">Nella barra degli indirizzi del browser aggiungere "swagger" all'URL e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="9d025-352">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="9d025-353">L'URL è `http://{apiappname}.azurewebsites.net/swagger`.</span><span class="sxs-lookup"><span data-stu-id="9d025-353">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="9d025-354">Il browser visualizza la stessa interfaccia utente di Swagger vista in precedenza per ToDoListDataAPI, ma `owner` non è un campo obbligatorio per l'operazione Get perché ora è l'app per le API del livello intermedio a inviare tale valore all'app per le API del livello dati.</span><span class="sxs-lookup"><span data-stu-id="9d025-354">The browser displays the same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for the Get operation, because the middle tier API app is sending that value to the data tier API app for you.</span></span> <span data-ttu-id="9d025-355">Quando si eseguiranno le esercitazioni sull'autenticazione, il livello intermedio invierà gli ID utente effettivi per il parametro `owner`. Per il momento imposta un asterisco come hardcoded.</span><span class="sxs-lookup"><span data-stu-id="9d025-355">(When you do the authentication tutorials, the middle tier will send actual user IDs for the `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="9d025-356">Provare a usare il metodo Get e gli altri metodi per verificare che l'app per le API di livello intermedio chiami correttamente l'app per le API di livello dati.</span><span class="sxs-lookup"><span data-stu-id="9d025-356">Try out the Get method and the other methods to validate that the middle tier API app is successfully calling the data tier API app.</span></span>
   
    ![Metodo Get dell'interfaccia utente di Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="9d025-358">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9d025-358">Troubleshooting</span></span>
<span data-ttu-id="9d025-359">In caso di problemi nel corso dell'esercitazione, ecco alcune idee per risolverli:</span><span class="sxs-lookup"><span data-stu-id="9d025-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="9d025-360">Verificare di usare la versione più recente di [Azure SDK per .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="9d025-360">Make sure that you're using the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="9d025-361">Due dei nomi di progetto sono simili (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="9d025-361">Two of the project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="9d025-362">Se l'aspetto degli elementi non è simile a quello descritto nelle istruzioni quando si utilizza un progetto, verificare di avere aperto il progetto corretto.</span><span class="sxs-lookup"><span data-stu-id="9d025-362">If things don't look as described in the instructions when you are working with a project, make sure you have opened the correct project.</span></span>
* <span data-ttu-id="9d025-363">Se si ha una rete aziendale e si prova a eseguire la distribuzione nel servizio app di Azure tramite un firewall, assicurarsi che le porte 443 e 8172 siano aperte per la distribuzione Web.</span><span class="sxs-lookup"><span data-stu-id="9d025-363">If you're on a corporate network and are trying to deploy to Azure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="9d025-364">Se non è possibile aprire tali porte, si possono usare altri metodi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9d025-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="9d025-365">Vedere [Distribuire l'app nel servizio app di Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9d025-365">See [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="9d025-366">Errori che indicano che i nomi delle route devono essere univoci: è possibile che vengano visualizzati se in un'app per le API è stato accidentalmente distribuito il progetto errato e successivamente viene distribuito quello corretto.</span><span class="sxs-lookup"><span data-stu-id="9d025-366">"Route names must be unique" errors -- you could get these if you accidentally deploy the wrong project to an API app and then later deploy the correct one to it.</span></span> <span data-ttu-id="9d025-367">Per risolvere il problema, ridistribuire il progetto corretto nell'app per le API e nella scheda **Impostazioni** della procedura guidata **Pubblica sito Web** selezionare **Rimuovi i file aggiuntivi nella destinazione**.</span><span class="sxs-lookup"><span data-stu-id="9d025-367">To correct this, redeploy the correct project to the API app, and on the **Settings** tab of the **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="9d025-368">Quando l'app per le API ASP.NET è in esecuzione nel servizio app di Azure, è possibile approfondire la conoscenza delle funzionalità di Visual Studio che semplificano la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="9d025-368">After you have your ASP.NET API app running in Azure App Service, you may want to learn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="9d025-369">Per informazioni sulla registrazione, il debug remoto e altro ancora, vedere [Risoluzione dei problemi di un'app Web nel servizio app di Azure tramite Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9d025-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d025-370">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d025-370">Next steps</span></span>
<span data-ttu-id="9d025-371">Si è appreso come distribuire i progetti di API Web esistenti nelle app per le API, generare il codice client per le app per le API e utilizzare le app per le API dai client .NET.</span><span class="sxs-lookup"><span data-stu-id="9d025-371">You've seen how to deploy existing Web API projects to API apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="9d025-372">L'esercitazione successiva di questa serie mostra come [usare CORS per utilizzare app per le API da client JavaScript](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="9d025-372">The next tutorial in this series shows how to [use CORS to consume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="9d025-373">Per altre informazioni sulla generazione di codice client, vedere il repository [Azure/AutoRest](https://github.com/azure/autorest) in GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="9d025-373">For more information about client code generation, see the [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com.</span></span> <span data-ttu-id="9d025-374">Per informazioni sui problemi relativi all'uso del client generato, aprire un [problema nel repository AutoRest](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="9d025-374">For help with problems using the generated client, open an [issue in the AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="9d025-375">Per creare nuovi progetti di app per le API da zero, usare il modello **App per le API di Azure** .</span><span class="sxs-lookup"><span data-stu-id="9d025-375">If you want to create new API app projects from scratch, use the **Azure API App** template.</span></span>

![Modello di app per le API in Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="9d025-377">Scegliere il modello di progetto **App per le API di Azure** equivale a scegliere il modello di ASP.NET 4.5.2 **vuoto**, fare clic sulla casella di controllo per aggiungere il supporto per l'API Web e installare il pacchetto NuGet Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="9d025-377">The **Azure API App** project template is equivalent to choosing the **Empty** ASP.NET 4.5.2 template, clicking the check box to add Web API support, and installing the Swashbuckle NuGet package.</span></span> <span data-ttu-id="9d025-378">Il modello aggiunge anche un codice di configurazione di Swashbuckle progettato per evitare la creazione di ID operazione di Swagger duplicati.</span><span class="sxs-lookup"><span data-stu-id="9d025-378">In addition, the template adds some Swashbuckle configuration code designed to prevent the creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="9d025-379">Una volta creato un progetto di app per le API, è possibile distribuirlo in un'app per le API nello stesso modo illustrato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9d025-379">Once you've created an API App project, you can deploy it to an API app the same way you saw in this tutorial.</span></span>

