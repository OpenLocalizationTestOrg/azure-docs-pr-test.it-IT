---
title: "Configurazione della scalabilità automatica di un servizio cloud nel portale classico | Microsoft Docs"
description: "(classico) Informazioni su come usare il portale classico per configurare le regole di scalabilità automatica per un ruolo Web o un ruolo di lavoro del servizio cloud in Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 90d55bbac6e113d6add848ace67cf0749e26342b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="21d1c-103">Come configurare la scalabilità automatica per un servizio cloud nel portale classico</span><span class="sxs-lookup"><span data-stu-id="21d1c-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21d1c-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="21d1c-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="21d1c-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="21d1c-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="21d1c-106">Nella pagina Scalabilità del portale di Azure classico, è possibile configurare le impostazioni di scalabilità automatica per il ruolo Web o per un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="21d1c-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="21d1c-107">In alternativa, è possibile configurare la scalabilità manuale invece della scalabilità automatica basata su regole.</span><span class="sxs-lookup"><span data-stu-id="21d1c-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="21d1c-108">Questo articolo è incentrato sui ruoli Web e di lavoro del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="21d1c-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="21d1c-109">Quando si crea una macchina virtuale (distribuzione classica) direttamente, questa viene ospitata in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="21d1c-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="21d1c-110">Alcune delle presenti informazioni si applicano a questi tipi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="21d1c-110">Some of this information applies to these types of virtual machines.</span></span> <span data-ttu-id="21d1c-111">Scalare un set di disponibilità di macchine virtuali significa semplicemente attivarle e disattivarle in base alle regole di scalabilità configurate.</span><span class="sxs-lookup"><span data-stu-id="21d1c-111">Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure.</span></span> <span data-ttu-id="21d1c-112">Per altre informazioni sulle macchine virtuali e sui set di disponibilità, vedere [Gestire la disponibilità delle macchine virtuali](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="21d1c-112">For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="21d1c-113">Prima di configurare la scalabilità per l'applicazione, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="21d1c-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="21d1c-114">La scalabilità è influenzata dall'utilizzo di core.</span><span class="sxs-lookup"><span data-stu-id="21d1c-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="21d1c-115">Le istanze del ruolo più ampie usano più core.</span><span class="sxs-lookup"><span data-stu-id="21d1c-115">Larger role instances use more cores.</span></span> <span data-ttu-id="21d1c-116">È possibile ridimensionare il numero di istanze di un'applicazione solo entro i limiti di core previsti dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="21d1c-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="21d1c-117">Si supponga, ad esempio, che la sottoscrizione abbia un limite di 20 core.</span><span class="sxs-lookup"><span data-stu-id="21d1c-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="21d1c-118">Se si esegue un'applicazione con due servizi cloud di medie dimensioni (per un totale di 4 core), l'aumento di altre distribuzioni del servizio cloud nella sottoscrizione è limitata ai 16 core rimanenti.</span><span class="sxs-lookup"><span data-stu-id="21d1c-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="21d1c-119">Per altre informazioni sulle dimensioni, vedere [Dimensioni dei servizi cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="21d1c-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="21d1c-120">È necessario creare una coda e associarla a un ruolo prima di ridimensionare il numero di istanze di un'applicazione in base a una soglia di messaggi.</span><span class="sxs-lookup"><span data-stu-id="21d1c-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="21d1c-121">Per altre informazioni, vedere [Come utilizzare il servizio di archiviazione di accodamento](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="21d1c-121">For more information, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="21d1c-122">È possibile scalare le risorse collegate al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="21d1c-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="21d1c-123">Per altre informazioni sul collegamento di risorse, vedere [Procedura: Collegare una risorsa a un servizio cloud](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="21d1c-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="21d1c-124">Per abilitare la disponibilità elevata dell'applicazione, è necessario accertarsi che sia distribuita con due o più istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="21d1c-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="21d1c-125">Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="21d1c-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="21d1c-126">Pianificazione della scalabilità</span><span class="sxs-lookup"><span data-stu-id="21d1c-126">Schedule scaling</span></span>
<span data-ttu-id="21d1c-127">Per impostazione predefinita, i ruoli non seguono una pianificazione specifica.</span><span class="sxs-lookup"><span data-stu-id="21d1c-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="21d1c-128">Per questo motivo, tutte le impostazioni modificate vengono applicate in qualsiasi momento e tutti i giorni dell'anno.</span><span class="sxs-lookup"><span data-stu-id="21d1c-128">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="21d1c-129">Se lo si desidera, è possibile configurare la scalabilità manuale o automatica per le modalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="21d1c-129">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="21d1c-130">Giorni della settimana</span><span class="sxs-lookup"><span data-stu-id="21d1c-130">Weekdays</span></span>
* <span data-ttu-id="21d1c-131">Fine settimana</span><span class="sxs-lookup"><span data-stu-id="21d1c-131">Weekends</span></span>
* <span data-ttu-id="21d1c-132">Ore notturne</span><span class="sxs-lookup"><span data-stu-id="21d1c-132">Week nights</span></span>
* <span data-ttu-id="21d1c-133">Ore diurne</span><span class="sxs-lookup"><span data-stu-id="21d1c-133">Week mornings</span></span>
* <span data-ttu-id="21d1c-134">Date specifiche</span><span class="sxs-lookup"><span data-stu-id="21d1c-134">Specific dates</span></span>
* <span data-ttu-id="21d1c-135">Intervalli di date specifiche</span><span class="sxs-lookup"><span data-stu-id="21d1c-135">Specific date ranges</span></span>

<span data-ttu-id="21d1c-136">L'impostazione della programmazione viene configurata nel [portale di Azure classico](https://manage.windowsazure.com/) in</span><span class="sxs-lookup"><span data-stu-id="21d1c-136">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="21d1c-137">**Servizi cloud** > **\[Servizio cloud utente\]** > **Piano** > **\[Produzione o Staging\]**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="21d1c-138">Fare clic sul pulsante **Imposta ore di pianificazione** per ogni ruolo che si desidera modificare.</span><span class="sxs-lookup"><span data-stu-id="21d1c-138">Click the **set up schedule times** button for each role you want to change.</span></span>

![Ridimensionamento automatico del servizio cloud in base a una pianificazione][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="21d1c-140">Scalabilità manuale</span><span class="sxs-lookup"><span data-stu-id="21d1c-140">Manual scale</span></span>
<span data-ttu-id="21d1c-141">Nella pagina **Ridimensiona** è possibile aumentare o diminuire manualmente il numero delle istanze in esecuzione in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="21d1c-141">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="21d1c-142">Questa configurazione è prevista per qualsiasi pianificazione creata o, in mancanza di una pianificazione, viene applicata sempre.</span><span class="sxs-lookup"><span data-stu-id="21d1c-142">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="21d1c-143">Nel [portale di Azure classico](https://manage.windowsazure.com/)fare clic su **Servizi cloud**e quindi sul nome del servizio cloud per aprire il dashboard.</span><span class="sxs-lookup"><span data-stu-id="21d1c-143">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="21d1c-144">Se il servizio cloud non viene visualizzato, potrebbe essere necessario passare da **Produzione** a **Staging** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="21d1c-144">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="21d1c-145">Fare clic su **Scale**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-145">Click **Scale**.</span></span>
3. <span data-ttu-id="21d1c-146">Selezionare la pianificazione di cui si desidera modificare le opzioni di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="21d1c-146">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="21d1c-147">In assenza di una pianificazione definita, l'impostazione predefinita è *Nessuna ora pianificata*.</span><span class="sxs-lookup"><span data-stu-id="21d1c-147">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="21d1c-148">Trovare la sezione **Ridimensiona in base alla metrica** e selezionare **Nessuna**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-148">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="21d1c-149">Questa è l'impostazione predefinita per tutti i ruoli.</span><span class="sxs-lookup"><span data-stu-id="21d1c-149">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="21d1c-150">In ogni ruolo nel servizio cloud è presente un dispositivo di scorrimento che consente di modificare il numero di istanze da usare.</span><span class="sxs-lookup"><span data-stu-id="21d1c-150">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![Ridimensionare manualmente un ruolo del servizio cloud][manual_scale]
   
    <span data-ttu-id="21d1c-152">Se sono richieste altre istanze, potrebbe essere necessario modificare le [dimensioni di macchine virtuali e di servizi cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="21d1c-152">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="21d1c-153">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-153">Click **Save**.</span></span>  
   <span data-ttu-id="21d1c-154">Verranno aggiunte o rimosse istanze del ruolo in base alle selezioni effettuate.</span><span class="sxs-lookup"><span data-stu-id="21d1c-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="21d1c-155">Per informazioni sulla funzione di una specifica impostazione, spostare il mouse sull'icona ![][tip_icon] ogni volta che viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="21d1c-155">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="21d1c-156">Scalabilità automatica - CPU</span><span class="sxs-lookup"><span data-stu-id="21d1c-156">Automatic scale - CPU</span></span>
<span data-ttu-id="21d1c-157">Questo tipo di scalabilità è possibile se la percentuale media di uso della CPU supera o scende al di sotto delle soglie specificate.</span><span class="sxs-lookup"><span data-stu-id="21d1c-157">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="21d1c-158">Quando accade questo, vengono create o eliminate istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="21d1c-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="21d1c-159">Nel [portale di Azure classico](https://manage.windowsazure.com/)fare clic su **Servizi cloud**e quindi sul nome del servizio cloud per aprire il dashboard.</span><span class="sxs-lookup"><span data-stu-id="21d1c-159">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="21d1c-160">Se il servizio cloud non viene visualizzato, potrebbe essere necessario passare da **Produzione** a **Staging** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="21d1c-160">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="21d1c-161">Fare clic su **Scale**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-161">Click **Scale**.</span></span>
3. <span data-ttu-id="21d1c-162">Selezionare la pianificazione di cui si desidera modificare le opzioni di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="21d1c-162">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="21d1c-163">In assenza di una pianificazione definita, l'impostazione predefinita è *Nessuna ora pianificata*.</span><span class="sxs-lookup"><span data-stu-id="21d1c-163">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="21d1c-164">Trovare la sezione **Ridimensiona in base alla metrica** e selezionare **CPU**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-164">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="21d1c-165">A questo punto è possibile configurare un intervallo minimo e massimo di istanze dei ruoli, l'intervallo di destinazione per l'uso della CPU (per attivare un aumento) e il numero di istanze da aumentare o ridurre.</span><span class="sxs-lookup"><span data-stu-id="21d1c-165">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![Ridimensionare un ruolo del servizio cloud per carico CPU][cpu_scale]

> [!TIP]
> <span data-ttu-id="21d1c-167">Per informazioni sulla funzione di una specifica impostazione, spostare il mouse sull'icona ![][tip_icon] ogni volta che viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="21d1c-167">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="21d1c-168">Scalabilità automatica - Coda</span><span class="sxs-lookup"><span data-stu-id="21d1c-168">Automatic scale - Queue</span></span>
<span data-ttu-id="21d1c-169">Questo tipo di scalabilità automatica è possibile se il numero di messaggi in una coda supera o scende al di sotto di una soglia specificata.</span><span class="sxs-lookup"><span data-stu-id="21d1c-169">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="21d1c-170">Quando accade questo, vengono create o eliminate istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="21d1c-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="21d1c-171">Nel [portale di Azure classico](https://manage.windowsazure.com/)fare clic su **Servizi cloud**e quindi sul nome del servizio cloud per aprire il dashboard.</span><span class="sxs-lookup"><span data-stu-id="21d1c-171">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="21d1c-172">Se il servizio cloud non viene visualizzato, potrebbe essere necessario passare da **Produzione** a **Staging** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="21d1c-172">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="21d1c-173">Fare clic su **Scale**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-173">Click **Scale**.</span></span>
3. <span data-ttu-id="21d1c-174">Trovare la sezione **Ridimensiona in base alla metrica** e selezionare **CODA**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-174">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="21d1c-175">A questo punto è possibile configurare un intervallo minimo e massimo di istanze dei ruoli, la coda, la quantità di messaggi in coda da elaborare per ogni istanza e il numero di istanze da aumentare o ridurre.</span><span class="sxs-lookup"><span data-stu-id="21d1c-175">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![Ridimensionare un ruolo del servizio cloud per coda di messaggi][queue_scale]

> [!TIP]
> <span data-ttu-id="21d1c-177">Per informazioni sulla funzione di una specifica impostazione, spostare il mouse sull'icona ![][tip_icon] ogni volta che viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="21d1c-177">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="21d1c-178">Scalare risorse collegate</span><span class="sxs-lookup"><span data-stu-id="21d1c-178">Scale linked resources</span></span>
<span data-ttu-id="21d1c-179">Quando si scala un ruolo, spesso risulta utile scalare anche il database utilizzato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="21d1c-179">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="21d1c-180">Se si collega il database al servizio cloud, è possibile accedere alle impostazioni di scalabilità per tale risorsa facendo clic sul collegamento appropriato.</span><span class="sxs-lookup"><span data-stu-id="21d1c-180">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="21d1c-181">Nel [portale di Azure classico](https://manage.windowsazure.com/)fare clic su **Servizi cloud**e quindi sul nome del servizio cloud per aprire il dashboard.</span><span class="sxs-lookup"><span data-stu-id="21d1c-181">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="21d1c-182">Se il servizio cloud non viene visualizzato, potrebbe essere necessario passare da **Produzione** a **Staging** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="21d1c-182">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="21d1c-183">Fare clic su **Scale**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-183">Click **Scale**.</span></span>
3. <span data-ttu-id="21d1c-184">Trovare la sezione **Risorse collegate** e fare clic su **Gestire la scalabilità per questo database**.</span><span class="sxs-lookup"><span data-stu-id="21d1c-184">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="21d1c-185">Se la sezione delle **risorse collegate** non viene visualizzata, è probabile che non sia presente alcuna risorsa.</span><span class="sxs-lookup"><span data-stu-id="21d1c-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
