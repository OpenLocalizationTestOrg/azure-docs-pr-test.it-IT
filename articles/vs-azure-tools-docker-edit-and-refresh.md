---
title: Debug di applicazioni in un contenitore Docker locale | Documentazione Microsoft
description: "Informazioni su come modificare un'app in esecuzione in un contenitore Docker locale, aggiornare il contenitore tramite la funzionalità di modifica e aggiornamento e impostare i punti di interruzione del debug"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: fcd58736d8915a61683a416fb9bf3892ba7b7bd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="821c6-103">Debug delle applicazioni in un contenitore Docker locale</span><span class="sxs-lookup"><span data-stu-id="821c6-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="821c6-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="821c6-104">Overview</span></span>
<span data-ttu-id="821c6-105">Visual Studio Tools per Docker consente di sviluppare e convalidare l'applicazione in locale in un contenitore Docker. di Linux.</span><span class="sxs-lookup"><span data-stu-id="821c6-105">The Visual Studio Tools for Docker provides a consistent way to develop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="821c6-106">Non è necessario riavviare il contenitore ogni volta che si esegue una modifica del codice.</span><span class="sxs-lookup"><span data-stu-id="821c6-106">You don't have to restart the container each time you make a code change.</span></span>
<span data-ttu-id="821c6-107">Questo articolo illustra come usare la funzionalità di modifica e aggiornamento per avviare un'app Web ASP.NET Core in un contenitore Docker locale, apportare le modifiche necessarie e quindi aggiornare il browser per visualizzare tali modifiche.</span><span class="sxs-lookup"><span data-stu-id="821c6-107">This article illustrates how to use the "Edit and Refresh" feature to start an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh the browser to see those changes.</span></span>
<span data-ttu-id="821c6-108">Illustra inoltre come impostare i punti di interruzione per il debug.</span><span class="sxs-lookup"><span data-stu-id="821c6-108">This article also shows you how to set breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="821c6-109">Il supporto del contenitore di Windows sarà disponibile nelle versioni future</span><span class="sxs-lookup"><span data-stu-id="821c6-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="821c6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="821c6-110">Prerequisites</span></span>
<span data-ttu-id="821c6-111">È necessario che siano installati gli strumenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="821c6-111">The following tools must be installed.</span></span>

* [<span data-ttu-id="821c6-112">Ultima versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="821c6-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="821c6-113">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="821c6-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="821c6-114">Per eseguire i contenitori Docker in locale, è necessario un client di Docker locale.</span><span class="sxs-lookup"><span data-stu-id="821c6-114">To run Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="821c6-115">È possibile usare la [casella degli strumenti di Docker](https://www.docker.com/products/docker-toolbox), che richiede la disabilitazione di Hyper-V, o in alternativa [Docker per Windows](https://www.docker.com/get-docker), che usa Hyper-V e richiede Windows 10.</span><span class="sxs-lookup"><span data-stu-id="821c6-115">You can use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V to be disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="821c6-116">Nella casella degli strumenti di Docker è necessario [configurare il client di Docker](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="821c6-116">If using Docker Toolbox, you'll need to [configure the Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="821c6-117">1. Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="821c6-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="821c6-118">2. Aggiungere il supporto di Docker</span><span class="sxs-lookup"><span data-stu-id="821c6-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="821c6-119">3. Modificare il codice e aggiornarlo</span><span class="sxs-lookup"><span data-stu-id="821c6-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="821c6-120">Per eseguire rapidamente l'iterazione delle modifiche, è possibile avviare l'applicazione in un contenitore e continuare ad apportare modifiche, visualizzandole come si farebbe con IIS Express.</span><span class="sxs-lookup"><span data-stu-id="821c6-120">To quickly iterate changes, you can start your application within a container, and continue to make changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="821c6-121">Impostare la configurazione della soluzione su `Debug` e premere **&lt;CTRL + F5>** per creare l'immagine Docker ed eseguirla localmente.</span><span class="sxs-lookup"><span data-stu-id="821c6-121">Set the Solution Configuration to `Debug` and press **&lt;CTRL + F5>** to build your docker image and run it locally.</span></span>

    <span data-ttu-id="821c6-122">Una volta che l'immagine del contenitore è stata compilata ed è in esecuzione in un contenitore Docker, Visual Studio avvierà l'App Web nel browser predefinito.</span><span class="sxs-lookup"><span data-stu-id="821c6-122">Once the container image has been built and is running in a Docker container, Visual Studio will launch the Web app in your default browser.</span></span>
    <span data-ttu-id="821c6-123">Se si usa il browser Microsoft Edge o se si verificano problemi, vedere la sezione relativa alla [risoluzione dei problemi](vs-azure-tools-docker-troubleshooting-docker-errors.md) .</span><span class="sxs-lookup"><span data-stu-id="821c6-123">If you are using the Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="821c6-124">Passare alla pagina About, da dove verranno apportate le modifiche.</span><span class="sxs-lookup"><span data-stu-id="821c6-124">Go to the About page, which is where we're going to make our changes.</span></span>
3. <span data-ttu-id="821c6-125">Tornare a Visual Studio e aprire `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="821c6-125">Return to Visual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="821c6-126">Aggiungere il contenuto HTML seguente alla fine del file e salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="821c6-126">Add the following HTML content to the end of the file and save the changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="821c6-127">Visualizzare la finestra di output e, quando viene completata la compilazione di .NET e vengono visualizzate queste righe, tornare al browser e aggiornare la pagina About.</span><span class="sxs-lookup"><span data-stu-id="821c6-127">Viewing the output window, when the .NET build is completed and you see these lines, switch back to your browser and refresh the About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down
   ```
6. <span data-ttu-id="821c6-128">Le modifiche sono state applicate.</span><span class="sxs-lookup"><span data-stu-id="821c6-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="821c6-129">4. Eseguire il debug con punti di interruzione</span><span class="sxs-lookup"><span data-stu-id="821c6-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="821c6-130">Spesso è necessario analizzare le modifiche in modo più approfondito, sfruttando le funzionalità di debug di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="821c6-130">Often, changes will need further inspection, leveraging the debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="821c6-131">Tornare a Visual Studio e aprire `Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="821c6-131">Return to Visual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="821c6-132">Sostituire il contenuto del metodo About() con quanto riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="821c6-132">Replace the contents of the About() method with the following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="821c6-133">Impostare un punto di interruzione a sinistra della riga `string message`.</span><span class="sxs-lookup"><span data-stu-id="821c6-133">Set a breakpoint to the left of the `string message`... line.</span></span>
4. <span data-ttu-id="821c6-134">Premere **&lt;F5>** per avviare il debug.</span><span class="sxs-lookup"><span data-stu-id="821c6-134">Hit **&lt;F5>** to start debugging.</span></span>
5. <span data-ttu-id="821c6-135">Accedere alla pagina About per raggiungere il punto di interruzione.</span><span class="sxs-lookup"><span data-stu-id="821c6-135">Navigate to the About page to hit your breakpoint.</span></span>
6. <span data-ttu-id="821c6-136">Passare a Visual Studio per visualizzare il punto di interruzione ed esaminare il valore del messaggio.</span><span class="sxs-lookup"><span data-stu-id="821c6-136">Switch to Visual Studio to view the breakpoint, and inspect the value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="821c6-137">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="821c6-137">Summary</span></span>
<span data-ttu-id="821c6-138">Con [Docker Tools for Visual Studio 2015](https://aka.ms/DockerToolsForVS)si ottiene la produttività tipica del lavoro in locale, con la realtà produttiva offerta dallo sviluppo in un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="821c6-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get the productivity of working locally, with the production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="821c6-139">risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="821c6-139">Troubleshooting</span></span>
[<span data-ttu-id="821c6-140">Risoluzione dei problemi di sviluppo di Docker in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="821c6-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="821c6-141">Altre informazioni su Docker con Visual Studio, Windows e Azure</span><span class="sxs-lookup"><span data-stu-id="821c6-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="821c6-142">[Docker Tools for Visual Studio 2015](http://aka.ms/dockertoolsforvs) : sviluppo di codice .NET Core in un contenitore</span><span class="sxs-lookup"><span data-stu-id="821c6-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="821c6-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) : compilare e distribuire contenitori Docker</span><span class="sxs-lookup"><span data-stu-id="821c6-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="821c6-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) : servizi di linguaggio per la modifica dei file di Docker, con altri scenari e2e presto disponibili</span><span class="sxs-lookup"><span data-stu-id="821c6-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="821c6-145">[Documentazione dei contenitori di Windows](http://aka.ms/containers): informazioni su Windows Server e Nano Server</span><span class="sxs-lookup"><span data-stu-id="821c6-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="821c6-146">[Servizio contenitore di Azure](https://azure.microsoft.com/services/container-service/) - [Contenuto servizio contenitore di Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="821c6-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="821c6-147">Per altri esempi di uso di Docker, vedere [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) (Uso di Docker) dalla [demo](https://github.com/Microsoft/HealthClinic.biz) [HealthClinic.biz](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/) 2015 Connect.</span><span class="sxs-lookup"><span data-stu-id="821c6-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="821c6-148">Per altre guide introduttive della demo HealthClinic.biz, vedere [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)(Guide introduttive agli strumenti di sviluppo di Azure).</span><span class="sxs-lookup"><span data-stu-id="821c6-148">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="821c6-149">Altri strumenti di Docker</span><span class="sxs-lookup"><span data-stu-id="821c6-149">Various Docker tools</span></span>
[<span data-ttu-id="821c6-150">Some great docker tools  (Importanti strumenti di Docker, blog di Steve Lasker)</span><span class="sxs-lookup"><span data-stu-id="821c6-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="821c6-151">Articoli utili</span><span class="sxs-lookup"><span data-stu-id="821c6-151">Good articles</span></span>
[<span data-ttu-id="821c6-152">Introduction to Microservices from NGINX (Introduzione ai microservizi di NGINX)</span><span class="sxs-lookup"><span data-stu-id="821c6-152">Introduction to Microservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="821c6-153">Presentazioni</span><span class="sxs-lookup"><span data-stu-id="821c6-153">Presentations</span></span>
* [<span data-ttu-id="821c6-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e (Presentazione dal vivo a Las Vegas nel 2016: e2e di Docker)</span><span class="sxs-lookup"><span data-stu-id="821c6-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="821c6-155">Introduction to ASP.NET Core @ Build 2016 - Where You At Demo (Introduzione ad ASP.NET Core in Build 2016 - Demo)</span><span class="sxs-lookup"><span data-stu-id="821c6-155">Introduction to ASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="821c6-156">Developing .NET apps in containers, Channel 9 (Sviluppo di applicazioni .NET in contenitori, Channel 9)</span><span class="sxs-lookup"><span data-stu-id="821c6-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
