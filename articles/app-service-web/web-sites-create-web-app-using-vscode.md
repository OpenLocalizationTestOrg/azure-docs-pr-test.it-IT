---
title: aaaCreate un'app web ASP.NET Core in Visual Studio Code
description: In questa esercitazione viene illustrato come toocreate un Core di ASP.NET web app con codice di Visual Studio.
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
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="2ac8b-103">Creare un'app Web ASP.NET Core in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2ac8b-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="2ac8b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2ac8b-104">Overview</span></span>
<span data-ttu-id="2ac8b-105">Questa esercitazione viene illustrato come toocreate un Core di ASP.NET web app usando [codice di Visual Studio (Visual Studio Code)](http://code.visualstudio.com//Docs/whyvscode) e distribuirlo troppo[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="2ac8b-106">Sebbene in questo articolo si riferisce tooweb App, si applica anche tooAPI App e App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="2ac8b-107">ASP.NET Core è un'importante riprogettazione di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="2ac8b-108">Costituisce un nuovo framework open source e multipiattaforma per la creazione tramite .NET di moderne app Web basate sul cloud.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="2ac8b-109">Per ulteriori informazioni, vedere [tooASP.NET introduzione Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="2ac8b-110">Per altre informazioni sulle app Web del servizio app di Azure, vedere [Panoramica delle app Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="2ac8b-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2ac8b-111">Prerequisites</span></span>
* <span data-ttu-id="2ac8b-112">Installare [Visual Studio Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="2ac8b-113">Installare Git: è possibile installarlo da una delle seguenti posizioni: [Chocolatey](https://chocolatey.org/packages/git) o [git-scm.com](http://git-scm.com/downloads). Se si tooGit nuovo, scegliere [git scm.com](http://git-scm.com/downloads) e selezionare opzione hello troppo**usare Git dal prompt dei comandi di Windows hello**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="2ac8b-114">Dopo aver installato Git, è necessario anche nome utente di tooset hello Git e di posta elettronica come è necessario più avanti nell'esercitazione hello (quando si esegue un'operazione di commit dal codice di Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="2ac8b-115">Installare ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2ac8b-115">Install ASP.NET Core</span></span>
<span data-ttu-id="2ac8b-116">ASP.NET Core è uno stack .NET snello per la creazione di un cloud moderno e di app Web in esecuzione su OS X, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="2ac8b-117">Si è stato compilato dalla hello messa a terra backup tooprovide un framework di sviluppo ottimizzato per le app che sono entrambi cloud toohello distribuito o vengono eseguiti in locale.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="2ac8b-118">È costituito da componenti modulari con un overhead minimo, in modo da garantire la massima flessibilità durante la creazione di soluzioni.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="2ac8b-119">In questa esercitazione è progettata tooget viene avviata la compilazione di applicazioni con versioni di sviluppo più recenti di hello di ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="2ac8b-120">Hello attenendosi alle istruzioni è tooWindows specifico.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="2ac8b-121">Per istruzioni sull'installazione in OS X, Linux e Windows, vedere [Getting started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started) (Introduzione ad ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="2ac8b-122">Per istruzioni di installazione più dettagliate per OS X, Linux e Windows, vedere [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx) (Installazione di ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="2ac8b-123">Creare l'app web hello</span><span class="sxs-lookup"><span data-stu-id="2ac8b-123">Create hello web app</span></span>
<span data-ttu-id="2ac8b-124">In questa sezione viene illustrato come una nuova app ASP.NET tooscaffold web app usando lo strumento .NET CLI hello.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="2ac8b-125">Immettere seguente hello al prompt dei comandi toocreate hello progetto cartella e lo scaffolding hello app hello.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![Generatore dell'interfaccia della riga di comando dotnet - ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="2ac8b-127">toorestore hello pacchetti NuGet necessari, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2ac8b-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="2ac8b-128">Eseguire localmente l'app web hello</span><span class="sxs-lookup"><span data-stu-id="2ac8b-128">Run hello web app locally</span></span>
<span data-ttu-id="2ac8b-129">Ora che è creato hello web app e recuperare tutti i pacchetti NuGet hello per hello app, è possibile eseguire app web hello in locale.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="2ac8b-130">Eseguire app hello (hello `dotnet run` comando verrà compilata l'applicazione hello quando è aggiornata):</span><span class="sxs-lookup"><span data-stu-id="2ac8b-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="2ac8b-131">Aprire un browser e passare toohello URL seguente.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="2ac8b-132">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="2ac8b-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="2ac8b-133">pagina predefinita Hello dell'app web hello apparirà come segue.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![App Web locale in un browser](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="2ac8b-135">Chiudere il browser.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-135">Close your browser.</span></span> <span data-ttu-id="2ac8b-136">In hello **finestra di comando**, premere **Ctrl + C** tooshut verso il basso di un'applicazione hello e chiude hello **finestra di comando**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="2ac8b-137">Creare un'app web nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="2ac8b-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="2ac8b-138">Hello seguente verrà procedura consente di creare un'app web nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="2ac8b-139">Accedi toohello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2ac8b-140">Fare clic su **NEW** in hello in alto a sinistra del portale hello.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="2ac8b-141">Fare clic su **App Web > App Web**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-141">Click **Web Apps > Web App**.</span></span>
   
    ![Nuova app Web di Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="2ac8b-143">Immettere un valore in **Nome**, ad esempio **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="2ac8b-144">Si noti che questo nome deve toobe univoco e portale hello imporrà che quando si tenta di nome hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="2ac8b-145">Pertanto, se si seleziona un invio di un valore diverso, è necessario toosubstitute tale valore per ogni occorrenza di **SampleWebAppDemo** visualizzati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="2ac8b-146">Selezionare un piano esistente in **Piano di servizio app** o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="2ac8b-147">Se si crea un nuovo piano, selezionare hello piano tariffario, posizione e altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="2ac8b-148">Per ulteriori informazioni sui piani di servizio App, vedere l'articolo hello [piani di servizio App di Azure ad approfondimenti su](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Pannello Nuova app Web di Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="2ac8b-150">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-150">Click **Create**.</span></span>
   
    ![Pannello dell'app Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="2ac8b-152">Abilitare la pubblicazione Git per hello nuova app web</span><span class="sxs-lookup"><span data-stu-id="2ac8b-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="2ac8b-153">GIT è un sistema di controllo della versione distribuita che è possibile utilizzare toodeploy l'app web di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="2ac8b-154">Archiviare il codice hello che scritto per l'app web in un repository Git locale e si distribuiranno tooAzure del codice mediante il push dei repository remoto tooa.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="2ac8b-155">Accedere al hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2ac8b-156">Fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-156">Click **Browse**.</span></span>
3. <span data-ttu-id="2ac8b-157">Fare clic su **App Web** tooview un elenco di App web hello associati alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="2ac8b-158">Selezionare l'app web hello che è stato creato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="2ac8b-159">Nel Pannello di hello web app, fare clic su **impostazioni** > **distribuzione continua**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Host dell'app Web di Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="2ac8b-161">Fare clic su **Scegliere l'origine > Repository Git locale**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="2ac8b-162">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-162">Click **OK**.</span></span>
   
    ![Repository Git locale di Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="2ac8b-164">Se le credenziali di distribuzione per la pubblicazione di un'app Web o di un'altra app del servizio app non sono ancora state configurate, è possibile farlo ora:</span><span class="sxs-lookup"><span data-stu-id="2ac8b-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="2ac8b-165">Fare clic su **Impostazioni** > **Credenziali di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="2ac8b-166">Hello **impostare le credenziali di distribuzione** pannello verrà visualizzato.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="2ac8b-167">Creare un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-167">Create a user name and password.</span></span>  <span data-ttu-id="2ac8b-168">La password sarà necessaria più avanti durante la configurazione di Git.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="2ac8b-169">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-169">Click **Save**.</span></span>
9. <span data-ttu-id="2ac8b-170">Nel pannello dell'app Web fare clic su **Impostazioni > Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="2ac8b-171">URL di Hello del repository Git remoto hello che verranno distribuite toois indicato nel **URL GIT**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="2ac8b-172">Hello copia **URL GIT** valore per un utilizzo successivo in esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![URL Git di Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="2ac8b-174">Pubblicare il tooAzure app web del servizio App</span><span class="sxs-lookup"><span data-stu-id="2ac8b-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="2ac8b-175">In questa sezione si crea un repository Git locale e push da tale toodeploy tooAzure repository del tooAzure app web.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="2ac8b-176">Nel codice di Visual Studio, selezionare hello **Git** opzione nella barra di spostamento sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![Icona di Git in Visual Studio Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="2ac8b-178">Selezionare **repository git Initialize** toomake che l'area di lavoro è nel controllo del codice sorgente git.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Initialize Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="2ac8b-180">Aprire una finestra di comando hello e passare alla directory di toohello directory dell'app web.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="2ac8b-181">Immettere quindi hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2ac8b-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="2ac8b-182">Questo comando evita un problema relativo al testo che concerne le terminazioni CRLF e LF.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="2ac8b-183">Nel codice di Visual Studio, aggiungere un messaggio di conferma e fare clic su hello **tutti i Commit** il segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![Commit All in Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="2ac8b-185">Al termine dell'elaborazione Git, si noterà che non sono presenti file elencati nella finestra di Git hello in **modifiche**.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Nessuna modifica in Git](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="2ac8b-187">Modificare toohello back-finestra di comando al prompt dei comandi di hello quale fa riferimento toohello directory in cui si trova l'app web.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="2ac8b-188">Creare un riferimento remoto per l'inserimento di app web tooyour di aggiornamenti tramite hello URL Git (che termina con "GIT") che è stato copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="2ac8b-189">Configurare Git toosave le credenziali in locale in modo che siano tooyour aggiunti automaticamente i comandi di push generati dal codice di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="2ac8b-190">Effettuare il push del tooAzure modifiche immettendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="2ac8b-191">Dopo questo tooAzure push iniziale, sarà in grado di toodo push hello tutti i comandi di Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="2ac8b-192">Viene chiesto di immettere la password di hello creato in precedenza in Azure.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="2ac8b-193">**Nota: La password non sarà visibile.**</span><span class="sxs-lookup"><span data-stu-id="2ac8b-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="2ac8b-194">output di Hello dalla hello sopra comando termina con un messaggio che la distribuzione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="2ac8b-195">Se si apportano modifiche tooyour app, è possibile ripubblicare direttamente nel codice di Visual Studio con Git funzionalità hello selezionando hello **Commit tutti** opzione seguita da hello **Push** opzione.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="2ac8b-196">Si noterà hello **Push** opzione è disponibile in hello dal menu a discesa successivo toohello **Commit tutti** e **aggiornamento** pulsanti.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="2ac8b-197">Se è necessario toocollaborate su un progetto, è consigliabile push tooGitHub tra tooAzure push.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="2ac8b-198">Eseguire l'applicazione hello in Azure</span><span class="sxs-lookup"><span data-stu-id="2ac8b-198">Run hello app in Azure</span></span>
<span data-ttu-id="2ac8b-199">Ora che è stato distribuito l'app web, eseguire app hello mentre ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="2ac8b-200">A questo scopo, è possibile eseguire una delle due operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ac8b-200">This can be done in two ways:</span></span>

* <span data-ttu-id="2ac8b-201">Aprire un browser e immettere il nome di hello dell'app web come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="2ac8b-202">In hello portale di Azure, individuare pannello app web di hello per le app web e fare clic su **Sfoglia** tooview l'app</span><span class="sxs-lookup"><span data-stu-id="2ac8b-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="2ac8b-203">nel browser predefinito.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-203">in your default browser.</span></span>

![App Web di Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="2ac8b-205">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2ac8b-205">Summary</span></span>
<span data-ttu-id="2ac8b-206">In questa esercitazione, si è appreso come toocreate un'app web nel codice di Visual Studio e distribuirlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2ac8b-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="2ac8b-207">Per ulteriori informazioni sul codice di Visual Studio, vedere l'articolo hello [perché Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="2ac8b-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="2ac8b-208">Per altre informazioni sulle app Web del servizio app, vedere [Panoramica delle app Web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ac8b-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

