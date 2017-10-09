---
title: app web per dispositivi mobili aaaDeploy un MVC ASP.NET 5 in Azure App Service
description: "Un'esercitazione che illustra come funzionalità toodeploy un tooAzure app web del servizio App tramite dispositivi mobili in ASP.NET MVC 5 applicazione web."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="705c4-103">Distribuzione di un'app Web ASP.NET MVC 5 per dispositivi mobili nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="705c4-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="705c4-104">Questa esercitazione verrà illustrato è hello nozioni di base di ricerca toobuild un MVC ASP.NET 5 web app mobile descrittivi e distribuirlo tooAzure servizio App.</span><span class="sxs-lookup"><span data-stu-id="705c4-104">This tutorial will teach you hello basics of how toobuild an ASP.NET MVC 5 web app that is mobile-friendly and deploy it tooAzure App Service.</span></span> <span data-ttu-id="705c4-105">Per questa esercitazione, è necessario [Visual Studio Express 2013 per Web] [ Visual Studio Express 2013] hello versione o professional di Visual Studio se si dispone già di.</span><span class="sxs-lookup"><span data-stu-id="705c4-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or hello professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="705c4-106">È possibile utilizzare [Visual Studio 2015] ma catture di schermata hello saranno diversi ed è necessario utilizzare modelli di hello ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="705c4-106">You can use [Visual Studio 2015] but hello screen shots will be different and you must use hello ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="705c4-107">Scopo dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="705c4-107">What You'll Build</span></span>
<span data-ttu-id="705c4-108">Per questa esercitazione si aggiungerà funzionalità mobili toohello conferenza listato applicazione semplice che viene fornito nella hello [progetto iniziale][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="705c4-108">For this tutorial, you'll add mobile features toohello simple conference-listing application that's provided in hello [starter project][StarterProject].</span></span> <span data-ttu-id="705c4-109">Hello schermata seguente mostra le sessioni ASP.NET hello in un'applicazione hello completata, come illustrato nell'emulatore di browser hello negli strumenti di sviluppo F12 di Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="705c4-109">hello following screenshot shows hello ASP.NET sessions in hello completed application, as seen in hello browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="705c4-110">È possibile utilizzare gli strumenti di sviluppo F12 di Internet Explorer 11 hello e hello [strumento Fiddler] [ Fiddler] toohelp il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="705c4-110">You can use hello Internet Explorer 11 F12 developer tools and hello [Fiddler tool][Fiddler] toohelp debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="705c4-111">Acquisizione di competenze</span><span class="sxs-lookup"><span data-stu-id="705c4-111">Skills You'll Learn</span></span>
<span data-ttu-id="705c4-112">In questa esercitazione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="705c4-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="705c4-113">Come toopublish toouse Visual Studio 2013 l'applicazione web direttamente tooa app web in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="705c4-113">How toouse Visual Studio 2013 toopublish your web application directly tooa web app in Azure App Service.</span></span>
* <span data-ttu-id="705c4-114">Utilizzano modelli ASP.NET MVC 5 hello framework Bootstrap CSS hello per migliorare la visualizzazione su dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="705c4-114">How hello ASP.NET MVC 5 templates use hello CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="705c4-115">Come toocreate mobile specifiche viste tootarget specifico browser per dispositivi mobili, come iPhone hello e Android</span><span class="sxs-lookup"><span data-stu-id="705c4-115">How toocreate mobile-specific views tootarget specific mobile browsers, such as hello iPhone and Android</span></span>
* <span data-ttu-id="705c4-116">Come toocreate reattiva viste (viste che rispondono toodifferent browser tra i dispositivi)</span><span class="sxs-lookup"><span data-stu-id="705c4-116">How toocreate responsive views (views that respond toodifferent browsers across devices)</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="705c4-117">Configurare un ambiente di sviluppo hello</span><span class="sxs-lookup"><span data-stu-id="705c4-117">Set up hello development environment</span></span>
<span data-ttu-id="705c4-118">Configurare l'ambiente di sviluppo installando hello Azure SDK per .NET 2.5.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="705c4-118">Set up your development environment by installing hello Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="705c4-119">tooinstall hello Azure SDK per .NET, fare clic su collegamento hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="705c4-119">tooinstall hello Azure SDK for .NET, click hello link below.</span></span> <span data-ttu-id="705c4-120">Se non si dispone di Visual Studio 2013, è ancora stato installato, si verrà installato dal collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-120">If you don't have Visual Studio 2013 installed yet, it will be installed by hello link.</span></span> <span data-ttu-id="705c4-121">Per completare questa esercitazione, è necessario disporre di Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="705c4-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="705c4-122">[Azure SDK per Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="705c4-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="705c4-123">Nella finestra di installazione guidata piattaforma Web hello, fare clic su **installare** e continuare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-123">In hello Web Platform Installer window, click **Install** and proceed with hello installation.</span></span>

<span data-ttu-id="705c4-124">Sarà inoltre necessario disporre di un emulatore del browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="705c4-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="705c4-125">Uno dei seguenti hello funzionerà:</span><span class="sxs-lookup"><span data-stu-id="705c4-125">Any of hello following will work:</span></span>

* <span data-ttu-id="705c4-126">Emulatore di browser disponibile negli [strumenti di sviluppo F12 di Internet Explorer 11][EmulatorIE11] (usato in tutte le schermate del browser per dispositivi mobili).</span><span class="sxs-lookup"><span data-stu-id="705c4-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="705c4-127">Dispone di set di impostazioni della stringa agente utente per Windows Phone 8, Windows Phone 7 e Apple iPad.</span><span class="sxs-lookup"><span data-stu-id="705c4-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="705c4-128">Emulatore di browser disponibile in [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="705c4-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="705c4-129">Sono disponibili set di impostazioni per diversi dispositivi Android, oltre che per Apple iPhone, Apple iPad e Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="705c4-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="705c4-130">Emula anche gli eventi tocco.</span><span class="sxs-lookup"><span data-stu-id="705c4-130">It also emulates touch events.</span></span>
* <span data-ttu-id="705c4-131">[Emulatore mobile di Opera][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="705c4-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="705c4-132">Progetti di Visual Studio c\# codice sorgente sono tooaccompany disponibili in questo argomento:</span><span class="sxs-lookup"><span data-stu-id="705c4-132">Visual Studio projects with C\# source code are available tooaccompany this topic:</span></span>

* <span data-ttu-id="705c4-133">[Download progetto iniziale][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="705c4-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="705c4-134">[Download progetto completato][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="705c4-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="705c4-135"><a name="bkmk_DeployStarterProject"></a>Distribuire l'app web di Azure di hello starter progetto tooan</span><span class="sxs-lookup"><span data-stu-id="705c4-135"><a name="bkmk_DeployStarterProject"></a>Deploy hello starter project tooan Azure web app</span></span>
1. <span data-ttu-id="705c4-136">Scarica un'applicazione hello conferenza listato [progetto iniziale][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="705c4-136">Download hello conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="705c4-137">Quindi in Esplora risorse, fare clic sul file con estensione ZIP scaricato hello e scegliere *proprietà*.</span><span class="sxs-lookup"><span data-stu-id="705c4-137">Then in Windows Explorer, right-click hello downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="705c4-138">In hello **proprietà** finestra di dialogo scegliere hello **Unblock** pulsante.</span><span class="sxs-lookup"><span data-stu-id="705c4-138">In hello **Properties** dialog box, choose hello **Unblock** button.</span></span> <span data-ttu-id="705c4-139">(Lo sblocco di un avviso di sicurezza che si verifica quando si tenta di toouse impedisce un *zip* file scaricato dal web hello.)</span><span class="sxs-lookup"><span data-stu-id="705c4-139">(Unblocking prevents a security warning that occurs when you try toouse a *.zip* file that you've downloaded from hello web.)</span></span>
4. <span data-ttu-id="705c4-140">Fare clic sul file ZIP hello e selezionare **Estrai tutto** per decomprimere file hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-140">Right-click hello ZIP file and select **Extract All** to unzip hello file.</span></span> 
5. <span data-ttu-id="705c4-141">In Visual Studio, aprire hello *C#\Mvc5Mobile.sln* file.</span><span class="sxs-lookup"><span data-stu-id="705c4-141">In Visual Studio, open hello *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="705c4-142">In Esplora soluzioni, fare clic sul progetto hello e fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="705c4-142">In Solution Explorer, right-click hello project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="705c4-143">In Pubblica sito Web fare clic su **Servizio app di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="705c4-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="705c4-144">Se non è già stato effettuato l'accesso ad Azure, fare clic su **Aggiungi un account**.</span><span class="sxs-lookup"><span data-stu-id="705c4-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="705c4-145">Seguire hello richieste toolog all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="705c4-145">Follow hello prompts toolog into your Azure account.</span></span>
10. <span data-ttu-id="705c4-146">finestra di dialogo di servizio App Hello vengono visualizzati è firmato.</span><span class="sxs-lookup"><span data-stu-id="705c4-146">hello App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="705c4-147">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="705c4-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="705c4-148">In hello **nome dell'applicazione Web** , specificare un prefisso del nome applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="705c4-148">In hello **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="705c4-149">Il nome completo dell'app sarà *&lt;prefix>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="705c4-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="705c4-150">Selezionare inoltre un gruppo di risorse o specificarne uno nuovo in **Gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="705c4-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="705c4-151">Quindi, fare clic su **New** toocreate un nuovo piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="705c4-151">Then, click **New** toocreate a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="705c4-152">Configurare il nuovo piano di servizio App hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="705c4-152">Configure hello new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="705c4-153">Nella finestra di dialogo Crea servizio App hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="705c4-153">Back in hello Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="705c4-154">Dopo hello Azure le risorse vengono create, finestra di dialogo Pubblica sito Web hello verrà compilato con le impostazioni di hello per le nuove applicazioni.</span><span class="sxs-lookup"><span data-stu-id="705c4-154">After hello Azure resources are created, hello Publish Web dialog will be filled with hello settings for your new app.</span></span> <span data-ttu-id="705c4-155">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="705c4-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="705c4-156">Al termine della pubblicazione hello starter progetto toohello Azure web app, Visual Studio browser desktop hello apre l'app web in tempo reale di hello toodisplay.</span><span class="sxs-lookup"><span data-stu-id="705c4-156">Once Visual Studio finishes publishing hello starter project toohello Azure web app, hello desktop browser opens toodisplay hello live web app.</span></span>
15. <span data-ttu-id="705c4-157">Avviare l'emulatore di browser per dispositivi mobili, copiare l'URL di hello per un'applicazione hello conferenza (*<prefix>*. azurewebsites.net) in un emulatore hello e quindi fare clic sul pulsante superiore destro e selezionare **Sfoglia per tag**.</span><span class="sxs-lookup"><span data-stu-id="705c4-157">Start your mobile browser emulator, copy hello URL for hello conference application (*<prefix>*.azurewebsites.net) into hello emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="705c4-158">Se si utilizza Internet Explorer 11 come browser predefinito hello, è sufficiente tootype `F12`, quindi `Ctrl+8`e quindi modificare il profilo di browser hello troppo**Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="705c4-158">If you are using Internet Explorer 11 as hello default browser, you just need tootype `F12`, then `Ctrl+8`, and then change hello browser profile too**Windows Phone**.</span></span> <span data-ttu-id="705c4-159">L'immagine seguente mostra hello *AllTags* vista in modalità verticale (dalla scelta di **Sfoglia per tag**).</span><span class="sxs-lookup"><span data-stu-id="705c4-159">The image below shows hello *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="705c4-160">Mentre l'applicazione MVC 5 da Visual Studio è possibile eseguire il debug, è possibile pubblicare il tooAzure app web nuovamente tooverify hello web in tempo reale app direttamente dal browser per dispositivi mobili o un emulatore del browser.</span><span class="sxs-lookup"><span data-stu-id="705c4-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app tooAzure again tooverify hello live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="705c4-161">visualizzazione di Hello è molto leggibile in un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="705c4-161">hello display is very readable on a mobile device.</span></span> <span data-ttu-id="705c4-162">È possibile visualizzare anche già alcuni effetti hello visual applicato dal framework Bootstrap CSS hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-162">You can also already see some of hello visual effects applied by hello Bootstrap CSS framework.</span></span>
<span data-ttu-id="705c4-163">Fare clic su hello **ASP.NET** collegamento.</span><span class="sxs-lookup"><span data-stu-id="705c4-163">Click hello **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="705c4-164">Hello visualizzazione tag ASP.NET è montato zoom toohello schermata Bootstrap esegue automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="705c4-164">hello ASP.NET tag view is zoom-fitted toohello screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="705c4-165">Tuttavia, è possibile migliorare il browser per dispositivi mobili vista toobetter seme hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-165">However, you can improve this view toobetter suit hello mobile browser.</span></span> <span data-ttu-id="705c4-166">Ad esempio, hello **data** colonna è difficile da leggere.</span><span class="sxs-lookup"><span data-stu-id="705c4-166">For example, hello **Date** column is difficult to read.</span></span> <span data-ttu-id="705c4-167">Più avanti nell'esercitazione di hello si modificherà hello *AllTags* visualizzare toomake è mobile descrittivi.</span><span class="sxs-lookup"><span data-stu-id="705c4-167">Later in hello tutorial you'll change hello *AllTags* view toomake it mobile-friendly.</span></span>

## <span data-ttu-id="705c4-168"><a name="bkmk_bootstrap"></a> Framework CSS Bootstrap</span><span class="sxs-lookup"><span data-stu-id="705c4-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="705c4-169">Novità hello MVC 5 modello è il supporto incorporato di Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="705c4-169">New in hello MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="705c4-170">È già stato illustrato come è immediatamente possibile migliorare le visualizzazioni hello nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="705c4-170">You have already seen how it immediately improves hello different views in your application.</span></span> <span data-ttu-id="705c4-171">Ad esempio, la barra di spostamento hello nella parte superiore di hello è comprimibile automaticamente quando larghezza browser hello è minore.</span><span class="sxs-lookup"><span data-stu-id="705c4-171">For example, hello navigation bar at hello top is automatically collapsible when hello browser width is smaller.</span></span> <span data-ttu-id="705c4-172">Nel browser desktop hello, provare a ridimensionare una finestra del browser hello e vedere come barra di spostamento hello modifica dell'aspetto.</span><span class="sxs-lookup"><span data-stu-id="705c4-172">On hello desktop browser, try resizing hello browser window and see how hello navigation bar changes its look and feel.</span></span> <span data-ttu-id="705c4-173">Si tratta di progettazione web reattiva hello è incorporata nel programma di avvio.</span><span class="sxs-lookup"><span data-stu-id="705c4-173">This is hello responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="705c4-174">toosee come app Web hello apparirebbe senza Bootstrap, aprire *App\_avviare\\BundleConfig.cs* e impostare come commento le righe di hello contenenti *bootstrap.js* e *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="705c4-174">toosee how hello Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out hello lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="705c4-175">Hello codice seguente viene illustrato hello ultime due istruzioni di hello `RegisterBundles` metodo dopo la modifica di hello:</span><span class="sxs-lookup"><span data-stu-id="705c4-175">hello following code shows hello last two statements of hello `RegisterBundles` method after hello change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="705c4-176">Premere `Ctrl+F5` toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-176">Press `Ctrl+F5` toorun hello application.</span></span>

<span data-ttu-id="705c4-177">Osservare che se la barra di spostamento comprimibile hello è semplicemente un elenco non ordinato normale.</span><span class="sxs-lookup"><span data-stu-id="705c4-177">Observe that hello collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="705c4-178">Fare ancora clic su **Browse by tag**, quindi su **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="705c4-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="705c4-179">Nella visualizzazione dell'emulatore di dispositivi mobili hello, si noterà che non è più montati zoom toohello schermata, è necessario scorrere lateralmente in ordine toosee hello destra della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-179">In hello mobile emulator view, you can see now that it is no longer zoom-fitted toohello screen, and you must scroll sideways in order toosee hello right side of hello table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="705c4-180">Annullare le modifiche e aggiornare hello tooverify di browser per dispositivi mobili che è stato ripristinato visualizzazione mobile descrittivi hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-180">Undo your changes and refresh hello mobile browser tooverify that hello mobile-friendly display has been restored.</span></span>

<span data-ttu-id="705c4-181">Bootstrap non specifico tooASP.NET MVC 5, ed è possibile sfruttare queste funzionalità in qualsiasi applicazione web.</span><span class="sxs-lookup"><span data-stu-id="705c4-181">Bootstrap is not specific tooASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="705c4-182">Ora, tuttavia, Bootstrap è integrato nel modello di progetto ASP.NET MVC 5 per consentire all'applicazione Web MVC 5 di sfruttarne i vantaggi per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="705c4-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="705c4-183">Per ulteriori informazioni sull'avvio, visitare toothe [Bootstrap] [ BootstrapSite] sito.</span><span class="sxs-lookup"><span data-stu-id="705c4-183">For more information about Bootstrap, go toothe [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="705c4-184">Nella sezione successiva hello si noterà come le viste specifiche tooprovide browser mobile.</span><span class="sxs-lookup"><span data-stu-id="705c4-184">In hello next section you'll see how tooprovide mobile-browser specific views.</span></span>

## <span data-ttu-id="705c4-185"><a name="bkmk_overrideviews"></a>Eseguire l'override di viste di hello, layout e le visualizzazioni parziali</span><span class="sxs-lookup"><span data-stu-id="705c4-185"><a name="bkmk_overrideviews"></a> Override hello Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="705c4-186">È possibile eseguire l'override di una visualizzazione (inclusi i layout e le visualizzazioni parziali) per i browser per dispositivi mobili in generale, per un singolo browser per dispositivi mobili o per un qualsiasi browser specifico.</span><span class="sxs-lookup"><span data-stu-id="705c4-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="705c4-187">visualizzare uno specifico di dispositivi mobili tooprovide, è possibile copiare un file di visualizzazione e aggiungere *. Mobile* toohello nome del file.</span><span class="sxs-lookup"><span data-stu-id="705c4-187">tooprovide a mobile-specific view, you can copy a view file and add *.Mobile* toohello file name.</span></span> <span data-ttu-id="705c4-188">Ad esempio, toocreate mobili *indice* vista, è possibile copiare *viste\\Home\\cshtml* a *viste\\Home\\ Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="705c4-188">For example, toocreate a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="705c4-189">In questa sezione verrà illustrato come creare un file di layout specifico per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="705c4-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="705c4-190">toostart, copia *viste\\Shared\\\_cshtml* a *viste\\Shared\\\_Layout.Mobile.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="705c4-190">toostart, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="705c4-191">Aprire  *\_Layout.Mobile.cshtml* e modificare il titolo di hello da **MVC5 applicazione** troppo**MVC5 applicazione (Mobile)**.</span><span class="sxs-lookup"><span data-stu-id="705c4-191">Open *\_Layout.Mobile.cshtml* and change hello title from **MVC5 Application** too**MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="705c4-192">In ogni `Html.ActionLink` chiamata per la barra di spostamento hello, rimuovere "Sfoglia per" in ogni collegamento *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="705c4-192">In each `Html.ActionLink` call for hello navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="705c4-193">Hello codice seguente viene illustrato hello completato `<ul class="nav navbar-nav">` tag del file di layout per dispositivi mobili hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-193">hello following code shows hello completed `<ul class="nav navbar-nav">` tag of hello mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="705c4-194">Hello copia *viste\\Home\\AllTags.cshtml* file *viste\\Home\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="705c4-194">Copy hello *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="705c4-195">Aprire il file nuovo hello e modificare il `<h2>` elemento da "Tags" troppo "tag (M)":</span><span class="sxs-lookup"><span data-stu-id="705c4-195">Open hello new file and change the `<h2>` element from "Tags" too"Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="705c4-196">Sfoglia toohello tag pagina utilizzando un browser per desktop e l'utilizzo dell'emulatore di browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="705c4-196">Browse toohello tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="705c4-197">emulatore di browser per dispositivi mobili Hello Mostra hello due modifiche apportate (hello titolo da  *\_Layout.Mobile.cshtml* e titolo hello da *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="705c4-197">hello mobile browser emulator shows hello two changes you made (hello title from *\_Layout.Mobile.cshtml* and hello title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="705c4-198">Al contrario, non è cambiato display desktop hello (con titoli da  *\_cshtml* e *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="705c4-198">In contrast, hello desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="705c4-199"><a name="bkmk_browserviews"></a> Creazione di visualizzazioni specifiche del browser</span><span class="sxs-lookup"><span data-stu-id="705c4-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="705c4-200">Inoltre visualizzazioni specifiche di desktop e toomobile, è possibile creare viste per un determinato browser.</span><span class="sxs-lookup"><span data-stu-id="705c4-200">In addition toomobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="705c4-201">Ad esempio, è possibile creare viste che sono specifici per iPhone hello o browser Android hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-201">For example, you can create views that are specifically for hello iPhone or hello Android browser.</span></span> <span data-ttu-id="705c4-202">In questa sezione si creerà un layout per browser iPhone hello e una versione di iPhone di hello *AllTags* visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="705c4-202">In this section, you'll create a layout for hello iPhone browser and an iPhone version of hello *AllTags* view.</span></span>

<span data-ttu-id="705c4-203">Aprire hello *Global. asax* file e aggiungere hello seguendo il toohello a fondo codice il `Application_Start` metodo.</span><span class="sxs-lookup"><span data-stu-id="705c4-203">Open hello *Global.asax* file and add hello following code toohello bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="705c4-204">Questo codice definisce una nuova modalità di visualizzazione denominata "iPhone" che verrà associata a ciascuna richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="705c4-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="705c4-205">Se la richiesta in ingresso hello soddisfa la condizione che è stato definito (vale a dire, se l'agente utente hello contiene la stringa hello "iPhone"), il cui nome contiene il suffisso "iPhone" viste verranno ricercati ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="705c4-205">If hello incoming request matches the condition you defined (that is, if hello user agent contains hello string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="705c4-206">Quando aggiunta specifiche del browser per dispositivi mobili le modalità di visualizzazione, ad esempio per iPhone e Android, è troppo che primo argomento hello tooset`0` toomake (inserimento all'inizio di hello dell'elenco di hello) assicurarsi che la modalità specifiche del browser hello ha la precedenza sul modello mobile hello (*. Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="705c4-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure tooset hello first argument too`0` (insert at hello top of hello list) toomake sure that hello browser-specific mode takes precedence over hello mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="705c4-207">Se hello mobili modello all'inizio di hello dell'elenco di hello al contrario, verrà selezionato tramite la modalità di visualizzazione desiderata (hello prima corrispondenza wins e modello mobile hello corrisponde a tutti i browser per dispositivi mobili).</span><span class="sxs-lookup"><span data-stu-id="705c4-207">If hello mobile template is at hello top of hello list instead, it will be selected over your intended display mode (hello first match wins, and hello mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="705c4-208">Nel codice hello, fare doppio clic su `DefaultDisplayMode`, scegliere **risolvere**, quindi scegliere `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="705c4-208">In hello code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="705c4-209">Aggiunge un riferimento toothe `System.Web.WebPages` spazio dei nomi, dove il `DisplayModeProvider` e `DefaultDisplayMode` tipi sono definiti.</span><span class="sxs-lookup"><span data-stu-id="705c4-209">This adds a reference toothe `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="705c4-210">In alternativa, è possibile aggiungere solo manualmente hello seguente riga toothe `using` sezione del file hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-210">Alternatively, you can just manually add hello following line toothe `using` section of hello file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="705c4-211">Salvare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-211">Save hello changes.</span></span> <span data-ttu-id="705c4-212">Copiare il file *Views\\Shared\\\_Layout.Mobile.cshtml* in *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="705c4-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="705c4-213">Aprire il file nuovo hello e quindi modificare il titolo di hello da `MVC5 Application (Mobile)` a `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="705c4-213">Open hello new file and then change hello title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="705c4-214">Hello copia *viste\\Home\\AllTags.Mobile.cshtml* file *viste\\Home\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="705c4-214">Copy hello *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="705c4-215">Nel nuovo file hello, modificare hello `<h2>` tag dell'elemento da "tag (M)" troppo"(iPhone)".</span><span class="sxs-lookup"><span data-stu-id="705c4-215">In hello new file, change hello `<h2>` element from "Tags (M)" too"Tags (iPhone)".</span></span>

<span data-ttu-id="705c4-216">Eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-216">Run hello application.</span></span> <span data-ttu-id="705c4-217">Eseguire un emulatore del browser per dispositivi mobili, assicurarsi che l'agente utente è stato impostato troppo "iPhone" e passare toohello *AllTags* visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="705c4-217">Run a mobile browser emulator, make sure its user agent is set too"iPhone", and browse toohello *AllTags* view.</span></span> <span data-ttu-id="705c4-218">Se si utilizza l'emulatore hello negli strumenti di sviluppo F12 di Internet Explorer 11, configurare seguente toohello emulazione:</span><span class="sxs-lookup"><span data-stu-id="705c4-218">If you are using hello emulator in Internet Explorer 11 F12 developer tools, configure emulation toohello following:</span></span>

* <span data-ttu-id="705c4-219">Profilo del browser = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="705c4-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="705c4-220">Stringa agente utente = **Custom**</span><span class="sxs-lookup"><span data-stu-id="705c4-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="705c4-221">Stringa personalizzata = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="705c4-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="705c4-222">Hello schermata riportata di seguito viene illustrato hello *AllTags* rendering della visualizzazione nell'emulatore negli strumenti di sviluppo F12 di Internet Explorer 11 con stringa agente utente personalizzata di hello (si tratta di una stringa agente utente di iPhone 5 C).</span><span class="sxs-lookup"><span data-stu-id="705c4-222">hello following screenshot shows hello *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with hello custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="705c4-223">Nel browser per dispositivi mobili hello, selezionare hello **altoparlanti** collegamento.</span><span class="sxs-lookup"><span data-stu-id="705c4-223">In hello mobile browser, select hello **Speakers** link.</span></span> <span data-ttu-id="705c4-224">Poiché non vi è una vista mobile (*AllSpeakers.Mobile.cshtml*), visualizzare altoparlanti predefinito hello (*AllSpeakers.cshtml*) viene eseguito il rendering visualizzazione layout mobili hello ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="705c4-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), hello default speakers view (*AllSpeakers.cshtml*) is rendered using hello mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="705c4-225">Come illustrato di seguito, il titolo di hello **MVC5 applicazione (Mobile)** è definito in  *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="705c4-225">As shown below, hello title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="705c4-226">A livello globale, è possibile disabilitare una visualizzazione (non mobile) predefinito per il rendering all'interno di un layout per dispositivi mobili impostando `RequireConsistentDisplayMode` a `true` in hello *viste\\\_ViewStart.cshtml* file, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="705c4-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in hello *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="705c4-227">Quando `RequireConsistentDisplayMode` è troppo`true`, layout mobili hello (*\_Layout.Mobile.cshtml*) viene utilizzato solo per le visualizzazioni mobili (ad esempio quando il file della visualizzazione è formato hello  ***ViewName** . Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="705c4-227">When `RequireConsistentDisplayMode` is set too`true`, hello mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of hello form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="705c4-228">Potrebbe essere necessario tooset `RequireConsistentDisplayMode` troppo`true` se il layout per dispositivi mobili non funziona bene con le visualizzazioni non mobili.</span><span class="sxs-lookup"><span data-stu-id="705c4-228">You might want tooset `RequireConsistentDisplayMode` too`true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="705c4-229">Hello schermata seguente viene illustrato come hello *altoparlanti* pagina esegue il rendering quando `RequireConsistentDisplayMode` è troppo`true` (senza stringa hello "(Mobile)" nella navigazione barra nella parte superiore di hello hello).</span><span class="sxs-lookup"><span data-stu-id="705c4-229">hello screenshot below shows how hello *Speakers* page renders when `RequireConsistentDisplayMode` is set too`true` (without hello string "(Mobile)" in hello navigational bar at hello top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="705c4-230">È possibile disabilitare la modalità di visualizzazione coerente in una visualizzazione specifica impostando `RequireConsistentDisplayMode` troppo`false` nel file di visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` too`false` in hello view file.</span></span> <span data-ttu-id="705c4-231">Il markup seguente in hello *viste\\Home\\AllSpeakers.cshtml* file imposta `RequireConsistentDisplayMode` troppo`false`:</span><span class="sxs-lookup"><span data-stu-id="705c4-231">The following markup in hello *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` too`false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="705c4-232">In questa sezione abbiamo visto come toocreate come toocreate layout e le visualizzazioni per i dispositivi specifici, ad esempio hello iPhone e le visualizzazioni e layout per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="705c4-232">In this section we've seen how toocreate mobile layouts and views and how toocreate layouts and views for specific devices such as hello iPhone.</span></span>
<span data-ttu-id="705c4-233">Tuttavia, hello principale sfruttare framework Bootstrap CSS hello è il layout reattivo, il che significa che un singolo foglio di stile può essere applicata ai desktop, telefono e tablet browser toocreate un aspetto coerente.</span><span class="sxs-lookup"><span data-stu-id="705c4-233">However, hello main advantage of hello Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers toocreate a consistent look and feel.</span></span> <span data-ttu-id="705c4-234">Nella sezione successiva hello verrà visualizzato come tooleverage Bootstrap toocreate mobile-friendly viste.</span><span class="sxs-lookup"><span data-stu-id="705c4-234">In hello next section you'll see how tooleverage Bootstrap toocreate mobile-friendly views.</span></span>

## <span data-ttu-id="705c4-235"><a name="bkmk_Improvespeakerslist"></a>Migliorare hello altoparlanti elenco</span><span class="sxs-lookup"><span data-stu-id="705c4-235"><a name="bkmk_Improvespeakerslist"></a> Improve hello Speakers List</span></span>
<span data-ttu-id="705c4-236">Come già visto hello *altoparlanti* visualizzazione è leggibile, ma hello collegamenti sono piccoli e sono di difficile tootap su un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="705c4-236">As you just saw, hello *Speakers* view is readable, but hello links are small and are difficult tootap on a mobile device.</span></span> <span data-ttu-id="705c4-237">In questa sezione si renderanno hello *AllSpeakers* mobile-friendly, che vengono visualizzati i collegamenti di grandi dimensioni, facile tap e contiene un tooquickly casella di ricerca trovare altoparlanti.</span><span class="sxs-lookup"><span data-stu-id="705c4-237">In this section, you'll make hello *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box tooquickly find speakers.</span></span>

<span data-ttu-id="705c4-238">È possibile utilizzare hello Bootstrap [gruppo dell'elenco collegato] [ linked list group] stili per migliorare hello *altoparlanti* visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="705c4-238">You can use hello Bootstrap [linked list group][linked list group] styling to improve hello *Speakers* view.</span></span> <span data-ttu-id="705c4-239">In *viste\\Home\\AllSpeakers.cshtml*, sostituire il contenuto di hello del file Razor hello con codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="705c4-239">In *Views\\Home\\AllSpeakers.cshtml*, replace hello contents of hello Razor file with hello code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="705c4-240">Hello `class="list-group"` attributo hello `<div>` tag si applica lo stile di elenco Bootstrap e hello `class="input-group-item"` attributo si applica tooeach collegamento lo stile di elemento di elenco Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="705c4-240">hello `class="list-group"` attribute in hello `<div>` tag applies the Bootstrap list styling, and hello `class="input-group-item"` attribute applies Bootstrap list item styling tooeach link.</span></span>

<span data-ttu-id="705c4-241">Aggiornamento del browser per dispositivi mobili hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-241">Refresh hello mobile browser.</span></span> <span data-ttu-id="705c4-242">Hello aggiornamento vista ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="705c4-242">hello updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="705c4-243">Hello Bootstrap [gruppo dell'elenco collegato] [ linked list group] stile rende hello intera casella per ciascun collegamento selezionabile, ovvero una quantità migliore esperienza utente.</span><span class="sxs-lookup"><span data-stu-id="705c4-243">hello Bootstrap [linked list group][linked list group] styling makes hello entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="705c4-244">Passare a vista desktop toothe e osservare hello un aspetto coerente.</span><span class="sxs-lookup"><span data-stu-id="705c4-244">Switch toothe desktop view and observe hello consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="705c4-245">Anche se è stata migliorata del browser per dispositivi mobili hello risulta difficile spostarsi lungo elenco di hello degli altoparlanti.</span><span class="sxs-lookup"><span data-stu-id="705c4-245">Although hello mobile browser view has improved, it's difficult to navigate hello long list of speakers.</span></span> <span data-ttu-id="705c4-246">Bootstrap non fornisce un filtro di ricerca pronto all'uso, ma è possibile aggiungere questa funzionalità con poche righe di codice.</span><span class="sxs-lookup"><span data-stu-id="705c4-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="705c4-247">Verrà innanzitutto aggiungere una visualizzazione toohello casella di ricerca, quindi collegare il codice JavaScript per la funzione di filtro hello hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-247">You will first add a search box toohello view, then hook up with hello JavaScript code for hello filter function.</span></span> <span data-ttu-id="705c4-248">In *viste\\Home\\AllSpeakers.cshtml*, aggiungere un \<modulo\> tag appena hello \<h2\> tag, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="705c4-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after hello \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="705c4-249">Si noti che hello `<form>` e `<input>` tag entrambi hanno toothem Bootstrap stili applicati hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-249">Notice that hello `<form>` and `<input>` tags both have hello Bootstrap styles applied toothem.</span></span> <span data-ttu-id="705c4-250">Hello `<span>` elemento aggiunge un Bootstrap [glyphicon] [ glyphicon] toothe casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="705c4-250">hello `<span>` element adds a Bootstrap [glyphicon][glyphicon] toothe search box.</span></span>

<span data-ttu-id="705c4-251">In hello *script* cartella, aggiungere un file JavaScript denominato *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="705c4-251">In hello *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="705c4-252">Aprire il file hello e incollare hello seguente codice al suo interno:</span><span class="sxs-lookup"><span data-stu-id="705c4-252">Open hello file and paste hello following code into it:</span></span>

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="705c4-253">È inoltre necessario tooinclude filter.js nei bundle registrati.</span><span class="sxs-lookup"><span data-stu-id="705c4-253">You also need tooinclude filter.js in your registered bundles.</span></span> <span data-ttu-id="705c4-254">Aprire *App\_avviare\\BundleConfig.cs* e modificare i pacchetti prima di hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-254">Open *App\_Start\\BundleConfig.cs* and change hello first bundles.</span></span> <span data-ttu-id="705c4-255">Modificare il primo `bundles.Add` istruzione (per hello **jquery** bundle) tooinclude *script\\filter.js*, come segue:</span><span class="sxs-lookup"><span data-stu-id="705c4-255">Change the first `bundles.Add` statement (for hello **jquery** bundle) tooinclude *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="705c4-256">Hello **jquery** bundle è già stato eseguito per impostazione predefinita hello  *\_Layout* visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="705c4-256">hello **jquery** bundle is already rendered by hello default *\_Layout* view.</span></span> <span data-ttu-id="705c4-257">In un secondo momento, è possibile utilizzare hello JavaScript stesso codice tooapply visualizzazioni elenco tooother funzionalità filtro.</span><span class="sxs-lookup"><span data-stu-id="705c4-257">Later, you can utilize hello same JavaScript code tooapply the filter functionality tooother list views.</span></span>

<span data-ttu-id="705c4-258">Aggiornamento del browser per dispositivi mobili hello e passare toohello *AllSpeakers* visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="705c4-258">Refresh hello mobile browser and go toohello *AllSpeakers* view.</span></span> <span data-ttu-id="705c4-259">Nella casella di ricerca digitare "sc".</span><span class="sxs-lookup"><span data-stu-id="705c4-259">In the search box, type "sc".</span></span> <span data-ttu-id="705c4-260">elenco degli altoparlanti Hello ora deve essere filtrato in base tooyour stringa di ricerca.</span><span class="sxs-lookup"><span data-stu-id="705c4-260">hello speakers list should now be filtered according tooyour search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="705c4-261"><a name="bkmk_improvetags"></a>Migliorare hello elenco tag</span><span class="sxs-lookup"><span data-stu-id="705c4-261"><a name="bkmk_improvetags"></a> Improve hello Tags List</span></span>
<span data-ttu-id="705c4-262">Ad esempio hello *altoparlanti* visualizzare, hello *tag* visualizzazione è leggibile, ma i collegamenti di hello sono di piccole dimensioni e difficili tootap su un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="705c4-262">Like hello *Speakers* view, hello *Tags* view is readable, but hello links are small and difficult tootap on a mobile device.</span></span> <span data-ttu-id="705c4-263">È possibile correggere hello *tag* visualizzazione hello stesso modo risolvere hello *altoparlanti* visualizzare, se si utilizzano le modifiche al codice hello descritti in precedenza, ma con i seguenti hello `Html.ActionLink` la sintassi del metodo in  *Viste\\Home\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="705c4-263">You can fix hello *Tags* view hello same way you fix hello *Speakers* view, if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="705c4-264">Hello aggiornato ha un aspetto browser desktop come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="705c4-264">hello refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="705c4-265">E hello aggiornato ha un aspetto browser per dispositivi mobili, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="705c4-265">And hello refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="705c4-266">Se si nota la formattazione elenco hello originale è ancora disponibile in hello browser per dispositivi mobili e chiedersi quali stile Bootstrap nice tooyour verificato anomalo, si tratta di un elemento le viste precedenti azione toocreate mobili specifico.</span><span class="sxs-lookup"><span data-stu-id="705c4-266">If you notice that hello original list formatting is still there in hello mobile browser and wonder what happened tooyour nice Bootstrap styling, this is an artifact of your earlier action toocreate mobile specific views.</span></span> <span data-ttu-id="705c4-267">Tuttavia, ora che si utilizza hello Bootstrap CSS framework toocreate una progettazione reattiva web, andare a capo e rimuovere queste visualizzazioni specifiche di dispositivi mobili e viste di hello layout specifici dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="705c4-267">However, now that you are using hello Bootstrap CSS framework toocreate a responsive web design, go head and remove these mobile-specific views and hello mobile-specific layout views.</span></span> <span data-ttu-id="705c4-268">Dopo aver eseguito questa operazione, i browser per dispositivi mobili aggiornati hello visualizzerà lo stile di Bootstrap hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-268">Once you have done so, hello refreshed mobile browser will show hello Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="705c4-269"><a name="bkmk_improvedates"></a>Migliorare hello elenco date</span><span class="sxs-lookup"><span data-stu-id="705c4-269"><a name="bkmk_improvedates"></a> Improve hello Dates List</span></span>
<span data-ttu-id="705c4-270">È possibile migliorare hello *date* visualizzare come migliori hello *altoparlanti* e *tag* viste se si utilizza hello modifiche al codice descritti in precedenza, ma con hello seguente `Html.ActionLink` la sintassi del metodo in *viste\\Home\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="705c4-270">You can improve hello *Dates* view like you improved hello *Speakers* and *Tags* views if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="705c4-271">Si otterrà una visualizzazione del browser per dispositivi mobili aggiornato simile a quella riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="705c4-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="705c4-272">È possibile migliorare ulteriormente hello *date* Visualizza per organizzare i valori di data e ora hello per Data.</span><span class="sxs-lookup"><span data-stu-id="705c4-272">You can further improve hello *Dates* view by organizing hello date-time values by date.</span></span> <span data-ttu-id="705c4-273">Questa operazione può essere eseguita con hello Bootstrap [pannelli] [ panels] stile.</span><span class="sxs-lookup"><span data-stu-id="705c4-273">This can be done with hello Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="705c4-274">Sostituire il contenuto di hello di hello *viste\\Home\\AllDates.cshtml* file con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="705c4-274">Replace hello contents of hello *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="705c4-275">Questo codice crea un oggetto separato `<div class="panel panel-primary">` tag per ogni data distinct nell'elenco di hello e utilizza hello [gruppo dell'elenco collegato] [ linked list group] per la rispettiva collega come prima.</span><span class="sxs-lookup"><span data-stu-id="705c4-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in hello list, and uses hello [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="705c4-276">Di seguito è riportato il browser per dispositivi mobili hello aspetto quando si esegue questo codice:</span><span class="sxs-lookup"><span data-stu-id="705c4-276">Here's what hello mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="705c4-277">Browser desktop toohello commutatore.</span><span class="sxs-lookup"><span data-stu-id="705c4-277">Switch toohello desktop browser.</span></span> <span data-ttu-id="705c4-278">Nuovamente, nota hello coerente.</span><span class="sxs-lookup"><span data-stu-id="705c4-278">Again, note hello consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="705c4-279"><a name="bkmk_improvesessionstable"></a>Migliorare la visualizzazione SessionsTable hello</span><span class="sxs-lookup"><span data-stu-id="705c4-279"><a name="bkmk_improvesessionstable"></a> Improve hello SessionsTable View</span></span>
<span data-ttu-id="705c4-280">In questa sezione si renderanno hello *SessionsTable* visualizzare altre mobile-friendly.</span><span class="sxs-lookup"><span data-stu-id="705c4-280">In this section, you'll make hello *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="705c4-281">Questa modifica è modifiche precedenti hello più estese.</span><span class="sxs-lookup"><span data-stu-id="705c4-281">This change is more extensive hello previous changes.</span></span>

<span data-ttu-id="705c4-282">Nel browser per dispositivi mobili hello, toccare hello **Tag** pulsante, quindi immettere `asp` nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="705c4-282">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="705c4-283">Toccare hello **ASP.NET** collegamento.</span><span class="sxs-lookup"><span data-stu-id="705c4-283">Tap hello **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="705c4-284">Come si può notare, visualizzazione hello viene formattata come una tabella, ovvero toobe progettato attualmente visualizzati in browser desktop hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-284">As you can see, hello display is formatted as a table, which is currently designed toobe viewed in hello desktop browser.</span></span> <span data-ttu-id="705c4-285">Tuttavia, è un po' difficile tooread in un browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="705c4-285">However, it's a little bit difficult tooread on a mobile browser.</span></span> <span data-ttu-id="705c4-286">toofix, aprire *viste\\Home\\SessionsTable.cshtml* quindi sostituire il contenuto di hello del file con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="705c4-286">toofix this, open *Views\\Home\\SessionsTable.cshtml* and then replace hello contents of the file with hello following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="705c4-287">codice Hello esegue 3 operazioni:</span><span class="sxs-lookup"><span data-stu-id="705c4-287">hello code does 3 things:</span></span>

* <span data-ttu-id="705c4-288">Usa hello Bootstrap [gruppo personalizzato di elenco collegato] [ custom linked list group] tooformat hello in verticale, le informazioni sulla sessione in modo che tutte queste informazioni sono leggibile in un browser per dispositivi mobili (utilizzando le classi, ad esempio elenco-gruppo-elemento-text)</span><span class="sxs-lookup"><span data-stu-id="705c4-288">uses hello Bootstrap [custom linked list group][custom linked list group] tooformat hello session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="705c4-289">si applica hello [sistema griglia] [ grid system] toothe layout, pertanto tale sessione hello elementi flusso orizzontalmente in browser desktop hello e verticalmente in browser per dispositivi mobili di hello (mediante la classe di hello col-md-4)</span><span class="sxs-lookup"><span data-stu-id="705c4-289">applies hello [grid system][grid system] toothe layout, so that hello session items flow horizontally in hello desktop browser and vertically in hello mobile browser (using hello col-md-4 class)</span></span>
* <span data-ttu-id="705c4-290">Usa hello [utilità reattiva] [ responsive utilities] per nascondere i tag di sessione hello quando viene visualizzato nel browser per dispositivi mobili di hello (mediante la classe nascosto-xs hello)</span><span class="sxs-lookup"><span data-stu-id="705c4-290">uses hello [responsive utilities][responsive utilities] to hide hello session tags when viewed in hello mobile browser (using hello hidden-xs class)</span></span>

<span data-ttu-id="705c4-291">È anche possibile toccare una titolo collegamento toogo toohello rispettivi della sessione.</span><span class="sxs-lookup"><span data-stu-id="705c4-291">You can also tap a title link toogo toohello respective session.</span></span> <span data-ttu-id="705c4-292">immagine di Hello seguente riflette le modifiche al codice hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-292">hello image below reflects hello code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="705c4-293">sistema di griglia Bootstrap Hello applicati automaticamente dispone le sessioni in senso verticale in browser per dispositivi mobili hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-293">hello Bootstrap grid system that you applied automatically arranges the sessions vertically in hello mobile browser.</span></span> <span data-ttu-id="705c4-294">Si noti inoltre che non vengono visualizzati i tag hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-294">Also, notice that hello tags are not shown.</span></span> <span data-ttu-id="705c4-295">Browser desktop toohello commutatore.</span><span class="sxs-lookup"><span data-stu-id="705c4-295">Switch toohello desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="705c4-296">Nel browser desktop hello, si noti che hello vengono ora visualizzati.</span><span class="sxs-lookup"><span data-stu-id="705c4-296">In hello desktop browser, notice that hello tags are now displayed.</span></span> <span data-ttu-id="705c4-297">Inoltre, si noterà che il sistema di griglia Bootstrap hello che è applicato dispone gli elementi di sessione hello in due colonne.</span><span class="sxs-lookup"><span data-stu-id="705c4-297">Also, you can see that hello Bootstrap grid system you applied arranges hello session items in two columns.</span></span> <span data-ttu-id="705c4-298">Se si ingrandisce il browser, si noterà che disposizione hello cambia toothree colonne.</span><span class="sxs-lookup"><span data-stu-id="705c4-298">If you enlarge the browser, you will see that hello arrangement changes toothree columns.</span></span>

## <span data-ttu-id="705c4-299"><a name="bkmk_improvesessionbycode"></a>Migliorare la visualizzazione SessionByCode hello</span><span class="sxs-lookup"><span data-stu-id="705c4-299"><a name="bkmk_improvesessionbycode"></a> Improve hello SessionByCode View</span></span>
<span data-ttu-id="705c4-300">Infine, sarà possibile risolvere hello *SessionByCode* visualizzare toomake è mobile descrittivi.</span><span class="sxs-lookup"><span data-stu-id="705c4-300">Finally, you'll fix hello *SessionByCode* view toomake it mobile-friendly.</span></span>

<span data-ttu-id="705c4-301">Nel browser per dispositivi mobili hello, toccare hello **Tag** pulsante, quindi immettere `asp` nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="705c4-301">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="705c4-302">Toccare hello **ASP.NET** collegamento.</span><span class="sxs-lookup"><span data-stu-id="705c4-302">Tap hello **ASP.NET** link.</span></span> <span data-ttu-id="705c4-303">Vengono visualizzate le sessioni per il tag ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-303">Sessions for hello ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="705c4-304">Scegliere hello **la creazione di un'applicazione a pagina singola con ASP.NET e AngularJS** collegamento.</span><span class="sxs-lookup"><span data-stu-id="705c4-304">Choose hello **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="705c4-305">visualizzazione desktop predefinita di Hello è correttamente, ma è possibile migliorare aspetto hello facilmente con alcuni componenti GUI di Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="705c4-305">hello default desktop view is fine, but you can improve hello look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="705c4-306">Aprire *viste\\Home\\SessionByCode.cshtml* e sostituire il contenuto di hello con hello markup seguente:</span><span class="sxs-lookup"><span data-stu-id="705c4-306">Open *Views\\Home\\SessionByCode.cshtml* and replace hello contents with hello following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="705c4-307">Nuovo markup Hello Usa stile di visualizzazione di tooimprove hello mobili i pannelli Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="705c4-307">hello new markup uses Bootstrap panels styling tooimprove hello mobile view.</span></span> 

<span data-ttu-id="705c4-308">Aggiornamento del browser per dispositivi mobili hello.</span><span class="sxs-lookup"><span data-stu-id="705c4-308">Refresh hello mobile browser.</span></span> <span data-ttu-id="705c4-309">Hello immagine seguente riflette le modifiche di codice hello appena apportate:</span><span class="sxs-lookup"><span data-stu-id="705c4-309">hello following image reflects hello code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="705c4-310">Riepilogo e revisione</span><span class="sxs-lookup"><span data-stu-id="705c4-310">Wrap Up and Review</span></span>
<span data-ttu-id="705c4-311">In questa esercitazione è stato illustrato come le applicazioni Web ASP.NET MVC 5 toodevelop mobile-friendly toouse.</span><span class="sxs-lookup"><span data-stu-id="705c4-311">This tutorial has shown you how toouse ASP.NET MVC 5 toodevelop mobile-friendly Web applications.</span></span> <span data-ttu-id="705c4-312">incluse le seguenti:</span><span class="sxs-lookup"><span data-stu-id="705c4-312">These include:</span></span>

* <span data-ttu-id="705c4-313">Distribuire un tooan applicazione ASP.NET MVC 5 App del servizio web app</span><span class="sxs-lookup"><span data-stu-id="705c4-313">Deploy an ASP.NET MVC 5 application tooan App Service web app</span></span>
* <span data-ttu-id="705c4-314">Utilizzare layout web reattiva toocreate Bootstrap nell'applicazione MVC 5</span><span class="sxs-lookup"><span data-stu-id="705c4-314">Use Bootstrap toocreate responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="705c4-315">Override di layout, visualizzazioni e visualizzazioni parziali, sia in modo globale sia per una singola visualizzazione</span><span class="sxs-lookup"><span data-stu-id="705c4-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="705c4-316">Controllo del layout ed esecuzione di un override parziale usando la proprietà `RequireConsistentDisplayMode`</span><span class="sxs-lookup"><span data-stu-id="705c4-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="705c4-317">Creazione di viste che utilizzano browser specifico, ad esempio browser iPhone hello</span><span class="sxs-lookup"><span data-stu-id="705c4-317">Create views that target specific browsers, such as hello iPhone browser</span></span>
* <span data-ttu-id="705c4-318">Applicazione di stili Bootstrap in codice Razor</span><span class="sxs-lookup"><span data-stu-id="705c4-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="705c4-319">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="705c4-319">See Also</span></span>
* [<span data-ttu-id="705c4-320">9 principi di base della progettazione Web reattiva</span><span class="sxs-lookup"><span data-stu-id="705c4-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="705c4-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="705c4-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="705c4-322">[Blog ufficiale di Bootstrap][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="705c4-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="705c4-323">[Tutorial Twitter Bootstrap su Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="705c4-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="705c4-324">[Hello palestra per Bootstrap][hello Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="705c4-324">[hello Bootstrap Playground][hello Bootstrap Playground]</span></span>
* <span data-ttu-id="705c4-325">[Procedure consigliate per applicazioni Web W3C per dispositivi mobili][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="705c4-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="705c4-326">[Candidate Recommendation W3C per query sui supporti][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="705c4-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="705c4-327">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="705c4-327">What's changed</span></span>
* <span data-ttu-id="705c4-328">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="705c4-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

