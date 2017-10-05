---
title: Come usare l'SDK del server back-end .NET per App per dispositivi mobili | Microsoft Docs
description: Informazioni su come usare l'SDK del server back-end .NET per App per dispositivi mobili del servizio app di Azure.
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
ms.openlocfilehash: 657fea16e47c15efd262c86d6a150a721476134a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="8804e-104">Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="8804e-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="8804e-105">Questo argomento mostra come usare l'SDK del server back-end .NET in scenari chiave di App per dispositivi mobili del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="8804e-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="8804e-106">Azure Mobile Apps SDK aiuta a lavorare con i client mobili dall'applicazione ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8804e-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="8804e-107">L'[SDK del server .NET per App per dispositivi mobili][2] di Azure è open source su GitHub.</span><span class="sxs-lookup"><span data-stu-id="8804e-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="8804e-108">Il repository contiene tutto il codice sorgente, incluso l'intero gruppo di unit test dell'SDK del server, e alcuni progetti di esempio.</span><span class="sxs-lookup"><span data-stu-id="8804e-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="8804e-109">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="8804e-109">Reference documentation</span></span>
<span data-ttu-id="8804e-110">La documentazione di riferimento per l'SDK del server è disponibile qui: [Riferimento .NET di App per dispositivi mobili di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="8804e-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="8804e-111"><a name="create-app"></a>Procedura: Creare un back-end dell'app per dispositivi mobili .NET</span><span class="sxs-lookup"><span data-stu-id="8804e-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="8804e-112">Se si inizia un nuovo progetto, è possibile creare un'applicazione del servizio app usando il [portale di Azure] o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8804e-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="8804e-113">È possibile eseguire l'applicazione del servizio app localmente o pubblicare il progetto nell'app per dispositivi mobili del servizio app basata sul cloud.</span><span class="sxs-lookup"><span data-stu-id="8804e-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>

<span data-ttu-id="8804e-114">Se si devono aggiungere funzionalità per dispositivi mobili a un progetto esistente, vedere la sezione [Scaricare e inizializzare l'SDK](#install-sdk) .</span><span class="sxs-lookup"><span data-stu-id="8804e-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="8804e-115">Creare un back-end .NET usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8804e-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="8804e-116">Per creare un back-end per dispositivi mobili del servizio app, seguire l'[esercitazione introduttiva][3] oppure questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="8804e-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="8804e-117">Nel pannello *Attività iniziali* in **Create a table API** (Creare un'API di tabella) scegliere **C#** come **Backend language** (Linguaggio back-end).</span><span class="sxs-lookup"><span data-stu-id="8804e-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="8804e-118">Fare clic su **Download**, estrarre i file di progetto compressi nel computer locale e aprire la soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8804e-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="8804e-119">Creare un back-end .NET usando Visual Studio 2013 e Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="8804e-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="8804e-120">Per creare un progetto App per dispositivi mobili di Azure in Visual Studio, installare [Azure SDK per .NET][4] (versione 2.9.0 o successiva).</span><span class="sxs-lookup"><span data-stu-id="8804e-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="8804e-121">Dopo avere installato l'SDK, creare un'applicazione ASP.NET seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8804e-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="8804e-122">Aprire la finestra di dialogo **Nuovo progetto** (da *File* > **Nuovo** > **Progetto...**).</span><span class="sxs-lookup"><span data-stu-id="8804e-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="8804e-123">Espandere **Modelli** > **Visual C#** e selezionare **Web**.</span><span class="sxs-lookup"><span data-stu-id="8804e-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="8804e-124">Selezionare **Applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="8804e-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="8804e-125">Immettere il nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="8804e-125">Fill in the project name.</span></span> <span data-ttu-id="8804e-126">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8804e-126">Then click **OK**.</span></span>
5. <span data-ttu-id="8804e-127">In *Modelli ASP.NET 4.5.2* selezionare **App mobile di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8804e-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="8804e-128">Selezionare **Host nel cloud** per creare un back-end mobile nel cloud in cui è possibile pubblicare questo progetto.</span><span class="sxs-lookup"><span data-stu-id="8804e-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="8804e-129">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8804e-129">Click **OK**.</span></span>

## <span data-ttu-id="8804e-130"><a name="install-sdk"></a>Procedura: Scaricare e inizializzare l'SDK</span><span class="sxs-lookup"><span data-stu-id="8804e-130"><a name="install-sdk"></a>How to: Download and initialize the SDK</span></span>
<span data-ttu-id="8804e-131">L'SDK è disponibile in [NuGet.org].</span><span class="sxs-lookup"><span data-stu-id="8804e-131">The SDK is available on [NuGet.org].</span></span> <span data-ttu-id="8804e-132">Il pacchetto include le funzionalità di base necessarie per iniziare a usare l'SDK.</span><span class="sxs-lookup"><span data-stu-id="8804e-132">This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="8804e-133">Per inizializzare l'SDK, è necessario eseguire alcune operazioni nell'oggetto **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="8804e-133">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="8804e-134">Installare l'SDK</span><span class="sxs-lookup"><span data-stu-id="8804e-134">Install the SDK</span></span>
<span data-ttu-id="8804e-135">Per installare l'SDK, fare clic con il pulsante destro del mouse sul progetto server in Visual Studio, scegliere **Gestisci pacchetti NuGet**, cercare il pacchetto [Microsoft.Azure.Mobile.Server] e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="8804e-135">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="8804e-136"><a name="server-project-setup"></a> Inizializzare il progetto server</span><span class="sxs-lookup"><span data-stu-id="8804e-136"><a name="server-project-setup"></a> Initialize the server project</span></span>
<span data-ttu-id="8804e-137">Un progetto server back-end .NET viene inizializzato in modo simile ad altri progetti ASP.NET, includendo una classe di avvio OWIN.</span><span class="sxs-lookup"><span data-stu-id="8804e-137">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="8804e-138">Assicurarsi che si sia fatto riferimento al pacchetto NuGet `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="8804e-138">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="8804e-139">Per aggiungere questa classe in Visual Studio, fare clic con il pulsante destro del mouse sul progetto server e scegliere **Aggiungi** >
**Nuovo elemento**, quindi **Web** > **Generale** > **Classe di avvio di OWIN**.</span><span class="sxs-lookup"><span data-stu-id="8804e-139">To add this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="8804e-140">Viene generata una classe con l'attributo seguente:</span><span class="sxs-lookup"><span data-stu-id="8804e-140">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="8804e-141">Nel metodo `Configuration()` della classe di avvio OWIN usare un oggetto **HttpConfiguration** per configurare l'ambiente di App per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="8804e-141">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="8804e-142">L'esempio seguente inizializza il progetto server senza funzionalità aggiuntive:</span><span class="sxs-lookup"><span data-stu-id="8804e-142">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="8804e-143">Per abilitare le singole funzionalità, è necessario chiamare i metodi di estensione nell'oggetto **MobileAppConfiguration** prima di chiamare **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="8804e-143">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="8804e-144">Ad esempio, il codice seguente aggiunge le route predefinite a tutti i controller API che hanno l'attributo `[MobileAppController]` durante l'inizializzazione:</span><span class="sxs-lookup"><span data-stu-id="8804e-144">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="8804e-145">L'avvio rapido del server nel portale di Azure chiama **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="8804e-145">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="8804e-146">Questo equivale alla configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="8804e-146">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="8804e-147">I metodi di estensione usati sono:</span><span class="sxs-lookup"><span data-stu-id="8804e-147">The extension methods used are:</span></span>

* <span data-ttu-id="8804e-148">`AddMobileAppHomeController()` fornisce la home page di App per dispositivi mobili di Azure predefinita.</span><span class="sxs-lookup"><span data-stu-id="8804e-148">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="8804e-149">`MapApiControllers()` fornisce le funzionalità API per i controller WebAPI decorati con l'attributo `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="8804e-149">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="8804e-150">`AddTables()` fornisce una mapping degli endpoint `/tables` ai controller delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="8804e-150">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="8804e-151">`AddTablesWithEntityFramework()` è una sintassi abbreviata per il mapping degli endpoint `/tables` con i controller basati su Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="8804e-151">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="8804e-152">`AddPushNotifications()` fornisce un semplice metodo di registrazione dei dispositivi per Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="8804e-152">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="8804e-153">`MapLegacyCrossDomainController()` fornisce intestazioni CORS standard per lo sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="8804e-153">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="8804e-154">Estensioni SDK</span><span class="sxs-lookup"><span data-stu-id="8804e-154">SDK extensions</span></span>
<span data-ttu-id="8804e-155">I pacchetti di estensione basati su NuGet seguenti forniscono diverse funzionalità per dispositivi mobili che l'applicazione può usare.</span><span class="sxs-lookup"><span data-stu-id="8804e-155">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="8804e-156">È possibile abilitare le estensioni durante l'inizializzazione usando l'oggetto **MobileAppConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="8804e-156">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="8804e-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supporta la configurazione di base di app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8804e-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="8804e-158">Viene aggiunta alla configurazione chiamando il metodo di estensione **UseDefaultConfiguration** durante l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-158">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="8804e-159">Questa estensione include le estensioni seguenti: pacchetti Notifications, Authentication, Entity, Tables, Crossdomain e Home.</span><span class="sxs-lookup"><span data-stu-id="8804e-159">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="8804e-160">Questo pacchetto viene usato da Avvio rapido di App per dispositivi mobili disponibile nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8804e-160">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="8804e-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implementa la pagina predefinita *this mobile app is up and running* per la radice del sito Web.</span><span class="sxs-lookup"><span data-stu-id="8804e-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="8804e-162">Viene aggiunta alla configurazione chiamando il metodo di estensione **AddMobileAppHomeController** .</span><span class="sxs-lookup"><span data-stu-id="8804e-162">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="8804e-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) include le classi per usare i dati e configura la pipeline dei dati.</span><span class="sxs-lookup"><span data-stu-id="8804e-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="8804e-164">Viene aggiunta alla configurazione chiamando il metodo di estensione **AddTables** .</span><span class="sxs-lookup"><span data-stu-id="8804e-164">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="8804e-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) consente a Entity Framework di accedere ai dati nel database SQL.</span><span class="sxs-lookup"><span data-stu-id="8804e-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="8804e-166">Viene aggiunta alla configurazione chiamando il metodo di estensione **AddTablesWithEntityFramework** .</span><span class="sxs-lookup"><span data-stu-id="8804e-166">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="8804e-167">[Microsoft.Azure.Mobile.Server.Authentication] Consente l'autenticazione e configura il middleware OWIN usato per convalidare i token.</span><span class="sxs-lookup"><span data-stu-id="8804e-167">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="8804e-168">Viene aggiunta alla configurazione chiamando i metodi di estensione **AddAppServiceAuthentication** e **IAppBuilder**.**UseAppServiceAuthentication**.</span><span class="sxs-lookup"><span data-stu-id="8804e-168">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="8804e-169">[Microsoft.Azure.Mobile.Server.Notifications] Consente le notifiche push e definisce un endpoint di registrazione push.</span><span class="sxs-lookup"><span data-stu-id="8804e-169">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="8804e-170">Viene aggiunta alla configurazione chiamando il metodo di estensione **AddPushNotifications** .</span><span class="sxs-lookup"><span data-stu-id="8804e-170">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="8804e-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Crea un controller che fornisce i dati ai Web browser legacy dall'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8804e-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="8804e-172">Viene aggiunta alla configurazione chiamando il metodo di estensione **MapLegacyCrossDomainController** .</span><span class="sxs-lookup"><span data-stu-id="8804e-172">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="8804e-173">[Microsoft.Azure.Mobile.Server.Login] offre il metodo AppServiceLoginHandler.CreateToken(), che è un metodo statico usato negli scenari di autenticazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8804e-173">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="8804e-174"><a name="publish-server-project"></a>Procedura: Pubblicare il progetto server</span><span class="sxs-lookup"><span data-stu-id="8804e-174"><a name="publish-server-project"></a>How to: Publish the server project</span></span>
<span data-ttu-id="8804e-175">Questa sezione illustra come pubblicare il progetto back-end .NET da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8804e-175">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="8804e-176">È anche possibile distribuire il progetto back-end usando Git o uno degli altri metodi illustrati nella [documentazione sulla distribuzione del servizio app di Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8804e-176">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="8804e-177">In Visual Studio compilare nuovamente il progetto per ripristinare i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="8804e-177">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="8804e-178">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="8804e-178">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="8804e-179">La prima volta che si crea una pubblicazione, è necessario definire un profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-179">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="8804e-180">Se si ha già un profilo definito, è possibile selezionarlo e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="8804e-180">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="8804e-181">Se viene richiesto di selezionare una destinazione di pubblicazione, fare clic su **Servizio app di Microsoft Azure** > **Avanti** e quindi, se necessario, accedere con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="8804e-181">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="8804e-182">Visual Studio scaricherà e memorizzerà le impostazioni di pubblicazione direttamente da Azure.</span><span class="sxs-lookup"><span data-stu-id="8804e-182">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="8804e-183">Scegliere la **Sottoscrizione**, selezionare **Tipo di risorsa** da **Visualizza**, espandere **App per dispositivi mobili** e fare clic sul back-end di App per dispositivi mobili, quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8804e-183">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="8804e-184">Verificare le informazioni sul profilo di pubblicazione e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="8804e-184">Verify the publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="8804e-185">Quando il back-end dell'app per dispositivi mobili ha eseguito la pubblicazione, viene visualizzata una pagina di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-185">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="8804e-186"><a name="define-table-controller"></a> Procedura: Definire un controller tabelle</span><span class="sxs-lookup"><span data-stu-id="8804e-186"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="8804e-187">Definire un controller tabelle per esporre una tabella SQL ai client per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8804e-187">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="8804e-188">Per configurare un controller tabelle, sono necessari tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="8804e-188">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="8804e-189">Creare una classe di oggetti di trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="8804e-189">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="8804e-190">Configurare un riferimento a tabella nella classe DbContext per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8804e-190">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="8804e-191">Creare un controller tabelle.</span><span class="sxs-lookup"><span data-stu-id="8804e-191">Create a table controller.</span></span>

<span data-ttu-id="8804e-192">Un oggetto di trasferimento dei dati è un oggetto C# normale che eredita `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="8804e-192">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="8804e-193">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8804e-193">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="8804e-194">L'oggetto di trasferimento dei dati viene usato per definire la tabella nel database SQL.</span><span class="sxs-lookup"><span data-stu-id="8804e-194">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="8804e-195">Per creare la voce del database, aggiungere una proprietà `DbSet<>` alla classe DbContext usata.</span><span class="sxs-lookup"><span data-stu-id="8804e-195">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="8804e-196">Nel modello di progetto predefinito per App per dispositivi mobili di Azure DbContext è chiamata `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="8804e-196">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="8804e-197">Se Azure SDK è installato, ora è possibile creare un controller tabelle per il modello, come segue:</span><span class="sxs-lookup"><span data-stu-id="8804e-197">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="8804e-198">Fare clic con il pulsante destro del mouse sulla cartella Controller e quindi scegliere **Aggiungi** > **Controller**.</span><span class="sxs-lookup"><span data-stu-id="8804e-198">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="8804e-199">Selezionare l'opzione **Controller tabelle di App mobili di Azure**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8804e-199">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="8804e-200">Nella finestra di dialogo **Aggiungi controller** :</span><span class="sxs-lookup"><span data-stu-id="8804e-200">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="8804e-201">Nell'elenco a discesa **Classe modello** selezionare il nuovo oggetto di trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="8804e-201">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="8804e-202">Nell'elenco a discesa **DbContext** selezionare la classe DbContext di Servizi mobili.</span><span class="sxs-lookup"><span data-stu-id="8804e-202">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="8804e-203">Viene automaticamente creato il nome Controller.</span><span class="sxs-lookup"><span data-stu-id="8804e-203">The Controller name is created for you.</span></span>
4. <span data-ttu-id="8804e-204">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8804e-204">Click **Add**.</span></span>

<span data-ttu-id="8804e-205">Il progetto server di Avvio rapido contiene un esempio di **TodoItemController**semplice.</span><span class="sxs-lookup"><span data-stu-id="8804e-205">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="8804e-206"><a name="adjust-pagesize"></a>Procedura: Modificare le dimensioni di paging delle tabelle</span><span class="sxs-lookup"><span data-stu-id="8804e-206"><a name="adjust-pagesize"></a>How to: Adjust the table paging size</span></span>
<span data-ttu-id="8804e-207">Per impostazione predefinita, App mobili di Azure restituisce 50 record per ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="8804e-207">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="8804e-208">Il paging garantisce che il client non occupi il thread dell'interfaccia utente o il server troppo a lungo e quindi un'esperienza utente ottimale.</span><span class="sxs-lookup"><span data-stu-id="8804e-208">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="8804e-209">Per modificare le dimensioni di paging delle tabelle, aumentare le "dimensioni della query consentite" lato server e le dimensioni della pagina lato client. Le "dimensioni della query consentite" lato server vengono regolate usando l'attributo `EnableQuery`:</span><span class="sxs-lookup"><span data-stu-id="8804e-209">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="8804e-210">Verificare che il valore di PageSize sia uguale o maggiore delle dimensioni richieste dal client.</span><span class="sxs-lookup"><span data-stu-id="8804e-210">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="8804e-211">Fare riferimento alle procedure specifiche del client per informazioni dettagliate su come modificare le dimensioni di pagina del client.</span><span class="sxs-lookup"><span data-stu-id="8804e-211">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="8804e-212">Procedura: Definire un controller API personalizzato</span><span class="sxs-lookup"><span data-stu-id="8804e-212">How to: Define a custom API controller</span></span>
<span data-ttu-id="8804e-213">Il controller API personalizzato fornisce le funzionalità di base per il back-end dell'app per dispositivi mobili esponendo un endpoint.</span><span class="sxs-lookup"><span data-stu-id="8804e-213">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="8804e-214">È possibile registrare un controller API specifico per dispositivi mobili usando l'attributo [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="8804e-214">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="8804e-215">L'attributo `MobileAppController` registra la route, configura il serializzatore JSON delle app per dispositivi mobili e attiva i [controlli di versione client](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="8804e-215">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="8804e-216">In Visual Studio fare clic con il pulsante destro del mouse sulla cartella Controller e quindi scegliere **Aggiungi** > **Controller**, selezionare **Controller API Web 2&mdash;Vuoto** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8804e-216">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="8804e-217">Specificare un nome in **Nome controller**, ad esempio `CustomController`, e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8804e-217">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="8804e-218">Nella nuovo file della classe controller aggiungere l'istruzione using seguente:</span><span class="sxs-lookup"><span data-stu-id="8804e-218">In the new controller class file, add the following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="8804e-219">Applicare l'attributo **[MobileAppController]** alla definizione di classe controller API, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8804e-219">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="8804e-220">Nel file App_Start/Startup.MobileApp.cs aggiungere una chiamata al metodo di estensione **MapApiControllers**, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8804e-220">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="8804e-221">È anche possibile usare il metodo di estensione `UseDefaultConfiguration()` invece di `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="8804e-221">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="8804e-222">I controller a cui non è applicato **MobileAppControllerAttribute** continuano a essere accessibili da parte dei client, ma potrebbero non essere usati correttamente dai client con l'SDK client di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8804e-222">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="8804e-223">Procedura: Usare l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="8804e-223">How to: Work with authentication</span></span>
<span data-ttu-id="8804e-224">App per dispositivi mobili di Azure usa l'autenticazione/autorizzazione del servizio app per proteggere il back-end mobile.</span><span class="sxs-lookup"><span data-stu-id="8804e-224">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="8804e-225">Questa sezione illustra come eseguire le attività seguenti relative all'autenticazione nel progetto server back-end .NET:</span><span class="sxs-lookup"><span data-stu-id="8804e-225">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="8804e-226">Procedura: Aggiungere l'autenticazione a un progetto server</span><span class="sxs-lookup"><span data-stu-id="8804e-226">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="8804e-227">Procedura: Usare l'autenticazione personalizzata per la propria applicazione</span><span class="sxs-lookup"><span data-stu-id="8804e-227">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="8804e-228">Procedura: Recuperare le informazioni sull'utente autenticato</span><span class="sxs-lookup"><span data-stu-id="8804e-228">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="8804e-229">Procedura: Limitare l'accesso ai dati per gli utenti autorizzati</span><span class="sxs-lookup"><span data-stu-id="8804e-229">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="8804e-230"><a name="add-auth"></a>Procedura: Aggiungere l'autenticazione a un progetto server</span><span class="sxs-lookup"><span data-stu-id="8804e-230"><a name="add-auth"></a>How to: Add authentication to a server project</span></span>
<span data-ttu-id="8804e-231">È possibile aggiungere l'autenticazione al progetto server estendendo l'oggetto **MobileAppConfiguration** e configurando il middleware OWIN.</span><span class="sxs-lookup"><span data-stu-id="8804e-231">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="8804e-232">Quando si installa il pacchetto [Microsoft.Azure.Mobile.Server.Quickstart] e si chiama il metodo di estensione **UseDefaultConfiguration** , è possibile andare al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="8804e-232">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="8804e-233">In Visual Studio installare il pacchetto [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="8804e-233">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="8804e-234">Nel file di progetto Startup.cs aggiungere la riga di codice seguente all'inizio del metodo **Configuration** :</span><span class="sxs-lookup"><span data-stu-id="8804e-234">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="8804e-235">Questo componente del middleware OWIN convalida i token rilasciati dal gateway del servizio app associato.</span><span class="sxs-lookup"><span data-stu-id="8804e-235">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="8804e-236">Aggiungere l'attributo `[Authorize]` a qualsiasi controller o metodo che richiede l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-236">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span>

<span data-ttu-id="8804e-237">Per informazioni su come autenticare i client nel back-end di App per dispositivi mobili, vedere l'articolo [Aggiungere l'autenticazione all'app](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="8804e-237">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="8804e-238"><a name="custom-auth"></a>Procedura: Usare l'autenticazione personalizzata per la propria applicazione</span><span class="sxs-lookup"><span data-stu-id="8804e-238"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="8804e-239">Se non si vuole usare uno dei provider di autenticazione/autorizzazione del servizio app, è possibile implementare il proprio sistema di accesso.</span><span class="sxs-lookup"><span data-stu-id="8804e-239">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="8804e-240">Installare il pacchetto [Microsoft.Azure.Mobile.Server.Login] per facilitare la generazione dei token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-240">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="8804e-241">Fornire il proprio codice per la convalida delle credenziali utente.</span><span class="sxs-lookup"><span data-stu-id="8804e-241">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="8804e-242">È possibile, ad esempio, confrontare le password con salting e hashing in un database.</span><span class="sxs-lookup"><span data-stu-id="8804e-242">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="8804e-243">Nell'esempio seguente il metodo `isValidAssertion()` (definito altrove) è responsabile di questi controlli.</span><span class="sxs-lookup"><span data-stu-id="8804e-243">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="8804e-244">L'autenticazione personalizzata viene esposta creando un ApiController ed esponendo le azioni `register` e `login`.</span><span class="sxs-lookup"><span data-stu-id="8804e-244">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="8804e-245">Il client dovrà usare un'interfaccia utente personalizzata per raccogliere le informazioni dall'utente.</span><span class="sxs-lookup"><span data-stu-id="8804e-245">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="8804e-246">Le informazioni vengono quindi inviate all'API con una chiamata HTTP POST standard.</span><span class="sxs-lookup"><span data-stu-id="8804e-246">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="8804e-247">Dopo la convalida dell'asserzione da parte del server, viene rilasciato un token con il metodo `AppServiceLoginHandler.CreateToken()` .</span><span class="sxs-lookup"><span data-stu-id="8804e-247">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="8804e-248">ApiController **non dovrà** usare l'attributo `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="8804e-248">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="8804e-249">Azione `login` di esempio:</span><span class="sxs-lookup"><span data-stu-id="8804e-249">An example `login` action:</span></span>

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

<span data-ttu-id="8804e-250">Nell'esempio precedente LoginResult e LoginResultUser sono oggetti serializzabili che espongono le proprietà necessarie.</span><span class="sxs-lookup"><span data-stu-id="8804e-250">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="8804e-251">Il client si aspetta che le risposte di accesso vengano restituite come oggetti JSON nel formato:</span><span class="sxs-lookup"><span data-stu-id="8804e-251">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="8804e-252">Il metodo `AppServiceLoginHandler.CreateToken()` include un parametro *audience* e un parametro *issuer*.</span><span class="sxs-lookup"><span data-stu-id="8804e-252">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="8804e-253">Entrambi i parametri vengono impostati sull'URL della radice dell'applicazione, usando lo schema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8804e-253">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="8804e-254">Allo stesso modo, è consigliabile impostare *secretKey* come valore della chiave per la firma dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-254">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="8804e-255">Non distribuire la chiave di firma in un client perché può essere usata per creare chiavi e rappresentare utenti.</span><span class="sxs-lookup"><span data-stu-id="8804e-255">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="8804e-256">È possibile ottenere la chiave di firma mentre è ospitata nel servizio app facendo riferimento alla variabile di ambiente *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="8804e-256">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="8804e-257">Se necessario in un contesto di debug locale, seguire le istruzioni nella sezione [Debug locale con autenticazione](#local-debug) per recuperare la chiave e archiviarla come impostazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-257">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="8804e-258">Il token rilasciato può anche includere altre attestazioni e una data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="8804e-258">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="8804e-259">Il token rilasciato deve includere almeno un'attestazione soggetto (**sub**).</span><span class="sxs-lookup"><span data-stu-id="8804e-259">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="8804e-260">È possibile supportare il metodo `loginAsync()` client standard tramite l'overload della route di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-260">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="8804e-261">Se il client chiama `client.loginAsync('custom');` per eseguire l'accesso, la route deve essere `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="8804e-261">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="8804e-262">È possibile impostare la route per il controller di autenticazione personalizzata usando `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="8804e-262">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="8804e-263">Usare l'approccio `loginAsync()` assicura che il token di autenticazione sia collegato a ogni chiamata successiva al servizio.</span><span class="sxs-lookup"><span data-stu-id="8804e-263">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
>
>

### <span data-ttu-id="8804e-264"><a name="user-info"></a>Procedura: Recuperare le informazioni sull'utente autenticato</span><span class="sxs-lookup"><span data-stu-id="8804e-264"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="8804e-265">Quando un utente viene autenticato dal servizio app, è possibile accedere all'ID utente assegnato e ad altre informazioni nel codice di back-end .NET.</span><span class="sxs-lookup"><span data-stu-id="8804e-265">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="8804e-266">Le informazioni utente possono essere usate per prendere decisioni relative all'autorizzazione nel back-end.</span><span class="sxs-lookup"><span data-stu-id="8804e-266">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="8804e-267">Il codice seguente ottiene l'ID utente associato a una richiesta:</span><span class="sxs-lookup"><span data-stu-id="8804e-267">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="8804e-268">Il SID è derivato dall'ID utente specifico del provider ed è statico per un determinato utente e provider di accesso.</span><span class="sxs-lookup"><span data-stu-id="8804e-268">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="8804e-269">Il SID è null per i token di autenticazione non validi.</span><span class="sxs-lookup"><span data-stu-id="8804e-269">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="8804e-270">Il servizio app consente anche di richiedere le attestazioni specifiche dal provider di accesso.</span><span class="sxs-lookup"><span data-stu-id="8804e-270">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="8804e-271">Ogni provider di identità può fornire altre informazioni usando l'SDK del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="8804e-271">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="8804e-272">È possibile, ad esempio, usare l'API Graph Facebook per informazioni sugli amici.</span><span class="sxs-lookup"><span data-stu-id="8804e-272">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="8804e-273">È possibile specificare le attestazioni richieste nel pannello del provider nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8804e-273">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="8804e-274">Alcune attestazioni richiedono una configurazione aggiuntiva con il provider di identità.</span><span class="sxs-lookup"><span data-stu-id="8804e-274">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="8804e-275">Il codice seguente chiama il metodo di estensione **GetAppServiceIdentityAsync** per ottenere le credenziali di accesso, che includono il token di accesso necessario per effettuare richieste nell'API Graph di Facebook:</span><span class="sxs-lookup"><span data-stu-id="8804e-275">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="8804e-276">Aggiungere un'istruzione using per `System.Security.Principal` per fornire il metodo di estensione **GetAppServiceIdentityAsync**.</span><span class="sxs-lookup"><span data-stu-id="8804e-276">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="8804e-277"><a name="authorize"></a>Procedura: Limitare l'accesso ai dati per gli utenti autorizzati</span><span class="sxs-lookup"><span data-stu-id="8804e-277"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="8804e-278">Nella sezione precedente, è stato illustrato come recuperare l'ID utente di un utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="8804e-278">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="8804e-279">È possibile limitare l'accesso ai dati e ad altre risorse in base a questo valore.</span><span class="sxs-lookup"><span data-stu-id="8804e-279">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="8804e-280">Ad esempio, l'aggiunta di una colonna userId alle tabelle e l'applicazione di filtri ai risultati delle query in base all'ID utente sono modi semplici per limitare i dati restituiti solo agli utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="8804e-280">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="8804e-281">Il codice seguente restituisce righe di dati solo quando il SID corrisponde al valore nella colonna UserId nella tabella TodoItem:</span><span class="sxs-lookup"><span data-stu-id="8804e-281">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="8804e-282">Il metodo `Query()` restituisce `IQueryable` che può essere modificato da LINQ per gestire i filtri.</span><span class="sxs-lookup"><span data-stu-id="8804e-282">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="8804e-283">Procedura: Aggiungere notifiche push a un progetto server</span><span class="sxs-lookup"><span data-stu-id="8804e-283">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="8804e-284">Aggiungere notifiche push al progetto server estendendo l'oggetto **MobileAppConfiguration** e creando un client di Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="8804e-284">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="8804e-285">In Visual Studio fare clic con il pulsante destro del mouse sul progetto server, quindi scegliere **Gestisci pacchetti NuGet**, cercare `Microsoft.Azure.Mobile.Server.Notifications` e infine fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="8804e-285">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="8804e-286">Ripetere questo passaggio per installare il pacchetto `Microsoft.Azure.NotificationHubs` , che include la libreria client di Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="8804e-286">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="8804e-287">In App_Start/Startup.MobileApp.cs aggiungere una chiamata al metodo di estensione **AddPushNotifications()** durante l'inizializzazione:</span><span class="sxs-lookup"><span data-stu-id="8804e-287">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="8804e-288">Aggiungere il codice seguente per creare un client di Hub di notifica:</span><span class="sxs-lookup"><span data-stu-id="8804e-288">Add the following code that creates a Notification Hubs client:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="8804e-289">Ora è possibile usare il client di Hub di notifica per inviare notifiche push ai dispositivi registrati.</span><span class="sxs-lookup"><span data-stu-id="8804e-289">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="8804e-290">Per altre informazioni, vedere [Aggiungere notifiche push all'app](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="8804e-290">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="8804e-291">Per altre informazioni su Hub di notifica, vedere [Panoramica di Hub di notifica](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8804e-291">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="8804e-292"><a name="tags"></a>Procedura: Abilitare le notifiche push mirate usando i tag</span><span class="sxs-lookup"><span data-stu-id="8804e-292"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="8804e-293">Hub di notifica consente di inviare notifiche mirate a registrazioni specifiche tramite tag.</span><span class="sxs-lookup"><span data-stu-id="8804e-293">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="8804e-294">Diversi tag vengono creati automaticamente:</span><span class="sxs-lookup"><span data-stu-id="8804e-294">Several tags are created automatically:</span></span>

* <span data-ttu-id="8804e-295">L'ID installazione identifica un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="8804e-295">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="8804e-296">L'ID utente basato sul SID autenticato identifica un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="8804e-296">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="8804e-297">È possibile accedere all'ID di installazione dalla proprietà **installationId** in**MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="8804e-297">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="8804e-298">L'esempio seguente illustra come usare un ID di installazione per aggiungere un tag a una specifica installazione di Hub di notifica:</span><span class="sxs-lookup"><span data-stu-id="8804e-298">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="8804e-299">I tag forniti dal client durante la registrazione per le notifiche push vengono ignorati dal back-end durante la creazione dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-299">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="8804e-300">Per consentire a un client di aggiungere tag all'installazione, è necessario creare un'API personalizzata che aggiunge tag usando il modello precedente.</span><span class="sxs-lookup"><span data-stu-id="8804e-300">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span>

<span data-ttu-id="8804e-301">Per un esempio, vedere [Client-added push notification tags][5] (Tag di notifica push aggiunti dal client) nell'esempio di avvio rapido completato di app per dispositivi mobili del servizio app.</span><span class="sxs-lookup"><span data-stu-id="8804e-301">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="8804e-302"><a name="push-user"></a>Procedura: Inviare notifiche push agli utenti autenticati</span><span class="sxs-lookup"><span data-stu-id="8804e-302"><a name="push-user"></a>How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="8804e-303">Se un utente autenticato esegue la registrazione per le notifiche push, viene automaticamente aggiunto un tag con l'ID utente.</span><span class="sxs-lookup"><span data-stu-id="8804e-303">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="8804e-304">Usando questo tag, è possibile inviare notifiche push a tutti i dispositivi registrati da tale persona.</span><span class="sxs-lookup"><span data-stu-id="8804e-304">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="8804e-305">Il codice seguente ottiene il SID dell'utente che esegue la richiesta e invia un modello di notifica push a ogni registrazione del dispositivo per tale persona:</span><span class="sxs-lookup"><span data-stu-id="8804e-305">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="8804e-306">Durante la registrazione per le notifiche push da un client autenticato, assicurarsi che l'autenticazione sia stata completata prima di tentare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-306">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="8804e-307">Per altre informazioni, vedere [Push to users][6] (Eseguire il push agli utenti) nell'esempio di avvio rapido completato per le app per dispositivi mobili del servizio app per back-end .NET.</span><span class="sxs-lookup"><span data-stu-id="8804e-307">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="8804e-308">Procedura: Eseguire il debug e risolvere i problemi di .NET Server SDK</span><span class="sxs-lookup"><span data-stu-id="8804e-308">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="8804e-309">Il servizio app di Azure offre diverse tecniche di debug e risoluzione dei problemi per le applicazioni ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="8804e-309">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="8804e-310">Monitoraggio di un servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="8804e-310">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="8804e-311">Abilitazione della registrazione diagnostica nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="8804e-311">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="8804e-312">Risoluzione dei problemi di un Servizio app di Azure in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8804e-312">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="8804e-313">Registrazione</span><span class="sxs-lookup"><span data-stu-id="8804e-313">Logging</span></span>
<span data-ttu-id="8804e-314">È possibile scrivere nei log di diagnostica del servizio app usando la scrittura di tracce ASP.NET standard:</span><span class="sxs-lookup"><span data-stu-id="8804e-314">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="8804e-315">Prima di poter scrivere nei log, è necessario abilitare la diagnostica nel back-end di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8804e-315">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="8804e-316">Per abilitare la diagnostica e scrivere nei log:</span><span class="sxs-lookup"><span data-stu-id="8804e-316">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="8804e-317">Seguire i passaggi in [Come abilitare la diagnostica](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="8804e-317">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="8804e-318">Aggiungere l'istruzione using seguente al file del codice:</span><span class="sxs-lookup"><span data-stu-id="8804e-318">Add the following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="8804e-319">Creare un writer di traccia per scrivere dal back-end .NET nei log di diagnostica, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8804e-319">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="8804e-320">Ripubblicare il progetto server e accedere al back-end di App per dispositivi mobili per eseguire il percorso del codice con la registrazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-320">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="8804e-321">Scaricare e valutare i log, come descritto in [Procedura: Scaricare i log](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="8804e-321">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="8804e-322"><a name="local-debug"></a>Debug locale con autenticazione</span><span class="sxs-lookup"><span data-stu-id="8804e-322"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="8804e-323">È possibile eseguire l'applicazione in locale per testare le modifiche prima di pubblicarle nel cloud.</span><span class="sxs-lookup"><span data-stu-id="8804e-323">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="8804e-324">Per la maggior parte dei back-end di App per dispositivi mobili di Azure, premere *F5* in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8804e-324">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="8804e-325">Esistono però alcune considerazioni aggiuntive quando si usa l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-325">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="8804e-326">È necessaria un'app per dispositivi mobili basata sul cloud con l'autenticazione/autorizzazione del servizio app configurata e il client deve avere l'endpoint cloud specificato come host di accesso alternativo.</span><span class="sxs-lookup"><span data-stu-id="8804e-326">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="8804e-327">Per i passaggi specifici da eseguire, vedere la documentazione della piattaforma client.</span><span class="sxs-lookup"><span data-stu-id="8804e-327">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="8804e-328">Verificare che nel back-end mobile sia installato [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="8804e-328">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="8804e-329">Quindi nella classe di avvio OWIN dell'applicazione aggiungere quanto segue, dopo che `MobileAppConfiguration` è stato applicato a `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="8804e-329">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="8804e-330">Nell'esempio precedente è consigliabile configurare le impostazioni dell'applicazione *authAudience* e *authIssuer* nel file Web.config in modo che ognuna sia l'URL della radice dell'applicazione, usando lo schema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8804e-330">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="8804e-331">Allo stesso modo, è consigliabile impostare *authSigningKey* come valore della chiave per la firma dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8804e-331">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span>
<span data-ttu-id="8804e-332">Per ottenere la chiave di firma:</span><span class="sxs-lookup"><span data-stu-id="8804e-332">To obtain the signing key:</span></span>

1. <span data-ttu-id="8804e-333">Andare all'app nel [portale di Azure]</span><span class="sxs-lookup"><span data-stu-id="8804e-333">Navigate to your app within the [Azure portal]</span></span>
2. <span data-ttu-id="8804e-334">Fare clic su **Strumenti**, **Kudu**, **Vai**.</span><span class="sxs-lookup"><span data-stu-id="8804e-334">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="8804e-335">Nel sito di gestione di Kudu fare clic su **Environment**(Ambiente).</span><span class="sxs-lookup"><span data-stu-id="8804e-335">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="8804e-336">Trovare il valore di *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="8804e-336">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="8804e-337">Usare la chiave di firma per il parametro *authSigningKey* nel file di configurazione dell'applicazione locale.</span><span class="sxs-lookup"><span data-stu-id="8804e-337">Use the signing key for the *authSigningKey* parameter in your local application config.</span></span>  <span data-ttu-id="8804e-338">Il back-end mobile, quando è in esecuzione in locale, ora riesce a convalidare i token che il client ottiene dall'endpoint basato sul cloud.</span><span class="sxs-lookup"><span data-stu-id="8804e-338">Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
<span data-ttu-id="8804e-339">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="8804e-339">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="8804e-340">[NuGet.org]: http://www.nuget.org/</span><span class="sxs-lookup"><span data-stu-id="8804e-340">[NuGet.org]: http://www.nuget.org/</span></span>
<span data-ttu-id="8804e-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span><span class="sxs-lookup"><span data-stu-id="8804e-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span></span>
<span data-ttu-id="8804e-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span><span class="sxs-lookup"><span data-stu-id="8804e-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span></span>
<span data-ttu-id="8804e-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span><span class="sxs-lookup"><span data-stu-id="8804e-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span></span>
<span data-ttu-id="8804e-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span><span class="sxs-lookup"><span data-stu-id="8804e-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span></span>
<span data-ttu-id="8804e-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span><span class="sxs-lookup"><span data-stu-id="8804e-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span></span>
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
