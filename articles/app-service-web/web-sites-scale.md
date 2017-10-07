---
title: aaaScale di un'app in Azure | Documenti Microsoft
description: "Informazioni su come tooscale di un'app in capacità tooadd di servizio App di Azure e funzionalità."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="033ba-103">Aumentare le prestazioni di un'app in Azure</span><span class="sxs-lookup"><span data-stu-id="033ba-103">Scale up an app in Azure</span></span>
<span data-ttu-id="033ba-104">In questo articolo illustra come tooscale l'app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="033ba-104">This article shows you how tooscale your app in Azure App Service.</span></span> <span data-ttu-id="033ba-105">Sono disponibili due flussi di lavoro per la scala di scalabilità, backup e la scalabilità orizzontale e in questo articolo illustra hello scala il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="033ba-105">There are two workflows for scaling, scale up and scale out, and this article explains hello scale up workflow.</span></span>

* <span data-ttu-id="033ba-106">[Aumentare le prestazioni](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): è possibile ottenere più CPU, memoria, spazio su disco e altre funzionalità, ad esempio macchine virtuali dedicate, domini e certificati personalizzati, slot di staging, ridimensionamento automatico e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="033ba-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="033ba-107">È la scalabilità verticale modificando hello piano tariffario del piano di servizio App dell'app a cui appartiene.</span><span class="sxs-lookup"><span data-stu-id="033ba-107">You scale up by changing hello pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="033ba-108">[Scalabilità orizzontale](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumentare il numero di hello di istanze di macchine Virtuali che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="033ba-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase hello number of VM instances that run your app.</span></span>
  <span data-ttu-id="033ba-109">È possibile scalare orizzontalmente tooas molte istanze di 20, a seconda del livello di prezzo.</span><span class="sxs-lookup"><span data-stu-id="033ba-109">You can scale out tooas many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="033ba-110">[Gli ambienti del servizio app](../app-service/app-service-app-service-environments-readme.md) in **Premium** livello faranno ulteriormente aumentare le istanze di too50 conteggio di scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="033ba-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count too50 instances.</span></span> <span data-ttu-id="033ba-111">Per altre informazioni sull'aumento del numero di istanze, vedere [Ridimensionare il conteggio delle istanze manualmente o automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="033ba-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="033ba-112">Sono disponibili come il ridimensionamento automatico toouse, ovvero il numero di istanze tooscale automaticamente in base a regole predefinite e le pianificazioni di out.</span><span class="sxs-lookup"><span data-stu-id="033ba-112">There you will find out how toouse autoscaling, which is tooscale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="033ba-113">scala impostazioni accettano solo secondi tooapply Hello e influiscono su tutte le app nel [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="033ba-113">hello scale settings take only seconds tooapply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="033ba-114">Non richiedono toochange è il codice o distribuire nuovamente l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="033ba-114">They do not require you toochange your code or redeploy your application.</span></span>

<span data-ttu-id="033ba-115">Per informazioni sui prezzi hello e le funzionalità dei singoli piani di servizio App, vedere [dettagli prezzi del servizio App](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="033ba-115">For information about hello pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="033ba-116">Prima di passare un piano di servizio App a hello **libero** livello, è necessario innanzitutto rimuovere hello [i limiti di spesa](https://azure.microsoft.com/pricing/spending-limits/) sul posto per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="033ba-116">Before you switch an App Service plan from hello **Free** tier, you must first remove hello [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="033ba-117">tooview o modificare le opzioni per la sottoscrizione di Microsoft Azure App Service, vedere [sottoscrizioni di Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="033ba-117">tooview or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="033ba-118">Passare al piano tariffario superiore</span><span class="sxs-lookup"><span data-stu-id="033ba-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="033ba-119">Nel browser aprire hello [portale di Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="033ba-119">In your browser, open hello [Azure portal][portal].</span></span>
2. <span data-ttu-id="033ba-120">Nel pannello dell'app fare clic su **Tutte le impostazioni** e quindi su **Aumenta prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="033ba-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Passare tooscale backup dell'app di Azure.][ChooseWHP]
3. <span data-ttu-id="033ba-122">Scegliere il livello e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="033ba-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="033ba-123">Hello **notifiche** scheda lampeggia una verde **successo** al termine dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="033ba-123">hello **Notifications** tab will flash a green **SUCCESS** after hello operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="033ba-124">Risorse correlate alla scalabilità</span><span class="sxs-lookup"><span data-stu-id="033ba-124">Scale related resources</span></span>
<span data-ttu-id="033ba-125">Se l'applicazione dipende da altri servizi, ad esempio database SQL o Archiviazione di Azure, è anche possibile aumentare le prestazioni di tali risorse in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="033ba-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="033ba-126">Queste risorse non vengono ridimensionate con il piano di servizio App hello e devono essere scalate separatamente.</span><span class="sxs-lookup"><span data-stu-id="033ba-126">These resources are not scaled with hello App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="033ba-127">In **Essentials**, fare clic su hello **gruppo di risorse** collegamento.</span><span class="sxs-lookup"><span data-stu-id="033ba-127">In **Essentials**, click hello **Resource group** link.</span></span>
   
    ![Aumentare le prestazioni delle risorse correlate all'app di Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="033ba-129">In hello **riepilogo** fa parte di hello **gruppo di risorse** pannello, fare clic su una risorsa che si desidera tooscale.</span><span class="sxs-lookup"><span data-stu-id="033ba-129">In hello **Summary** part of hello **Resource group** blade, click a resource that you want tooscale.</span></span> <span data-ttu-id="033ba-130">Hello seguente schermata mostra una risorsa del Database SQL e una risorsa di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="033ba-130">hello following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Passare tooresource gruppo blade tooscale backup dell'app di Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="033ba-132">Per una risorsa del Database SQL, fare clic su **impostazioni** > **tariffario** hello tooscale piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="033ba-132">For a SQL Database resource, click **Settings** > **Pricing tier** tooscale hello pricing tier.</span></span>
   
    ![Applicare la scalabilità verticale hello Database di SQL back-end per l'app Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="033ba-134">Per l'istanza di database SQL è anche possibile attivare la [replica geografica](../sql-database/sql-database-geo-replication-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="033ba-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="033ba-135">Per una risorsa di archiviazione di Azure, fare clic su **impostazioni** > **configurazione** tooscale le opzioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="033ba-135">For an Azure Storage resource, click **Settings** > **Configuration** tooscale up your storage options.</span></span>
   
    ![Applicare la scalabilità verticale account di archiviazione di Azure hello usato dalla tua app di Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="033ba-137">Informazioni sulle funzionalità per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="033ba-137">Learn about developer features</span></span>
<span data-ttu-id="033ba-138">A seconda di hello a livello di prezzo, hello orientate agli sviluppatori funzionalità seguenti sono disponibili:</span><span class="sxs-lookup"><span data-stu-id="033ba-138">Depending on hello pricing tier, hello following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="033ba-139">Numero di bit</span><span class="sxs-lookup"><span data-stu-id="033ba-139">Bitness</span></span>
* <span data-ttu-id="033ba-140">Hello **base**, **Standard**, e **Premium** livelli supportano applicazioni a 32 e 64 bit.</span><span class="sxs-lookup"><span data-stu-id="033ba-140">hello **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="033ba-141">Hello **libero** e **Shared** piano livelli supportano solo applicazioni a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="033ba-141">hello **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="033ba-142">Supporto del debugger</span><span class="sxs-lookup"><span data-stu-id="033ba-142">Debugger support</span></span>
* <span data-ttu-id="033ba-143">Supporto del debugger è disponibile per hello **libero**, **Shared**, e **base** modalità di una connessione per ogni piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="033ba-143">Debugger support is available for hello **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="033ba-144">Supporto del debugger è disponibile per hello **Standard** e **Premium** modalità di cinque connessioni simultanee per piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="033ba-144">Debugger support is available for hello **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="033ba-145">Informazioni sulle altre funzionalità</span><span class="sxs-lookup"><span data-stu-id="033ba-145">Learn about other features</span></span>
* <span data-ttu-id="033ba-146">Per informazioni dettagliate su tutti i rimanenti funzionalità nel servizio App hello hello piani, inclusi i prezzi e le funzioni di utenti di interesse tooall (inclusi gli sviluppatori), vedere [dettagli prezzi del servizio App](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="033ba-146">For detailed information about all of hello remaining features in hello App Service plans, including pricing and features of interest tooall users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="033ba-147">Se si desidera tooget avviato con il servizio App di Azure prima di iscriversi per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/) in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="033ba-147">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="033ba-148">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="033ba-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="033ba-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="033ba-149">Next steps</span></span>
* <span data-ttu-id="033ba-150">tooget introduttiva di Azure, vedere [versione di valutazione gratuita di Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="033ba-150">tooget started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="033ba-151">Per informazioni sui prezzi, supporto e contratto di servizio, visitare hello seguenti collegamenti.</span><span class="sxs-lookup"><span data-stu-id="033ba-151">For information about pricing, support, and SLA, visit hello following links.</span></span>
  
    [<span data-ttu-id="033ba-152">Dettagli prezzi dei trasferimenti di dati</span><span class="sxs-lookup"><span data-stu-id="033ba-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="033ba-153">Piani di supporto per Azure</span><span class="sxs-lookup"><span data-stu-id="033ba-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="033ba-154">Contratti di servizio</span><span class="sxs-lookup"><span data-stu-id="033ba-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="033ba-155">Dettagli prezzi - Database SQL</span><span class="sxs-lookup"><span data-stu-id="033ba-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="033ba-156">[Dimensioni delle macchine virtuali e dei servizi cloud per Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="033ba-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="033ba-157">Dettagli prezzi del servizio app</span><span class="sxs-lookup"><span data-stu-id="033ba-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="033ba-158">Dettagli prezzi del servizio app - Connessioni SSL</span><span class="sxs-lookup"><span data-stu-id="033ba-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="033ba-159">Per informazioni sulle procedure consigliate per Servizio app di Azure, inclusa la creazione di un'architettura scalabile e resiliente, vedere il post di blog relativo alle [procedure consigliate per le app Web del servizio app di Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="033ba-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="033ba-160">Per i video sulla scalabilità delle app di servizio App, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="033ba-160">For videos about scaling App Service apps, see hello following resources:</span></span>
  
  * [<span data-ttu-id="033ba-161">Quando siti Web di Azure - con Stefan Schackow tooScale</span><span class="sxs-lookup"><span data-stu-id="033ba-161">When tooScale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="033ba-162">Scalabilità automatica per i siti Web di Azure, pianificata o in base alla CPU - con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="033ba-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="033ba-163">Che cosa accade durante il ridimensionamento dei siti Web di Azure - con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="033ba-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
