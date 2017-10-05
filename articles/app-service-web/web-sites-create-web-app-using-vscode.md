---
title: Creare un'app Web ASP.NET Core in Visual Studio Code
description: Questa esercitazione illustra come creare un'app Web ASP.NET Core usando Visual Studio Code.
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="4e563-103">Creare un'app Web ASP.NET Core in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4e563-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="4e563-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4e563-104">Overview</span></span>
<span data-ttu-id="4e563-105">Questa esercitazione illustra come creare un'app Web ASP.NET Core usando [Visual Studio Code](http://code.visualstudio.com//Docs/whyvscode) e come distribuirla nel [Servizio app di Azure](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4e563-105">This tutorial shows you how to create an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="4e563-106">Sebbene in questo articolo si faccia riferimento alle app Web, è applicabile anche ad app per le API e app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4e563-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="4e563-107">ASP.NET Core è un'importante riprogettazione di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4e563-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="4e563-108">Costituisce un nuovo framework open source e multipiattaforma per la creazione tramite .NET di moderne app Web basate sul cloud.</span><span class="sxs-lookup"><span data-stu-id="4e563-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="4e563-109">Per altre informazioni, vedere [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html) (Cenni preliminari su ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="4e563-109">For more information, see [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="4e563-110">Per altre informazioni sulle app Web del servizio app di Azure, vedere [Panoramica delle app Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e563-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="4e563-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4e563-111">Prerequisites</span></span>
* <span data-ttu-id="4e563-112">Installare [Visual Studio Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="4e563-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="4e563-113">Installare Git: è possibile installarlo da una delle seguenti posizioni: [Chocolatey](https://chocolatey.org/packages/git) o [git-scm.com](http://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="4e563-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="4e563-114">Se non si ha familiarità con Git, scegliere [git-scm.com](http://git-scm.com/downloads) e selezionare l'opzione **Usare Git dal prompt dei comandi di Windows**.</span><span class="sxs-lookup"><span data-stu-id="4e563-114">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="4e563-115">Dopo aver installato Git, è necessario impostare il nome utente e l'indirizzo di posta elettronica Git, poiché verrà richiesto più avanti nell'esercitazione (quando si eseguirà un'operazione di commit da Visual Studio Code).</span><span class="sxs-lookup"><span data-stu-id="4e563-115">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="4e563-116">Installare ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4e563-116">Install ASP.NET Core</span></span>
<span data-ttu-id="4e563-117">ASP.NET Core è uno stack .NET snello per la creazione di un cloud moderno e di app Web in esecuzione su OS X, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="4e563-117">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="4e563-118">È stato completamente riprogettato per fornire un framework di sviluppo ottimizzato per le app che vengono distribuite nel cloud o eseguite in locale.</span><span class="sxs-lookup"><span data-stu-id="4e563-118">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="4e563-119">È costituito da componenti modulari con un overhead minimo, in modo da garantire la massima flessibilità durante la creazione di soluzioni.</span><span class="sxs-lookup"><span data-stu-id="4e563-119">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="4e563-120">Questa esercitazione è stata realizzata per illustrare la creazione di applicazioni con le più recenti versioni di sviluppo di ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="4e563-120">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="4e563-121">Le istruzioni seguenti sono specifiche di Windows.</span><span class="sxs-lookup"><span data-stu-id="4e563-121">The following instructions are specific to Windows.</span></span> <span data-ttu-id="4e563-122">Per istruzioni sull'installazione in OS X, Linux e Windows, vedere [Getting started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started) (Introduzione ad ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="4e563-122">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="4e563-123">Per istruzioni di installazione più dettagliate per OS X, Linux e Windows, vedere [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx) (Installazione di ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="4e563-123">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="4e563-124">Creare l'app Web</span><span class="sxs-lookup"><span data-stu-id="4e563-124">Create the web app</span></span>
<span data-ttu-id="4e563-125">Questa sezione illustra come eseguire lo scaffolding di una nuova app Web ASP.NET usando lo strumento dell'interfaccia della riga di comando .NET.</span><span class="sxs-lookup"><span data-stu-id="4e563-125">This section shows you how to scaffold a new app ASP.NET web app using the .NET CLI tool.</span></span> 

1. <span data-ttu-id="4e563-126">Digitare quanto segue al prompt dei comandi per creare la cartella di progetto ed eseguire lo scaffolding dell'app.</span><span class="sxs-lookup"><span data-stu-id="4e563-126">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![Generatore dell'interfaccia della riga di comando dotnet - ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="4e563-128">Per ripristinare i pacchetti NuGet necessari, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="4e563-128">To restore the necessary NuGet packages, run the following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a><span data-ttu-id="4e563-129">Eseguire l'app Web in locale</span><span class="sxs-lookup"><span data-stu-id="4e563-129">Run the web app locally</span></span>
<span data-ttu-id="4e563-130">Dopo aver creato l'app Web e recuperato tutti i pacchetti NuGet per l'app, è ora possibile eseguire l'app Web in locale.</span><span class="sxs-lookup"><span data-stu-id="4e563-130">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="4e563-131">Eseguire l'app (il comando `dotnet run` compilerà l'app quando è scaduta):</span><span class="sxs-lookup"><span data-stu-id="4e563-131">Run the app  (the `dotnet run` command will build the app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="4e563-132">Aprire un browser e passare all'URL seguente.</span><span class="sxs-lookup"><span data-stu-id="4e563-132">Open a browser and navigate to the following URL.</span></span>
   
    <span data-ttu-id="4e563-133">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="4e563-133">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="4e563-134">Verrà visualizzata la pagina predefinita dell'app Web, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4e563-134">The default page of the web app will appear as follows.</span></span>
   
    ![App Web locale in un browser](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="4e563-136">Chiudere il browser.</span><span class="sxs-lookup"><span data-stu-id="4e563-136">Close your browser.</span></span> <span data-ttu-id="4e563-137">Nella **finestra di comando** premere **Ctrl+C** per arrestare l'applicazione e chiudere la **finestra di comando**.</span><span class="sxs-lookup"><span data-stu-id="4e563-137">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="4e563-138">Creazione di un'app Web nel portale di Azure ##</span><span class="sxs-lookup"><span data-stu-id="4e563-138">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="4e563-139">La procedura seguente consente di creare di un'app Web nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e563-139">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="4e563-140">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e563-140">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4e563-141">Fare clic su **NUOVO** nella parte superiore sinistra del portale.</span><span class="sxs-lookup"><span data-stu-id="4e563-141">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="4e563-142">Fare clic su **App Web > App Web**.</span><span class="sxs-lookup"><span data-stu-id="4e563-142">Click **Web Apps > Web App**.</span></span>
   
    ![Nuova app Web di Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="4e563-144">Immettere un valore in **Nome**, ad esempio **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="4e563-144">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="4e563-145">Il nome deve essere univoco, come imposto dal portale quando si tenta di immettere il nome.</span><span class="sxs-lookup"><span data-stu-id="4e563-145">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="4e563-146">Se si immette un valore diverso, sarà necessario sostituirlo per ogni occorrenza di **SampleWebAppDemo** presente in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4e563-146">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="4e563-147">Selezionare un piano esistente in **Piano di servizio app** o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="4e563-147">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="4e563-148">Se si crea un nuovo piano, selezionare i piano tariffario, la posizione e altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="4e563-148">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="4e563-149">Per altre informazioni sui piani di servizio app, vedere l'articolo [Panoramica approfondita dei piani del servizio app di Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e563-149">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Pannello Nuova app Web di Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="4e563-151">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4e563-151">Click **Create**.</span></span>
   
    ![Pannello dell'app Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="4e563-153">Abilitare la pubblicazione Git per la nuova app Web</span><span class="sxs-lookup"><span data-stu-id="4e563-153">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="4e563-154">Git è un sistema di controllo delle versioni distribuite che è possibile usare per distribuire l'app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e563-154">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="4e563-155">Il codice scritto per l'app Web verrà archiviato in un repository Git locale e verrà distribuito in Azure tramite il push in un repository remoto.</span><span class="sxs-lookup"><span data-stu-id="4e563-155">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="4e563-156">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e563-156">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4e563-157">Fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="4e563-157">Click **Browse**.</span></span>
3. <span data-ttu-id="4e563-158">Fare clic su **App Web** per visualizzare un elenco delle app Web associate alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e563-158">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="4e563-159">Selezionare l'app Web creata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4e563-159">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="4e563-160">Nel pannello dell'app Web fare clic su **Impostazioni** > **Distribuzione continua**.</span><span class="sxs-lookup"><span data-stu-id="4e563-160">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Host dell'app Web di Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="4e563-162">Fare clic su **Scegliere l'origine > Repository Git locale**.</span><span class="sxs-lookup"><span data-stu-id="4e563-162">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="4e563-163">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e563-163">Click **OK**.</span></span>
   
    ![Repository Git locale di Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="4e563-165">Se le credenziali di distribuzione per la pubblicazione di un'app Web o di un'altra app del servizio app non sono ancora state configurate, è possibile farlo ora:</span><span class="sxs-lookup"><span data-stu-id="4e563-165">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="4e563-166">Fare clic su **Impostazioni** > **Credenziali di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="4e563-166">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="4e563-167">Verrà visualizzato il pannello **Imposta credenziali di distribuzione** .</span><span class="sxs-lookup"><span data-stu-id="4e563-167">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="4e563-168">Creare un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="4e563-168">Create a user name and password.</span></span>  <span data-ttu-id="4e563-169">La password sarà necessaria più avanti durante la configurazione di Git.</span><span class="sxs-lookup"><span data-stu-id="4e563-169">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="4e563-170">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="4e563-170">Click **Save**.</span></span>
9. <span data-ttu-id="4e563-171">Nel pannello dell'app Web fare clic su **Impostazioni > Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="4e563-171">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="4e563-172">L'URL del repository Git remoto in cui verrà effettuata la distribuzione è visualizzato in **URL GIT**.</span><span class="sxs-lookup"><span data-stu-id="4e563-172">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="4e563-173">Copiare il valore dell'opzione **URL GIT** , che sarà necessario più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4e563-173">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![URL Git di Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="4e563-175">Pubblicare l'app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="4e563-175">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="4e563-176">In questa sezione si creerà un repository Git locale e si eseguirà il push dal repository ad Azure per poter distribuire l'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="4e563-176">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="4e563-177">In Visual Studio Code selezionare l'opzione **Git** nella barra di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4e563-177">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![Icona di Git in Visual Studio Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="4e563-179">Selezionare **Initialize git repository** per accertarsi che l'area di lavoro sia sotto il controllo del codice sorgente di Git.</span><span class="sxs-lookup"><span data-stu-id="4e563-179">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![Initialize Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="4e563-181">Aprire la finestra di comando e passare alla directory dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="4e563-181">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="4e563-182">Immettere quindi il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4e563-182">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="4e563-183">Questo comando evita un problema relativo al testo che concerne le terminazioni CRLF e LF.</span><span class="sxs-lookup"><span data-stu-id="4e563-183">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="4e563-184">In Visual Studio Code, aggiungere un messaggio per il commit e fare clic sull'icona con il segno di spunta per **Commit All** .</span><span class="sxs-lookup"><span data-stu-id="4e563-184">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![Commit All in Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="4e563-186">Al termine dell'operazione di elaborazione, nella finestra Git non sarà più elencato alcun file e verrà invece visualizzata la voce **Changes**.</span><span class="sxs-lookup"><span data-stu-id="4e563-186">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![Nessuna modifica in Git](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="4e563-188">Tornare alla finestra di comando in cui il prompt dei comandi punta alla directory in cui si trova l'app Web.</span><span class="sxs-lookup"><span data-stu-id="4e563-188">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="4e563-189">Creare un riferimento remoto per effettuare il push degli aggiornamenti nell'app Web usando l'URL GIT (che termina con "git") copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4e563-189">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="4e563-190">Configurare Git per salvare le credenziali a livello locale, in modo che siano aggiunte automaticamente ai comandi push generati da Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="4e563-190">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="4e563-191">Effettuare il push delle modifiche in Azure usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="4e563-191">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="4e563-192">Dopo questo push iniziale in Azure, sarà possibile eseguire tutti i comandi push di Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="4e563-192">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="4e563-193">Verrà richiesto di specificare la password creata in precedenza in Azure.</span><span class="sxs-lookup"><span data-stu-id="4e563-193">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="4e563-194">**Nota: La password non sarà visibile.**</span><span class="sxs-lookup"><span data-stu-id="4e563-194">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="4e563-195">L'output generato dal comando precedente termina con un messaggio in cui si specifica che la distribuzione è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="4e563-195">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="4e563-196">Se si apportano modifiche all'app, è possibile ripetere la pubblicazione direttamente in Visual Studio Code con la funzionalità Git predefinita integrata selezionando l'opzione **Commit All** seguita dall'opzione **Push**.</span><span class="sxs-lookup"><span data-stu-id="4e563-196">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="4e563-197">L'opzione **Push** è disponibile nel menu a discesa accanto ai pulsanti **Commit all** e **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="4e563-197">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="4e563-198">Se è necessario collaborare a un progetto, considerare la possibilità di effettuare il push in GitHub mentre si effettua il push in Azure.</span><span class="sxs-lookup"><span data-stu-id="4e563-198">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="4e563-199">Eseguire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="4e563-199">Run the app in Azure</span></span>
<span data-ttu-id="4e563-200">Dopo aver distribuito l'app Web, è possibile ora eseguirla mentre è ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="4e563-200">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="4e563-201">A questo scopo, è possibile eseguire una delle due operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4e563-201">This can be done in two ways:</span></span>

* <span data-ttu-id="4e563-202">Aprire un browser e immettere il nome dell'app Web come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4e563-202">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="4e563-203">Nel Portale di Azure, individuare il pannello dell'app Web e fare clic su **Sfoglia** per visualizzare l'app</span><span class="sxs-lookup"><span data-stu-id="4e563-203">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="4e563-204">nel browser predefinito.</span><span class="sxs-lookup"><span data-stu-id="4e563-204">in your default browser.</span></span>

![App Web di Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="4e563-206">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="4e563-206">Summary</span></span>
<span data-ttu-id="4e563-207">In questa esercitazione si è appreso come creare un'app Web in Visual Studio Code e distribuirla in Azure.</span><span class="sxs-lookup"><span data-stu-id="4e563-207">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="4e563-208">Per altre informazioni su Visual Studio Code, vedere l'articolo [Vantaggi di Visual Studio Code](https://code.visualstudio.com/Docs/).</span><span class="sxs-lookup"><span data-stu-id="4e563-208">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="4e563-209">Per altre informazioni sulle app Web del servizio app, vedere [Panoramica delle app Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e563-209">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

