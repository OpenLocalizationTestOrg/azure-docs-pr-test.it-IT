---
title: un'app di WordPress nel portale di Azure in cinque minuti hello aaaDeploy | Documenti Microsoft
description: "Informazioni su come è facile toorun App web nel servizio App distribuendo un'applicazione WordPress. Visualizzare i risultati immediatamente."
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
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="33370-104">Distribuire un'app di WordPress nel portale di Azure hello in cinque minuti</span><span class="sxs-lookup"><span data-stu-id="33370-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="33370-105">In questa esercitazione illustra come toodeploy il primo [WordPress](https://wordpress.org/) app web troppo[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minuti.</span><span class="sxs-lookup"><span data-stu-id="33370-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Sito WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="33370-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="33370-107">Prerequisites</span></span>
<span data-ttu-id="33370-108">È necessario un account Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="33370-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="33370-109">Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="33370-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="33370-110">È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure.</span><span class="sxs-lookup"><span data-stu-id="33370-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="33370-111">Creare un'app di avvio e riprodurre per tooan orari, è richiesto alcun carta di credito, nessun impegni.</span><span class="sxs-lookup"><span data-stu-id="33370-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="33370-112">Distribuire app WordPress hello</span><span class="sxs-lookup"><span data-stu-id="33370-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="33370-113">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="33370-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="33370-114">Aprire [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="33370-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="33370-115">Questo collegamento è un tooimmediately di scelta rapida configurare una nuova app di WordPress in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="33370-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="33370-116">In **Nome app**, digitare un nome per l'App Web.</span><span class="sxs-lookup"><span data-stu-id="33370-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="33370-117">Verrà visualizzato un segno di spunta verde nella casella hello se hello nome è univoco in hello `azurewebsites.net` dominio.</span><span class="sxs-lookup"><span data-stu-id="33370-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="33370-118">In **gruppo di risorse**, fare clic su **Crea nuovo** toocreate un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md), assegnargli un nome.</span><span class="sxs-lookup"><span data-stu-id="33370-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="33370-119">In **Provider di database** selezionare **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="33370-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="33370-120">Fare clic su **Piano di servizio app/Località** > **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="33370-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="33370-121">Configurare hello [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) come illustrato:</span><span class="sxs-lookup"><span data-stu-id="33370-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="33370-122">In **piano di servizio App**, il nome di tipo hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="33370-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="33370-123">In **percorso**, scegliere un percorso toohost il piano.</span><span class="sxs-lookup"><span data-stu-id="33370-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="33370-124">Fare clic su **Piano tariffario**, quindi selezionare **F1 Free** (F1 gratuito) o un altro livello adatto e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="33370-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="33370-125">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="33370-125">Click **OK**.</span></span>

8. <span data-ttu-id="33370-126">Fare clic su **Database** > **Creare nuovo**.</span><span class="sxs-lookup"><span data-stu-id="33370-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="33370-127">Configurare hello Database SQL, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="33370-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="33370-128">In **Nome database** digitare un nome per il database.</span><span class="sxs-lookup"><span data-stu-id="33370-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="33370-129">In **percorso**, scegliere hello stesso percorso hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="33370-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="33370-130">Fare clic su **Piano tariffario**, quindi selezionare **Mercurio** o un altro livello adatto e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="33370-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="33370-131">Fare clic su **Note legali** e quindi su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="33370-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="33370-132">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="33370-132">Click **OK**.</span></span>

9. <span data-ttu-id="33370-133">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="33370-133">Click **Create**.</span></span>

    <span data-ttu-id="33370-134">A questo punto, Azure crea l'app di WordPress in base alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="33370-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="33370-135">Verrà visualizzata la notifica **La distribuzione è stata avviata...**.</span><span class="sxs-lookup"><span data-stu-id="33370-135">You should see a **Deployment started...** notification.</span></span>

    ![Distribuzione avviata, la prima app di WordPress nel servizio app di Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="33370-137">Avviare e gestire l'app Web WordPress</span><span class="sxs-lookup"><span data-stu-id="33370-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="33370-138">Quando Azure completa la distribuzione dell'app viene visualizzata un'altra notifica.</span><span class="sxs-lookup"><span data-stu-id="33370-138">When Azure completes app deployment you see another notification.</span></span>

![Distribuzione riuscita, la prima app di WordPress nel servizio app di Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="33370-140">Fare clic sulla notifica hello.</span><span class="sxs-lookup"><span data-stu-id="33370-140">Click hello notification.</span></span> <span data-ttu-id="33370-141">Se non viene individuato, è sempre possibile accedervi facendo clic sul controllo del segnale acustico notifica hello (![di sotto di notifica - primo WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="33370-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="33370-142">Dovrebbe ora essere visualizzato il [pannello](../azure-resource-manager/resource-group-portal.md#manage-resources) per la gestione dell'app Web (*pannello*: una pagina del portale visualizzata in orizzontale).</span><span class="sxs-lookup"><span data-stu-id="33370-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="33370-143">Nella parte superiore di hello della pagina di panoramica hello, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="33370-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Sfoglia, la prima app di WordPress nel servizio app di Azure](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="33370-145">Ora vengono visualizzate hello WordPress **iniziale** pagina.</span><span class="sxs-lookup"><span data-stu-id="33370-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="33370-146">Configurare l'installazione WordPress hello e avviare la riproduzione con esso.</span><span class="sxs-lookup"><span data-stu-id="33370-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![Configurazione di WordPress, la prima app di WordPress nel Servizio app di Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="33370-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33370-148">Next steps</span></span>
* <span data-ttu-id="33370-149">[Creare, configurare e distribuire un tooAzure di app web Laravel](app-service-web-php-get-started.md) -acquisire le competenze di base hello è necessario toorun qualsiasi applicazione web PHP in Azure, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="33370-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="33370-150">Creare e configurare app in Azure da PowerShell/Bash.</span><span class="sxs-lookup"><span data-stu-id="33370-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="33370-151">Impostare la versione di PHP.</span><span class="sxs-lookup"><span data-stu-id="33370-151">Set PHP version.</span></span>
    * <span data-ttu-id="33370-152">Utilizzare un file di avvio che non è presente nella directory dell'applicazione hello radice.</span><span class="sxs-lookup"><span data-stu-id="33370-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="33370-153">Abilitare l'automazione Composer.</span><span class="sxs-lookup"><span data-stu-id="33370-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="33370-154">Accedere a variabili specifiche dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="33370-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="33370-155">Risolvere i problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="33370-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="33370-156">[Distribuire il servizio App di tooAzure codice](web-sites-deploy.md)-informazioni su come toodeploy da FTP o da origine controllare repository.</span><span class="sxs-lookup"><span data-stu-id="33370-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="33370-157">[Aggiungere app web prima di funzionalità tooyour](app-service-web-get-started-2.md) -richiedere toohello l'applicazione Azure che successivamente livello.</span><span class="sxs-lookup"><span data-stu-id="33370-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="33370-158">autenticare gli utenti,</span><span class="sxs-lookup"><span data-stu-id="33370-158">Authenticate your users.</span></span> <span data-ttu-id="33370-159">ridimensionare l'app in base alla richiesta</span><span class="sxs-lookup"><span data-stu-id="33370-159">Scale it based on demand.</span></span> <span data-ttu-id="33370-160">e configurare alcuni avvisi sulle prestazioni,</span><span class="sxs-lookup"><span data-stu-id="33370-160">Set up some performance alerts.</span></span> <span data-ttu-id="33370-161">tutto con pochi clic.</span><span class="sxs-lookup"><span data-stu-id="33370-161">All with a few clicks.</span></span>
