---
title: Distribuire un'app di WordPress nel Portale di Azure in cinque minuti | Microsoft Docs
description: Informazioni su come eseguire facilmente App Web nel servizio app mediante la distribuzione di un'app di WordPress. Visualizzare i risultati immediatamente.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: ef3be9823384bd8dc978c86f5cfde00d1117c4a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-wordpress-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="27f67-104">Distribuire un'app di WordPress nel Portale di Azure in cinque minuti</span><span class="sxs-lookup"><span data-stu-id="27f67-104">Deploy a WordPress app in the Azure portal in five minutes</span></span>

<span data-ttu-id="27f67-105">Questa esercitazione illustra come distribuire la prima App Web di [WordPress](https://wordpress.org/) nel [servizio app di Azure](../app-service/app-service-value-prop-what-is.md) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="27f67-105">This tutorial shows you how to deploy your first [WordPress](https://wordpress.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Sito WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="27f67-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="27f67-107">Prerequisites</span></span>
<span data-ttu-id="27f67-108">È necessario un account Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="27f67-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="27f67-109">Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="27f67-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="27f67-110">È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure.</span><span class="sxs-lookup"><span data-stu-id="27f67-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="27f67-111">Creare un'app iniziale e provarla per un'ora, senza impegno e senza dover usare la carta di credito.</span><span class="sxs-lookup"><span data-stu-id="27f67-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-wordpress-app"></a><span data-ttu-id="27f67-112">Distribuire l'app di WordPress</span><span class="sxs-lookup"><span data-stu-id="27f67-112">Deploy the WordPress app</span></span>
1. <span data-ttu-id="27f67-113">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27f67-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="27f67-114">Aprire [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="27f67-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="27f67-115">Questo collegamento è un scelta rapida per configurare immediatamente una nuova app di WordPress nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="27f67-115">This link is a shortcut to immediately configure a new WordPress app in the Azure portal.</span></span>

3. <span data-ttu-id="27f67-116">In **Nome app**, digitare un nome per l'App Web.</span><span class="sxs-lookup"><span data-stu-id="27f67-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="27f67-117">Se il nome è univoco nel dominio `azurewebsites.net`, verrà visualizzato un segno di spunta verde nella casella.</span><span class="sxs-lookup"><span data-stu-id="27f67-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="27f67-118">In **Gruppi risorse**, fare clic su **Crea nuovo** per creare un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md), quindi assegnargli un nome.</span><span class="sxs-lookup"><span data-stu-id="27f67-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="27f67-119">In **Provider di database** selezionare **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="27f67-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="27f67-120">Fare clic su **Piano di servizio app/Località** > **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="27f67-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="27f67-121">Configurare il [piano di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) come illustrato:</span><span class="sxs-lookup"><span data-stu-id="27f67-121">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="27f67-122">In **Piano di servizio app** digitare il nome desiderato.</span><span class="sxs-lookup"><span data-stu-id="27f67-122">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="27f67-123">In **Località**, scegliere un percorso per ospitare il piano.</span><span class="sxs-lookup"><span data-stu-id="27f67-123">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="27f67-124">Fare clic su **Piano tariffario**, quindi selezionare **F1 Free** (F1 gratuito) o un altro livello adatto e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="27f67-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="27f67-125">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="27f67-125">Click **OK**.</span></span>

8. <span data-ttu-id="27f67-126">Fare clic su **Database** > **Creare nuovo**.</span><span class="sxs-lookup"><span data-stu-id="27f67-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="27f67-127">Configurare il Database SQL come illustrato:</span><span class="sxs-lookup"><span data-stu-id="27f67-127">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="27f67-128">In **Nome database** digitare un nome per il database.</span><span class="sxs-lookup"><span data-stu-id="27f67-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="27f67-129">In **Località** scegliere la stessa ubicazione del piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="27f67-129">In **Location**, choose the same location as the App Service plan.</span></span>
    - <span data-ttu-id="27f67-130">Fare clic su **Piano tariffario**, quindi selezionare **Mercurio** o un altro livello adatto e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="27f67-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="27f67-131">Fare clic su **Note legali** e quindi su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="27f67-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="27f67-132">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="27f67-132">Click **OK**.</span></span>

9. <span data-ttu-id="27f67-133">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="27f67-133">Click **Create**.</span></span>

    <span data-ttu-id="27f67-134">A questo punto, Azure crea l'app di WordPress in base alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="27f67-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="27f67-135">Verrà visualizzata la notifica **La distribuzione è stata avviata...**.</span><span class="sxs-lookup"><span data-stu-id="27f67-135">You should see a **Deployment started...** notification.</span></span>

    ![Distribuzione avviata, la prima app di WordPress nel servizio app di Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="27f67-137">Avviare e gestire l'app Web WordPress</span><span class="sxs-lookup"><span data-stu-id="27f67-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="27f67-138">Quando Azure completa la distribuzione dell'app viene visualizzata un'altra notifica.</span><span class="sxs-lookup"><span data-stu-id="27f67-138">When Azure completes app deployment you see another notification.</span></span>

![Distribuzione riuscita, la prima app di WordPress nel servizio app di Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="27f67-140">Fare clic sulla notifica.</span><span class="sxs-lookup"><span data-stu-id="27f67-140">Click the notification.</span></span> <span data-ttu-id="27f67-141">Se non è stata letta, è sempre possibile accedervi facendo clic sul simbolo della campana della notifica (![Campana di notifica, prima app di WordPress nel Servizio app di Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="27f67-141">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="27f67-142">Dovrebbe ora essere visualizzato il [pannello](../azure-resource-manager/resource-group-portal.md#manage-resources) per la gestione dell'App Web (*pannello*: una pagina del portale visualizzata in orizzontale).</span><span class="sxs-lookup"><span data-stu-id="27f67-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="27f67-143">Nella parte superiore della pagina Panoramica, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="27f67-143">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Sfoglia, la prima app di WordPress nel servizio app di Azure](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="27f67-145">A questo punto viene visualizzata la pagina di **Benvenuto** di WordPress.</span><span class="sxs-lookup"><span data-stu-id="27f67-145">Now you see the WordPress **Welcome** page.</span></span> <span data-ttu-id="27f67-146">Configurare l'installazione di WordPress e iniziare a usarlo.</span><span class="sxs-lookup"><span data-stu-id="27f67-146">Configure the WordPress installation and start playing with it!</span></span>

    ![Configurazione di WordPress, la prima app di WordPress nel Servizio app di Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="27f67-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27f67-148">Next steps</span></span>
* <span data-ttu-id="27f67-149">[Creare, configurare e distribuire un'App Web Laravel in Azure](app-service-web-php-get-started.md): informazioni sulle nozioni di base necessarie per eseguire le App Web PHP in Azure, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="27f67-149">[Create, configure, and deploy a Laravel web app to Azure](app-service-web-php-get-started.md) - Learn the basic skills you need to run any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="27f67-150">Creare e configurare app in Azure da PowerShell/Bash.</span><span class="sxs-lookup"><span data-stu-id="27f67-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="27f67-151">Impostare la versione di PHP.</span><span class="sxs-lookup"><span data-stu-id="27f67-151">Set PHP version.</span></span>
    * <span data-ttu-id="27f67-152">Usare un file di avvio che non si trova nella directory dell'applicazione radice.</span><span class="sxs-lookup"><span data-stu-id="27f67-152">Use a start file that is not in the root application directory.</span></span>
    * <span data-ttu-id="27f67-153">Abilitare l'automazione Composer.</span><span class="sxs-lookup"><span data-stu-id="27f67-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="27f67-154">Accedere a variabili specifiche dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="27f67-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="27f67-155">Risolvere i problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="27f67-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="27f67-156">[Distribuire il codice nel Servizio app di Azure](web-sites-deploy.md): informazioni su come distribuire da FTP o da repository di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="27f67-156">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="27f67-157">[Aggiungere funzionalità alla prima app Web](app-service-web-get-started-2.md): eseguire l'app di Azure nel livello successivo.</span><span class="sxs-lookup"><span data-stu-id="27f67-157">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="27f67-158">autenticare gli utenti,</span><span class="sxs-lookup"><span data-stu-id="27f67-158">Authenticate your users.</span></span> <span data-ttu-id="27f67-159">ridimensionare l'app in base alla richiesta</span><span class="sxs-lookup"><span data-stu-id="27f67-159">Scale it based on demand.</span></span> <span data-ttu-id="27f67-160">e configurare alcuni avvisi sulle prestazioni,</span><span class="sxs-lookup"><span data-stu-id="27f67-160">Set up some performance alerts.</span></span> <span data-ttu-id="27f67-161">tutto con pochi clic.</span><span class="sxs-lookup"><span data-stu-id="27f67-161">All with a few clicks.</span></span>
