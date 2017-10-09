---
title: aaaUse .NET Core nell'App Web in Linux | Documenti Microsoft
description: Usare .NET Core in un'app Web in Linux.
keywords: Servizio app di Azure, app Web, dotnet, core, linux, oss
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="2a2a5-104">Usare .NET Core in un'app Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="2a2a5-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="2a2a5-105">[App Web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) in Linux fornisce un servizio di hosting web scalabile, applicazione automatica di patch utilizzando hello del sistema operativo Linux.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using hello Linux operating system.</span></span> <span data-ttu-id="2a2a5-106">In questa esercitazione vengono fornite istruzioni dettagliate che mostra come toocreate un [.NET Core](https://docs.microsoft.com/aspnet/core/) app in app web di Azure in Linux.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-106">This tutorial contains step-by-step instructions showing how toocreate a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![App Web in Linux][10]

<span data-ttu-id="2a2a5-108">È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a2a5-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2a2a5-109">Prerequisites</span></span> ##

<span data-ttu-id="2a2a5-110">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-110">toocomplete this tutorial:</span></span> 

* <span data-ttu-id="2a2a5-111">Installare hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="2a2a5-111">Install hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="2a2a5-112">Installare [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="2a2a5-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="2a2a5-113">Creare un'applicazione .NET Core locale</span><span class="sxs-lookup"><span data-stu-id="2a2a5-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="2a2a5-114">Avviare una nuova sessione terminal.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-114">Start a new terminal session.</span></span> <span data-ttu-id="2a2a5-115">Creare una directory denominata `hellodotnetcore`e modificare hello tooit di directory corrente.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-115">Create a directory named `hellodotnetcore`, and change hello current directory tooit.</span></span> <span data-ttu-id="2a2a5-116">Quindi digitare hello segue:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-116">Then type hello following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="2a2a5-117">Questo comando crea tre file (*hellodotnetcore.csproj*, *Program.cs*, e *Startup.cs*) e una cartella vuota (*wwwroot /*) nella directory corrente hello.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under hello current directory.</span></span> <span data-ttu-id="2a2a5-118">contenuto di Hello `.csproj` file dovrebbe essere simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-118">hello content of `.csproj` file should look like hello following:</span></span> 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

<span data-ttu-id="2a2a5-119">Poiché questa applicazione è un'applicazione web, tooan un riferimento pacchetto ASP.NET Core è stato automaticamente aggiunto toohello *hellodotnetcore.csproj* file.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-119">Since this app is a web application, a reference tooan ASP.NET Core package was automatically added toohello *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="2a2a5-120">numero di versione di Hello del pacchetto di hello è impostato in base toohello framework scelto.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-120">hello version number of hello package is set according toohello chosen framework.</span></span> <span data-ttu-id="2a2a5-121">Questo esempio fa riferimento ad ASP.NET Core versione 1.1.2 perché è in uso .NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-hello-application-locally"></a><span data-ttu-id="2a2a5-122">Compilare e testare un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="2a2a5-122">Build and test hello application locally</span></span> ##

<span data-ttu-id="2a2a5-123">È possibile compilare ed eseguire l'app .NET Core con hello `dotnet restore` comando seguito da hello `dotnet run` comando, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-123">You can build and run your .NET Core app with hello `dotnet restore` command followed by hello `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="2a2a5-124">All'avvio di un'applicazione hello, viene visualizzato un messaggio che indica l'applicazione hello è in ascolto delle richieste di tooincoming su una porta.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-124">When hello application starts, it displays a message indicating hello app is listening tooincoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

<span data-ttu-id="2a2a5-125">Test esplorando troppo`http://localhost:5000/` con il browser.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-125">Test it by browsing too`http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="2a2a5-126">Se tutto funziona correttamente, viene visualizzato il testo</span><span class="sxs-lookup"><span data-stu-id="2a2a5-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="2a2a5-127">come testo risultato hello.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-127">as hello result text.</span></span>

![Eseguire il test con il browser][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a><span data-ttu-id="2a2a5-129">Creare un'applicazione .NET Core in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2a2a5-129">Create a .NET Core app in hello Azure Portal</span></span> ##

<span data-ttu-id="2a2a5-130">È necessario innanzitutto toocreate un'app web vuota.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-130">First you need toocreate an empty web app.</span></span> <span data-ttu-id="2a2a5-131">Accedi toohello [portale di Azure](https://portal.azure.com/) e creare un nuovo [App Web in Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="2a2a5-131">Log in toohello [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Creazione di un'app Web][1]

<span data-ttu-id="2a2a5-133">Quando hello **crea** verrà visualizzata la pagina, fornire i dettagli sull'app web:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-133">When hello **Create** page opens, provide details about your web app:</span></span>

![Scelta di uno stack di runtime .NET Core][2]

<span data-ttu-id="2a2a5-135">Seguente hello utilizzare tabella come una Guida toofill out hello **crea** pagina, quindi selezionare **OK** e **crea** toocreate hello app.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-135">Use hello following table as a guide toofill out hello **Create** page, then select **OK** and **Create** toocreate hello app.</span></span>

| <span data-ttu-id="2a2a5-136">Impostazione</span><span class="sxs-lookup"><span data-stu-id="2a2a5-136">Setting</span></span>      | <span data-ttu-id="2a2a5-137">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="2a2a5-137">Suggested value</span></span>  | <span data-ttu-id="2a2a5-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a2a5-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="2a2a5-139">Nome app</span><span class="sxs-lookup"><span data-stu-id="2a2a5-139">App name</span></span> | <span data-ttu-id="2a2a5-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="2a2a5-140">hellodotnetcore</span></span>  | <span data-ttu-id="2a2a5-141">nome Hello dell'app.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-141">hello name of your app.</span></span> <span data-ttu-id="2a2a5-142">Il nome deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-142">This name must be unique.</span></span> |
| <span data-ttu-id="2a2a5-143">Subscription</span><span class="sxs-lookup"><span data-stu-id="2a2a5-143">Subscription</span></span> | <span data-ttu-id="2a2a5-144">Scelta di una sottoscrizione esistente</span><span class="sxs-lookup"><span data-stu-id="2a2a5-144">Choose an existing subscription</span></span> | <span data-ttu-id="2a2a5-145">Hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-145">hello Azure subscription.</span></span> |
| <span data-ttu-id="2a2a5-146">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="2a2a5-146">Resource Group</span></span> | <span data-ttu-id="2a2a5-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2a2a5-147">myResourceGroup</span></span> |  <span data-ttu-id="2a2a5-148">risorse di Azure gruppo toocontain hello web app Hello.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-148">hello Azure resource group toocontain hello web app.</span></span> |
| <span data-ttu-id="2a2a5-149">Piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="2a2a5-149">App Service Plan</span></span> | <span data-ttu-id="2a2a5-150">Nome del piano di servizio app esistente</span><span class="sxs-lookup"><span data-stu-id="2a2a5-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="2a2a5-151">Hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-151">hello App Service plan.</span></span>  |
| <span data-ttu-id="2a2a5-152">Configura contenitore</span><span class="sxs-lookup"><span data-stu-id="2a2a5-152">Configure Container</span></span> | <span data-ttu-id="2a2a5-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="2a2a5-153">.NET Core 1.1</span></span> | <span data-ttu-id="2a2a5-154">tipo di contenitore per questa app web Hello: Registro di sistema predefinite, Docker o Private.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-154">hello type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="2a2a5-155">Origine immagine</span><span class="sxs-lookup"><span data-stu-id="2a2a5-155">Image source</span></span>  | <span data-ttu-id="2a2a5-156">Predefinito</span><span class="sxs-lookup"><span data-stu-id="2a2a5-156">Built-in</span></span>  |  <span data-ttu-id="2a2a5-157">origine Hello dell'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-157">hello source of hello image.</span></span> |
| <span data-ttu-id="2a2a5-158">Stack di runtime</span><span class="sxs-lookup"><span data-stu-id="2a2a5-158">Runtime Stack</span></span>  | <span data-ttu-id="2a2a5-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="2a2a5-159">.NET Core 1.1</span></span>  | <span data-ttu-id="2a2a5-160">stack di runtime Hello e versione.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-160">hello runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="2a2a5-161">Distribuire l'applicazione tramite Git</span><span class="sxs-lookup"><span data-stu-id="2a2a5-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="2a2a5-162">Usare Git toodeploy hello .NET Core applicazione tooAzure App del servizio Web App in Linux.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-162">Use Git toodeploy hello .NET Core application tooAzure App Service Web App on Linux.</span></span>

<span data-ttu-id="2a2a5-163">nuova app web di Azure di Hello dispone già di distribuzione Git configurata.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-163">hello new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="2a2a5-164">URL di distribuzione Git hello noterai passando toohello URL seguente dopo aver inserito il nome dell'applicazione web:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-164">You will find hello Git deployment URL by navigating toohello following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="2a2a5-165">URL Git Hello è hello modulo basato sul nome dell'app web seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-165">hello Git URL has hello following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="2a2a5-166">Eseguire hello seguenti app web di Azure tooyour di comandi toodeploy hello applicazione locale:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-166">Run hello following commands toodeploy hello local application tooyour Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="2a2a5-167">Non è necessario di tutti i file in toopush *bin /* o *obj /* directory perché la compilazione dell'applicazione nel cloud hello quando hello dell'applicazione i file di origine vengono inseriti tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-167">You don't need toopush any files under *bin/* or *obj/* directories because your application is built in hello cloud when hello application's source files are pushed tooAzure.</span></span> <span data-ttu-id="2a2a5-168">Una volta completato il processo di compilazione hello, i file binari vengono copiati nella directory dell'applicazione hello in */home/sito/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-168">After hello build process is complete, binary files are copied into hello application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="2a2a5-169">Verificare che le operazioni di distribuzione remoto hello segnalano l'esito positivo.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-169">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="2a2a5-170">Le operazioni di push potrebbero richiedere alcuni minuti dopo la risoluzione di pacchetto ed eseguito nel cloud hello processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-170">Push operations may take a while since package resolution and build process run in hello cloud.</span></span> <span data-ttu-id="2a2a5-171">Verranno visualizzati alcuni messaggi di stato, di cui uno informa che i file sono stati copiati.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="2a2a5-172">output di Hello dovrebbe essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-172">hello output should look similar toohello following:</span></span>

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="2a2a5-173">Una volta completata la distribuzione di hello, riavviare l'app web per effetto di tootake distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-173">Once hello deployment has completed, restart your web app for hello deployment tootake effect.</span></span> <span data-ttu-id="2a2a5-174">toodo, andare toohello portale di Azure e passare toohello **Panoramica** pagina dell'app web.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-174">toodo this, go toohello Azure portal and navigate toohello **Overview** page of your web app.</span></span> <span data-ttu-id="2a2a5-175">Seleziona hello **riavviare** nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-175">Select hello **Restart** button in hello page.</span></span> <span data-ttu-id="2a2a5-176">Quando una finestra popup viene visualizzato, selezionare **Sì** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="2a2a5-176">When a popup window shows up, select **Yes** tooconfirm.</span></span> <span data-ttu-id="2a2a5-177">È quindi possibile passare all'app Web, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2a2a5-177">You can then browse your web app, as shown here:</span></span>

![Esplorazione di .NET Core app distribuita tooAzure servizio App in Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="2a2a5-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a2a5-179">Next steps</span></span>
* [<span data-ttu-id="2a2a5-180">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="2a2a5-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
