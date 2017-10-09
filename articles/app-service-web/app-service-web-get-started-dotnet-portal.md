---
title: un'app web Umbraco nel portale di Azure in cinque minuti hello aaaDeploy | Documenti Microsoft
description: "Informazioni su come è facile toorun App web nel servizio App distribuendo un'applicazione ASP.NET di esempio. Visualizzare i risultati immediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="2881b-104">Distribuire un'app web Umbraco nel portale di Azure hello in cinque minuti</span><span class="sxs-lookup"><span data-stu-id="2881b-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="2881b-105">In questa esercitazione consente di distribuire n [Umbraco](https://our.umbraco.org/) app web troppo[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minuti.</span><span class="sxs-lookup"><span data-stu-id="2881b-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![App Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="2881b-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2881b-107">Prerequisites</span></span>
<span data-ttu-id="2881b-108">È necessario un account Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2881b-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="2881b-109">Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="2881b-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="2881b-110">È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure.</span><span class="sxs-lookup"><span data-stu-id="2881b-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="2881b-111">Creare un'app di avvio e riprodurre per tooan orari, è richiesto alcun carta di credito, nessun impegni.</span><span class="sxs-lookup"><span data-stu-id="2881b-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="2881b-112">Distribuire l'applicazione ASP.NET hello</span><span class="sxs-lookup"><span data-stu-id="2881b-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="2881b-113">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2881b-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2881b-114">Aprire [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="2881b-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="2881b-115">Questo collegamento è un tooimmediately di scelta rapida configurare una nuova app Umbraco hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2881b-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="2881b-116">In **Nome app**, digitare un nome per l'App Web.</span><span class="sxs-lookup"><span data-stu-id="2881b-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="2881b-117">Verrà visualizzato un segno di spunta verde nella casella hello se hello nome è univoco in hello `azurewebsites.net` dominio.</span><span class="sxs-lookup"><span data-stu-id="2881b-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="2881b-118">In **gruppo di risorse**, fare clic su **Crea nuovo** toocreate un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md), assegnargli un nome.</span><span class="sxs-lookup"><span data-stu-id="2881b-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="2881b-119">Fare clic su **Piano di servizio app/Località** > **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="2881b-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="2881b-120">Configurare hello [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) come illustrato:</span><span class="sxs-lookup"><span data-stu-id="2881b-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="2881b-121">In **piano di servizio App**, il nome di tipo hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="2881b-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="2881b-122">In **percorso**, scegliere un percorso toohost il piano.</span><span class="sxs-lookup"><span data-stu-id="2881b-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="2881b-123">Fare clic su **Piano tariffario**, quindi selezionare **F1 Free** (F1 gratuito) o un altro livello adatto e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2881b-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="2881b-124">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2881b-124">Click **OK**.</span></span>

    <span data-ttu-id="2881b-125">La configurazione di Umbraco CMS sarà ora simile hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="2881b-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configurazione in corso: la prima app Umbraco in Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="2881b-127">Fare clic su **Database SQL** > **Crea un nuovo database**.</span><span class="sxs-lookup"><span data-stu-id="2881b-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="2881b-128">Configurare hello Database SQL, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="2881b-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="2881b-129">In **Nome** digitare un nome, ad esempio **myDB**.</span><span class="sxs-lookup"><span data-stu-id="2881b-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="2881b-130">Fare clic su **Piano tariffario**, quindi selezionare **F Free** (F gratuito) o un altro livello adatto e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2881b-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="2881b-131">Fare clic su **Server di destinazione** > **Creare un nuovo server**.</span><span class="sxs-lookup"><span data-stu-id="2881b-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="2881b-132">Configurare il server di database di hello, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="2881b-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="2881b-133">In **Nome server** digitare il nome del server.</span><span class="sxs-lookup"><span data-stu-id="2881b-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="2881b-134">Verrà visualizzato un segno di spunta verde nella casella hello se hello nome è univoco in hello `.database.windows.net` dominio.</span><span class="sxs-lookup"><span data-stu-id="2881b-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="2881b-135">In **account di accesso amministratore Server**, hello tipo desiderato di nome utente amministratore.</span><span class="sxs-lookup"><span data-stu-id="2881b-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="2881b-136">In **Password** e **Conferma password**, digitare la password desiderata hello.</span><span class="sxs-lookup"><span data-stu-id="2881b-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="2881b-137">Nel percorso, selezionare hello nello stesso percorso utilizzato per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="2881b-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="2881b-138">Assicurarsi che **server tooaccess di servizi di azure Consenti** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="2881b-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="2881b-139">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2881b-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="2881b-140">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2881b-140">Click **Select**.</span></span>

13. <span data-ttu-id="2881b-141">Fare clic su **impostazioni app Web**, specificare nome utente di database hello e una password e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2881b-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="2881b-142">La configurazione di Umbraco CMS sarà ora simile hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="2881b-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configurazione completata: la prima app Umbraco in Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="2881b-144">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2881b-144">Click **Create**.</span></span>
    
    <span data-ttu-id="2881b-145">A questo punto, Azure crea l'app di Umbraco in base alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="2881b-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="2881b-146">Verrà visualizzata la notifica **La distribuzione è stata avviata...**.</span><span class="sxs-lookup"><span data-stu-id="2881b-146">You should see a **Deployment started...** notification.</span></span>

    ![Distribuzione riuscita, la prima app di Umbraco nel servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="2881b-148">Avviare e gestire l'app Web Umbraco</span><span class="sxs-lookup"><span data-stu-id="2881b-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="2881b-149">Quando Azure completa la distribuzione dell'app viene visualizzata un'altra notifica.</span><span class="sxs-lookup"><span data-stu-id="2881b-149">When Azure completes app deployment you see another notification.</span></span>

![Distribuzione riuscita, la prima app di Umbraco nel servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="2881b-151">Fare clic sulla notifica hello.</span><span class="sxs-lookup"><span data-stu-id="2881b-151">Click hello notification.</span></span> <span data-ttu-id="2881b-152">Se non viene individuato, è sempre possibile accedervi facendo clic sul controllo del segnale acustico notifica hello (![di sotto di notifica - Umbraco prima in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="2881b-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="2881b-153">Dovrebbe ora essere visualizzato il [pannello](../azure-resource-manager/resource-group-portal.md#manage-resources) per la gestione dell'app Web (*pannello*: una pagina del portale visualizzata in orizzontale).</span><span class="sxs-lookup"><span data-stu-id="2881b-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="2881b-154">Nella parte superiore di hello della pagina di panoramica hello, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="2881b-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Sfoglia, la prima app di Umbraco nel servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="2881b-156">Ora vengono visualizzate hello Umbraco **iniziale** pagina.</span><span class="sxs-lookup"><span data-stu-id="2881b-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="2881b-157">Configurare l'installazione Umbraco hello e avviare la riproduzione con esso.</span><span class="sxs-lookup"><span data-stu-id="2881b-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Configurazione di Umbraco: la prima app Umbraco in Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="2881b-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2881b-159">Next steps</span></span>
* <span data-ttu-id="2881b-160">[Distribuire un tooAzure di app web ASP.NET servizio App, tramite Visual Studio](app-service-web-get-started-dotnet.md) -informazioni su come una nuova app web di Azure da Visual Studio, utilizzando uno qualsiasi dei hello toocreate inclusi modelli di applicazione.</span><span class="sxs-lookup"><span data-stu-id="2881b-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="2881b-161">[Distribuire il servizio App di tooAzure codice](web-sites-deploy.md)-informazioni su come toodeploy da FTP o da origine controllare repository.</span><span class="sxs-lookup"><span data-stu-id="2881b-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="2881b-162">[Aggiungere app web prima di funzionalità tooyour](app-service-web-get-started-2.md) -richiedere toohello l'applicazione Azure che successivamente livello.</span><span class="sxs-lookup"><span data-stu-id="2881b-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="2881b-163">autenticare gli utenti,</span><span class="sxs-lookup"><span data-stu-id="2881b-163">Authenticate your users.</span></span> <span data-ttu-id="2881b-164">ridimensionare l'app in base alla richiesta</span><span class="sxs-lookup"><span data-stu-id="2881b-164">Scale it based on demand.</span></span> <span data-ttu-id="2881b-165">e configurare alcuni avvisi sulle prestazioni,</span><span class="sxs-lookup"><span data-stu-id="2881b-165">Set up some performance alerts.</span></span> <span data-ttu-id="2881b-166">tutto con pochi clic.</span><span class="sxs-lookup"><span data-stu-id="2881b-166">All with a few clicks.</span></span>
