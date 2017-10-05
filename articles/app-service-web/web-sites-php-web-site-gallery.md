---
title: Creare un'App Web WordPress nel Servizio app di Azure | Microsoft Docs
description: Informazioni su come creare una nuova app Web di Azure per un blog WordPress mediante il portale di Azure.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 460afdabed947fb4018a9ea8a7a5bc7dc5bc89c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="60bd0-103">Creare un'app WordPress nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="60bd0-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="60bd0-104">Questa esercitazione illustra come distribuire un sito blog di WordPress da Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="60bd0-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="60bd0-105">Al termine dell'esercitazione si otterrà un sito di blog WordPress attivo e in esecuzione sul cloud.</span><span class="sxs-lookup"><span data-stu-id="60bd0-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![Sito WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="60bd0-107">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="60bd0-107">You'll learn:</span></span>

* <span data-ttu-id="60bd0-108">Come trovare un modello di applicazione in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="60bd0-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="60bd0-109">Come creare un'app Web basata sul modello nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="60bd0-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="60bd0-110">Come configurare le impostazioni del servizio app di Azure per la nuova app Web e il database.</span><span class="sxs-lookup"><span data-stu-id="60bd0-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="60bd0-111">Azure Marketplace rende disponibile un'ampia varietà di applicazioni Web ampiamente diffuse, sviluppate da Microsoft, da terze parti e tramite iniziative software open source.</span><span class="sxs-lookup"><span data-stu-id="60bd0-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="60bd0-112">Le app Web si basano su una vasta gamma di framework noti, come [PHP](/develop/nodejs/) in questo esempio di WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/) e [Python](/develop/python/), per citarne alcuni.</span><span class="sxs-lookup"><span data-stu-id="60bd0-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="60bd0-113">Per creare un'app Web da Azure Marketplace, l'unico software necessario è il browser usato per il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="60bd0-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="60bd0-114">Il sito WordPress distribuito in questa esercitazione usa MySQL come database.</span><span class="sxs-lookup"><span data-stu-id="60bd0-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="60bd0-115">Se invece si vuole usare il database SQL come database, vedere [progetto Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="60bd0-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="60bd0-116">**Progetto Nami** è disponibile anche tramite il Marketplace.</span><span class="sxs-lookup"><span data-stu-id="60bd0-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="60bd0-117">Per completare l'esercitazione, è necessario un account Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="60bd0-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="60bd0-118">Se non si dispone di un account, è possibile [attivare i benefici della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) oppure [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="60bd0-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="60bd0-119">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, passare alla pagina [Prova il servizio app](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="60bd0-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="60bd0-120">In questa pagina è possibile creare immediatamente un'app Web iniziale temporanea nel servizio app. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="60bd0-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="60bd0-121">Selezionare WordPress ed eseguire la configurazione per il servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="60bd0-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="60bd0-122">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="60bd0-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="60bd0-123">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-123">Click **New**.</span></span>
   
    ![Creazione di un nuovo sito][5]
3. <span data-ttu-id="60bd0-125">Cercare **WordPress** e quindi fare clic su **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="60bd0-126">Se si vuole usare il database SQL invece di MySQL, cercare **progetto Nami**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress nell'elenco][7]
4. <span data-ttu-id="60bd0-128">Dopo aver letto la descrizione dell'app WordPress, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![Crea](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="60bd0-130">Immettere un nome per l'app Web nella casella **App Web** .</span><span class="sxs-lookup"><span data-stu-id="60bd0-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="60bd0-131">Il nome deve essere univoco nel dominio azurewebsites.net perché l'URL dell'app Web sarà {nome}.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="60bd0-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="60bd0-132">Se il nome immesso non è univoco, nella casella di testo verrà visualizzato un punto esclamativo rosso.</span><span class="sxs-lookup"><span data-stu-id="60bd0-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="60bd0-133">Se sono disponibili più sottoscrizioni, scegliere quella che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="60bd0-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="60bd0-134">Selezionare un **Gruppo di risorse** o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="60bd0-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="60bd0-135">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60bd0-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="60bd0-136">Selezionare un **Piano di servizio app/Posizione** o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="60bd0-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="60bd0-137">Per altre informazioni sui piani del servizio app, vedere [Panoramica approfondita dei piani del servizio app di Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="60bd0-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="60bd0-138">Fare clic su **Database**, quindi nel pannello **Nuovo database MySQL** specificare i valori necessari per configurare il database MySQL.</span><span class="sxs-lookup"><span data-stu-id="60bd0-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="60bd0-139">a.</span><span class="sxs-lookup"><span data-stu-id="60bd0-139">a.</span></span> <span data-ttu-id="60bd0-140">Immettere un nuovo nome o lasciare il nome predefinito.</span><span class="sxs-lookup"><span data-stu-id="60bd0-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="60bd0-141">b.</span><span class="sxs-lookup"><span data-stu-id="60bd0-141">b.</span></span> <span data-ttu-id="60bd0-142">Lasciare **Tipo database** impostato su **Condiviso**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="60bd0-143">c.</span><span class="sxs-lookup"><span data-stu-id="60bd0-143">c.</span></span> <span data-ttu-id="60bd0-144">Scegliere la stessa posizione usata per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="60bd0-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="60bd0-145">d.</span><span class="sxs-lookup"><span data-stu-id="60bd0-145">d.</span></span> <span data-ttu-id="60bd0-146">Scegliere un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="60bd0-146">Choose a pricing tier.</span></span> <span data-ttu-id="60bd0-147">Mercury (gratuito con quantità minima di connessioni consentite e di spazio su disco) è ottimale per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="60bd0-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="60bd0-148">Nel pannello **Nuovo database MySQL** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="60bd0-149">Nel pannello **WordPress** accettare le condizioni legali, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![Configurazione dell'app Web](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="60bd0-151">Il servizio app di Azure crea l'app Web, in genere in meno di un minuto.</span><span class="sxs-lookup"><span data-stu-id="60bd0-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="60bd0-152">È possibile verificare lo stato facendo clic sull'icona a forma di campana nella parte superiore della pagina del portale.</span><span class="sxs-lookup"><span data-stu-id="60bd0-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![Indicatore di stato](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="60bd0-154">Avviare e gestire l'app Web WordPress</span><span class="sxs-lookup"><span data-stu-id="60bd0-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="60bd0-155">Al termine della creazione dell'app Web, nel portale di Azure passare al gruppo di risorse in cui è stata creata l'applicazione. L'app Web e il database saranno visualizzati nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="60bd0-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="60bd0-156">La risorsa aggiuntiva con l'icona a forma di lampadina è [Application Insights](/services/application-insights/), che fornisce servizi di monitoraggio per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="60bd0-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="60bd0-157">Nel pannello **Gruppo di risorse** fare clic sulla riga dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="60bd0-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![Configurazione dell'app Web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="60bd0-159">Nel pannello dell'app Web fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="60bd0-159">In the Web app blade, click **Browse**.</span></span>
   
    ![URL sito][browse]
4. <span data-ttu-id="60bd0-161">Nella **pagina iniziale** di WordPress immettere le informazioni di configurazione richieste da WordPress, quindi fare clic su **Install WordPress** (Installa WordPress).</span><span class="sxs-lookup"><span data-stu-id="60bd0-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Configurazione di WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="60bd0-163">Accedere usando le credenziali create nella pagina **iniziale** .</span><span class="sxs-lookup"><span data-stu-id="60bd0-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="60bd0-164">Verrà visualizzata la pagina del dashboard del sito.</span><span class="sxs-lookup"><span data-stu-id="60bd0-164">Your site Dashboard page opens.</span></span>    
   
    ![Sito WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="60bd0-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60bd0-166">Next steps</span></span>
<span data-ttu-id="60bd0-167">Si è appreso come creare e distribuire un'app Web PHP dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="60bd0-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="60bd0-168">Per altre informazioni sull'uso di PHP in Azure, vedere il [centro per sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="60bd0-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="60bd0-169">Per altre informazioni su come utilizzare le app Web del servizio app, vedere i collegamenti nel lato sinistro della pagina (nelle finestre del browser di grandi dimensioni) o nella parte superiore della pagina (per le finestre del browser ridotte).</span><span class="sxs-lookup"><span data-stu-id="60bd0-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="60bd0-170">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="60bd0-170">What's changed</span></span>
* <span data-ttu-id="60bd0-171">Per indicazioni sul passaggio dai Siti Web al servizio app, vedere [Servizio app di Azure e i servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="60bd0-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
