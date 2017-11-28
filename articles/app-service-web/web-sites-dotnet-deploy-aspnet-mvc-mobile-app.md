---
title: Distribuzione di un'app Web ASP.NET MVC 5 per dispositivi mobili nel servizio app di Azure
description: "Un'esercitazione che illustra come distribuire un'app Web in App Service di Azure usando le funzionalità dei dispositivi mobili nell'applicazione Web ASP.NET MVC 5."
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
ms.openlocfilehash: c98e9b485c52a82e5be5c0f6b0b67912d1e890b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="8e0cd-103">Distribuzione di un'app Web ASP.NET MVC 5 per dispositivi mobili nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="8e0cd-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="8e0cd-104">In questa esercitazione verranno illustrate le nozioni di base per lo sviluppo di un'app Web ASP.NET MVC 5 per dispositivi mobili e la distribuzione di tale app nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-104">This tutorial will teach you the basics of how to build an ASP.NET MVC 5 web app that is mobile-friendly and deploy it to Azure App Service.</span></span> <span data-ttu-id="8e0cd-105">Ai fini di questa esercitazione, è necessario disporre di [Visual Studio Express 2013 per il Web][Visual Studio Express 2013] o della versione professionale di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or the professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="8e0cd-106">È possibile utilizzare [Visual Studio 2015] , ma le schermate saranno diverse ed è necessario utilizzare i modelli ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-106">You can use [Visual Studio 2015] but the screen shots will be different and you must use the ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="8e0cd-107">Scopo dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="8e0cd-107">What You'll Build</span></span>
<span data-ttu-id="8e0cd-108">Ai fini di questa esercitazione, si aggiungeranno funzionalità mobili alla semplice applicazione di elenco conferenze fornita nel [progetto iniziale][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="8e0cd-108">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project][StarterProject].</span></span> <span data-ttu-id="8e0cd-109">La schermata seguente mostra le sessioni ASP.NET nell'applicazione completata, così come vengono visualizzate nell'emulatore di browser negli strumenti di sviluppo F12 di Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-109">The following screenshot shows the ASP.NET sessions in the completed application, as seen in the browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="8e0cd-110">È possibile usare gli strumenti di sviluppo F12 di Internet Explorer 11 e lo [strumento Fiddler][Fiddler] per eseguire il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-110">You can use the Internet Explorer 11 F12 developer tools and the [Fiddler tool][Fiddler] to help debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="8e0cd-111">Acquisizione di competenze</span><span class="sxs-lookup"><span data-stu-id="8e0cd-111">Skills You'll Learn</span></span>
<span data-ttu-id="8e0cd-112">In questa esercitazione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="8e0cd-113">Come usare Visual Studio 2013 per pubblicare un'applicazione Web direttamente in un'app Web nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-113">How to use Visual Studio 2013 to publish your web application directly to a web app in Azure App Service.</span></span>
* <span data-ttu-id="8e0cd-114">Come i modelli ASP.NET MVC 5 usano il framework CSS Bootstrap per migliorare la visualizzazione sui dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="8e0cd-114">How the ASP.NET MVC 5 templates use the CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="8e0cd-115">Come creare visualizzazioni specifiche del dispositivo per browser di destinazione specifici del dispositivo, ad esempio quelli di iPhone e Android.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-115">How to create mobile-specific views to target specific mobile browsers, such as the iPhone and Android</span></span>
* <span data-ttu-id="8e0cd-116">Come creare visualizzazioni reattive (che rispondono a browser differenti su dispositivi differenti).</span><span class="sxs-lookup"><span data-stu-id="8e0cd-116">How to create responsive views (views that respond to different browsers across devices)</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="8e0cd-117">Configurare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="8e0cd-117">Set up the development environment</span></span>
<span data-ttu-id="8e0cd-118">Installare Azure SDK per .NET 2.5.1 o versione successiva per configurare l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-118">Set up your development environment by installing the Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="8e0cd-119">Per installare Azure SDK per .NET, fare clic sul collegamento seguente.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-119">To install the Azure SDK for .NET, click the link below.</span></span> <span data-ttu-id="8e0cd-120">Se Visual Studio 2013 non è ancora presente, verrà installato tramite questo collegamento.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-120">If you don't have Visual Studio 2013 installed yet, it will be installed by the link.</span></span> <span data-ttu-id="8e0cd-121">Per completare questa esercitazione, è necessario disporre di Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="8e0cd-122">[Azure SDK per Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="8e0cd-123">Nell'Installazione guidata piattaforma Web fare clic su **Installa** e procedere con l'installazione.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-123">In the Web Platform Installer window, click **Install** and proceed with the installation.</span></span>

<span data-ttu-id="8e0cd-124">Sarà inoltre necessario disporre di un emulatore del browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="8e0cd-125">Eseguire una o più delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-125">Any of the following will work:</span></span>

* <span data-ttu-id="8e0cd-126">Emulatore di browser disponibile negli [strumenti di sviluppo F12 di Internet Explorer 11][EmulatorIE11] (usato in tutte le schermate del browser per dispositivi mobili).</span><span class="sxs-lookup"><span data-stu-id="8e0cd-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="8e0cd-127">Dispone di set di impostazioni della stringa agente utente per Windows Phone 8, Windows Phone 7 e Apple iPad.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="8e0cd-128">Emulatore di browser disponibile in [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="8e0cd-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="8e0cd-129">Sono disponibili set di impostazioni per diversi dispositivi Android, oltre che per Apple iPhone, Apple iPad e Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="8e0cd-130">Emula anche gli eventi tocco.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-130">It also emulates touch events.</span></span>
* <span data-ttu-id="8e0cd-131">[Emulatore mobile di Opera][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="8e0cd-132">Sono disponibili alcuni progetti con codice sorgente C\# a integrazione di questo argomento:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-132">Visual Studio projects with C\# source code are available to accompany this topic:</span></span>

* <span data-ttu-id="8e0cd-133">[Download progetto iniziale][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="8e0cd-134">[Download progetto completato][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="8e0cd-135"><a name="bkmk_DeployStarterProject"></a>Distribuire il progetto iniziale in un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="8e0cd-135"><a name="bkmk_DeployStarterProject"></a>Deploy the starter project to an Azure web app</span></span>
1. <span data-ttu-id="8e0cd-136">Scaricare il [progetto iniziale][StarterProject] dell'applicazione di elenco conferenze.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-136">Download the conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="8e0cd-137">In Esplora risorse fare quindi clic con il pulsante destro del mouse sul file ZIP scaricato e scegliere *Proprietà*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-137">Then in Windows Explorer, right-click the downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="8e0cd-138">Nella finestra di dialogo **Proprietà** fare clic sul pulsante **Sblocca**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-138">In the **Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="8e0cd-139">L'operazione di sblocco impedisce la visualizzazione dell'avviso di sicurezza quando si tenta di utilizzare un file *ZIP* scaricato dal Web.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-139">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>
4. <span data-ttu-id="8e0cd-140">Fare clic con il pulsante destro del mouse sul file ZIP e selezionare **Estrai tutto** per decomprimere il file.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-140">Right-click the ZIP file and select **Extract All** to unzip the file.</span></span> 
5. <span data-ttu-id="8e0cd-141">In Visual Studio aprire il file *C#\Mvc5Mobile.sln*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-141">In Visual Studio, open the *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="8e0cd-142">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-142">In Solution Explorer, right-click the project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="8e0cd-143">In Pubblica sito Web fare clic su **Servizio app di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="8e0cd-144">Se non è già stato effettuato l'accesso ad Azure, fare clic su **Aggiungi un account**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="8e0cd-145">Attenersi alla richiesta per accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-145">Follow the prompts to log into your Azure account.</span></span>
10. <span data-ttu-id="8e0cd-146">All'accesso viene visualizzata la finestra di dialogo Servizio App.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-146">The App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="8e0cd-147">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="8e0cd-148">Nel campo **Nome app Web** specificare un prefisso univoco per il nome dell'app.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-148">In the **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="8e0cd-149">Il nome completo dell'app sarà *&lt;prefix>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="8e0cd-150">Selezionare inoltre un gruppo di risorse o specificarne uno nuovo in **Gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="8e0cd-151">Quindi fare clic su **Nuovo** per creare un nuovo piano del servizio app.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-151">Then, click **New** to create a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="8e0cd-152">Configurare il nuovo piano del servizio app e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-152">Configure the new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="8e0cd-153">Nella finestra di dialogo Crea servizio app, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-153">Back in the Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="8e0cd-154">Dopo aver creato le risorse Azure, nella finestra di dialogo Pubblica sito Web verranno inserite le impostazioni relative alla nuova app.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-154">After the Azure resources are created, the Publish Web dialog will be filled with the settings for your new app.</span></span> <span data-ttu-id="8e0cd-155">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="8e0cd-156">Completata la pubblicazione del progetto iniziale nell'app Web di Azure con Visual Studio, si avvia il browser desktop e viene visualizzata l'app Web live.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-156">Once Visual Studio finishes publishing the starter project to the Azure web app, the desktop browser opens to display the live web app.</span></span>
15. <span data-ttu-id="8e0cd-157">Avviare l'emulatore di browser per dispositivi mobili, copiare l'URL dell'applicazione per conferenze (*<prefix>*.azurewebsites.net) nell'emulatore, quindi fare clic sul pulsante nell'angolo superiore destro e selezionare **Sfoglia per tag**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-157">Start your mobile browser emulator, copy the URL for the conference application (*<prefix>*.azurewebsites.net) into the emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="8e0cd-158">Se si usa Internet Explorer 11 come browser predefinito, è sufficiente digitare `F12`, quindi `Ctrl+8` e infine modificare il profilo del browser in **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-158">If you are using Internet Explorer 11 as the default browser, you just need to type `F12`, then `Ctrl+8`, and then change the browser profile to **Windows Phone**.</span></span> <span data-ttu-id="8e0cd-159">L'immagine riportata di seguito mostra la visualizzazione *AllTags*, risultante dalla selezione **Browse by tag** in modalità verticale.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-159">The image below shows the *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="8e0cd-160">Mentre si esegue il debug dell'applicazione MVC 5 da Visual Studio, è possibile pubblicare di nuovo l'app Web in Azure per verificare l'app Web live direttamente dall'emulatore per dispositivi mobili o dall'emulatore del browser.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app to Azure again to verify the live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="8e0cd-161">Il display è molto leggibile su un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-161">The display is very readable on a mobile device.</span></span> <span data-ttu-id="8e0cd-162">È già possibile vedere alcuni degli effetti grafici applicati dal framework CSS Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-162">You can also already see some of the visual effects applied by the Bootstrap CSS framework.</span></span>
<span data-ttu-id="8e0cd-163">Fare clic sul collegamento **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="8e0cd-163">Click the **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="8e0cd-164">La visualizzazione relativa ai tag ASP.NET viene ridotta in modo da rientrare per intero nello schermo, operazione eseguita automaticamente da Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-164">The ASP.NET tag view is zoom-fitted to the screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="8e0cd-165">È tuttavia possibile migliorare tale visualizzazione per adattarla al browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-165">However, you can improve this view to better suit the mobile browser.</span></span> <span data-ttu-id="8e0cd-166">La colonna **Date** , ad esempio, è di difficile lettura.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-166">For example, the **Date** column is difficult to read.</span></span> <span data-ttu-id="8e0cd-167">Più avanti in questa esercitazione verrà illustrato come modificare la visualizzazione *AllTags* per adattarla allo schermo dei dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-167">Later in the tutorial you'll change the *AllTags* view to make it mobile-friendly.</span></span>

## <span data-ttu-id="8e0cd-168"><a name="bkmk_bootstrap"></a> Framework CSS Bootstrap</span><span class="sxs-lookup"><span data-stu-id="8e0cd-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="8e0cd-169">Una delle novità del modello MVC 5 è il supporto integrato per Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-169">New in the MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="8e0cd-170">È già stato illustrato come Bootstrap consenta di migliorare le diverse schermate dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-170">You have already seen how it immediately improves the different views in your application.</span></span> <span data-ttu-id="8e0cd-171">Ad esempio, quando la larghezza del browser è ridotta, la barra di spostamento nella parte superiore della schermata è automaticamente comprimibile.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-171">For example, the navigation bar at the top is automatically collapsible when the browser width is smaller.</span></span> <span data-ttu-id="8e0cd-172">Sul browser desktop, provare a ridimensionare la finestra e osservare come cambiano le dimensioni e l'aspetto della barra di spostamento.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-172">On the desktop browser, try resizing the browser window and see how the navigation bar changes its look and feel.</span></span> <span data-ttu-id="8e0cd-173">Questa è una dimostrazione della progettazione Web reattiva integrata in Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-173">This is the responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="8e0cd-174">Per vedere l'aspetto dell'app Web senza Bootstrap, aprire *App\_Start\\BundleConfig.cs* e impostare come commento le righe contenenti *bootstrap.js* e *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-174">To see how the Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out the lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="8e0cd-175">Il codice riportato di seguito mostra le ultime due istruzioni del metodo `RegisterBundles` dopo la modifica:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-175">The following code shows the last two statements of the `RegisterBundles` method after the change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="8e0cd-176">Premere `Ctrl+F5` per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-176">Press `Ctrl+F5` to run the application.</span></span>

<span data-ttu-id="8e0cd-177">La barra di spostamento comprimibile è ora un normale elenco non ordinato.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-177">Observe that the collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="8e0cd-178">Fare ancora clic su **Browse by tag**, quindi su **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="8e0cd-179">Nella schermata dell'emulatore per dispositivi mobili, la tabella non è più ridotta per rientrare interamente nello schermo ed è necessario scorrerla in senso orizzontale per visualizzarne la parte destra.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-179">In the mobile emulator view, you can see now that it is no longer zoom-fitted to the screen, and you must scroll sideways in order to see the right side of the table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="8e0cd-180">Annullare le modifiche e aggiornare il browser per verificare che la schermata per i dispositivi mobili sia stata ripristinata.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-180">Undo your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="8e0cd-181">Bootstrap non è specifico di ASP.NET MVC 5 e le funzionalità che fornisce possono essere usate in qualsiasi applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-181">Bootstrap is not specific to ASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="8e0cd-182">Ora, tuttavia, Bootstrap è integrato nel modello di progetto ASP.NET MVC 5 per consentire all'applicazione Web MVC 5 di sfruttarne i vantaggi per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="8e0cd-183">Per altre informazioni, visitare il sito Web di [Bootstrap][BootstrapSite].</span><span class="sxs-lookup"><span data-stu-id="8e0cd-183">For more information about Bootstrap, go to the [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="8e0cd-184">Nella sezione seguente verrà illustrato come creare visualizzazioni specifiche del browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-184">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <span data-ttu-id="8e0cd-185"><a name="bkmk_overrideviews"></a> Eseguire l'override di viste, layout e viste parziali</span><span class="sxs-lookup"><span data-stu-id="8e0cd-185"><a name="bkmk_overrideviews"></a> Override the Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="8e0cd-186">È possibile eseguire l'override di una visualizzazione (inclusi i layout e le visualizzazioni parziali) per i browser per dispositivi mobili in generale, per un singolo browser per dispositivi mobili o per un qualsiasi browser specifico.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="8e0cd-187">Per fornire una vista specifica per dispositivi mobili è possibile copiare un file di visualizzazione e aggiungere *.Mobile* al nome del file.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-187">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="8e0cd-188">Ad esempio, per creare la visualizzazione *Index* per dispositivi mobili, è possibile copiare *Views\\Home\\Index.cshtml* in *Views\\Home\\Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-188">For example, to create a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="8e0cd-189">In questa sezione verrà illustrato come creare un file di layout specifico per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="8e0cd-190">Per iniziare, copiare *Views\\Shared\\\_Layout.cshtml* in *Views\\Shared\\\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-190">To start, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="8e0cd-191">Aprire *\_Layout.Mobile.cshtml* e modificare il titolo da **MVC5 Application** a **MVC5 Application (Mobile)**.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-191">Open *\_Layout.Mobile.cshtml* and change the title from **MVC5 Application** to **MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="8e0cd-192">In ogni chiamata di `Html.ActionLink` per la barra di spostamento, rimuovere "Browse by" da ciascun collegamento *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-192">In each `Html.ActionLink` call for the navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="8e0cd-193">Il codice seguente mostra il tag `<ul class="nav navbar-nav">` completato del file di layout per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-193">The following code shows the completed `<ul class="nav navbar-nav">` tag of the mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="8e0cd-194">Copiare il file *Views\\Home\\AllTags.cshtml* in *Views\\Home\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-194">Copy the *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="8e0cd-195">Aprire il nuovo file e modificare l'elemento `<h2>` da "Tags" in "Tags (M)":</span><span class="sxs-lookup"><span data-stu-id="8e0cd-195">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="8e0cd-196">Passare alla pagina Tags utilizzando un browser desktop e un emulatore di browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-196">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="8e0cd-197">L'emulatore di browser per dispositivi mobili mostra le due modifiche apportate (titolo da *\_Layout.Mobile.cshtml* e titolo da *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="8e0cd-197">The mobile browser emulator shows the two changes you made (the title from *\_Layout.Mobile.cshtml* and the title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="8e0cd-198">La visualizzazione desktop, invece, non è stata modificata (con i titoli da *\_Layout.cshtml* e *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="8e0cd-198">In contrast, the desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="8e0cd-199"><a name="bkmk_browserviews"></a> Creazione di visualizzazioni specifiche del browser</span><span class="sxs-lookup"><span data-stu-id="8e0cd-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="8e0cd-200">Oltre a visualizzazioni specifiche del dispositivo mobile e del desktop, è possibile anche creare visualizzazioni per un particolare browser.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-200">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="8e0cd-201">È possibile, ad esempio, creare visualizzazioni specifiche per i browser di iPhone o Android.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-201">For example, you can create views that are specifically for the iPhone or the Android browser.</span></span> <span data-ttu-id="8e0cd-202">In questa sezione verrà illustrato come creare un layout per il browser di iPhone e una versione iPhone della visualizzazione *AllTags* .</span><span class="sxs-lookup"><span data-stu-id="8e0cd-202">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="8e0cd-203">Aprire il file *Global.asax* e aggiungere il codice seguente all'ultima riga del metodo `Application_Start`.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-203">Open the *Global.asax* file and add the following code to the bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="8e0cd-204">Questo codice definisce una nuova modalità di visualizzazione denominata "iPhone" che verrà associata a ciascuna richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="8e0cd-205">Se la richiesta in ingresso soddisfa la condizione definita, ovvero se l'agente utente contiene la stringa"iPhone", ASP.NET MVC cercherà le visualizzazioni il cui nome contiene il suffisso"iPhone".</span><span class="sxs-lookup"><span data-stu-id="8e0cd-205">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="8e0cd-206">Quando si aggiungono modalità di visualizzazione specifiche del browser per dispositivi mobili, ad esempio per i browser di iPhone e Android, assicurarsi di impostare il primo argomento su `0` (inserirlo all'inizio dell'elenco), in modo che la modalità specifica del browser abbia la precedenza sul modello mobile (*.Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="8e0cd-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure to set the first argument to `0` (insert at the top of the list) to make sure that the browser-specific mode takes precedence over the mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="8e0cd-207">Se invece il primo posto dell'elenco è occupato dal modello mobile, questo sarà selezionato al posto della modalità di visualizzazione specificata (la prima corrispondenza ha la priorità e il modello mobile viene usato per tutti i browser per dispositivi mobili).</span><span class="sxs-lookup"><span data-stu-id="8e0cd-207">If the mobile template is at the top of the list instead, it will be selected over your intended display mode (the first match wins, and the mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="8e0cd-208">Nel codice fare clic con il pulsante destro del mouse su `DefaultDisplayMode`, scegliere **Risolvi** quindi scegliere `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-208">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="8e0cd-209">In questo modo viene aggiunto un riferimento allo spazio dei nomi `System.Web.WebPages`, ovvero la posizione in cui i tipi `DisplayModeProvider` e `DefaultDisplayMode` vengono definiti.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-209">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="8e0cd-210">In alternativa, è possibile aggiungere manualmente la riga seguente alla sezione `using` del file.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-210">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="8e0cd-211">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-211">Save the changes.</span></span> <span data-ttu-id="8e0cd-212">Copiare il file *Views\\Shared\\\_Layout.Mobile.cshtml* in *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="8e0cd-213">Aprire il nuovo file e modificare il titolo da `MVC5 Application (Mobile)` in `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-213">Open the new file and then change the title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="8e0cd-214">Copiare il file *Views\\Home\\AllTags.Mobile.cshtml* in *Views\\Home\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-214">Copy the *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="8e0cd-215">Nel nuovo file modificare l'elemento `<h2>` da "Tags (M)" in "Tags (iPhone)".</span><span class="sxs-lookup"><span data-stu-id="8e0cd-215">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="8e0cd-216">Eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-216">Run the application.</span></span> <span data-ttu-id="8e0cd-217">Eseguire un emulatore di browser per dispositivi mobili, assicurarsi che il relativo agente utente sia impostato su "iPhone" e passare alla visualizzazione *AllTags* .</span><span class="sxs-lookup"><span data-stu-id="8e0cd-217">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="8e0cd-218">Se si usa l'emulatore negli strumenti di sviluppo F12 di Internet Explorer 11, configurare l'emulazione come segue:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-218">If you are using the emulator in Internet Explorer 11 F12 developer tools, configure emulation to the following:</span></span>

* <span data-ttu-id="8e0cd-219">Profilo del browser = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="8e0cd-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="8e0cd-220">Stringa agente utente = **Custom**</span><span class="sxs-lookup"><span data-stu-id="8e0cd-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="8e0cd-221">Stringa personalizzata = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="8e0cd-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="8e0cd-222">La schermata seguente mostra la visualizzazione *AllTags* sottoposta a rendering nell'emulatore negli strumenti di sviluppo F12 di Internet Explorer 11 con la stringa agente utente personalizzata (in questo caso, una stringa agente utente iPhone 5C).</span><span class="sxs-lookup"><span data-stu-id="8e0cd-222">The following screenshot shows the *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with the custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="8e0cd-223">Nel browser per dispositivi mobili selezionare il collegamento **Speakers** .</span><span class="sxs-lookup"><span data-stu-id="8e0cd-223">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="8e0cd-224">Poiché non è disponibile una visualizzazione per dispositivi mobili (*AllSpeakers.Mobile.cshtml*), viene eseguito il rendering della visualizzazione dei relatori predefinita (*AllSpeakers.cshtml*) usando la visualizzazione di layout per dispositivi mobili(*\_Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="8e0cd-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), the default speakers view (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="8e0cd-225">Come mostrato di seguito, il titolo **MVC5 Application (Mobile)** è definito in *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-225">As shown below, the title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="8e0cd-226">È possibile disabilitare a livello globale il rendering di una visualizzazione predefinita (non per dispositivi mobili) all'interno di un layout mobile impostando `RequireConsistentDisplayMode` su `true` nel file *Views\\\_ViewStart.cshtml*, come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="8e0cd-227">Se `RequireConsistentDisplayMode` è impostato su `true`, il layout mobile (*\_Layout.Mobile.cshtml*) viene usato solo per le visualizzazioni per dispositivi mobili, ovvero quando il file della visualizzazione è in formato ***ViewName**.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-227">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of the form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="8e0cd-228">Può essere opportuno impostare `RequireConsistentDisplayMode` su `true` se il layout mobile non interagisce correttamente con le visualizzazioni non mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-228">You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="8e0cd-229">Lo screenshot seguente mostra il modo in cui la pagina *Speakers* viene sottoposta a rendering quando `RequireConsistentDisplayMode` è impostato su `true`, senza la stringa "(Mobile)" nella barra di spostamento nella parte superiore della schermata.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-229">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true` (without the string "(Mobile)" in the navigational bar at the top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="8e0cd-230">È possibile disabilitare la modalità di visualizzazione coerente in una visualizzazione specifica impostando `RequireConsistentDisplayMode` su `false` nel file di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="8e0cd-231">Il markup seguente presente nel file *Views\\Home\\AllSpeakers.cshtml* imposta `RequireConsistentDisplayMode` su `false`:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-231">The following markup in the *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="8e0cd-232">In questa sezione è stato spiegato come creare layout e visualizzazioni mobili e come creare layout e visualizzazioni per dispositivi specifici, ad esempio iPhone.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-232">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span>
<span data-ttu-id="8e0cd-233">Il principale vantaggio offerto dal framework CSS Bootstrap, tuttavia, è il layout reattivo, ovvero la possibilità di applicare un singolo foglio di stile a browser per desktop, telefoni cellulari e tablet per assicurare un aspetto uniforme e coerente.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-233">However, the main advantage of the Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers to create a consistent look and feel.</span></span> <span data-ttu-id="8e0cd-234">Nella sezione seguente verrà illustrato come usare Bootstrap per creare visualizzazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-234">In the next section you'll see how to leverage Bootstrap to create mobile-friendly views.</span></span>

## <span data-ttu-id="8e0cd-235"><a name="bkmk_Improvespeakerslist"></a> Migliorare l'elenco Speakers</span><span class="sxs-lookup"><span data-stu-id="8e0cd-235"><a name="bkmk_Improvespeakerslist"></a> Improve the Speakers List</span></span>
<span data-ttu-id="8e0cd-236">Come si è appena osservato, la vista *Speakers* è leggibile, ma i collegamenti sono di dimensioni ridotte e difficili da selezionare con un tocco su un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-236">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="8e0cd-237">In questa sezione verrà illustrato come rendere la visualizzazione *AllSpeakers* adatta a dispositivi mobili, con collegamenti ben visibili e facili da toccare e una casella di ricerca per trovare rapidamente i relatori.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-237">In this section, you'll make the *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="8e0cd-238">È possibile usare lo stile di Bootstrap relativo ai [gruppi elenchi collegati][linked list group] per migliorare la visualizzazione *Speakers*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-238">You can use the Bootstrap [linked list group][linked list group] styling to improve the *Speakers* view.</span></span> <span data-ttu-id="8e0cd-239">In *Views\\Home\\AllSpeakers.cshtml* sostituire il contenuto del file Razor con il codice riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-239">In *Views\\Home\\AllSpeakers.cshtml*, replace the contents of the Razor file with the code below.</span></span>

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

<span data-ttu-id="8e0cd-240">L'attributo `class="list-group"` presente nel tag `<div>` applica lo stile di Bootstrap relativo agli elenchi, mentre l'attributo `class="input-group-item"` applica a ogni collegamento lo stile di Bootstrap relativo alle voci di elenco.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-240">The `class="list-group"` attribute in the `<div>` tag applies the Bootstrap list styling, and the `class="input-group-item"` attribute applies Bootstrap list item styling to each link.</span></span>

<span data-ttu-id="8e0cd-241">Aggiornare il browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-241">Refresh the mobile browser.</span></span> <span data-ttu-id="8e0cd-242">La vista aggiornata avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-242">The updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="8e0cd-243">Lo stile di Bootstrap relativo ai [ gruppi elenchi collegati][linked list group] rende l'intera casella di ogni collegamento selezionabile con un clic, agevolando in questo modo l'esperienza utente.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-243">The Bootstrap [linked list group][linked list group] styling makes the entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="8e0cd-244">Passare alla visualizzazione desktop e osservare l'aspetto uniforme e coerente.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-244">Switch to the desktop view and observe the consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="8e0cd-245">Anche se la visualizzazione per il browser per dispositivi mobili è stata migliorata, scorrere il lungo elenco di relatori è ancora difficile.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-245">Although the mobile browser view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="8e0cd-246">Bootstrap non fornisce un filtro di ricerca pronto all'uso, ma è possibile aggiungere questa funzionalità con poche righe di codice.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="8e0cd-247">È necessario innanzitutto aggiungere alla visualizzazione una casella di ricerca e quindi collegare tale casella al codice JavaScript relativo alla funzione di filtro.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-247">You will first add a search box to the view, then hook up with the JavaScript code for the filter function.</span></span> <span data-ttu-id="8e0cd-248">In *Views\\Home\\AllSpeakers.cshtml* aggiungere un tag \<form\> subito dopo il tag \<h2\>, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after the \<h2\> tag, as shown below:</span></span>

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

<span data-ttu-id="8e0cd-249">Si noti che a entrambi i tag `<form>` e `<input>` sono applicati gli stili di Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-249">Notice that the `<form>` and `<input>` tags both have the Bootstrap styles applied to them.</span></span> <span data-ttu-id="8e0cd-250">L'elemento `<span>` aggiunge un'icona [glyphicon][glyphicon] di Bootstrap alla casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-250">The `<span>` element adds a Bootstrap [glyphicon][glyphicon] to the search box.</span></span>

<span data-ttu-id="8e0cd-251">Nella cartella *Scripts* aggiungere un file JavaScript denominato *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-251">In the *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="8e0cd-252">Aprire il file e incollarvi il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-252">Open the file and paste the following code into it:</span></span>

    $(function () {

        // reset the search form when the page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up the events to the <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with the typed text and hide others
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

<span data-ttu-id="8e0cd-253">È inoltre necessario includere il filtro.js nei bundle registrati.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-253">You also need to include filter.js in your registered bundles.</span></span> <span data-ttu-id="8e0cd-254">Aprire *App\_Start\\BundleConfig.cs* e modificare i primi bundle.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-254">Open *App\_Start\\BundleConfig.cs* and change the first bundles.</span></span> <span data-ttu-id="8e0cd-255">Modificare la prima istruzione `bundles.Add` (per il bundle **jquery**) in modo che includa *Scripts\\filter.js*, come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-255">Change the first `bundles.Add` statement (for the **jquery** bundle) to include *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="8e0cd-256">Il bundle **jquery** è già stato sottoposto a rendering dalla visualizzazione predefinita *\_Layout*.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-256">The **jquery** bundle is already rendered by the default *\_Layout* view.</span></span> <span data-ttu-id="8e0cd-257">In un secondo tempo è possibile usare lo stesso codice JavaScript per applicare la funzionalità di filtro ad altre visualizzazioni elenco.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-257">Later, you can utilize the same JavaScript code to apply the filter functionality to other list views.</span></span>

<span data-ttu-id="8e0cd-258">Aggiornare il browser per dispositivi mobili e passare alla visualizzazione *AllSpeakers* .</span><span class="sxs-lookup"><span data-stu-id="8e0cd-258">Refresh the mobile browser and go to the *AllSpeakers* view.</span></span> <span data-ttu-id="8e0cd-259">Nella casella di ricerca digitare "sc".</span><span class="sxs-lookup"><span data-stu-id="8e0cd-259">In the search box, type "sc".</span></span> <span data-ttu-id="8e0cd-260">L'elenco dei relatori viene ora filtrato in base alla stringa di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-260">The speakers list should now be filtered according to your search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="8e0cd-261"><a name="bkmk_improvetags"></a> Migliorare l'elenco Tags</span><span class="sxs-lookup"><span data-stu-id="8e0cd-261"><a name="bkmk_improvetags"></a> Improve the Tags List</span></span>
<span data-ttu-id="8e0cd-262">Come la visualizzazione *Speakers*, anche la visualizzazione *Tags* è leggibile, ma i collegamenti sono di dimensioni ridotte e difficili da selezionare con un tocco su un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-262">Like the *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="8e0cd-263">È possibile intervenire sulla visualizzazione *Tags* nello stesso modo in cui è stata migliorata la visualizzazione *Speakers*. Usare le modifiche del codice descritte in precedenza, ma applicare la sintassi del metodo `Html.ActionLink` seguente in *Views\\Home\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-263">You can fix the *Tags* view the same way you fix the *Speakers* view, if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="8e0cd-264">Il browser desktop aggiornato avrà il seguente aspetto:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-264">The refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="8e0cd-265">Il browser per dispositivi mobili aggiornato avrà il seguente aspetto:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-265">And the refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="8e0cd-266">È possibile che sul browser per dispositivi mobili sia ancora presente la formattazione originale dell'elenco, senza l'applicazione dello stile di Bootstrap: si tratta del risultato della precedente azione di creazione di visualizzazioni specifiche del dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-266">If you notice that the original list formatting is still there in the mobile browser and wonder what happened to your nice Bootstrap styling, this is an artifact of your earlier action to create mobile specific views.</span></span> <span data-ttu-id="8e0cd-267">Tuttavia, poiché ora si sta usando il framework CSS Bootstrap per creare una progettazione Web reattiva, rimuovere le visualizzazioni e il layout specifici del dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-267">However, now that you are using the Bootstrap CSS framework to create a responsive web design, go head and remove these mobile-specific views and the mobile-specific layout views.</span></span> <span data-ttu-id="8e0cd-268">Una volta eseguita l'eliminazione, il browser per dispositivi mobili aggiornato visualizzerà lo stile di Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-268">Once you have done so, the refreshed mobile browser will show the Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="8e0cd-269"><a name="bkmk_improvedates"></a> Migliorare l'elenco Dates</span><span class="sxs-lookup"><span data-stu-id="8e0cd-269"><a name="bkmk_improvedates"></a> Improve the Dates List</span></span>
<span data-ttu-id="8e0cd-270">È possibile intervenire sulla visualizzazione *Dates* nello stesso modo in cui sono state migliorate le visualizzazioni *Speakers *e* Tags`Html.ActionLink`. Usare le modifiche del codice descritte in precedenza, ma , ma applicare la sintassi del metodo* seguente in *Views\\Home\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-270">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="8e0cd-271">Si otterrà una visualizzazione del browser per dispositivi mobili aggiornato simile a quella riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="8e0cd-272">È possibile migliorare ulteriormente la visualizzazione *Dates* organizzando i valori di data e ora in base alla data.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-272">You can further improve the *Dates* view by organizing the date-time values by date.</span></span> <span data-ttu-id="8e0cd-273">È possibile eseguire questa operazione usando lo stile di Bootstrap relativo ai [pannelli][panels].</span><span class="sxs-lookup"><span data-stu-id="8e0cd-273">This can be done with the Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="8e0cd-274">Sostituire il contenuto del file *Views\\Home\\AllDates.cshtml* con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-274">Replace the contents of the *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="8e0cd-275">Il codice crea un tag `<div class="panel panel-primary">` separato per ogni data dell'elenco e usa il [gruppo elenchi collegati][linked list group] per i rispettivi collegamenti, come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in the list, and uses the [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="8e0cd-276">Si osservi di seguito l'aspetto del browser per dispositivi mobili quando viene eseguito questo codice:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-276">Here's what the mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="8e0cd-277">Passare al browser desktop.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-277">Switch to the desktop browser.</span></span> <span data-ttu-id="8e0cd-278">Si noti ancora una volta l'aspetto uniforme e coerente.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-278">Again, note the consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="8e0cd-279"><a name="bkmk_improvesessionstable"></a> Migliorare la vista SessionsTable</span><span class="sxs-lookup"><span data-stu-id="8e0cd-279"><a name="bkmk_improvesessionstable"></a> Improve the SessionsTable View</span></span>
<span data-ttu-id="8e0cd-280">In questa sezione verrà illustrato come creare la visualizzazione *SessionsTable* in modo specifico per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-280">In this section, you'll make the *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="8e0cd-281">Questa modifica è più impegnativa di quelle apportate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-281">This change is more extensive the previous changes.</span></span>

<span data-ttu-id="8e0cd-282">Nel browser per dispositivi mobili toccare il pulsante **Tag**, quindi immettere `asp` nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-282">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="8e0cd-283">Toccare il collegamento **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="8e0cd-283">Tap the **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="8e0cd-284">Come mostrato dalla figura, la visualizzazione è formattata come tabella, soluzione normalmente adottata per il browser desktop.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-284">As you can see, the display is formatted as a table, which is currently designed to be viewed in the desktop browser.</span></span> <span data-ttu-id="8e0cd-285">Questa formattazione, tuttavia, risulta di difficile lettura su un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-285">However, it's a little bit difficult to read on a mobile browser.</span></span> <span data-ttu-id="8e0cd-286">Per risolvere questo problema, aprire il file *Views\\Home\\SessionsTable.cshtml* e sostituirne il contenuto con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-286">To fix this, open *Views\\Home\\SessionsTable.cshtml* and then replace the contents of the file with the following code:</span></span>

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

<span data-ttu-id="8e0cd-287">Il codice esegue tre operazioni:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-287">The code does 3 things:</span></span>

* <span data-ttu-id="8e0cd-288">usa il [gruppo elenchi collegati personalizzato][custom linked list group] di Bootstrap per formattare le informazioni della sessione in verticale, in modo da facilitarne la lettura su un browser per dispositivi mobili (usando classi quali list-group-item-text)</span><span class="sxs-lookup"><span data-stu-id="8e0cd-288">uses the Bootstrap [custom linked list group][custom linked list group] to format the session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="8e0cd-289">applica il [sistema griglia][grid system] al layout, in modo che gli elementi della sessione scorrano in orizzontale nel browser desktop e in verticale in quello per dispositivi mobili (usando la classe col-md-4)</span><span class="sxs-lookup"><span data-stu-id="8e0cd-289">applies the [grid system][grid system] to the layout, so that the session items flow horizontally in the desktop browser and vertically in the mobile browser (using the col-md-4 class)</span></span>
* <span data-ttu-id="8e0cd-290">usa [utilità reattive][responsive utilities] per nascondere i tag della sessione durante la visualizzazione sul browser per dispositivi mobili (usando la classe hidden-xs)</span><span class="sxs-lookup"><span data-stu-id="8e0cd-290">uses the [responsive utilities][responsive utilities] to hide the session tags when viewed in the mobile browser (using the hidden-xs class)</span></span>

<span data-ttu-id="8e0cd-291">È possibile anche toccare il collegamento di un titolo per passare alla relativa sessione.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-291">You can also tap a title link to go to the respective session.</span></span> <span data-ttu-id="8e0cd-292">Nell'immagine seguente è illustrato l'aspetto risultante dopo aver apportato le modifiche al codice.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-292">The image below reflects the code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="8e0cd-293">Il sistema griglia di Bootstrap applicato formatta automaticamente le sessioni in senso verticale nel browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-293">The Bootstrap grid system that you applied automatically arranges the sessions vertically in the mobile browser.</span></span> <span data-ttu-id="8e0cd-294">Si noti anche che i tag non vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-294">Also, notice that the tags are not shown.</span></span> <span data-ttu-id="8e0cd-295">Passare al browser desktop.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-295">Switch to the desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="8e0cd-296">Si noti che ora nel browser desktop i tag sono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-296">In the desktop browser, notice that the tags are now displayed.</span></span> <span data-ttu-id="8e0cd-297">Si noti anche che il sistema griglia di Bootstrap applicato ha organizzato gli elementi della sessione in due colonne.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-297">Also, you can see that the Bootstrap grid system you applied arranges the session items in two columns.</span></span> <span data-ttu-id="8e0cd-298">Se si ingrandisce la finestra del browser, gli elementi verranno visualizzati in tre colonne.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-298">If you enlarge the browser, you will see that the arrangement changes to three columns.</span></span>

## <span data-ttu-id="8e0cd-299"><a name="bkmk_improvesessionbycode"></a> Migliorare la vista SessionByCode</span><span class="sxs-lookup"><span data-stu-id="8e0cd-299"><a name="bkmk_improvesessionbycode"></a> Improve the SessionByCode View</span></span>
<span data-ttu-id="8e0cd-300">Come operazione conclusiva, la visualizzazione *SessionByCode* verrà modificata per adattarla allo schermo dei dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-300">Finally, you'll fix the *SessionByCode* view to make it mobile-friendly.</span></span>

<span data-ttu-id="8e0cd-301">Nel browser per dispositivi mobili toccare il pulsante **Tag**, quindi immettere `asp` nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-301">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="8e0cd-302">Toccare il collegamento **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="8e0cd-302">Tap the **ASP.NET** link.</span></span> <span data-ttu-id="8e0cd-303">Vengono visualizzate le sessioni relative ai tag ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-303">Sessions for the ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="8e0cd-304">Scegliere il collegamento **Building a Single Page Application with ASP.NET and AngularJS** .</span><span class="sxs-lookup"><span data-stu-id="8e0cd-304">Choose the **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="8e0cd-305">La visualizzazione desktop è accettabile, ma è possibile migliorarne facilmente l'aspetto usando i componenti dell'interfaccia utente grafica di Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-305">The default desktop view is fine, but you can improve the look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="8e0cd-306">Aprire il file *Views\\Home\\SessionByCode.cshtml* e sostituirne il contenuto con il markup seguente:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-306">Open *Views\\Home\\SessionByCode.cshtml* and replace the contents with the following markup:</span></span>

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

<span data-ttu-id="8e0cd-307">Il nuovo markup usa lo stile di Bootstrap relativo ai pannelli per adattare la visualizzazione allo schermo dei dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-307">The new markup uses Bootstrap panels styling to improve the mobile view.</span></span> 

<span data-ttu-id="8e0cd-308">Aggiornare il browser per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-308">Refresh the mobile browser.</span></span> <span data-ttu-id="8e0cd-309">Nell'immagine seguente è illustrato l'aspetto risultante dopo aver apportato le ultime modifiche:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-309">The following image reflects the code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="8e0cd-310">Riepilogo e revisione</span><span class="sxs-lookup"><span data-stu-id="8e0cd-310">Wrap Up and Review</span></span>
<span data-ttu-id="8e0cd-311">Nel corso di questa esercitazione è stato mostrato come usare ASP.NET MVC 5 per sviluppare applicazioni Web per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8e0cd-311">This tutorial has shown you how to use ASP.NET MVC 5 to develop mobile-friendly Web applications.</span></span> <span data-ttu-id="8e0cd-312">Sono state illustrate le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="8e0cd-312">These include:</span></span>

* <span data-ttu-id="8e0cd-313">Distribuzione di un'applicazione ASP.NET MVC 5 in un'app Web del servizio app</span><span class="sxs-lookup"><span data-stu-id="8e0cd-313">Deploy an ASP.NET MVC 5 application to an App Service web app</span></span>
* <span data-ttu-id="8e0cd-314">Uso di Bootstrap per creare un layout Web reattivo nell'applicazione MVC 5</span><span class="sxs-lookup"><span data-stu-id="8e0cd-314">Use Bootstrap to create responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="8e0cd-315">Override di layout, visualizzazioni e visualizzazioni parziali, sia in modo globale sia per una singola visualizzazione</span><span class="sxs-lookup"><span data-stu-id="8e0cd-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="8e0cd-316">Controllo del layout ed esecuzione di un override parziale usando la proprietà `RequireConsistentDisplayMode`</span><span class="sxs-lookup"><span data-stu-id="8e0cd-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="8e0cd-317">Creazione di visualizzazioni per browser specifici, ad esempio quello per iPhone</span><span class="sxs-lookup"><span data-stu-id="8e0cd-317">Create views that target specific browsers, such as the iPhone browser</span></span>
* <span data-ttu-id="8e0cd-318">Applicazione di stili Bootstrap in codice Razor</span><span class="sxs-lookup"><span data-stu-id="8e0cd-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="8e0cd-319">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8e0cd-319">See Also</span></span>
* [<span data-ttu-id="8e0cd-320">9 principi di base della progettazione Web reattiva</span><span class="sxs-lookup"><span data-stu-id="8e0cd-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="8e0cd-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="8e0cd-322">[Blog ufficiale di Bootstrap][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="8e0cd-323">[Tutorial Twitter Bootstrap su Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="8e0cd-324">[Editor e strumenti Bootstrap][The Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-324">[The Bootstrap Playground][The Bootstrap Playground]</span></span>
* <span data-ttu-id="8e0cd-325">[Procedure consigliate per applicazioni Web W3C per dispositivi mobili][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="8e0cd-326">[Candidate Recommendation W3C per query sui supporti][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="8e0cd-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="8e0cd-327">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="8e0cd-327">What's changed</span></span>
* <span data-ttu-id="8e0cd-328">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8e0cd-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy the starter project to an Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override the Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve the Speakers List]: #bkmk_Improvespeakerslist
[Improve the Tags List]: #bkmk_improvetags
[Improve the Dates List]: #bkmk_improvedates
[Improve the SessionsTable View]: #bkmk_improvesessionstable
[Improve the SessionByCode View]: #bkmk_improvesessionbycode

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
[The Bootstrap Playground]: http://www.bootply.com/
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

