---
title: Creare un'app line-of-business in Azure con l'autenticazione di AD FS | Documentazione Microsoft
description: Informazioni su come creare un'app line-of-business nel servizio app di Azure che esegue l'autenticazione con il servizio token di sicurezza locale. In questa esercitazione viene usato AD FS come destinazione del servizio token di sicurezza locale.
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
ms.openlocfilehash: f9a8984400378d154a504af8a41609900128d052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="c4d7c-104">Creare un'app line-of-business in Azure con l'autenticazione di AD FS</span><span class="sxs-lookup"><span data-stu-id="c4d7c-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="c4d7c-105">Questo articolo descrive come creare un'applicazione line-of-business ASP.NET MVC nel [Servizio app di Azure](../app-service/app-service-value-prop-what-is.md) usando un'istanza locale di [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-105">This article shows you how to create an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as the identity provider.</span></span> <span data-ttu-id="c4d7c-106">Questo scenario può essere usato quando si vogliono creare applicazioni line-of-business del servizio app di Azure, mentre l'organizzazione richiede che i dati della directory siano archiviati sul posto.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-106">This scenario can work when you want to create line-of-business applications in Azure App Service but your organization requires directory data to be stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="c4d7c-107">Per una panoramica delle diverse opzioni di autenticazione e autorizzazione aziendali per il servizio app di Azure, vedere [Eseguire l'autenticazione con l'istanza locale di Active Directory nell'app Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="c4d7c-107">For an overview of the different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="c4d7c-108">Obiettivo di compilazione</span><span class="sxs-lookup"><span data-stu-id="c4d7c-108">What you will build</span></span>
<span data-ttu-id="c4d7c-109">Si creerà un'applicazione ASP.NET di base nelle app Web di Servizio app di Azure con le seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-109">You will build a basic ASP.NET application in Azure App Service Web Apps with the following features:</span></span>

* <span data-ttu-id="c4d7c-110">Autenticazione degli utenti in ADFS</span><span class="sxs-lookup"><span data-stu-id="c4d7c-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="c4d7c-111">Uso di `[Authorize]` per autorizzare gli utenti per diverse azioni</span><span class="sxs-lookup"><span data-stu-id="c4d7c-111">Uses `[Authorize]` to authorize users for different actions</span></span>
* <span data-ttu-id="c4d7c-112">Configurazione statica per il debug in Visual Studio e pubblicazione nelle app Web di Servizio app di Azure (creazione della configurazione una sola volta, esecuzione del debug e pubblicazione in qualsiasi momento)</span><span class="sxs-lookup"><span data-stu-id="c4d7c-112">Static configuration for both debugging in Visual Studio and publishing to App Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="c4d7c-113">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="c4d7c-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="c4d7c-114">Per completare questa esercitazione sarà necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-114">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="c4d7c-115">Distribuzione locale di AD FS. Per una procedura dettagliata end-to-end del lab di test in uso, vedere il post di blog [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/) (Lab di test: Istanza autonoma del servizio token di sicurezza con AD FS in una VM di Azure - solo per test)</span><span class="sxs-lookup"><span data-stu-id="c4d7c-115">An on-premises AD FS deployment (for an end-to-end walkthrough of the test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="c4d7c-116">Autorizzazioni per creare una o più attendibilità della relying party nel componente di gestione di ADFS</span><span class="sxs-lookup"><span data-stu-id="c4d7c-116">Permissions to create relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="c4d7c-117">Visual Studio 2013 Update 4 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="c4d7c-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="c4d7c-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) o versioni successive</span><span class="sxs-lookup"><span data-stu-id="c4d7c-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="c4d7c-119">Usare l'applicazione di esempio per il modello line-of-business</span><span class="sxs-lookup"><span data-stu-id="c4d7c-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="c4d7c-120">L'applicazione di esempio in questa esercitazione, [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), è stata creata dal team di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-120">The sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by the Azure Active Directory team.</span></span> <span data-ttu-id="c4d7c-121">Poiché AD FS supporta la specifica WS-Federation, è possibile usarla come modello per creare nuove applicazioni line-of-business in modo semplice.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-121">Since AD FS supports WS-Federation, you can use it as a template to create line-of-business applications with ease.</span></span> <span data-ttu-id="c4d7c-122">L'applicazione presenta le seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-122">It has the following features:</span></span>

* <span data-ttu-id="c4d7c-123">Uso di [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) per eseguire l'autenticazione con una distribuzione di ADFS locale</span><span class="sxs-lookup"><span data-stu-id="c4d7c-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) to authenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="c4d7c-124">Funzionalità di accesso e di disconnessione</span><span class="sxs-lookup"><span data-stu-id="c4d7c-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="c4d7c-125">Uso di [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (invece di Windows Identity Foundation), che rappresenta il futuro di ASP.NET e offre una configurazione molto più semplice per l'autenticazione e l'autorizzazione rispetto a WIF</span><span class="sxs-lookup"><span data-stu-id="c4d7c-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is the future of ASP.NET and much simpler to set up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a><span data-ttu-id="c4d7c-126">Configurare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="c4d7c-126">Set up the sample application</span></span>
1. <span data-ttu-id="c4d7c-127">Clonare o scaricare la soluzione di esempio da [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) nella directory locale.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-127">Clone or download the sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) to your local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c4d7c-128">Le istruzioni disponibili in [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) illustrano come configurare l'applicazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-128">The instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how to set up the application with Azure Active Directory.</span></span> <span data-ttu-id="c4d7c-129">Tuttavia, in questa esercitazione la configurazione viene eseguita senza AD FS, quindi seguire i passaggi descritti qui.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-129">But in this tutorial, you set it up with AD FS, so follow the steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="c4d7c-130">Aprire la soluzione e quindi aprire Controllers\AccountController.cs in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-130">Open the solution, and then open Controllers\AccountController.cs in the **Solution Explorer**.</span></span>
   
   <span data-ttu-id="c4d7c-131">Si noterà che il codice genera semplicemente una richiesta di autenticazione per l'utente mediante WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-131">You will see that the code simply issues an authentication challenge to authenticate the user using WS-Federation.</span></span> <span data-ttu-id="c4d7c-132">Tutte le autenticazioni sono configurate in App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="c4d7c-133">Aprire App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="c4d7c-134">Nel metodo `ConfigureAuth` notare la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-134">In the `ConfigureAuth` method, note the line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="c4d7c-135">In ambito OWIN questo frammento di codice è il minimo indispensabile per configurare l'autenticazione con WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-135">In the OWIN world, this snippet is really the bare minimum you need to configure WS-Federation authentication.</span></span> <span data-ttu-id="c4d7c-136">Si tratta di un metodo più semplice ed elegante rispetto a WIF, in cui XML viene inserito in Web.config un po' ovunque.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over the place.</span></span> <span data-ttu-id="c4d7c-137">Le uniche informazioni realmente necessarie sono l'identificatore della relying party e l'URL del file di metadati del servizio ADFS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-137">The only information you need is the relying party's (RP) identifier and the URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="c4d7c-138">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-138">Here's an example:</span></span>
   
   * <span data-ttu-id="c4d7c-139">Identificatore della relying party: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="c4d7c-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="c4d7c-140">Indirizzo dei metadati: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="c4d7c-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="c4d7c-141">In App_Start\Startup.Auth.cs modificare le definizioni delle stringhe statiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-141">In App_Start\Startup.Auth.cs, change the following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="c4d7c-142">Ora apportare le modifiche corrispondenti nel file Web.config.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-142">Now, make the corresponding changes in Web.config.</span></span> <span data-ttu-id="c4d7c-143">Aprire Web.config e modificare le impostazioni dell'app seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-143">Open the Web.config and modify the following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter the App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter the relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter the FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="c4d7c-144">Compilare i valori delle chiavi in base a quanto previsto per l'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-144">Fill in the key values based on your respective environment.</span></span>
6. <span data-ttu-id="c4d7c-145">Compilare l'applicazione e verificare che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-145">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="c4d7c-146">È tutto.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-146">That's it.</span></span> <span data-ttu-id="c4d7c-147">Ora l'applicazione di esempio è pronta per l'uso con ADFS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-147">Now the sample application is ready to work with AD FS.</span></span> <span data-ttu-id="c4d7c-148">In seguito sarà comunque necessario configurare un trust della relying party con questa applicazione in AD FS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-148">You still need to configure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a><span data-ttu-id="c4d7c-149">Distribuire l'applicazione di esempio nelle app Web di Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="c4d7c-149">Deploy the sample application to Azure App Service Web Apps</span></span>
<span data-ttu-id="c4d7c-150">Qui si pubblicherà l'applicazione in un'app Web nelle app Web del servizio app di Azure mantenendo l'ambiente di debug.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-150">Here, you publish the application to a web app in App Service Web Apps while preserving the debug environment.</span></span> <span data-ttu-id="c4d7c-151">Si noti che si pubblicherà l'applicazione prima che questa disponga di un'attendibilità della relying party con ADFS, pertanto l'autenticazione non sarà ancora funzionante.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-151">Note that you're going to publish the application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="c4d7c-152">Se tuttavia si esegue questa operazione adesso, è possibile ottenere l'URL dell'app Web da usare per la configurazione del trust della relying party in un secondo tempo.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-152">However, if you do it now you can have the web app URL that you can use to configure the RP trust later.</span></span>

1. <span data-ttu-id="c4d7c-153">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-153">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="c4d7c-154">Selezionare **Servizio app di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-154">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="c4d7c-155">Se non è stato eseguito l'accesso ad Azure, fare clic su **Accedi** e usare l'account Microsoft relativo alla sottoscrizione di Azure per accedere.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-155">If you haven't signed in to Azure, click **Sign In** and use the Microsoft account for your Azure subscription to sign in.</span></span>
4. <span data-ttu-id="c4d7c-156">Dopo l'accesso, fare clic su **Nuovo** per creare un'app Web.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-156">Once signed in, click **New** to create a web app.</span></span>
5. <span data-ttu-id="c4d7c-157">Compilare tutti i campi obbligatori.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-157">Fill in all required fields.</span></span> <span data-ttu-id="c4d7c-158">Poiché in un secondo tempo si stabilirà la connessione ai dati locali, non occorre creare un database per questa app Web.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-158">You are going to connect to on-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="c4d7c-159">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-159">Click **Create**.</span></span> <span data-ttu-id="c4d7c-160">Dopo la creazione dell'app Web, verrà aperta la finestra di dialogo Pubblica sito Web.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-160">Once the web app is created, the Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="c4d7c-161">In **URL di destinazione** sostituire **http** con **https**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-161">In **Destination URL**, change **http** to **https**.</span></span> <span data-ttu-id="c4d7c-162">Copiare l'intero URL in un editor di testo per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-162">Copy the entire URL to a text editor for later use.</span></span> <span data-ttu-id="c4d7c-163">Fare quindi clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-163">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="c4d7c-164">In Visual Studio aprire **Web.Release.config** nel progetto.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-164">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="c4d7c-165">Inserire il seguente codice XML nel tag `<configuration>` e sostituire il valore della chiave con l'URL dell'app Web di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-165">Insert the following XML into the `<configuration>` tag, and replace the key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="c4d7c-166">Al termine, saranno disponibili due identificatori della relying party configurati nel progetto, uno per l'ambiente di debug in Visual Studio e uno per l'app Web pubblicata in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-166">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for the published web app in Azure.</span></span> <span data-ttu-id="c4d7c-167">Si procederà all'impostazione di un'attendibilità della relying Party per ciascuno dei due ambienti in ADFS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-167">You will set up an RP trust for each of the two environments in AD FS.</span></span> <span data-ttu-id="c4d7c-168">Durante il debug le impostazioni dell'app in Web.config vengono usate per consentire il funzionamento della configurazione di **Debug** con AD FS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-168">During debugging, the app settings in Web.config are used to make your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="c4d7c-169">In caso di pubblicazione (per impostazione predefinita viene pubblicata la configurazione di **Release** ), viene caricato un file Web.config trasformato che incorpora le modifiche alle impostazioni dell'app nel file Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-169">When it's published (by default, the **Release** configuration is published), a transformed Web.config is uploaded that incorporates the app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="c4d7c-170">Se si desidera collegare l'app Web pubblicata di Azure al debugger (ad esempio se è necessario caricare i simboli di debug del codice nell'app Web pubblicata), è possibile creare un clone della configurazione Debug per il debug di Azure, ma con una trasformazione Web.config personalizzata (ad esempio Web.AzureDebug.config) che usa le impostazioni dell'app disponibili in Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-170">If you want to attach the published web app in Azure to the debugger (i.e. you must upload debug symbols of your code in the published web app), you can create a clone of the Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses the app settings from Web.Release.config.</span></span> <span data-ttu-id="c4d7c-171">Ciò permette di mantenere una configurazione statica in ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-171">This allows you to maintain a static configuration across the different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="c4d7c-172">Configurare l'attendibilità della relying party nel componente di gestione di ADFS</span><span class="sxs-lookup"><span data-stu-id="c4d7c-172">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="c4d7c-173">Prima di poter usare l'applicazione di esempio e autenticarla effettivamente con AD FS, è necessario configurare un trust della relying party in Gestione AD FS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-173">Now you need to configure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="c4d7c-174">Sarà necessario impostare due attendibilità della relying party separate, una per l'ambiente di debug e una per l'app Web pubblicata.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-174">You will need to set up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="c4d7c-175">Assicurarsi di ripetere i passaggi seguenti per entrambi gli ambienti.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-175">Make sure that you repeat the following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="c4d7c-176">Accedere al server ADFS con le credenziali dotate di diritti di gestione per ADFS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-176">On your AD FS server, log in with credentials that have management rights to AD FS.</span></span>
2. <span data-ttu-id="c4d7c-177">Aprire il componente di gestione di ADFS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-177">Open AD FS Management.</span></span> <span data-ttu-id="c4d7c-178">Fare clic con il pulsante destro del mouse su **AD FS\Relazioni di attendibilità\Attendibilità componente** e selezionare **Aggiungi attendibilità componente**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-178">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="c4d7c-179">Nella pagina **Seleziona origine dati** selezionare **Immetti dati sul componente manualmente**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-179">In the **Select Data Source** page, select **Enter data about the relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="c4d7c-180">Nella pagina **Specifica nome visualizzato** digitare un nome visualizzato per l'applicazione e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-180">In the **Specify Display Name** page, type a display name for the application and click **Next**.</span></span>
5. <span data-ttu-id="c4d7c-181">Nella pagina **Choose Protocol** (Scegli protocollo) fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-181">In the **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="c4d7c-182">Nella pagina **Configura certificato** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-182">In the **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c4d7c-183">Poiché dovrebbe essere già in uso HTTPS, i token crittografati sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-183">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="c4d7c-184">Se si vogliono comunque crittografare i token di ADFS in questa pagina, è anche necessario aggiungere della logica di decrittografia di token nel codice.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-184">If you really want to encrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="c4d7c-185">Per altre informazioni, vedere il post sulla [configurazione manuale di middleware WS-Federation OWIN e sull'accettazione di token crittografati](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4d7c-185">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="c4d7c-186">Prima di passare al prossimo passaggio, è necessario ottenere delle informazioni dal progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-186">Before you move onto the next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="c4d7c-187">Nelle proprietà del progetto prendere nota dell' **URL SSL** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-187">In the project properties, note the **SSL URL** of the application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="c4d7c-188">Nuovamente in Gestione AD FS, nella pagina **Configura URL** di **Aggiunta guidata attendibilità componente** selezionare **Abilita supporto del protocollo passivo WS-Federation** e digitare l'URL SSL del progetto di Visual Studio di cui si è preso nota nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-188">Back in AD FS Management, in the **Configure URL** page of the **Add Relying Party Trust Wizard**, select **Enable support for the WS-Federation Passive protocol** and type in the SSL URL of your Visual Studio project that you noted in the previous step.</span></span> <span data-ttu-id="c4d7c-189">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-189">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="c4d7c-190">L'URL specifica dove inviare il client dopo la riuscita dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-190">URL specifies where to send the client after authentication succeeds.</span></span> <span data-ttu-id="c4d7c-191">Per l'ambiente di debug, l'URL dovrebbe essere <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-191">For the debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="c4d7c-192">Per l'app Web pubblicata, deve corrispondere all'URL dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-192">For the published web app, it should be the web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="c4d7c-193">Nella pagina **Configura identificatori** verificare che l'URL SSL del progetto sia già elencato, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-193">In the **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="c4d7c-194">Fare clic su **Next** fino al termine della procedura guidata, accettando le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-194">Click **Next** all the way to the end of the wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c4d7c-195">In App_Start\Startup.Auth.cs del progetto di Visual Studio questo identificatore viene confrontato con il valore di <code>WsFederationAuthenticationOptions.Wtrealm</code> durante l'autenticazione federata.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-195">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against the value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="c4d7c-196">Per impostazione predefinita, l'URL dell'applicazione nel passaggio precedente viene aggiunto come identificatore della relying party.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-196">By default, the application's URL from the previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="c4d7c-197">A questo punto la configurazione dell'applicazione relying party per il progetto in ADFS è completa.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-197">You have now finished configuring the RP application for your project in AD FS.</span></span> <span data-ttu-id="c4d7c-198">Si procederà quindi alla configurazione di questa applicazione per l'invio delle attestazioni richieste dalla propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-198">Next, you configure this application to send the claims needed by your application.</span></span> <span data-ttu-id="c4d7c-199">La finestra di dialogo **Edit Claim Rules** si apre per impostazione predefinita al termine della procedura guidata e sarà pertanto possibile iniziare immediatamente.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-199">The **Edit Claim Rules** dialog is opened by default for you at the end of the wizard so you can start immediately.</span></span> <span data-ttu-id="c4d7c-200">Configurare almeno le attestazioni seguenti (con gli schemi tra parentesi):</span><span class="sxs-lookup"><span data-stu-id="c4d7c-200">Let's configure at least the following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="c4d7c-201">Nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name): usata da ASP.NET per attivare `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-201">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET to hydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="c4d7c-202">Nome dell'entità utente (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn): usata per identificare in modo univoco gli utenti nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-202">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used to uniquely identify users in the organization.</span></span>
    * <span data-ttu-id="c4d7c-203">Appartenenze a gruppi come ruoli (http://schemas.microsoft.com/ws/2008/06/identity/claims/role): può essere usata con la decoration `[Authorize(Roles="role1, role2,...")]` per autorizzare controller/azioni.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-203">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration to authorize controllers/actions.</span></span> <span data-ttu-id="c4d7c-204">In realtà, questo approccio potrebbe non essere il più efficiente per l'autorizzazione dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-204">In reality, this approach may not be the most performant for role authorization.</span></span> <span data-ttu-id="c4d7c-205">Se gli utenti di Active Directory appartengono a centinaia di gruppi di sicurezza, diventano centinaia di attestazioni di ruolo nel token SAML.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-205">If your AD users belong to hundreds of security groups, they become hundreds of role claims in the SAML token.</span></span> <span data-ttu-id="c4d7c-206">Un approccio alternativo consiste nell'inviare una singola attestazione di ruolo in modo condizionale in base all'appartenenza dell'utente a un determinato gruppo.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-206">An alternative approach is to send a single role claim conditionally depending on the user's membership in a particular group.</span></span> <span data-ttu-id="c4d7c-207">Tuttavia, ai fini della presente esercitazione si manterrà una configurazione semplice.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-207">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="c4d7c-208">ID nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) può essere usata per la convalida antifalsificazione.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-208">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="c4d7c-209">Per altre informazioni sul funzionamento con la convalida antifalsificazione, vedere la sezione **Aggiungere funzionalità line-of-business** dell'articolo [Creare un'app line-of-business in Azure con l'autenticazione di Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="c4d7c-209">For more information on how to make it work with anti-forgery validation, see the **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c4d7c-210">I tipi di attestazione da configurare per la propria applicazione sono determinati dai requisiti dell'applicazione stessa.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-210">The claim types you need to configure for your application is determined by your application's needs.</span></span> <span data-ttu-id="c4d7c-211">Per un elenco delle attestazioni supportate dalle applicazioni Azure Active Directory (ovvero le attendibilità della relying party), vedere ad esempio [Token e tipi di attestazioni supportati](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4d7c-211">For the list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="c4d7c-212">Nella finestra di dialogo Edit Claim Rules fare clic su **Add Rule**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-212">In the Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="c4d7c-213">Configurare il nome, l'UPN e le attestazioni di ruolo come illustrato nello screenshot seguente e quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-213">Configure the name, UPN, and role claims as shown in the screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="c4d7c-214">In seguito si creerà un'attestazione ID nome temporanea usando i passaggi descritti nel post di blog [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)(Identificatori di nome nelle asserzioni SAML).</span><span class="sxs-lookup"><span data-stu-id="c4d7c-214">Next, you create a transient name ID claim using the steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="c4d7c-215">Fare nuovamente clic su **Add Rule** .</span><span class="sxs-lookup"><span data-stu-id="c4d7c-215">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="c4d7c-216">Selezionare **Inviare attestazioni mediante una regola personalizzata** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-216">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="c4d7c-217">Incollare la seguente lingua delle regole nella casella **Regola personalizzata**, assegnare il nome di **identificazione per sessione** alla regola e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-217">Paste the following rule language into the **Custom rule** box, name the rule **Per Session Identifier** and click **Finish**.</span></span>  
    
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
    
    <span data-ttu-id="c4d7c-218">La regola personalizzata sarà simile allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-218">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="c4d7c-219">Fare nuovamente clic su **Add Rule** .</span><span class="sxs-lookup"><span data-stu-id="c4d7c-219">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="c4d7c-220">Selezionare **Trasformare un'attestazione in ingresso** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-220">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="c4d7c-221">Configurare la regola come illustrato nello screenshot seguente, usando il tipo di attestazione creato nella regola personalizzata e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-221">Configure the rule as shown in the screenshot (using the claim type you created in the custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="c4d7c-222">Per informazioni dettagliate sui passaggi da eseguire per l'attestazione ID nome temporanea, vedere il post di blog [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)(Identificatori di nome nelle asserzioni SAML).</span><span class="sxs-lookup"><span data-stu-id="c4d7c-222">For detailed information on the steps for the transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="c4d7c-223">Fare clic su **Applica** nella finestra di dialogo **Modifica regole attestazione**,</span><span class="sxs-lookup"><span data-stu-id="c4d7c-223">Click **Apply** in the **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="c4d7c-224">che ora sarà simile allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-224">It should now look like the following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="c4d7c-225">Assicurarsi di ripetere questi passaggi sia per l'ambiente di debug che per l'app Web pubblicata.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-225">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="c4d7c-226">Testare l'autenticazione federata per la propria applicazione</span><span class="sxs-lookup"><span data-stu-id="c4d7c-226">Test federated authentication for your application</span></span>
<span data-ttu-id="c4d7c-227">Si è ora pronti per testare la logica di autenticazione dell'applicazione in ADFS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-227">You are ready to test your application's authentication logic against AD FS.</span></span> <span data-ttu-id="c4d7c-228">Nell'ambiente di laboratorio usato in questo esempio è presente un utente test che appartiene a un gruppo di test in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-228">In my AD FS lab environment, I have a test user that belongs to a test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="c4d7c-229">Per testare l'autenticazione nel debugger, sarà sufficiente premere `F5`.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-229">To test authentication in the debugger, all you need to do now is type `F5`.</span></span> <span data-ttu-id="c4d7c-230">Se si desidera testare l'autenticazione nell'app Web pubblicata, passare all'URL dell'app.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-230">If you want to test authentication in the published web app, navigate to the URL.</span></span>

<span data-ttu-id="c4d7c-231">Dopo il caricamento dell'applicazione Web, fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-231">After the web application loads, click **Sign In**.</span></span> <span data-ttu-id="c4d7c-232">Dovrebbe ora venire visualizzata una finestra di dialogo di accesso o la pagina di accesso presentata da ADFS, a seconda del metodo di autenticazione scelto da ADFS.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-232">You should now get either a login dialog or the login page served by AD FS, depending on the authentication method chosen by AD FS.</span></span> <span data-ttu-id="c4d7c-233">Di seguito è riportato ciò che viene visualizzato in Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-233">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="c4d7c-234">Dopo l'accesso come utente nel dominio AD della distribuzione di AD FS, verrà ora nuovamente visualizzata la home page con **Hello, <User Name>!**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-234">Once you log in with a user in the AD domain of the AD FS deployment, you should now see the homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="c4d7c-235">nell'angolo.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-235">in the corner.</span></span> <span data-ttu-id="c4d7c-236">Questo è quanto viene visualizzato nell'ambiente di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-236">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="c4d7c-237">Finora, sono stati raggiunti gli obiettivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-237">So far, you've succeeded in the following ways:</span></span>

* <span data-ttu-id="c4d7c-238">L'applicazione ha raggiunto correttamente ADFS e il corrispondente identificatore della relying party è presente nel database di ADFS</span><span class="sxs-lookup"><span data-stu-id="c4d7c-238">Your application has successfully reached AD FS and a matching RP identifier is found in the AD FS database</span></span>
* <span data-ttu-id="c4d7c-239">ADFS ha correttamente autenticato un utente AD e ha reindirizzato l'utente alla home page dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="c4d7c-239">AD FS has successfully authenticated an AD user and redirect you back to the application's homepage</span></span>
* <span data-ttu-id="c4d7c-240">AD FS ha correttamente inviato l'attestazione basata su nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) all'applicazione, come indicato dalla visualizzazione del nome utente in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-240">AD FS as successfully sent the name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) to your application, as indicated by the fact that the user name is displayed in the corner.</span></span> 

<span data-ttu-id="c4d7c-241">In caso di assenza dell'attestazione basata su nome, verrebbe visualizzato solo **Hello, !**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-241">If the name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="c4d7c-242">Se si esamina il file Views\Shared\\_LoginPartial.cshtml, si noterà che viene usato `User.Identity.Name` per visualizzare il nome utente.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-242">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` to display the user name.</span></span> <span data-ttu-id="c4d7c-243">Come già accennato, ASP.NET attiva questa proprietà con l'attestazione nome dell'utente autenticato, se questa è disponibile nel token SAML.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-243">As mentioned previously, if the name claim of the authenticated user is available in the SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="c4d7c-244">Per visualizzare tutte le attestazioni inviate da ADFS, inserire un punto di interruzione in Controllers\HomeController.cs, nel metodo di azione Index.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-244">To see all the claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in the Index action method.</span></span> <span data-ttu-id="c4d7c-245">Dopo l'autenticazione dell'utente, controllare la raccolta `System.Security.Claims.Current.Claims` .</span><span class="sxs-lookup"><span data-stu-id="c4d7c-245">After the user is authenticated, inspect the `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="c4d7c-246">Autorizzare utenti per controller o azioni specifiche</span><span class="sxs-lookup"><span data-stu-id="c4d7c-246">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="c4d7c-247">Poiché sono state incluse le appartenenze a gruppi come attestazioni di tipo ruolo nella configurazione del trust della relying party, è possibile usarle direttamente nell'effetto `[Authorize(Roles="...")]` per controller e azioni.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-247">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in the `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="c4d7c-248">In un'applicazione line-of-business in cui si usa il modello Create-Read-Update-Delete (CRUD) è possibile autorizzare ruoli specifici per accedere a ogni azione.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-248">In a line-of-business application with the Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles to access each action.</span></span> <span data-ttu-id="c4d7c-249">Per il momento, si sperimenterà questa funzionalità nel controller Home esistente.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-249">For now, you will just try out this feature on the existing Home controller.</span></span>

1. <span data-ttu-id="c4d7c-250">Aprire Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-250">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="c4d7c-251">Assegnare i metodi di azione `About` e `Contact` in modo simile al codice seguente, usando le appartenenze ai gruppi di sicurezza disponibili per l'utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-251">Decorate the `About` and `Contact` action methods similar to the following code, using security group memberships that your authenticated user has.</span></span>  
   
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
   
    <span data-ttu-id="c4d7c-252">Poiché nell'ambiente lab AD FS è stato aggiunto **Test User** a **Test Group**, si userà Test Group per il test dell'autorizzazione in `About`.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-252">Since I added **Test User** to **Test Group** in my AD FS lab environment, I'll use Test Group to test authorization on `About`.</span></span> <span data-ttu-id="c4d7c-253">Per `Contact`, si testerà il caso negativo di **Domain Admins**, a cui **Test User** non appartiene.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-253">For `Contact`, I'll test the negative case of **Domain Admins**, to which **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="c4d7c-254">Avviare il debugger premendo `F5` e accedere, quindi fare clic su **About**.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-254">Start the debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="c4d7c-255">Dovrebbe ora essere possibile visualizzare la pagina `~/About/Index` , se l'utente autenticato è autorizzato per tale azione.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-255">You should now be viewing the `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="c4d7c-256">Ora fare clic su **Contact**, che nel caso di questo esempio non autorizza **Test User** per l'azione.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-256">Now click **Contact**, which in my case should not authorize **Test User** for the action.</span></span> <span data-ttu-id="c4d7c-257">Tuttavia, il browser viene reindirizzato ad ADFS, che visualizzerà un messaggio analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-257">However, the browser is redirected to AD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="c4d7c-258">Se si esamina l'errore nel Visualizzatore eventi del server AD FS, verrà visualizzato questo messaggio di eccezione:</span><span class="sxs-lookup"><span data-stu-id="c4d7c-258">If you investigate this error in Event Viewer on the AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="c4d7c-259">Il motivo di questo errore è che, per impostazione predefinita, MVC restituisce un codice 401 Unauthorized quando i ruoli di un utente non sono autorizzati.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-259">The reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="c4d7c-260">Questo attiva una richiesta di ri-autenticazione al provider di identità (ovvero ADFS).</span><span class="sxs-lookup"><span data-stu-id="c4d7c-260">This triggers a reauthentication request to your identity provider (AD FS).</span></span> <span data-ttu-id="c4d7c-261">Poiché l'utente è già autenticato, ADFS torna alla stessa pagina, che a sua volta invia un nuovo codice 401, creando un ciclo di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-261">Since the user is already authenticated, AD FS returns to the same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="c4d7c-262">Verrà eseguito l'override del metodo `HandleUnauthorizedRequest` di AuthorizeAttribute con una logica semplice per visualizzare qualcosa di sensato anziché continuare il ciclo di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-262">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic to show something that makes sense instead of continuing the redirect loop.</span></span>
5. <span data-ttu-id="c4d7c-263">Creare un file denominato AuthorizeAttribute.cs nel progetto e incollare il codice seguente nel file.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-263">Create a file in the project called AuthorizeAttribute.cs, and paste the following code into it.</span></span>
   
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
   
    <span data-ttu-id="c4d7c-264">Il codice di override invia un messaggio HTTP 403 (accesso negato) invece di HTTP 401 (non autorizzato) per i casi autenticati ma non autorizzati.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-264">The override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="c4d7c-265">Eseguire nuovamente il debug con `F5`.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-265">Run the debugger again with `F5`.</span></span> <span data-ttu-id="c4d7c-266">Facendo clic su **Contact** verrà visualizzato un messaggio di errore più informativo (anche se graficamente meno elegante):</span><span class="sxs-lookup"><span data-stu-id="c4d7c-266">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="c4d7c-267">Pubblicare nuovamente l'applicazione nelle app Web di Servizio app di Azure, quindi testare il comportamento dell'applicazione attiva.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-267">Publish the application to Azure App Service Web Apps again, and test the behavior of the live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a><span data-ttu-id="c4d7c-268">Connettersi ai dati locali</span><span class="sxs-lookup"><span data-stu-id="c4d7c-268">Connect to on-premises data</span></span>
<span data-ttu-id="c4d7c-269">Un motivo per cui si potrebbe voler implementare la propria applicazione line-of-business in ADFS anziché in Azure Active Directory potrebbe essere correlato a questioni di conformità nella conservazione dei dati dell'organizzazione all'esterno dell'organizzazione stessa.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-269">A reason that you would want to implement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="c4d7c-270">Questo può anche significare che il sito Web di Azure deve accedere a database locali, poiché non si è autorizzati a usare il [database SQL](/services/sql-database/) come livello dati per le app Web.</span><span class="sxs-lookup"><span data-stu-id="c4d7c-270">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed to use [SQL Database](/services/sql-database/) as the data tier for your web apps.</span></span>

<span data-ttu-id="c4d7c-271">App Web del servizio app di Azure supporta l'accesso ai database locali tramite due approcci: [connessioni ibride](../biztalk-services/integration-hybrid-connection-overview.md) e [reti virtuali](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="c4d7c-271">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="c4d7c-272">Per altre informazioni, vedere il post relativo all' [uso dell'integrazione con una rete virtuale e delle connessioni ibride con App Web del servizio app di Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="c4d7c-272">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="c4d7c-273">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="c4d7c-273">Further resources</span></span>
* [<span data-ttu-id="c4d7c-274">Eseguire l'autenticazione con l'istanza locale di Active Directory nell'app Azure</span><span class="sxs-lookup"><span data-stu-id="c4d7c-274">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="c4d7c-275">Creare un'app line-of-business in Azure con l'autenticazione di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4d7c-275">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="c4d7c-276">Usare l'opzione di autenticazione dell'organizzazione locale (ADFS) con ASP.NET in Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c4d7c-276">Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="c4d7c-277">Eseguire la migrazione di un progetto Web di VS2013 da WIF a Katana</span><span class="sxs-lookup"><span data-stu-id="c4d7c-277">Migrate a VS2013 Web Project From WIF to Katana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="c4d7c-278">Informazioni generali su Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="c4d7c-278">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="c4d7c-279">Specifica WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="c4d7c-279">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

