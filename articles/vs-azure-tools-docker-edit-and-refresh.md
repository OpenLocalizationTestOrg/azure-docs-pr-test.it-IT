---
title: App aaaDebugging in un contenitore Docker locale | Documenti Microsoft
description: "Informazioni su come toomodify un'app è in esecuzione in un contenitore Docker locale, aggiornare il contenitore di hello mediante modifica e aggiornamento e impostare i punti di interruzione di debug"
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
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="997ae-103">Debug delle applicazioni in un contenitore Docker locale</span><span class="sxs-lookup"><span data-stu-id="997ae-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="997ae-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="997ae-104">Overview</span></span>
<span data-ttu-id="997ae-105">Hello Visual Studio Tools per Docker offre un modo coerente di toodevelop in e convalidare l'applicazione localmente in un contenitore Linux Docker.</span><span class="sxs-lookup"><span data-stu-id="997ae-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="997ae-106">Non è il contenitore di hello toorestart ogni volta che si applica un codice di modifica.</span><span class="sxs-lookup"><span data-stu-id="997ae-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="997ae-107">Questo articolo illustra come toouse hello "Modifica e Aggiorna" funzionalità toostart un'app Web di ASP.NET Core in un contenitore Docker locale, apportare le modifiche necessarie e quindi aggiornare hello browser toosee tali modifiche.</span><span class="sxs-lookup"><span data-stu-id="997ae-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="997ae-108">In questo articolo illustra anche come tooset i punti di interruzione per il debug.</span><span class="sxs-lookup"><span data-stu-id="997ae-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="997ae-109">Il supporto del contenitore di Windows sarà disponibile nelle versioni future</span><span class="sxs-lookup"><span data-stu-id="997ae-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="997ae-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="997ae-110">Prerequisites</span></span>
<span data-ttu-id="997ae-111">Hello seguenti strumenti deve essere installato.</span><span class="sxs-lookup"><span data-stu-id="997ae-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="997ae-112">Ultima versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="997ae-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="997ae-113">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="997ae-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="997ae-114">toorun contenitori di Docker in locale, è necessario un client di docker locale.</span><span class="sxs-lookup"><span data-stu-id="997ae-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="997ae-115">È possibile utilizzare hello [della casella degli strumenti di Docker](https://www.docker.com/products/docker-toolbox), che richiede di Hyper-V toobe disabilitato o è possibile utilizzare [Docker per Windows](https://www.docker.com/get-docker), che utilizza la tecnologia Hyper-V e Windows 10 è necessario.</span><span class="sxs-lookup"><span data-stu-id="997ae-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="997ae-116">Utilizzo della casella degli strumenti di Docker, è necessario troppo[configurare hello client di Docker](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="997ae-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="997ae-117">1. Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="997ae-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="997ae-118">2. Aggiungere il supporto di Docker</span><span class="sxs-lookup"><span data-stu-id="997ae-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="997ae-119">3. Modificare il codice e aggiornarlo</span><span class="sxs-lookup"><span data-stu-id="997ae-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="997ae-120">tooquickly scorrere le modifiche, è possibile avviare l'applicazione in un contenitore e continuare toomake modifiche, visualizzarli come si farebbe con IIS Express.</span><span class="sxs-lookup"><span data-stu-id="997ae-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="997ae-121">Impostare hello configurazione soluzione troppo`Debug` e premere  **&lt;CTRL + F5 >** toobuild il docker immagine ed eseguirlo in locale.</span><span class="sxs-lookup"><span data-stu-id="997ae-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="997ae-122">Una volta immagine contenitore hello è stata compilata e viene eseguito in un contenitore Docker, Visual Studio verrà avviato hello app Web nel browser predefinito.</span><span class="sxs-lookup"><span data-stu-id="997ae-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="997ae-123">Se si utilizza browser Microsoft Edge hello o in caso contrario sono errori, vedere [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) sezione.</span><span class="sxs-lookup"><span data-stu-id="997ae-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="997ae-124">Passare toohello sulla pagina, è qui che vedremo toomake le modifiche.</span><span class="sxs-lookup"><span data-stu-id="997ae-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="997ae-125">Restituire tooVisual Studio e aprire `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="997ae-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="997ae-126">Aggiungere hello successivo HTML toohello contenuto alla fine del file hello e salvare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="997ae-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="997ae-127">Visualizza finestra di output di hello, quando viene completata hello compilazione .NET e viene visualizzato di queste righe, passa indietro tooyour browser e aggiornare hello sulla pagina.</span><span class="sxs-lookup"><span data-stu-id="997ae-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="997ae-128">Le modifiche sono state applicate.</span><span class="sxs-lookup"><span data-stu-id="997ae-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="997ae-129">4. Eseguire il debug con punti di interruzione</span><span class="sxs-lookup"><span data-stu-id="997ae-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="997ae-130">Spesso, le modifiche saranno necessario ulteriore ispezione, sfruttando le funzionalità di Visual Studio di debug hello.</span><span class="sxs-lookup"><span data-stu-id="997ae-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="997ae-131">Restituire tooVisual Studio e aprire`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="997ae-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="997ae-132">Sostituire il contenuto di hello del metodo di hello About () con il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="997ae-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="997ae-133">Toohello un punto di interruzione a sinistra di hello set `string message`… riga.</span><span class="sxs-lookup"><span data-stu-id="997ae-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="997ae-134">Riscontri  **&lt;F5 >** toostart debug.</span><span class="sxs-lookup"><span data-stu-id="997ae-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="997ae-135">Passare toohello sulla pagina toohit il punto di interruzione.</span><span class="sxs-lookup"><span data-stu-id="997ae-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="997ae-136">Commutatore tooVisual Studio tooview hello punto di interruzione e per controllare il valore di hello del messaggio.</span><span class="sxs-lookup"><span data-stu-id="997ae-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="997ae-137">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="997ae-137">Summary</span></span>
<span data-ttu-id="997ae-138">Con [Visual Studio 2015 Tools per Docker](https://aka.ms/DockerToolsForVS), è possibile ottenere una produttività hello dell'utilizzo in locale, realismo produzione hello di sviluppo all'interno di un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="997ae-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="997ae-139">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="997ae-139">Troubleshooting</span></span>
[<span data-ttu-id="997ae-140">Risoluzione dei problemi di sviluppo di Docker in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="997ae-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="997ae-141">Altre informazioni su Docker con Visual Studio, Windows e Azure</span><span class="sxs-lookup"><span data-stu-id="997ae-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="997ae-142">[Docker Tools for Visual Studio 2015](http://aka.ms/dockertoolsforvs) : sviluppo di codice .NET Core in un contenitore</span><span class="sxs-lookup"><span data-stu-id="997ae-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="997ae-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) : compilare e distribuire contenitori Docker</span><span class="sxs-lookup"><span data-stu-id="997ae-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="997ae-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) : servizi di linguaggio per la modifica dei file di Docker, con altri scenari e2e presto disponibili</span><span class="sxs-lookup"><span data-stu-id="997ae-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="997ae-145">[Documentazione dei contenitori di Windows](http://aka.ms/containers): informazioni su Windows Server e Nano Server</span><span class="sxs-lookup"><span data-stu-id="997ae-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="997ae-146">[Servizio contenitore di Azure](https://azure.microsoft.com/services/container-service/) - [Contenuto servizio contenitore di Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="997ae-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="997ae-147">Per ulteriori esempi di utilizzo di Docker, vedere [utilizzo Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) da hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connetti [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="997ae-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="997ae-148">Per altre guide rapide dalla demo HealthClinic.biz hello, vedere [strumenti Guida introduttiva per sviluppatori di Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="997ae-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="997ae-149">Altri strumenti di Docker</span><span class="sxs-lookup"><span data-stu-id="997ae-149">Various Docker tools</span></span>
[<span data-ttu-id="997ae-150">Some great docker tools  (Importanti strumenti di Docker, blog di Steve Lasker)</span><span class="sxs-lookup"><span data-stu-id="997ae-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="997ae-151">Articoli utili</span><span class="sxs-lookup"><span data-stu-id="997ae-151">Good articles</span></span>
[<span data-ttu-id="997ae-152">Introduzione tooMicroservices da NGINX</span><span class="sxs-lookup"><span data-stu-id="997ae-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="997ae-153">Presentazioni</span><span class="sxs-lookup"><span data-stu-id="997ae-153">Presentations</span></span>
* [<span data-ttu-id="997ae-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e (Presentazione dal vivo a Las Vegas nel 2016: e2e di Docker)</span><span class="sxs-lookup"><span data-stu-id="997ae-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="997ae-155">Introduzione tooASP.NET Core @ compilazione 2016 - in cui è in Demo</span><span class="sxs-lookup"><span data-stu-id="997ae-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="997ae-156">Developing .NET apps in containers, Channel 9 (Sviluppo di applicazioni .NET in contenitori, Channel 9)</span><span class="sxs-lookup"><span data-stu-id="997ae-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
