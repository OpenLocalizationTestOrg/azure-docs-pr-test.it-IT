---
title: toowork aaaHow con server di back-end .NET hello SDK per App per dispositivi mobili | Documenti Microsoft
description: Informazioni su come toowork con hello server back-end .NET SDK per App Mobile di servizio App di Azure.
keywords: "servizio app, servizio app di Azure, app per dispositivi mobili, servizio mobile, scalabilità, scalabile, distribuzione app, distribuzione app di Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="e9769-104">Usare i server back-end di hello .NET SDK per App mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="e9769-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="e9769-105">Questo argomento viene illustrato come toouse hello server back-end .NET SDK gli scenari principali di App Mobile di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9769-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="e9769-106">Hello App Mobile di Azure SDK consente di lavorare con i client per dispositivi mobili da un'applicazione ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e9769-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="e9769-107">Hello [server .NET SDK per App mobili di Azure] [ 2] è open source su GitHub.</span><span class="sxs-lookup"><span data-stu-id="e9769-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="e9769-108">repository di Hello contiene tutto il codice sorgente tra gruppo di hello intero server SDK unit test e alcuni progetti di esempio.</span><span class="sxs-lookup"><span data-stu-id="e9769-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="e9769-109">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="e9769-109">Reference documentation</span></span>
<span data-ttu-id="e9769-110">documentazione di riferimento Hello per server hello SDK è disponibile in: [Azure Mobile app .NET Reference][1].</span><span class="sxs-lookup"><span data-stu-id="e9769-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="e9769-111"><a name="create-app"></a>Procedura: Creare un back-end dell'app per dispositivi mobili .NET</span><span class="sxs-lookup"><span data-stu-id="e9769-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="e9769-112">Se si sta avviando un nuovo progetto, è possibile creare un'applicazione di servizio App utilizzando entrambi hello [portale di Azure] o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9769-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="e9769-113">È possibile eseguire localmente hello applicazione di servizio App o pubblicare hello progetto tooyour basato su cloud App servizio app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e9769-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="e9769-114">Se si sta aggiungendo progetto esistente tooan di funzionalità per dispositivi mobili, vedere hello [scaricare e inizializzare hello SDK](#install-sdk) sezione.</span><span class="sxs-lookup"><span data-stu-id="e9769-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="e9769-115">Creare un back-end .NET utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e9769-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="e9769-116">toocreate un'App mobile back-end, di seguire hello [esercitazione rapida] [ 3] o eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e9769-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="e9769-117">In hello *iniziare* pannello, in **creare una tabella API**, scegliere **c#** come il **language back-end**.</span><span class="sxs-lookup"><span data-stu-id="e9769-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="e9769-118">Fare clic su **scaricare**, estrarre il progetto in formato compresso file tooyour locale computer e aprire la soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9769-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="e9769-119">Creare un back-end .NET usando Visual Studio 2013 e Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e9769-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="e9769-120">Installare hello [Azure SDK per .NET] [ 4] (versione 2.9.0 o versione successiva) toocreate un progetto di App mobili di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9769-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="e9769-121">Dopo aver installato hello SDK, è possibile creare un'applicazione ASP.NET tramite hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e9769-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="e9769-122">Aprire hello **nuovo progetto** finestra di dialogo (da *File* > **New** > **progetto...** ).</span><span class="sxs-lookup"><span data-stu-id="e9769-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="e9769-123">Espandere **Modelli** > **Visual C#** e selezionare **Web**.</span><span class="sxs-lookup"><span data-stu-id="e9769-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="e9769-124">Selezionare **Applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="e9769-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="e9769-125">Inserire il nome di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-125">Fill in hello project name.</span></span> <span data-ttu-id="e9769-126">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e9769-126">Then click **OK**.</span></span>
5. <span data-ttu-id="e9769-127">In *Modelli ASP.NET 4.5.2* selezionare **App mobile di Azure**.</span><span class="sxs-lookup"><span data-stu-id="e9769-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="e9769-128">Controllare **Host nel cloud hello** toocreate un back-end mobile in hello cloud toowhich è possibile pubblicare il progetto.</span><span class="sxs-lookup"><span data-stu-id="e9769-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="e9769-129">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e9769-129">Click **OK**.</span></span>

## <span data-ttu-id="e9769-130"><a name="install-sdk"></a>Procedura: scaricare e inizializzare hello SDK</span><span class="sxs-lookup"><span data-stu-id="e9769-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="e9769-131">Hello SDK è disponibile in [NuGet.org]. Il pacchetto include tooget funzionalità di base necessarie hello avviato utilizzando hello SDK.</span><span class="sxs-lookup"><span data-stu-id="e9769-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="e9769-132">tooinitialize hello SDK, è necessario tooperform azioni hello **HttpConfiguration** oggetto.</span><span class="sxs-lookup"><span data-stu-id="e9769-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="e9769-133">Installare hello SDK</span><span class="sxs-lookup"><span data-stu-id="e9769-133">Install hello SDK</span></span>
<span data-ttu-id="e9769-134">hello tooinstall SDK, destro del mouse sul progetto server hello in Visual Studio, selezionare **Gestisci pacchetti NuGet**, cercare hello [Microsoft.Azure.Mobile.Server] del pacchetto, quindi fare clic su  **Installare**.</span><span class="sxs-lookup"><span data-stu-id="e9769-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="e9769-135"><a name="server-project-setup"></a>Inizializzare il progetto server hello</span><span class="sxs-lookup"><span data-stu-id="e9769-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="e9769-136">Un progetto server di back-end .NET è inizializzato tooother ASP.NET progetti simili, con l'inclusione di una classe di avvio OWIN.</span><span class="sxs-lookup"><span data-stu-id="e9769-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="e9769-137">Verificare che si è fatto riferimento pacchetto NuGet hello `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="e9769-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="e9769-138">Fare doppio clic su questa classe in Visual Studio, tooadd nel progetto server e selezionare **Aggiungi** >
**nuovo elemento**, quindi **Web**  >  ** Generale** > **classe di avvio di OWIN**.</span><span class="sxs-lookup"><span data-stu-id="e9769-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="e9769-139">Viene generata una classe con hello seguente attributo:</span><span class="sxs-lookup"><span data-stu-id="e9769-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="e9769-140">In hello `Configuration()` metodo della classe di avvio OWIN, utilizzare un **HttpConfiguration** ambiente a oggetti tooconfigure hello App mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9769-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="e9769-141">Hello di esempio seguente consente di inizializzare il progetto server hello alcuna funzionalità aggiuntive:</span><span class="sxs-lookup"><span data-stu-id="e9769-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="e9769-142">tooenable singole funzionalità, è necessario chiamare metodi di estensione su hello **MobileAppConfiguration** oggetto prima di chiamare **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="e9769-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="e9769-143">Ad esempio, hello seguente di codice aggiunge predefinito hello instrada controller tooall API con attributo hello `[MobileAppController]` durante l'inizializzazione:</span><span class="sxs-lookup"><span data-stu-id="e9769-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="e9769-144">avvio rapido server Hello da hello chiamate portale Azure **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="e9769-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="e9769-145">Questo toohello equivalente dopo l'installazione:</span><span class="sxs-lookup"><span data-stu-id="e9769-145">This equivalent toohello following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="e9769-146">metodi di estensione Hello utilizzati sono:</span><span class="sxs-lookup"><span data-stu-id="e9769-146">hello extension methods used are:</span></span>

* <span data-ttu-id="e9769-147">`AddMobileAppHomeController()`fornisce una home page di hello predefinita App mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9769-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="e9769-148">`MapApiControllers()`fornisce funzionalità dell'API personalizzata per i controller WebAPI decorati con hello `[MobileAppController]` attributo.</span><span class="sxs-lookup"><span data-stu-id="e9769-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="e9769-149">`AddTables()`fornisce un mapping di hello `/tables` controller tootable endpoint.</span><span class="sxs-lookup"><span data-stu-id="e9769-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="e9769-150">`AddTablesWithEntityFramework()`è una sintassi abbreviata per hello mapping `/tables` controller basati su endpoint che usa Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="e9769-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="e9769-151">`AddPushNotifications()` fornisce un semplice metodo di registrazione dei dispositivi per Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="e9769-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="e9769-152">`MapLegacyCrossDomainController()` fornisce intestazioni CORS standard per lo sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="e9769-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="e9769-153">Estensioni SDK</span><span class="sxs-lookup"><span data-stu-id="e9769-153">SDK extensions</span></span>
<span data-ttu-id="e9769-154">Hello seguenti pacchetti di estensione basato su NuGet fornisce varie funzionalità mobile che può essere usata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="e9769-155">Abilitare le estensioni durante l'inizializzazione mediante hello **MobileAppConfiguration** oggetto.</span><span class="sxs-lookup"><span data-stu-id="e9769-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="e9769-156">[Microsoft.Azure.Mobile.Server.Quickstart] supporta hello base programma di installazione di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e9769-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="e9769-157">Configurazione toohello aggiunto dal chiamante hello **UseDefaultConfiguration** il metodo di estensione durante l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="e9769-158">Questa estensione include le estensioni seguenti: pacchetti Notifications, Authentication, Entity, Tables, Crossdomain e Home.</span><span class="sxs-lookup"><span data-stu-id="e9769-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="e9769-159">Questo pacchetto viene utilizzato da hello Guida introduttiva di App mobili disponibili nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="e9769-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementa predefinito hello *questa app per dispositivi mobili sia in esecuzione pagina* per la radice del sito web di hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="e9769-161">Aggiungi configurazione toohello chiamando il **AddMobileAppHomeController** metodo di estensione.</span><span class="sxs-lookup"><span data-stu-id="e9769-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="e9769-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) include le classi per l'utilizzo di dati e set di backup della pipeline di dati hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="e9769-163">Aggiungi configurazione toohello dal chiamante hello **AddTables** metodo di estensione.</span><span class="sxs-lookup"><span data-stu-id="e9769-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="e9769-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) consente hello Entity Framework tooaccess dati hello Database SQL.</span><span class="sxs-lookup"><span data-stu-id="e9769-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="e9769-165">Aggiungi configurazione toohello dal chiamante hello **AddTablesWithEntityFramework** metodo di estensione.</span><span class="sxs-lookup"><span data-stu-id="e9769-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="e9769-166">[Microsoft.Azure.Mobile.Server.Authentication] Abilita middleware OWIN hello l'autenticazione e set di backup utilizzato toovalidate token.</span><span class="sxs-lookup"><span data-stu-id="e9769-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="e9769-167">Aggiungi configurazione toohello dal chiamante hello **AddAppServiceAuthentication** e **IAppBuilder**. **UseAppServiceAuthentication** metodi di estensione.</span><span class="sxs-lookup"><span data-stu-id="e9769-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="e9769-168">[Microsoft.Azure.Mobile.Server.Notifications] Consente le notifiche push e definisce un endpoint di registrazione push.</span><span class="sxs-lookup"><span data-stu-id="e9769-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="e9769-169">Aggiungi configurazione toohello dal chiamante hello **AddPushNotifications** metodo di estensione.</span><span class="sxs-lookup"><span data-stu-id="e9769-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="e9769-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) viene creato un controller che serve dati toolegacy browser dall'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="e9769-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="e9769-171">Aggiungi configurazione toohello chiamando il **MapLegacyCrossDomainController** metodo di estensione.</span><span class="sxs-lookup"><span data-stu-id="e9769-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="e9769-172">[Microsoft.Azure.Mobile.Server.Login] fornisce il metodo AppServiceLoginHandler.CreateToken() hello, che è un metodo statico utilizzato durante gli scenari di autenticazione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e9769-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="e9769-173"><a name="publish-server-project"></a>Procedura: pubblicare il progetto server di hello</span><span class="sxs-lookup"><span data-stu-id="e9769-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="e9769-174">In questa sezione viene illustrato come toopublish progetto back-end .NET da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9769-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="e9769-175">È inoltre possibile distribuire il progetto back-end tramite Git o uno qualsiasi dei hello altri metodi descritti in hello [documentazione sulla distribuzione di servizio App di Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e9769-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="e9769-176">In Visual Studio, ricompilare i pacchetti hello progetto toorestore NuGet.</span><span class="sxs-lookup"><span data-stu-id="e9769-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="e9769-177">In Esplora soluzioni, progetti hello pulsante destro del mouse, fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e9769-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="e9769-178">Hello prima volta che si pubblica, è necessario toodefine un profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="e9769-179">Se si ha già un profilo definito, è possibile selezionarlo e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e9769-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="e9769-180">Se viene richiesto di tooselect una destinazione di pubblicazione, fare clic su **servizio App di Microsoft Azure** > **Avanti**, quindi, se necessario, accedi con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9769-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="e9769-181">Visual Studio scaricherà e memorizzerà le impostazioni di pubblicazione direttamente da Azure.</span><span class="sxs-lookup"><span data-stu-id="e9769-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="e9769-182">Scegliere la **Sottoscrizione**, selezionare **Tipo di risorsa** da **Visualizza**, espandere **App per dispositivi mobili** e fare clic sul back-end di App per dispositivi mobili, quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e9769-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="e9769-183">Verificare hello pubblicare informazioni sul profilo e fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e9769-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="e9769-184">Quando il back-end dell'app per dispositivi mobili ha eseguito la pubblicazione, viene visualizzata una pagina di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="e9769-185"><a name="define-table-controller"></a> Procedura: Definire un controller tabelle</span><span class="sxs-lookup"><span data-stu-id="e9769-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="e9769-186">Definire un tooexpose Controller tabella un client di toomobile tabella SQL.</span><span class="sxs-lookup"><span data-stu-id="e9769-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="e9769-187">Per configurare un controller tabelle, sono necessari tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="e9769-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="e9769-188">Creare una classe di oggetti di trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="e9769-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="e9769-189">Configurare un riferimento alla tabella nella classe DbContext Mobile hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="e9769-190">Creare un controller tabelle.</span><span class="sxs-lookup"><span data-stu-id="e9769-190">Create a table controller.</span></span>

<span data-ttu-id="e9769-191">Un oggetto di trasferimento dei dati è un oggetto C# normale che eredita `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="e9769-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="e9769-192">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e9769-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="e9769-193">Hello DTO è tabella hello toodefine utilizzato nel database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="e9769-194">hello toocreate voce del database, aggiungere un `DbSet<>` proprietà hello DbContext in uso.</span><span class="sxs-lookup"><span data-stu-id="e9769-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="e9769-195">Nel modello di progetto predefinito hello per le applicazioni mobili di Azure, hello DbContext viene chiamato `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="e9769-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="e9769-196">Se si dispone di hello che Azure SDK installato, è ora possibile creare un controller di tabella del modello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e9769-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="e9769-197">Fare clic sulla cartella controller hello e selezionare **Aggiungi** > **Controller...** .</span><span class="sxs-lookup"><span data-stu-id="e9769-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="e9769-198">Seleziona hello **Controller tabelle di Azure Mobile app** opzione, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e9769-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="e9769-199">In hello **Aggiungi Controller** finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="e9769-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="e9769-200">In hello **classe modello** elenco a discesa selezionare il nuovo DTO.</span><span class="sxs-lookup"><span data-stu-id="e9769-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="e9769-201">In hello **DbContext** classe DbContext servizio Mobile hello selezionare elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="e9769-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="e9769-202">nome del Controller Hello viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e9769-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="e9769-203">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e9769-203">Click **Add**.</span></span>

<span data-ttu-id="e9769-204">progetto server di avvio rapido Hello contiene un esempio di una semplice **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="e9769-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="e9769-205"><a name="adjust-pagesize"></a>Procedura: ridimensionare hello tabella paging</span><span class="sxs-lookup"><span data-stu-id="e9769-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="e9769-206">Per impostazione predefinita, App mobili di Azure restituisce 50 record per ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="e9769-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="e9769-207">Paging assicura che il client hello non utilizza i server dell'interfaccia utente di thread né hello troppo a lungo, garantire un'esperienza utente soddisfacente.</span><span class="sxs-lookup"><span data-stu-id="e9769-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="e9769-208">toochange hello tabella dimensioni di paging sul lato server di aumento hello "consentito dimensioni della query" e hello sul lato server hello dimensioni pagina sul lato client "consentito dimensioni della query" viene regolato utilizzando hello `EnableQuery` attributo:</span><span class="sxs-lookup"><span data-stu-id="e9769-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="e9769-209">Verificare che sia di hello PageSize hello uguale o maggiore di dimensione hello richiesta dal client hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="e9769-210">Consultare la documentazione di HOWTO toohello client specifico per informazioni dettagliate sulla modifica delle dimensioni della pagina client hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="e9769-211">Procedura: Definire un controller API personalizzato</span><span class="sxs-lookup"><span data-stu-id="e9769-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="e9769-212">controller API personalizzato Hello fornisce hello più semplice funzionalità tooyour App Mobile back-end esponendo un endpoint.</span><span class="sxs-lookup"><span data-stu-id="e9769-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="e9769-213">È possibile registrare un controller di API specifici dispositivi mobili con attributo hello [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="e9769-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="e9769-214">Hello `MobileAppController` attributi Registra route hello, configura un serializzatore JSON di App mobili hello e attiva [il controllo della versione di client](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e9769-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="e9769-215">In Visual Studio, cartella Controllers di hello pulsante destro del mouse, quindi fare clic su **Aggiungi** > **Controller**selezionare **Web API 2 Controller&mdash;vuoto** e Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e9769-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="e9769-216">Specificare un nome in **Nome controller**, ad esempio `CustomController`, e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e9769-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="e9769-217">In file di classe controller nuovo hello, aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="e9769-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="e9769-218">Applicare hello **[MobileAppController]** attributo definizione della classe controller toohello API, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e9769-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="e9769-219">Nel file di App_Start/Startup.MobileApp.cs, aggiungere una chiamata toohello **MapApiControllers** il metodo di estensione, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e9769-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="e9769-220">È inoltre possibile utilizzare hello `UseDefaultConfiguration()` il metodo di estensione anziché `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="e9769-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="e9769-221">I controller a cui non è applicato **MobileAppControllerAttribute** continuano a essere accessibili da parte dei client, ma potrebbero non essere usati correttamente dai client con l'SDK client di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e9769-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="e9769-222">Procedura: Usare l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="e9769-222">How to: Work with authentication</span></span>
<span data-ttu-id="e9769-223">App per dispositivi mobili Azure utilizza l'autenticazione del servizio App / autorizzazione toosecure mobile back-end.</span><span class="sxs-lookup"><span data-stu-id="e9769-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="e9769-224">In questa sezione illustra come hello tooperform seguenti attività correlate all'autenticazione in un progetto server di back-end .NET:</span><span class="sxs-lookup"><span data-stu-id="e9769-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="e9769-225">Procedura: aggiungere project server tooa di autenticazione</span><span class="sxs-lookup"><span data-stu-id="e9769-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="e9769-226">Procedura: Usare l'autenticazione personalizzata per la propria applicazione</span><span class="sxs-lookup"><span data-stu-id="e9769-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="e9769-227">Procedura: Recuperare le informazioni sull'utente autenticato</span><span class="sxs-lookup"><span data-stu-id="e9769-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="e9769-228">Procedura: Limitare l'accesso ai dati per gli utenti autorizzati</span><span class="sxs-lookup"><span data-stu-id="e9769-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="e9769-229"><a name="add-auth"></a>Procedura: aggiungere project server tooa di autenticazione</span><span class="sxs-lookup"><span data-stu-id="e9769-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="e9769-230">È possibile aggiungere un progetto server di autenticazione tooyour estendendo hello **MobileAppConfiguration** oggetto e la configurazione di middleware OWIN.</span><span class="sxs-lookup"><span data-stu-id="e9769-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="e9769-231">Quando si installa hello [Microsoft.Azure.Mobile.Server.Quickstart] hello pacchetto e chiamare **UseDefaultConfiguration** metodo di estensione, è possibile ignorare toostep 3.</span><span class="sxs-lookup"><span data-stu-id="e9769-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="e9769-232">In Visual Studio, installare hello [Microsoft.Azure.Mobile.Server.Authentication] pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e9769-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="e9769-233">Nel file di progetto Startup.cs hello, aggiungere hello successiva riga di codice all'inizio di hello di hello **configurazione** metodo:</span><span class="sxs-lookup"><span data-stu-id="e9769-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="e9769-234">Questo componente middleware OWIN convalida i token rilasciati da gateway di servizio App hello associata.</span><span class="sxs-lookup"><span data-stu-id="e9769-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="e9769-235">Aggiungere hello `[Authorize]` attributo tooany controller o al metodo che richiede l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="e9769-236">toolearn sulla tooauthenticate client tooyour back-end App per dispositivi mobili, vedere [Aggiungi autenticazione tooyour app](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="e9769-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="e9769-237"><a name="custom-auth"></a>Procedura: Usare l'autenticazione personalizzata per la propria applicazione</span><span class="sxs-lookup"><span data-stu-id="e9769-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="e9769-238">Se non si desidera toouse uno dei provider di autenticazione/autorizzazione del servizio App hello, è possibile implementare il sistema di account di accesso.</span><span class="sxs-lookup"><span data-stu-id="e9769-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="e9769-239">Installare hello [Microsoft.Azure.Mobile.Server.Login] tooassist con generazione di token di autenticazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e9769-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="e9769-240">Fornire il proprio codice per la convalida delle credenziali utente.</span><span class="sxs-lookup"><span data-stu-id="e9769-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="e9769-241">È possibile, ad esempio, confrontare le password con salting e hashing in un database.</span><span class="sxs-lookup"><span data-stu-id="e9769-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="e9769-242">Nel seguente esempio hello hello `isValidAssertion()` metodo (definito altrove) è responsabile di questi controlli.</span><span class="sxs-lookup"><span data-stu-id="e9769-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="e9769-243">autenticazione personalizzata Hello viene esposto tramite la creazione di un ApiController e l'esposizione di `register` e `login` azioni.</span><span class="sxs-lookup"><span data-stu-id="e9769-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="e9769-244">client Hello deve utilizzare una personalizzata dell'interfaccia utente toocollect hello le informazioni utente hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="e9769-245">informazioni di Hello sono chiamare inviato toohello API con un POST HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="e9769-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="e9769-246">Una volta server hello convalida asserzione hello, viene emesso un token utilizzando hello `AppServiceLoginHandler.CreateToken()` metodo.</span><span class="sxs-lookup"><span data-stu-id="e9769-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="e9769-247">Hello ApiController **non** utilizzare hello `[MobileAppController]` attributo.</span><span class="sxs-lookup"><span data-stu-id="e9769-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="e9769-248">Azione `login` di esempio:</span><span class="sxs-lookup"><span data-stu-id="e9769-248">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="e9769-249">In hello sopra riportato, LoginResult e LoginResultUser sono oggetti serializzabili che espone le proprietà necessarie.</span><span class="sxs-lookup"><span data-stu-id="e9769-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="e9769-250">client Hello prevede l'account di accesso risposte toobe restituiti come oggetti JSON del modulo hello:</span><span class="sxs-lookup"><span data-stu-id="e9769-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="e9769-251">Hello `AppServiceLoginHandler.CreateToken()` metodo include un *destinatari* e *dell'autorità di certificazione* parametro.</span><span class="sxs-lookup"><span data-stu-id="e9769-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="e9769-252">Entrambi questi parametri vengono impostate URL toohello della directory radice dell'applicazione utilizzando lo schema HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="e9769-253">Analogamente è necessario impostare *secretKey* chiave di firma del valore di hello toobe dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="e9769-254">Non distribuire hello chiave in un client per la firma come può essere utilizzato toomint chiavi e rappresentare gli utenti.</span><span class="sxs-lookup"><span data-stu-id="e9769-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="e9769-255">È possibile ottenere hello firma chiave mentre ospitato nel servizio App facendo riferimento hello *sito Web\_AUTH\_firma\_chiave* variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="e9769-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="e9769-256">Se necessario in un contesto di debug locale, attenersi alle istruzioni hello hello [il debug locale con l'autenticazione](#local-debug) sezione chiave hello tooretrieve e archiviarle come un'impostazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="e9769-257">il token emesso Hello può includere anche altre attestazioni e una data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="e9769-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="e9769-258">Come minimo, il token emesso hello deve includere un oggetto (**sub**) di attestazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="e9769-259">È possibile supportare client standard hello `loginAsync()` metodo route autenticazione hello l'overload.</span><span class="sxs-lookup"><span data-stu-id="e9769-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="e9769-260">Se il client hello chiama `client.loginAsync('custom');` toolog in, il route deve essere `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="e9769-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="e9769-261">È possibile impostare route hello per l'utilizzo di controller di autenticazione personalizzata hello `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="e9769-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="e9769-262">Utilizzando hello `loginAsync()` assicura è collegato il token di autenticazione hello tooevery chiamata successiva toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="e9769-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="e9769-263"><a name="user-info"></a>Procedura: Recuperare le informazioni sull'utente autenticato</span><span class="sxs-lookup"><span data-stu-id="e9769-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="e9769-264">Quando un utente viene autenticato dal servizio App, è possibile accedere hello assegnato ID utente e altre informazioni nel codice di back-end .NET.</span><span class="sxs-lookup"><span data-stu-id="e9769-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="e9769-265">informazioni utente Hello è utilizzabile per prendere decisioni di autorizzazione nel back-end hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="e9769-266">Hello codice seguente ottiene l'ID utente hello associata a una richiesta:</span><span class="sxs-lookup"><span data-stu-id="e9769-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="e9769-267">Hello SID derivato dall'ID utente specifico del provider hello e static per un determinato utente e i provider di accesso.</span><span class="sxs-lookup"><span data-stu-id="e9769-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="e9769-268">Hello SID è null per i token di autenticazione non valido.</span><span class="sxs-lookup"><span data-stu-id="e9769-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="e9769-269">Il servizio app consente anche di richiedere le attestazioni specifiche dal provider di accesso.</span><span class="sxs-lookup"><span data-stu-id="e9769-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="e9769-270">Ogni provider di identità può fornire altre informazioni usando l'SDK del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="e9769-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="e9769-271">Ad esempio, è possibile utilizzare hello API Graph di Facebook per informazioni di amici.</span><span class="sxs-lookup"><span data-stu-id="e9769-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="e9769-272">Nel Pannello di provider hello in hello portale di Azure, è possibile specificare le attestazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="e9769-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="e9769-273">Alcune richieste richiedono un'ulteriore configurazione con il provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="e9769-274">esempio di codice seguente Hello hello chiamate **GetAppServiceIdentityAsync** estensione metodo tooget hello le credenziali di accesso, che includono le richieste di token toomake necessari accesso hello contro hello API Graph di Facebook:</span><span class="sxs-lookup"><span data-stu-id="e9769-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="e9769-275">Aggiungere un tramite l'istruzione per `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** metodo di estensione.</span><span class="sxs-lookup"><span data-stu-id="e9769-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="e9769-276"><a name="authorize"></a>Procedura: Limitare l’accesso ai dati per gli utenti autorizzati</span><span class="sxs-lookup"><span data-stu-id="e9769-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="e9769-277">Nella sezione precedente hello, abbiamo anche mostrato come tooretrieve hello ID utente di un utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="e9769-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="e9769-278">È possibile limitare l'accesso toodata e altre risorse in base a questo valore.</span><span class="sxs-lookup"><span data-stu-id="e9769-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="e9769-279">Ad esempio, l'aggiunta di un tootables colonna ID utente e filtro dei risultati di query hello dall'ID utente hello è toolimit un modo semplice restituiti dati solo tooauthorized gli utenti.</span><span class="sxs-lookup"><span data-stu-id="e9769-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="e9769-280">Hello codice seguente restituisce le righe di dati solo quando hello SID corrisponde al valore nella colonna di ID utente hello nella tabella TodoItem hello:</span><span class="sxs-lookup"><span data-stu-id="e9769-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="e9769-281">Hello `Query()` metodo restituisce un `IQueryable` che può essere modificato dal filtro toohandle LINQ.</span><span class="sxs-lookup"><span data-stu-id="e9769-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="e9769-282">Procedura: aggiungere project server tooa le notifiche di push</span><span class="sxs-lookup"><span data-stu-id="e9769-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="e9769-283">Aggiungi progetto server tooyour di notifiche push estendendo hello **MobileAppConfiguration** oggetto e la creazione di un client di hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="e9769-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="e9769-284">In Visual Studio, fare clic sul progetto server hello e fare clic su **Gestisci pacchetti NuGet**, cercare `Microsoft.Azure.Mobile.Server.Notifications`, quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="e9769-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="e9769-285">Ripetere questo hello tooinstall passaggio `Microsoft.Azure.NotificationHubs` pacchetto, che include una libreria client di hello hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="e9769-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="e9769-286">In App_Start/Startup.MobileApp.cs e aggiungere una chiamata toohello **AddPushNotifications()** il metodo di estensione durante l'inizializzazione:</span><span class="sxs-lookup"><span data-stu-id="e9769-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="e9769-287">Aggiungere hello dopo il codice che crea un client di hub di notifica:</span><span class="sxs-lookup"><span data-stu-id="e9769-287">Add hello following code that creates a Notification Hubs client:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="e9769-288">È ora possibile usare dispositivi tooregistered hello hub di notifica client toosend push delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="e9769-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="e9769-289">Per ulteriori informazioni, vedere [Aggiungi push notifiche tooyour app](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="e9769-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="e9769-290">toolearn più sugli hub di notifica, vedere [Panoramica di hub di notifica](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9769-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="e9769-291"><a name="tags"></a>Procedura: Abilitare le notifiche push mirate usando i tag</span><span class="sxs-lookup"><span data-stu-id="e9769-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="e9769-292">Gli hub di notifica consente di inviare notifiche destinazione toospecific registrazioni con tag.</span><span class="sxs-lookup"><span data-stu-id="e9769-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="e9769-293">Diversi tag vengono creati automaticamente:</span><span class="sxs-lookup"><span data-stu-id="e9769-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="e9769-294">ID di installazione Hello identifica un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="e9769-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="e9769-295">Hello Id utente in base alle hello autenticato SID identifica un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="e9769-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="e9769-296">Hello installazione ID è possibile accedere da hello **installationId** proprietà hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="e9769-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="e9769-297">Hello esempio seguente viene illustrato come utilizzare un tooadd ID installazione un'installazione specifica di tag tooa nell'hub di notifica:</span><span class="sxs-lookup"><span data-stu-id="e9769-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="e9769-298">Qualsiasi tag forniti dal client hello durante la registrazione della notifica push vengono ignorate dal back-end hello durante la creazione di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="e9769-299">installazione toohello i tag tooenable tooadd un client, è necessario creare un'API personalizzata che consente di aggiungere tag usando hello modello precedente.</span><span class="sxs-lookup"><span data-stu-id="e9769-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="e9769-300">Vedere [tag di notifica push Client aggiunto] [ 5] nell'esempio di Guida introduttiva completato hello servizio App dell'App Mobile per un esempio.</span><span class="sxs-lookup"><span data-stu-id="e9769-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="e9769-301"><a name="push-user"></a>Procedura: tooan di notifiche push trasmissione l'utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="e9769-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="e9769-302">Quando un utente autenticato registrati per le notifiche push, un tag di ID utente viene aggiunto automaticamente toohello registrazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="e9769-303">Con questo tag, è possibile inviare registrati da questa persona dispositivi tooall di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="e9769-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="e9769-304">Hello codice seguente ottiene hello SID dell'utente che effettua la richiesta e invia una registrazione di modello push notifica tooevery dispositivo per tale persona:</span><span class="sxs-lookup"><span data-stu-id="e9769-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="e9769-305">Durante la registrazione per le notifiche push da un client autenticato, assicurarsi che l'autenticazione sia stata completata prima di tentare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="e9769-306">Per ulteriori informazioni, vedere [Push toousers] [ 6] nell'esempio di Guida introduttiva completato hello App per dispositivi mobili del servizio App di back-end .NET.</span><span class="sxs-lookup"><span data-stu-id="e9769-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="e9769-307">Procedura: eseguire il Debug e risoluzione dei problemi hello .NET Server SDK</span><span class="sxs-lookup"><span data-stu-id="e9769-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="e9769-308">Il servizio app di Azure offre diverse tecniche di debug e risoluzione dei problemi per le applicazioni ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="e9769-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="e9769-309">Monitoraggio di un servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="e9769-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="e9769-310">Abilitazione della registrazione diagnostica nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="e9769-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="e9769-311">Risoluzione dei problemi di un Servizio app di Azure in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e9769-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="e9769-312">Registrazione</span><span class="sxs-lookup"><span data-stu-id="e9769-312">Logging</span></span>
<span data-ttu-id="e9769-313">È possibile scrivere i log di diagnostica servizio tooApp mediante scrittura di traccia ASP.NET standard hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="e9769-314">Prima di scrivere log toohello, è necessario attivare la diagnostica di back-end App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e9769-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="e9769-315">tooenable di diagnostica e di scrittura toohello registri:</span><span class="sxs-lookup"><span data-stu-id="e9769-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="e9769-316">Seguire i passaggi di hello in [come diagnostica tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="e9769-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="e9769-317">Aggiungere hello seguente istruzione using nel file di codice:</span><span class="sxs-lookup"><span data-stu-id="e9769-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="e9769-318">Creare un toowrite writer di traccia da hello .NET back-end toohello i log di diagnostica, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e9769-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="e9769-319">Pubblicare il progetto server e accedere hello App Mobile back-end tooexecute hello percorso del codice con la registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="e9769-320">Scaricare e valutare i log di hello, come descritto in [procedura: scaricare i log](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="e9769-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="e9769-321"><a name="local-debug"></a>Debug locale con autenticazione</span><span class="sxs-lookup"><span data-stu-id="e9769-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="e9769-322">È possibile eseguire l'applicazione localmente tootest modifiche prima di pubblicarli toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="e9769-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="e9769-323">Per la maggior parte dei back-end di App per dispositivi mobili di Azure, premere *F5* in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9769-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="e9769-324">Esistono però alcune considerazioni aggiuntive quando si usa l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="e9769-325">È necessario disporre di un'app per dispositivi mobili basati su cloud con applicazione servizio di autenticazione/autorizzazione configurato e il client deve disporre di endpoint di cloud hello specificato come host di accesso alternativo hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="e9769-326">Vedere la documentazione di hello per la piattaforma del client per i passaggi specifici di hello necessari.</span><span class="sxs-lookup"><span data-stu-id="e9769-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="e9769-327">Verificare che nel back-end mobile sia installato [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="e9769-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="e9769-328">Quindi, nella classe di avvio dell'applicazione OWIN, aggiungere seguenti hello, dopo `MobileAppConfiguration` è stato applicato tooyour `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="e9769-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="e9769-329">In hello sopra riportato, è necessario configurare hello *authAudience* e *authIssuer* le impostazioni dell'applicazione nel file Web. config file tooeach essere l'URL della directory radice dell'applicazione utilizzando hello HTTPS schema.</span><span class="sxs-lookup"><span data-stu-id="e9769-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="e9769-330">Analogamente è necessario impostare *authSigningKey* chiave di firma del valore di hello toobe dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e9769-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="e9769-331">chiave di firma hello tooobtain:</span><span class="sxs-lookup"><span data-stu-id="e9769-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="e9769-332">Esplorare app tooyour all'interno di hello [portale di Azure]</span><span class="sxs-lookup"><span data-stu-id="e9769-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="e9769-333">Fare clic su **Strumenti**, **Kudu**, **Vai**.</span><span class="sxs-lookup"><span data-stu-id="e9769-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="e9769-334">Nel sito di gestione di Kudu hello, fare clic su **ambiente**.</span><span class="sxs-lookup"><span data-stu-id="e9769-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="e9769-335">Trovare il valore di hello per *sito Web\_AUTH\_firma\_chiave*.</span><span class="sxs-lookup"><span data-stu-id="e9769-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="e9769-336">Hello utilizzare firma chiave per hello *authSigningKey* parametro nel file config dell'applicazione locale.  Il back-end per dispositivi mobili è ora token toovalidate forniti durante l'esecuzione in locale, quali client hello Ottiene token hello dall'endpoint basato su cloud hello.</span><span class="sxs-lookup"><span data-stu-id="e9769-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portale di Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
