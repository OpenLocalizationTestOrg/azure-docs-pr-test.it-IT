---
title: Distribuire un'app Umbraco nel Portale di Azure in cinque minuti | Microsoft Docs
description: Informazioni su come eseguire facilmente app Web nel servizio app distribuendo un'app ASP.NET di esempio. Visualizzare i risultati immediatamente.
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
ms.openlocfilehash: 9e3e2130a66cdfe5f06eb3b366e53028c44e7e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="4e41f-104">Distribuire un'app Umbraco nel Portale di Azure in cinque minuti</span><span class="sxs-lookup"><span data-stu-id="4e41f-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="4e41f-105">Questa esercitazione illustra come distribuire un'app Web [Umbraco](https://our.umbraco.org/) nel [Servizio app di Azure](../app-service/app-service-value-prop-what-is.md) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="4e41f-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![App Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="4e41f-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4e41f-107">Prerequisites</span></span>
<span data-ttu-id="4e41f-108">È necessario un account Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4e41f-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="4e41f-109">Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="4e41f-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="4e41f-110">È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure.</span><span class="sxs-lookup"><span data-stu-id="4e41f-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="4e41f-111">Creare un'app iniziale e provarla per un'ora, senza impegno e senza dover usare la carta di credito.</span><span class="sxs-lookup"><span data-stu-id="4e41f-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="4e41f-112">Distribuire l'app ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4e41f-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="4e41f-113">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e41f-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4e41f-114">Aprire [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="4e41f-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="4e41f-115">Questo collegamento è un scelta rapida per configurare immediatamente una nuova app di Umbraco nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e41f-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="4e41f-116">In **Nome app**, digitare un nome per l'App Web.</span><span class="sxs-lookup"><span data-stu-id="4e41f-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="4e41f-117">Se il nome è univoco nel dominio `azurewebsites.net`, verrà visualizzato un segno di spunta verde nella casella.</span><span class="sxs-lookup"><span data-stu-id="4e41f-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="4e41f-118">In **Gruppi risorse**, fare clic su **Crea nuovo** per creare un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md), quindi assegnargli un nome.</span><span class="sxs-lookup"><span data-stu-id="4e41f-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="4e41f-119">Fare clic su **Piano di servizio app/Località** > **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="4e41f-120">Configurare il [piano di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) come illustrato:</span><span class="sxs-lookup"><span data-stu-id="4e41f-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="4e41f-121">In **Piano di servizio app** digitare il nome desiderato.</span><span class="sxs-lookup"><span data-stu-id="4e41f-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="4e41f-122">In **Località**, scegliere un percorso per ospitare il piano.</span><span class="sxs-lookup"><span data-stu-id="4e41f-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="4e41f-123">Fare clic su **Piano tariffario**, quindi selezionare **F1 Free** (F1 gratuito) o un altro livello adatto e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="4e41f-124">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-124">Click **OK**.</span></span>

    <span data-ttu-id="4e41f-125">La configurazione CMS di Umbraco sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="4e41f-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configurazione in corso: la prima app Umbraco in Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="4e41f-127">Fare clic su **Database SQL** > **Crea un nuovo database**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="4e41f-128">Configurare il Database SQL come illustrato:</span><span class="sxs-lookup"><span data-stu-id="4e41f-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="4e41f-129">In **Nome** digitare un nome, ad esempio **myDB**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="4e41f-130">Fare clic su **Piano tariffario**, quindi selezionare **F Free** (F gratuito) o un altro livello adatto e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="4e41f-131">Fare clic su **Server di destinazione** > **Creare un nuovo server**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="4e41f-132">Configurare il server del database, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="4e41f-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="4e41f-133">In **Nome server** digitare il nome del server.</span><span class="sxs-lookup"><span data-stu-id="4e41f-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="4e41f-134">Se il nome è univoco nel dominio `.database.windows.net`, verrà visualizzato un segno di spunta verde nella casella.</span><span class="sxs-lookup"><span data-stu-id="4e41f-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="4e41f-135">In **Account di accesso amministratore server** digitare il nome utente amministratore desiderato.</span><span class="sxs-lookup"><span data-stu-id="4e41f-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="4e41f-136">In **Password** e **Conferma password** digitare la password desiderata.</span><span class="sxs-lookup"><span data-stu-id="4e41f-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="4e41f-137">In Località, selezionare la stessa località usata per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="4e41f-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="4e41f-138">Verificare che l'opzione **Consenti ai servizi di Azure di accedere al server** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="4e41f-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="4e41f-139">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="4e41f-140">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-140">Click **Select**.</span></span>

13. <span data-ttu-id="4e41f-141">Fare clic su **Impostazioni app Web**, specificare il nome utente e la password del database e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="4e41f-142">La configurazione CMS di Umbraco sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="4e41f-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configurazione completata: la prima app Umbraco in Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="4e41f-144">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-144">Click **Create**.</span></span>
    
    <span data-ttu-id="4e41f-145">A questo punto, Azure crea l'app di Umbraco in base alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="4e41f-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="4e41f-146">Verrà visualizzata la notifica **La distribuzione è stata avviata...**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-146">You should see a **Deployment started...** notification.</span></span>

    ![Distribuzione riuscita, la prima app di Umbraco nel servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="4e41f-148">Avviare e gestire l'app Web Umbraco</span><span class="sxs-lookup"><span data-stu-id="4e41f-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="4e41f-149">Quando Azure completa la distribuzione dell'app viene visualizzata un'altra notifica.</span><span class="sxs-lookup"><span data-stu-id="4e41f-149">When Azure completes app deployment you see another notification.</span></span>

![Distribuzione riuscita, la prima app di Umbraco nel servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="4e41f-151">Fare clic sulla notifica.</span><span class="sxs-lookup"><span data-stu-id="4e41f-151">Click the notification.</span></span> <span data-ttu-id="4e41f-152">Se non è stata letta, è sempre possibile accedervi facendo clic sul simbolo della campana della notifica (![Campana di notifica, prima app di Umbraco nel Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="4e41f-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="4e41f-153">Dovrebbe ora essere visualizzato il [pannello](../azure-resource-manager/resource-group-portal.md#manage-resources) per la gestione dell'app Web (*pannello*: una pagina del portale visualizzata in orizzontale).</span><span class="sxs-lookup"><span data-stu-id="4e41f-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="4e41f-154">Nella parte superiore della pagina Panoramica, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="4e41f-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Sfoglia, la prima app di Umbraco nel servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="4e41f-156">A questo punto viene visualizzata la pagina di **Benvenuto** di Umbraco.</span><span class="sxs-lookup"><span data-stu-id="4e41f-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="4e41f-157">Configurare l'installazione di Umbraco e iniziare a usarla.</span><span class="sxs-lookup"><span data-stu-id="4e41f-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Configurazione di Umbraco: la prima app Umbraco in Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="4e41f-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4e41f-159">Next steps</span></span>
* <span data-ttu-id="4e41f-160">[Distribuire un'app web ASP.NET in Servizio app di Azure, tramite Visual Studio](app-service-web-get-started-dotnet.md): informazioni su come creare una nuova app Web di Azure da Visual Studio, mediante uno dei modelli di applicazione incluso.</span><span class="sxs-lookup"><span data-stu-id="4e41f-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="4e41f-161">[Distribuire il codice nel Servizio app di Azure](web-sites-deploy.md): informazioni su come distribuire da FTP o da repository di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="4e41f-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="4e41f-162">[Aggiungere funzionalità alla prima app Web](app-service-web-get-started-2.md): eseguire l'app di Azure nel livello successivo.</span><span class="sxs-lookup"><span data-stu-id="4e41f-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="4e41f-163">autenticare gli utenti,</span><span class="sxs-lookup"><span data-stu-id="4e41f-163">Authenticate your users.</span></span> <span data-ttu-id="4e41f-164">ridimensionare l'app in base alla richiesta</span><span class="sxs-lookup"><span data-stu-id="4e41f-164">Scale it based on demand.</span></span> <span data-ttu-id="4e41f-165">e configurare alcuni avvisi sulle prestazioni,</span><span class="sxs-lookup"><span data-stu-id="4e41f-165">Set up some performance alerts.</span></span> <span data-ttu-id="4e41f-166">tutto con pochi clic.</span><span class="sxs-lookup"><span data-stu-id="4e41f-166">All with a few clicks.</span></span>
