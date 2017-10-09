---
title: un'app web WordPress in Azure App Service aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate una nuova versione di Azure web app per un blog di WordPress usando hello portale di Azure.
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
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="33c9c-103">Creare un'app WordPress nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="33c9c-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="33c9c-104">Questa esercitazione viene illustrato come un blog di WordPress toodeploy del sito da hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="33c9c-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="33c9c-105">Una volta terminato con l'esercitazione hello è necessario il proprio sito blog di WordPress backup e in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![Sito WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="33c9c-107">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="33c9c-107">You'll learn:</span></span>

* <span data-ttu-id="33c9c-108">Come un modello di applicazione in Azure Marketplace hello toofind.</span><span class="sxs-lookup"><span data-stu-id="33c9c-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="33c9c-109">Come toocreate un'app web in Azure App Service che è basato sul modello di hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="33c9c-110">Come le impostazioni di servizio App di Azure tooconfigure hello nuovo web app e il database.</span><span class="sxs-lookup"><span data-stu-id="33c9c-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="33c9c-111">Hello Azure Marketplace rende disponibile un'ampia gamma di applicazioni web comuni sviluppato da Microsoft, le aziende di terze parti e Apri origine software iniziative.</span><span class="sxs-lookup"><span data-stu-id="33c9c-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="33c9c-112">le applicazioni web Hello sono basate su una vasta gamma di popolari Framework, ad esempio [PHP](/develop/nodejs/) in questo esempio WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), e [Python](/develop/python/), tooname qualche.</span><span class="sxs-lookup"><span data-stu-id="33c9c-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="33c9c-113">un'app web da Azure Marketplace hello solo software necessario è browser hello usato per hello hello toocreate [portale Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="33c9c-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="33c9c-114">sito WordPress Hello da distribuire in questa esercitazione Usa MySQL per il database di hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="33c9c-115">Se si desidera utilizzare tooinstead Database SQL per database hello, vedere [Nami progetto](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="33c9c-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="33c9c-116">**Progetto Nami** è anche disponibile tramite Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="33c9c-117">toocomplete questa esercitazione, è necessario un account di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="33c9c-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="33c9c-118">Se non si dispone di un account, è possibile [attivare i benefici della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) oppure [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="33c9c-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="33c9c-119">Se si desidera tooget avviato con il servizio App di Azure prima di iscriversi per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="33c9c-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="33c9c-120">In questa pagina è possibile creare immediatamente un'app Web iniziale temporanea nel servizio app. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="33c9c-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="33c9c-121">Selezionare WordPress ed eseguire la configurazione per il servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="33c9c-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="33c9c-122">Accedi toohello [portale Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="33c9c-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="33c9c-123">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="33c9c-123">Click **New**.</span></span>
   
    ![Creazione di un nuovo sito][5]
3. <span data-ttu-id="33c9c-125">Cercare **WordPress** e quindi fare clic su **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="33c9c-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="33c9c-126">Se si desidera toouse Database SQL anziché MySQL, cercare **Nami progetto**.</span><span class="sxs-lookup"><span data-stu-id="33c9c-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress nell'elenco][7]
4. <span data-ttu-id="33c9c-128">Dopo aver letto descrizione hello di hello WordPress app, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="33c9c-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![Create](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="33c9c-130">Immettere un nome per l'app web hello in hello **app Web** casella.</span><span class="sxs-lookup"><span data-stu-id="33c9c-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="33c9c-131">Questo nome deve essere univoco nel dominio azurewebsites.net hello perché hello URL dell'app web hello sarà {name}. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="33c9c-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="33c9c-132">Se specifica un nome hello non è univoco, viene visualizzato un punto esclamativo rosso nella casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="33c9c-133">Se si dispone di più di una sottoscrizione, scegliere hello quello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="33c9c-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="33c9c-134">Selezionare un **Gruppo di risorse** o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="33c9c-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="33c9c-135">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33c9c-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="33c9c-136">Selezionare un **Piano di servizio app/Posizione** o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="33c9c-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="33c9c-137">Per altre informazioni sui piani del servizio app, vedere [Panoramica approfondita dei piani del servizio app di Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="33c9c-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="33c9c-138">Fare clic su **Database**e quindi in hello **Nuovo MySQL Database** pannello sono valori hello necessario per la configurazione del database MySQL.</span><span class="sxs-lookup"><span data-stu-id="33c9c-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="33c9c-139">a.</span><span class="sxs-lookup"><span data-stu-id="33c9c-139">a.</span></span> <span data-ttu-id="33c9c-140">Immettere un nuovo nome o lasciare il nome predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="33c9c-141">b.</span><span class="sxs-lookup"><span data-stu-id="33c9c-141">b.</span></span> <span data-ttu-id="33c9c-142">Lasciare hello **tipo di Database** impostare troppo**Shared**.</span><span class="sxs-lookup"><span data-stu-id="33c9c-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="33c9c-143">c.</span><span class="sxs-lookup"><span data-stu-id="33c9c-143">c.</span></span> <span data-ttu-id="33c9c-144">Scegliere hello nello stesso percorso come hello è selezionato per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="33c9c-145">d.</span><span class="sxs-lookup"><span data-stu-id="33c9c-145">d.</span></span> <span data-ttu-id="33c9c-146">Scegliere un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="33c9c-146">Choose a pricing tier.</span></span> <span data-ttu-id="33c9c-147">Mercury (gratuito con quantità minima di connessioni consentite e di spazio su disco) è ottimale per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="33c9c-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="33c9c-148">In hello **Nuovo MySQL Database** pannello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="33c9c-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="33c9c-149">In hello **WordPress** pannello, accettare i termini legali specifici hello e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="33c9c-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![Configurazione dell'app Web](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="33c9c-151">Servizio App di Azure crea app web hello, in genere in meno di un minuto.</span><span class="sxs-lookup"><span data-stu-id="33c9c-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="33c9c-152">È possibile controllare lo stato di avanzamento hello facendo clic sull'icona di campanello hello nella parte superiore di hello della pagina del portale hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![Indicatore di stato](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="33c9c-154">Avviare e gestire l'app Web WordPress</span><span class="sxs-lookup"><span data-stu-id="33c9c-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="33c9c-155">Al termine della creazione dell'app web hello, passare in hello Azure Portal toohello gruppo di risorse in cui è stato creato un'applicazione hello e si può vedere hello web app e database hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="33c9c-156">sono Hello risorse aggiuntive con icona lampadina hello [Application Insights](/services/application-insights/), che fornisce servizi di monitoraggio per l'app web.</span><span class="sxs-lookup"><span data-stu-id="33c9c-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="33c9c-157">In hello **gruppo di risorse** pannello, fare clic sulla riga di hello web app.</span><span class="sxs-lookup"><span data-stu-id="33c9c-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![Configurazione dell'app Web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="33c9c-159">Nel Pannello di hello Web app, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="33c9c-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![URL sito][browse]
4. <span data-ttu-id="33c9c-161">In hello WordPress **iniziale** immettere le informazioni di configurazione hello richieste da WordPress e quindi fare clic su **installa WordPress**.</span><span class="sxs-lookup"><span data-stu-id="33c9c-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Configurazione di WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="33c9c-163">Accedere con credenziali hello è stato creato in hello **iniziale** pagina.</span><span class="sxs-lookup"><span data-stu-id="33c9c-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="33c9c-164">Verrà visualizzata la pagina del dashboard del sito.</span><span class="sxs-lookup"><span data-stu-id="33c9c-164">Your site Dashboard page opens.</span></span>    
   
    ![Sito WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="33c9c-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33c9c-166">Next steps</span></span>
<span data-ttu-id="33c9c-167">Si è visto come toocreate e distribuire un'app web PHP dalla raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="33c9c-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="33c9c-168">Per ulteriori informazioni sull'utilizzo di PHP in Azure, vedere hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="33c9c-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="33c9c-169">Per ulteriori informazioni su come toowork con applicazione servizio Web App, vedere i collegamenti di hello in hello il lato sinistro di pagina hello (per le finestre del browser "wide") o nella parte superiore di hello della pagina di hello (per le finestre del browser "narrow").</span><span class="sxs-lookup"><span data-stu-id="33c9c-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="33c9c-170">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="33c9c-170">What's changed</span></span>
* <span data-ttu-id="33c9c-171">Per una modifica di toohello della Guida da tooApp di siti Web del servizio, vedere [servizio App di Azure e il relativo impatto sui servizi di Azure esistente](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="33c9c-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
