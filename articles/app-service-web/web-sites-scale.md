---
title: Aumentare le prestazioni di un'app in Azure | Documentazione Microsoft
description: "Informazioni su come aumentare le prestazioni di un'app nel servizio app di Azure per aggiungere capacità e funzionalità."
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
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="e7aa2-103">Aumentare le prestazioni di un'app in Azure</span><span class="sxs-lookup"><span data-stu-id="e7aa2-103">Scale up an app in Azure</span></span>
<span data-ttu-id="e7aa2-104">Questo articolo illustra come passare a un piano superiore per un'app nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="e7aa2-105">Sono disponibili due flussi di lavoro per la scalabilità, l'aumento delle prestazioni e l'aumento del numero di istanze. Questo articolo illustra come aumentare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="e7aa2-106">[Aumentare le prestazioni](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): è possibile ottenere più CPU, memoria, spazio su disco e altre funzionalità, ad esempio macchine virtuali dedicate, domini e certificati personalizzati, slot di staging, ridimensionamento automatico e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="e7aa2-107">È possibile aumentare le prestazioni cambiando il piano tariffario del piano di servizio app a cui appartiene l'app.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="e7aa2-108">[Aumentare il numero di istanze](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): è possibile incrementare il numero di istanze di macchine virtuali che eseguono l'app.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="e7aa2-109">È possibile specificare al massimo 20 istanze, in base al piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="e7aa2-110">[ambienti del servizio app](../app-service/app-service-app-service-environments-readme.md) nel piano **Premium** tier will further nel pianocrease your scale-out count to 50 nel pianostances.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="e7aa2-111">Per altre informazioni sull'aumento del numero di istanze, vedere [Ridimensionare il conteggio delle istanze manualmente o automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="e7aa2-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="e7aa2-112">Questo articolo illustra come usare la scalabilità automatica, ovvero come ridimensionare automaticamente il numero di istanze sulla base di regole e pianificazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="e7aa2-113">Le impostazioni di scalabilità diventano effettive in pochi secondi e interessano tutte le app nel [piano di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7aa2-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="e7aa2-114">Non richiedono di modificare il codice o ridistribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="e7aa2-115">Per informazioni sui prezzi e le funzionalità dei singoli piani di servizio app, vedere [Dettagli prezzi del servizio app](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="e7aa2-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="e7aa2-116">Prima di modificare il livello **Gratuito** di un piano di servizio app, è necessario innanzitutto rimuovere i [limiti di spesa](https://azure.microsoft.com/pricing/spending-limits/) applicati alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="e7aa2-117">Per visualizzare o modificare le opzioni per la sottoscrizione del servizio app di Microsoft Azure, vedere [Sottoscrizioni di Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="e7aa2-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="e7aa2-118">Passare al piano tariffario superiore</span><span class="sxs-lookup"><span data-stu-id="e7aa2-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="e7aa2-119">Accedere al [portale di Azure][portal] dal browser.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="e7aa2-120">Nel pannello dell'app fare clic su **Tutte le impostazioni** e quindi su **Aumenta prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Passare al ridimensionamento di un'app di Azure.][ChooseWHP]
3. <span data-ttu-id="e7aa2-122">Scegliere il livello e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="e7aa2-123">Al termine dell'operazione, nella scheda **Notifiche** verrà visualizzata la scritta verde lampeggiante **OPERAZIONE RIUSCITA**.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="e7aa2-124">Risorse correlate alla scalabilità</span><span class="sxs-lookup"><span data-stu-id="e7aa2-124">Scale related resources</span></span>
<span data-ttu-id="e7aa2-125">Se l'applicazione dipende da altri servizi, ad esempio database SQL o Archiviazione di Azure, è anche possibile aumentare le prestazioni di tali risorse in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="e7aa2-126">Queste risorse non vengono ridimensionate con il piano di servizio app ma separatamente.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="e7aa2-127">In **Informazioni di base** fare clic sul collegamento **Gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Aumentare le prestazioni delle risorse correlate all'app di Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="e7aa2-129">Nella parte **Riepilogo** del pannello **Gruppo di risorse** fare quindi clic su una delle risorse da ridimensionare.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="e7aa2-130">La schermata seguente mostra una risorsa database SQL e una risorsa di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Passare al pannello gruppo di risorse per aumentare le prestazioni dell'app di Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="e7aa2-132">Per una risorsa database SQL, fare clic su **Impostazioni** > **Piano tariffario** per passare al piano tariffario superiore.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![Aumentare le prestazioni di back-end del database SQL per l'app di Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="e7aa2-134">Per l'istanza di database SQL è anche possibile attivare la [replica geografica](../sql-database/sql-database-geo-replication-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="e7aa2-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="e7aa2-135">Per una risorsa di Archiviazione di Azure, fare clic su **Impostazioni** > **Configurazione** per aumentare le prestazioni delle opzioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![Aumentare le prestazioni dell'account di Archiviazione di Azure usato dall'app di Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="e7aa2-137">Informazioni sulle funzionalità per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="e7aa2-137">Learn about developer features</span></span>
<span data-ttu-id="e7aa2-138">A seconda del piano tariffario, sono disponibili le seguenti funzionalità orientate agli sviluppatori:</span><span class="sxs-lookup"><span data-stu-id="e7aa2-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="e7aa2-139">Numero di bit</span><span class="sxs-lookup"><span data-stu-id="e7aa2-139">Bitness</span></span>
* <span data-ttu-id="e7aa2-140">Le modalità **Base**, **Standard** e **Premium** supportano applicazioni a 64 bit e a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="e7aa2-141">Le modalità del piano **Gratuito** e **Condiviso** supportano solo applicazioni a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="e7aa2-142">Supporto del debugger</span><span class="sxs-lookup"><span data-stu-id="e7aa2-142">Debugger support</span></span>
* <span data-ttu-id="e7aa2-143">Il supporto del debugger è disponibile per i piani **Gratuito**, **Condiviso** e **Basic** con una connessione per piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="e7aa2-144">Il supporto del debugger è disponibile per i piani **Standard** e **Premium** con 5 connessioni simultanee per piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="e7aa2-145">Informazioni sulle altre funzionalità</span><span class="sxs-lookup"><span data-stu-id="e7aa2-145">Learn about other features</span></span>
* <span data-ttu-id="e7aa2-146">Per informazioni dettagliate su tutte le altre funzionalità disponibili nei piani di servizio app, inclusi i prezzi e le funzionalità di interesse per tutti gli utenti (compresi gli sviluppatori), vedere [Dettagli prezzi del servizio app](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="e7aa2-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="e7aa2-147">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/) , dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e7aa2-148">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="e7aa2-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e7aa2-149">Next steps</span></span>
* <span data-ttu-id="e7aa2-150">Per iniziare a usare Azure, vedere la pagina relativa alla [versione di valutazione gratuita di Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7aa2-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e7aa2-151">Per informazioni su prezzi, supporto e contratti di servizio, visitare i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="e7aa2-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="e7aa2-152">Dettagli prezzi dei trasferimenti di dati</span><span class="sxs-lookup"><span data-stu-id="e7aa2-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="e7aa2-153">Piani di supporto per Azure</span><span class="sxs-lookup"><span data-stu-id="e7aa2-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="e7aa2-154">Contratti di servizio</span><span class="sxs-lookup"><span data-stu-id="e7aa2-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="e7aa2-155">Dettagli prezzi - Database SQL</span><span class="sxs-lookup"><span data-stu-id="e7aa2-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="e7aa2-156">[Dimensioni delle macchine virtuali e dei servizi cloud per Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="e7aa2-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="e7aa2-157">Dettagli prezzi del servizio app</span><span class="sxs-lookup"><span data-stu-id="e7aa2-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="e7aa2-158">Dettagli prezzi del servizio app - Connessioni SSL</span><span class="sxs-lookup"><span data-stu-id="e7aa2-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="e7aa2-159">Per informazioni sulle procedure consigliate per Servizio app di Azure, inclusa la creazione di un'architettura scalabile e resiliente, vedere il post di blog relativo alle [procedure consigliate per le app Web del servizio app di Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7aa2-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="e7aa2-160">Per i video sul ridimensionamento delle app del servizio app, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7aa2-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="e7aa2-161">Quando è necessario ridimensionare i siti Web di Azure - con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="e7aa2-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="e7aa2-162">Scalabilità automatica per i siti Web di Azure, pianificata o in base alla CPU - con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="e7aa2-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="e7aa2-163">Che cosa accade durante il ridimensionamento dei siti Web di Azure - con Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="e7aa2-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
