---
title: un'app di Azure line-of-business con l'autenticazione di ADFS aaaCreate | Documenti Microsoft
description: "Informazioni su come un'app line-of-business nel servizio App di Azure che esegue l'autenticazione con toocreate locale servizio token di sicurezza. In questa esercitazione è destinato AD FS come hello servizio token di sicurezza locale."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="83ff5-104">Creare un'app line-of-business in Azure con l'autenticazione di AD FS</span><span class="sxs-lookup"><span data-stu-id="83ff5-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="83ff5-105">In questo articolo illustra come applicazione toocreate un ASP.NET MVC line-of-business in [Azure App Service](../app-service/app-service-value-prop-what-is.md) tramite un locale [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) come provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="83ff5-106">Questo scenario è possibile utilizzare quando si desidera che le applicazioni line-of-business toocreate in Azure App Service ma l'organizzazione richiede toobe di dati di directory archiviate localmente.</span><span class="sxs-lookup"><span data-stu-id="83ff5-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="83ff5-107">Per una panoramica delle opzioni hello enterprise diversi autenticazione e autorizzazione per il servizio App di Azure, vedere [autentica con locale di Active Directory in Azure app](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="83ff5-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="83ff5-108">Obiettivo di compilazione</span><span class="sxs-lookup"><span data-stu-id="83ff5-108">What you will build</span></span>
<span data-ttu-id="83ff5-109">Si creerà un'applicazione ASP.NET di base nelle App Web di servizio App di Azure con hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="83ff5-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="83ff5-110">Autenticazione degli utenti in ADFS</span><span class="sxs-lookup"><span data-stu-id="83ff5-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="83ff5-111">Usa `[Authorize]` utenti tooauthorize per azioni diverse</span><span class="sxs-lookup"><span data-stu-id="83ff5-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="83ff5-112">Configurazione statica per il debug in Visual Studio e la pubblicazione del servizio Web App tooApp (configurare una sola volta, eseguire il debug e pubblicare in qualsiasi momento)</span><span class="sxs-lookup"><span data-stu-id="83ff5-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="83ff5-113">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="83ff5-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="83ff5-114">È necessario hello seguenti toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="83ff5-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="83ff5-115">Un locale di distribuzione di ADFS (per una procedura dettagliata end-to-end di testing hello utilizzati in questa esercitazione, vedere [Lab di Test: STS autonomo con AD FS in una macchina virtuale di Azure (solo per test)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="83ff5-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="83ff5-116">Trust di relying party di autorizzazioni toocreate in Gestione ADFS</span><span class="sxs-lookup"><span data-stu-id="83ff5-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="83ff5-117">Visual Studio 2013 Update 4 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="83ff5-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="83ff5-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) o versioni successive</span><span class="sxs-lookup"><span data-stu-id="83ff5-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="83ff5-119">Usare l'applicazione di esempio per il modello line-of-business</span><span class="sxs-lookup"><span data-stu-id="83ff5-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="83ff5-120">applicazione di esempio in questa esercitazione, Hello [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), viene creato dal team di Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="83ff5-121">Poiché ADFS supporta WS-Federation, è possibile utilizzare come le applicazioni line-of-business toocreate un modello con facilità.</span><span class="sxs-lookup"><span data-stu-id="83ff5-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="83ff5-122">Dispone di hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="83ff5-122">It has hello following features:</span></span>

* <span data-ttu-id="83ff5-123">Usa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate con un locale di distribuzione di ADFS</span><span class="sxs-lookup"><span data-stu-id="83ff5-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="83ff5-124">Funzionalità di accesso e di disconnessione</span><span class="sxs-lookup"><span data-stu-id="83ff5-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="83ff5-125">Usa [italiano](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (anziché Windows Identity Foundation), che è hello future di ASP.NET e tooset molto più semplice per l'autenticazione e autorizzazione di WIF</span><span class="sxs-lookup"><span data-stu-id="83ff5-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="83ff5-126">Configurare l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="83ff5-126">Set up hello sample application</span></span>
1. <span data-ttu-id="83ff5-127">Clona o download soluzione di esempio hello in [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour directory locale.</span><span class="sxs-lookup"><span data-stu-id="83ff5-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="83ff5-128">Hello istruzioni [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) illustrano come tooset di un'applicazione hello con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83ff5-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="83ff5-129">Ma in questa esercitazione, impostare con AD FS, quindi seguire questa procedura hello invece.</span><span class="sxs-lookup"><span data-stu-id="83ff5-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="83ff5-130">Aprire la soluzione hello e quindi aprire Controllers\AccountController.cs in hello **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="83ff5-131">Si noterà che il codice hello genera semplicemente un autenticazione challenge tooauthenticate hello utente che utilizza WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="83ff5-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="83ff5-132">Tutte le autenticazioni sono configurate in App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="83ff5-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="83ff5-133">Aprire App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="83ff5-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="83ff5-134">In hello `ConfigureAuth` (metodo), riga hello Nota:</span><span class="sxs-lookup"><span data-stu-id="83ff5-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="83ff5-135">Nell'ambiente OWIN hello questo frammento è davvero hello bare che minimo è necessario l'autenticazione WS-Federation tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="83ff5-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="83ff5-136">È molto più semplice e più elegante di WIF, in Web. config viene inserito con XML in tutto a posto hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="83ff5-137">Hello solo informazioni necessarie sono hello della relying party (RP) identificatore e hello dell'URL del file di metadati del servizio ADFS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="83ff5-138">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="83ff5-138">Here's an example:</span></span>
   
   * <span data-ttu-id="83ff5-139">Identificatore della relying party: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="83ff5-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="83ff5-140">Indirizzo dei metadati: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="83ff5-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="83ff5-141">In App_Start\Startup.Auth.cs, modificare le definizioni di stringa statica che seguono hello:</span><span class="sxs-lookup"><span data-stu-id="83ff5-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="83ff5-142">A questo punto, è possibile apportare le modifiche corrispondenti di hello in Web. config. Aprire Web. config hello e modificare hello seguendo le impostazioni dell'app:</span><span class="sxs-lookup"><span data-stu-id="83ff5-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="83ff5-143">Inserire i valori di chiave hello in base all'ambiente corrispondente.</span><span class="sxs-lookup"><span data-stu-id="83ff5-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="83ff5-144">Toomake applicazione hello che non siano presenti errori di compilazione.</span><span class="sxs-lookup"><span data-stu-id="83ff5-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="83ff5-145">È tutto.</span><span class="sxs-lookup"><span data-stu-id="83ff5-145">That's it.</span></span> <span data-ttu-id="83ff5-146">Applicazione di esempio hello è ora pronto toowork con AD FS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="83ff5-147">È comunque necessario tooconfigure un trust della relying Party con questa applicazione in ADFS in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="83ff5-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="83ff5-148">Distribuire tooAzure applicazione di esempio hello App del servizio Web App</span><span class="sxs-lookup"><span data-stu-id="83ff5-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="83ff5-149">In questo caso, pubblicare app web di tooa applicazione hello in App del servizio Web App mantenendo l'ambiente di debug di hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="83ff5-150">Si noti che si userà un'applicazione hello toopublish prima che abbia un trust della relying Party con AD FS, in modo autenticazione ancora non funziona ancora.</span><span class="sxs-lookup"><span data-stu-id="83ff5-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="83ff5-151">Se si effettua questa ora si possono tuttavia avere hello URL dell'app web che è possibile utilizzare trust della relying Party tooconfigure hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="83ff5-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="83ff5-152">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="83ff5-153">Selezionare **Servizio app di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="83ff5-154">Se è ancora stato effettuato tooAzure, fare clic su **Accedi** e utilizzare l'account Microsoft hello per toosign la sottoscrizione di Azure in.</span><span class="sxs-lookup"><span data-stu-id="83ff5-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="83ff5-155">Una volta effettuato l'accesso, fare clic su **New** toocreate un'app web.</span><span class="sxs-lookup"><span data-stu-id="83ff5-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="83ff5-156">Compilare tutti i campi obbligatori.</span><span class="sxs-lookup"><span data-stu-id="83ff5-156">Fill in all required fields.</span></span> <span data-ttu-id="83ff5-157">Si sta dati locali tooon tooconnect in un secondo momento, in modo da non creare un database per questa app web.</span><span class="sxs-lookup"><span data-stu-id="83ff5-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="83ff5-158">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-158">Click **Create**.</span></span> <span data-ttu-id="83ff5-159">Una volta creato l'app web hello, finestra di dialogo Pubblica sito Web hello viene aperto.</span><span class="sxs-lookup"><span data-stu-id="83ff5-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="83ff5-160">In **URL di destinazione**, modificare **http** troppo**https**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="83ff5-161">Copia hello intero URL tooa editor di testo per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="83ff5-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="83ff5-162">Fare quindi clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="83ff5-163">In Visual Studio aprire **Web.Release.config** nel progetto.</span><span class="sxs-lookup"><span data-stu-id="83ff5-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="83ff5-164">Inserisci hello seguente XML in hello `<configuration>` tag e sostituire l'URL dell'app web pubblica valore chiave hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="83ff5-165">Al termine, si dispone di due identificatori RP configurati nel progetto, uno per l'ambiente di debug in Visual Studio, e uno per hello pubblicato app web in Azure.</span><span class="sxs-lookup"><span data-stu-id="83ff5-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="83ff5-166">Si imposterà un trust della relying Party per ognuno dei due ambienti di hello in ADFS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="83ff5-167">Durante il debug, le impostazioni dell'app hello in Web. config vengono utilizzati toomake il **Debug** delle operazioni di configurazione con AD FS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="83ff5-168">Quando viene pubblicato (per impostazione predefinita, hello **versione** è pubblicato configurazione), viene caricato un file Web. config trasformato che incorpori le modifiche dell'impostazione applicazione hello in Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="83ff5-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="83ff5-169">Se si desidera tooattach hello web pubblicata app in Azure toohello debugger (ad esempio, è necessario caricare i simboli di debug del codice nell'applicazione web pubblicata hello), è possibile creare un clone di hello configurazione per il debug di Azure per il Debug, ma con il proprio file Web. config personalizzati trasformare ( ad esempio Web.AzureDebug.config) che utilizza le impostazioni dell'applicazione hello Web.Release.config. Ciò consente una configurazione statica toomaintain tra ambienti diversi hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="83ff5-170">Configurare l'attendibilità della relying party nel componente di gestione di ADFS</span><span class="sxs-lookup"><span data-stu-id="83ff5-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="83ff5-171">È ora necessario un trust della relying Party in Gestione ADFS tooconfigure prima di poter utilizzare l'applicazione di esempio ed effettivamente l'autenticazione con AD FS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="83ff5-172">Sarà necessario tooset i due trust relying Party separati, uno per l'ambiente di debug e uno per l'applicazione web pubblicata.</span><span class="sxs-lookup"><span data-stu-id="83ff5-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="83ff5-173">Assicurarsi che si ripetuta hello seguendo i passaggi per entrambi gli ambienti.</span><span class="sxs-lookup"><span data-stu-id="83ff5-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="83ff5-174">Nel server AD FS, accedere con le credenziali che dispongono di diritti di gestione tooAD ADFS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="83ff5-175">Aprire il componente di gestione di ADFS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-175">Open AD FS Management.</span></span> <span data-ttu-id="83ff5-176">Fare clic con il pulsante destro del mouse su **AD FS\Relazioni di attendibilità\Attendibilità componente** e selezionare **Aggiungi attendibilità componente**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="83ff5-177">In hello **Seleziona origine dati** selezionare **immettere manualmente i dati sulla relying party di hello**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="83ff5-178">In hello **Specifica nome visualizzato** pagina, digitare un nome visualizzato per un'applicazione hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="83ff5-179">In hello **scegliere protocollo** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="83ff5-180">In hello **Configura certificato** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="83ff5-181">Poiché dovrebbe essere già in uso HTTPS, i token crittografati sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="83ff5-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="83ff5-182">Se si vuole token tooencrypt da AD FS in questa pagina, è inoltre necessario aggiungere logica di decrittografia di token nel codice.</span><span class="sxs-lookup"><span data-stu-id="83ff5-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="83ff5-183">Per altre informazioni, vedere il post sulla [configurazione manuale di middleware WS-Federation OWIN e sull'accettazione di token crittografati](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="83ff5-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="83ff5-184">Prima di passare al passaggio successivo hello, è necessario un'informazione dal progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83ff5-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="83ff5-185">Nelle proprietà del progetto hello, si noti hello **URL SSL** dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="83ff5-186">In Gestione ADFS, in hello **Configura URL** pagina di hello **Aggiunta guidata attendibilità componente**selezionare **abilitare il supporto per hello protocollo passivo WS-Federation** e digitare hello URL SSL del progetto di Visual Studio che si è preso nota nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="83ff5-187">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="83ff5-188">URL specifica in cui il client hello toosend dopo l'autenticazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="83ff5-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="83ff5-189">Per l'ambiente di debug hello, dovrebbe essere <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="83ff5-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="83ff5-190">Per l'applicazione web pubblicata hello, dovrebbe essere hello URL dell'app web.</span><span class="sxs-lookup"><span data-stu-id="83ff5-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="83ff5-191">In hello **Configura identificatori** pagina, verificare che il progetto URL SSL è già configurato e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="83ff5-192">Fare clic su **Avanti** tutti hello fine toohello modo della procedura guidata hello con le selezioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="83ff5-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="83ff5-193">In App_Start\Startup.Auth.cs del progetto di Visual Studio, questo identificatore viene confrontato con il valore di hello di <code>WsFederationAuthenticationOptions.Wtrealm</code> durante l'autenticazione federata.</span><span class="sxs-lookup"><span data-stu-id="83ff5-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="83ff5-194">Per impostazione predefinita, l'URL dell'applicazione hello dal passaggio precedente hello viene aggiunto come un identificatore della relying Party.</span><span class="sxs-lookup"><span data-stu-id="83ff5-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="83ff5-195">Completata la configurazione di hello applicazione relying Party per il progetto in ADFS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="83ff5-196">Successivamente, si configura questo toosend applicazione hello attestazioni richieste dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="83ff5-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="83ff5-197">Hello **Modifica regole attestazione** finestra di dialogo è aperto per impostazione predefinita per l'utente alla fine di hello della procedura guidata hello in modo che è possibile iniziare immediatamente.</span><span class="sxs-lookup"><span data-stu-id="83ff5-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="83ff5-198">Consente di configurare almeno hello seguenti attestazioni (con gli schemi tra parentesi):</span><span class="sxs-lookup"><span data-stu-id="83ff5-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="83ff5-199">Nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - utilizzato da ASP.NET toohydrate `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="83ff5-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="83ff5-200">Utente il nome dell'entità (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - utilizzato toouniquely identificare gli utenti dell'organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="83ff5-201">Appartenenze ai ruoli (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - può essere utilizzato con `[Authorize(Roles="role1, role2,...")]` decorazione tooauthorize controller/azioni.</span><span class="sxs-lookup"><span data-stu-id="83ff5-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="83ff5-202">In realtà, questo approccio potrebbe non essere hello ad alte prestazioni la maggior parte delle autorizzazioni dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="83ff5-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="83ff5-203">Se gli utenti AD appartengono toohundreds dei gruppi di sicurezza, diventano centinaia di attestazioni di ruolo in token SAML hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="83ff5-204">Un approccio alternativo è toosend un solo ruolo di attestazione in modo condizionale in base hello appartenenza in un determinato gruppo.</span><span class="sxs-lookup"><span data-stu-id="83ff5-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="83ff5-205">Tuttavia, ai fini della presente esercitazione si manterrà una configurazione semplice.</span><span class="sxs-lookup"><span data-stu-id="83ff5-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="83ff5-206">ID nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) può essere usata per la convalida antifalsificazione.</span><span class="sxs-lookup"><span data-stu-id="83ff5-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="83ff5-207">Per ulteriori informazioni su come toomake funziona con anti-falsificazione convalida, vedere hello **aggiungere funzionalità line-of-business** sezione [creare un'app di Azure line-of-business con l'autenticazione di Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="83ff5-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="83ff5-208">Hello tipi di attestazioni è necessario tooconfigure per l'applicazione è determinata dalle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="83ff5-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="83ff5-209">Per hello l'elenco di attestazioni supportati dalle applicazioni di Azure Active Directory (ad esempio i trust di relying Party), ad esempio, vedere [supportati Token e tipi di attestazione](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="83ff5-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="83ff5-210">Nella finestra di dialogo Modifica regole attestazione hello, fare clic su **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="83ff5-211">Configurare le attestazioni di nome UPN e ruolo hello, come illustrato nella schermata di hello e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="83ff5-212">Creare quindi un nome temporaneo ID attestazione utilizzando hello passaggi illustrati in [identificatori del nome di asserzioni SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="83ff5-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="83ff5-213">Fare nuovamente clic su **Add Rule** .</span><span class="sxs-lookup"><span data-stu-id="83ff5-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="83ff5-214">Selezionare **Inviare attestazioni mediante una regola personalizzata** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="83ff5-215">Linguaggio di regola seguente di hello Incolla in hello **regola personalizzata** casella, una regola di hello nome **per ogni identificatore di sessione** e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    <span data-ttu-id="83ff5-216">La regola personalizzata sarà simile allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="83ff5-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="83ff5-217">Fare nuovamente clic su **Add Rule** .</span><span class="sxs-lookup"><span data-stu-id="83ff5-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="83ff5-218">Selezionare **Trasformare un'attestazione in ingresso** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="83ff5-219">Configurare la regola di hello, come illustrato nella schermata di hello (utilizzando il tipo di attestazione hello è stato creato in una regola personalizzata hello) e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="83ff5-220">Per informazioni dettagliate sui passaggi di hello di attestazione ID nome temporaneo hello, vedere [identificatori del nome di asserzioni SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="83ff5-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="83ff5-221">Fare clic su **applica** in hello **Modifica regole attestazione** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="83ff5-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="83ff5-222">Ora dovrebbe essere simile hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="83ff5-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="83ff5-223">Assicurarsi di ripetere questi passaggi sia per l'ambiente di debug che per l'app Web pubblicata.</span><span class="sxs-lookup"><span data-stu-id="83ff5-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="83ff5-224">Testare l'autenticazione federata per la propria applicazione</span><span class="sxs-lookup"><span data-stu-id="83ff5-224">Test federated authentication for your application</span></span>
<span data-ttu-id="83ff5-225">Si sono pronti tootest la logica di autenticazione dell'applicazione in ADFS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="83ff5-226">Nel mio ambiente di laboratorio di ADFS, è necessario un utente di test a cui appartiene il gruppo di test tooa in Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="83ff5-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="83ff5-227">autenticazione tootest nel debugger hello, è sufficiente toodo ora è di tipo `F5`.</span><span class="sxs-lookup"><span data-stu-id="83ff5-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="83ff5-228">Se si desidera tootest autenticazione nell'applicazione web pubblicata hello, passare toohello URL.</span><span class="sxs-lookup"><span data-stu-id="83ff5-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="83ff5-229">Dopo il caricamento di un'applicazione hello web, fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="83ff5-230">Ora è necessario ottenere un account di accesso finestra di dialogo o hello account di accesso pagina servita da AD FS, in base al metodo di autenticazione hello scelto da ADFS.</span><span class="sxs-lookup"><span data-stu-id="83ff5-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="83ff5-231">Di seguito è riportato ciò che viene visualizzato in Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="83ff5-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="83ff5-232">Quando si accede con un account utente nel dominio hello Active Directory di distribuzione FS hello Active Directory, si dovrebbe essere hello home page con **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="83ff5-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="83ff5-233">Nell'angolo hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-233">in hello corner.</span></span> <span data-ttu-id="83ff5-234">Questo è quanto viene visualizzato nell'ambiente di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="83ff5-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="83ff5-235">Fino a questo punto, una volta completata hello seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="83ff5-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="83ff5-236">L'applicazione ha raggiunto ADFS e un identificatore della relying Party corrispondente si trova in hello database AD FS</span><span class="sxs-lookup"><span data-stu-id="83ff5-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="83ff5-237">ADFS è stato autenticato un utente di Active Directory e reindirizza la home page dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="83ff5-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="83ff5-238">AD FS come nome hello inviati attestazione applicazione tooyour (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name), come indicato dal fatto di hello utente hello nome viene visualizzato nell'angolo hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="83ff5-239">Se l'attestazione nome hello manca, si sarebbe verificato **Hello,!**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="83ff5-240">Se si osserva Views\Shared\_LoginPartial.cshtml, trovare che utilizza `User.Identity.Name` nome utente di toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="83ff5-241">Come accennato in precedenza, se l'attestazione nome hello di hello autenticata utente è disponibile nel token SAML hello, ASP.NET hydrates questa proprietà con esso.</span><span class="sxs-lookup"><span data-stu-id="83ff5-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="83ff5-242">toosee che Hello tutte le attestazioni inviate da AD FS, inserire un punto di interruzione in controllers\homecontroller.cs., hello metodo di azione Index.</span><span class="sxs-lookup"><span data-stu-id="83ff5-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="83ff5-243">Dopo l'autenticazione utente hello, controllare hello `System.Security.Claims.Current.Claims` insieme.</span><span class="sxs-lookup"><span data-stu-id="83ff5-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="83ff5-244">Autorizzare utenti per controller o azioni specifiche</span><span class="sxs-lookup"><span data-stu-id="83ff5-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="83ff5-245">Poiché sono stati inclusi appartenenze a gruppi come le attestazioni dei ruoli nella configurazione di trust della relying Party, è possibile utilizzarli direttamente in hello `[Authorize(Roles="...")]` decorazione per controller e azioni.</span><span class="sxs-lookup"><span data-stu-id="83ff5-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="83ff5-246">In un'applicazione line-of-business con modello di hello crea-lettura, aggiornamento ed eliminazione (CRUD), è possibile autorizzare tooaccess ruoli specifici di ogni azione.</span><span class="sxs-lookup"><span data-stu-id="83ff5-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="83ff5-247">Per il momento, è sufficiente verrà provare questa funzionalità sul controller Home esistente hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="83ff5-248">Aprire Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="83ff5-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="83ff5-249">Decorare hello `About` e `Contact` azione metodi simili toohello seguente di codice, tramite l'appartenenza ai gruppi di sicurezza dell'utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="83ff5-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    <span data-ttu-id="83ff5-250">Poiché è stato aggiunto **utente Test** troppo**gruppo di Test** nel mio ambiente di laboratorio di ADFS, si utilizzerà autorizzazione tootest gruppo di Test su `About`.</span><span class="sxs-lookup"><span data-stu-id="83ff5-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="83ff5-251">Per `Contact`, verificherà hello negativo maiuscole **Domain Admins**, toowhich **utente Test** non appartiene.</span><span class="sxs-lookup"><span data-stu-id="83ff5-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="83ff5-252">Avviare il debugger hello digitando `F5` accedere, quindi fare clic su **su**.</span><span class="sxs-lookup"><span data-stu-id="83ff5-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="83ff5-253">Si dovrebbe ora essere visualizzando hello `~/About/Index` pagina correttamente, se l'utente autenticato è autorizzato per l'azione.</span><span class="sxs-lookup"><span data-stu-id="83ff5-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="83ff5-254">Fare clic su **contatto**, che in questo caso non è necessario autorizzare **utente Test** per azione di hello.</span><span class="sxs-lookup"><span data-stu-id="83ff5-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="83ff5-255">Tuttavia, i browser hello è reindirizzato tooAD ADFS, che viene infine illustrato questo messaggio:</span><span class="sxs-lookup"><span data-stu-id="83ff5-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="83ff5-256">Se è esaminare l'errore nel Visualizzatore eventi sul server AD FS hello, viene visualizzato questo messaggio di eccezione:</span><span class="sxs-lookup"><span data-stu-id="83ff5-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="83ff5-257">motivo di Hello di questo errore è che per impostazione predefinita, MVC restituisce un 401 non autorizzato quando i ruoli di un utente non autorizzati.</span><span class="sxs-lookup"><span data-stu-id="83ff5-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="83ff5-258">In questo modo viene attivato un provider di identità tooyour richiesta riautenticazione (AD FS).</span><span class="sxs-lookup"><span data-stu-id="83ff5-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="83ff5-259">Dal momento che hello è già autenticato, ADFS restituisce toohello stessa pagina, che quindi pubblica 401 un'altra, la creazione di un ciclo di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="83ff5-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="83ff5-260">Si eseguirà l'override di AuthorizeAttribute `HandleUnauthorizedRequest` metodo con logica semplice tooshow un elemento che ha senso anziché ciclo di reindirizzamento hello continua.</span><span class="sxs-lookup"><span data-stu-id="83ff5-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="83ff5-261">Creare un file nel progetto hello chiamato AuthorizeAttribute.cs e Incolla hello seguente codice al suo interno.</span><span class="sxs-lookup"><span data-stu-id="83ff5-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    <span data-ttu-id="83ff5-262">Hello di eseguire l'override di codice inviato un HTTP 403 (accesso negato) invece di HTTP 401 (non autorizzato) in casi autenticati ma non autorizzati.</span><span class="sxs-lookup"><span data-stu-id="83ff5-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="83ff5-263">Eseguire il debugger hello con `F5`.</span><span class="sxs-lookup"><span data-stu-id="83ff5-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="83ff5-264">Facendo clic su **Contact** verrà visualizzato un messaggio di errore più informativo (anche se graficamente meno elegante):</span><span class="sxs-lookup"><span data-stu-id="83ff5-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="83ff5-265">Pubblicare nuovamente tooAzure applicazione hello App del servizio Web App e verificare il comportamento di hello di un'applicazione hello in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="83ff5-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="83ff5-266">La connessione dati tooon locali</span><span class="sxs-lookup"><span data-stu-id="83ff5-266">Connect tooon-premises data</span></span>
<span data-ttu-id="83ff5-267">Un motivo che si tooimplement l'applicazione line-of-business con AD FS invece di Azure Active Directory è problemi di conformità del mantenimento dati dell'organizzazione non locali.</span><span class="sxs-lookup"><span data-stu-id="83ff5-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="83ff5-268">Ciò significa anche che l'app web in Azure deve accedere ai database locali, perché non è consentito toouse [Database SQL](/services/sql-database/) come livello dati hello per le app web.</span><span class="sxs-lookup"><span data-stu-id="83ff5-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="83ff5-269">App Web del servizio app di Azure supporta l'accesso ai database locali tramite due approcci: [connessioni ibride](../biztalk-services/integration-hybrid-connection-overview.md) e [reti virtuali](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="83ff5-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="83ff5-270">Per altre informazioni, vedere il post relativo all' [uso dell'integrazione con una rete virtuale e delle connessioni ibride con App Web del servizio app di Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="83ff5-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="83ff5-271">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="83ff5-271">Further resources</span></span>
* [<span data-ttu-id="83ff5-272">Eseguire l'autenticazione con l'istanza locale di Active Directory nell'app Azure</span><span class="sxs-lookup"><span data-stu-id="83ff5-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="83ff5-273">Creare un'app line-of-business in Azure con l'autenticazione di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83ff5-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="83ff5-274">Utilizzare l'opzione di autenticazione aziendale locale (ADFS) con ASP.NET hello in Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="83ff5-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="83ff5-275">Eseguire la migrazione di un tooKatana VS2013 progetto Web da WIF</span><span class="sxs-lookup"><span data-stu-id="83ff5-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="83ff5-276">Informazioni generali su Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="83ff5-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="83ff5-277">Specifica WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="83ff5-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

