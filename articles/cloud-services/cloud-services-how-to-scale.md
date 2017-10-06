---
title: aaaAuto scalare un servizio cloud nel portale classico hello | Documenti Microsoft
description: "(versione classica) Informazioni su come toouse hello tooconfigure portale classico regole di scalabilità automatica per un ruolo web del servizio cloud o un ruolo di lavoro in Azure."
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
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="0a73b-103">Come tooconfigure auto scaling per un servizio Cloud nel portale classico hello</span><span class="sxs-lookup"><span data-stu-id="0a73b-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a73b-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0a73b-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="0a73b-105">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="0a73b-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="0a73b-106">Nella pagina di scala hello di hello portale di Azure classico, è possibile configurare le impostazioni di scalabilità automatica per il ruolo web o un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0a73b-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="0a73b-107">In alternativa, è possibile configurare la scalabilità manuale invece della scalabilità automatica basata su regole.</span><span class="sxs-lookup"><span data-stu-id="0a73b-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="0a73b-108">Questo articolo è incentrato sui ruoli Web e di lavoro del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0a73b-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="0a73b-109">Quando si crea una macchina virtuale (distribuzione classica) direttamente, questa viene ospitata in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0a73b-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="0a73b-110">Alcune di queste informazioni si applicano tipi toothese di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0a73b-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="0a73b-111">Ridimensionamento di un set di disponibilità delle macchine virtuali è solo in corso l'arresto li attivare e disattivare in base alle regole di scala hello che è configurare.</span><span class="sxs-lookup"><span data-stu-id="0a73b-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="0a73b-112">Per ulteriori informazioni sulle macchine virtuali e i set di disponibilità, vedere [Gestisci hello disponibilità delle macchine virtuali](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0a73b-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="0a73b-113">È necessario considerare le seguenti informazioni prima di configurare la scalabilità per l'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="0a73b-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="0a73b-114">La scalabilità è influenzata dall'utilizzo di core.</span><span class="sxs-lookup"><span data-stu-id="0a73b-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="0a73b-115">Le istanze del ruolo più ampie usano più core.</span><span class="sxs-lookup"><span data-stu-id="0a73b-115">Larger role instances use more cores.</span></span> <span data-ttu-id="0a73b-116">È possibile scalare un'applicazione solo entro il limite di hello di core per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0a73b-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="0a73b-117">Si supponga, ad esempio, che la sottoscrizione abbia un limite di 20 core.</span><span class="sxs-lookup"><span data-stu-id="0a73b-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="0a73b-118">Se si esegue un'applicazione con i due servizi di cloud di medie dimensioni (un totale di 4 core), è possibile solo scalabilità verticale altre distribuzioni del servizio cloud nella sottoscrizione da 16 core hello rimanenti.</span><span class="sxs-lookup"><span data-stu-id="0a73b-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="0a73b-119">Per altre informazioni sulle dimensioni, vedere [Dimensioni dei servizi cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="0a73b-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="0a73b-120">È necessario creare una coda e associarla a un ruolo prima di ridimensionare il numero di istanze di un'applicazione in base a una soglia di messaggi.</span><span class="sxs-lookup"><span data-stu-id="0a73b-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="0a73b-121">Per ulteriori informazioni, vedere [come toouse hello servizio di archiviazione code](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="0a73b-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="0a73b-122">È possibile scalare le risorse che sono collegati tooyour servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0a73b-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="0a73b-123">Per ulteriori informazioni sul collegamento di risorse, vedere [procedura: collegamento di un servizio cloud di risorse tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="0a73b-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="0a73b-124">tooenable la disponibilità elevata dell'applicazione, è necessario assicurarsi che venga distribuito con due o più istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="0a73b-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="0a73b-125">Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="0a73b-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="0a73b-126">Pianificazione della scalabilità</span><span class="sxs-lookup"><span data-stu-id="0a73b-126">Schedule scaling</span></span>
<span data-ttu-id="0a73b-127">Per impostazione predefinita, i ruoli non seguono una pianificazione specifica.</span><span class="sxs-lookup"><span data-stu-id="0a73b-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="0a73b-128">Pertanto, le impostazioni modificate valide tooall volte e tutti i giorni anno hello.</span><span class="sxs-lookup"><span data-stu-id="0a73b-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="0a73b-129">Se si desidera, è possibile configurare il ridimensionamento manuale o automatica per una delle seguenti modalità hello:</span><span class="sxs-lookup"><span data-stu-id="0a73b-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="0a73b-130">Giorni della settimana</span><span class="sxs-lookup"><span data-stu-id="0a73b-130">Weekdays</span></span>
* <span data-ttu-id="0a73b-131">Fine settimana</span><span class="sxs-lookup"><span data-stu-id="0a73b-131">Weekends</span></span>
* <span data-ttu-id="0a73b-132">Ore notturne</span><span class="sxs-lookup"><span data-stu-id="0a73b-132">Week nights</span></span>
* <span data-ttu-id="0a73b-133">Ore diurne</span><span class="sxs-lookup"><span data-stu-id="0a73b-133">Week mornings</span></span>
* <span data-ttu-id="0a73b-134">Date specifiche</span><span class="sxs-lookup"><span data-stu-id="0a73b-134">Specific dates</span></span>
* <span data-ttu-id="0a73b-135">Intervalli di date specifiche</span><span class="sxs-lookup"><span data-stu-id="0a73b-135">Specific date ranges</span></span>

<span data-ttu-id="0a73b-136">Hello pianificazione è configurata in hello [portale di Azure classico](https://manage.windowsazure.com/) su hello</span><span class="sxs-lookup"><span data-stu-id="0a73b-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="0a73b-137">**Servizi cloud** > **\[Servizio cloud utente\]** > **Piano** > **\[Produzione o Staging\]**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="0a73b-138">Fare clic su hello **Imposta ore di pianificazione** pulsante per ogni ruolo desiderato toochange.</span><span class="sxs-lookup"><span data-stu-id="0a73b-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![Ridimensionamento automatico del servizio cloud in base a una pianificazione][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="0a73b-140">Scalabilità manuale</span><span class="sxs-lookup"><span data-stu-id="0a73b-140">Manual scale</span></span>
<span data-ttu-id="0a73b-141">In hello **scala** pagina, è possibile manualmente aumentare o diminuire il numero di hello di istanze in esecuzione in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0a73b-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="0a73b-142">Questa impostazione è configurata per ogni pianificazione che è stato creato o tooall tempo se non è stata creata una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="0a73b-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="0a73b-143">In hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **servizi Cloud**, quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="0a73b-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0a73b-144">Se non viene visualizzato il servizio cloud, potrebbe essere necessario toochange da **produzione** troppo**gestione temporanea** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="0a73b-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="0a73b-145">Fare clic su **Scale**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-145">Click **Scale**.</span></span>
3. <span data-ttu-id="0a73b-146">Selezionare una pianificazione di hello desiderata toochange sicure per.</span><span class="sxs-lookup"><span data-stu-id="0a73b-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="0a73b-147">*Non orari pianificati* è hello predefinito se non si dispone di Nessuna pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="0a73b-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="0a73b-148">Trovare hello **scala in base alla metrica** sezione e selezionare **Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="0a73b-149">Questa impostazione è predefinita hello per tutti i ruoli.</span><span class="sxs-lookup"><span data-stu-id="0a73b-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="0a73b-150">Ogni ruolo nel servizio cloud hello dispone di un dispositivo di scorrimento per modificare il numero di hello di toouse di istanze.</span><span class="sxs-lookup"><span data-stu-id="0a73b-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![Ridimensionare manualmente un ruolo del servizio cloud][manual_scale]
   
    <span data-ttu-id="0a73b-152">Se è necessario più istanze, potrebbe essere necessario hello toochange [dimensione di macchina virtuale del servizio cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="0a73b-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="0a73b-153">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-153">Click **Save**.</span></span>  
   <span data-ttu-id="0a73b-154">Verranno aggiunte o rimosse istanze del ruolo in base alle selezioni effettuate.</span><span class="sxs-lookup"><span data-stu-id="0a73b-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="0a73b-155">Ogni volta che viene visualizzato ![][tip_icon] spostare tooit il mouse ed è possibile ottenere la Guida sulle quali un'impostazione specifica.</span><span class="sxs-lookup"><span data-stu-id="0a73b-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="0a73b-156">Scalabilità automatica - CPU</span><span class="sxs-lookup"><span data-stu-id="0a73b-156">Automatic scale - CPU</span></span>
<span data-ttu-id="0a73b-157">Questa modalità è adatta se percentuale media di hello di utilizzo della CPU è superiore o inferiore alle soglie specificate.</span><span class="sxs-lookup"><span data-stu-id="0a73b-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="0a73b-158">Quando accade questo, vengono create o eliminate istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="0a73b-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="0a73b-159">In hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **servizi Cloud**, quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="0a73b-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0a73b-160">Se non viene visualizzato il servizio cloud, potrebbe essere necessario toochange da **produzione** troppo**gestione temporanea** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="0a73b-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="0a73b-161">Fare clic su **Scale**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-161">Click **Scale**.</span></span>
3. <span data-ttu-id="0a73b-162">Selezionare una pianificazione di hello desiderata toochange sicure per.</span><span class="sxs-lookup"><span data-stu-id="0a73b-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="0a73b-163">*Non orari pianificati* è hello predefinito se non si dispone di Nessuna pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="0a73b-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="0a73b-164">Trovare hello **scala in base alla metrica** sezione e selezionare **CPU**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="0a73b-165">È ora possibile configurare un intervallo minimo e massimo di istanze dei ruoli, l'utilizzo di CPU destinazione hello (tootrigger una scalabilità verticale) e il numero di istanze tooscale su e giù per.</span><span class="sxs-lookup"><span data-stu-id="0a73b-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![Ridimensionare un ruolo del servizio cloud per carico CPU][cpu_scale]

> [!TIP]
> <span data-ttu-id="0a73b-167">Ogni volta che viene visualizzato ![][tip_icon] spostare tooit il mouse ed è possibile ottenere la Guida sulle quali un'impostazione specifica.</span><span class="sxs-lookup"><span data-stu-id="0a73b-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="0a73b-168">Scalabilità automatica - Coda</span><span class="sxs-lookup"><span data-stu-id="0a73b-168">Automatic scale - Queue</span></span>
<span data-ttu-id="0a73b-169">Questa modalità viene ridimensionato automaticamente se il numero di hello di messaggi in una coda passa sopra o sotto la soglia specificata.</span><span class="sxs-lookup"><span data-stu-id="0a73b-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="0a73b-170">Quando accade questo, vengono create o eliminate istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="0a73b-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="0a73b-171">In hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **servizi Cloud**, quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="0a73b-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0a73b-172">Se non viene visualizzato il servizio cloud, potrebbe essere necessario toochange da **produzione** troppo**gestione temporanea** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="0a73b-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="0a73b-173">Fare clic su **Scale**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-173">Click **Scale**.</span></span>
3. <span data-ttu-id="0a73b-174">Trovare hello **scala in base alla metrica** sezione e selezionare **coda**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="0a73b-175">È ora possibile configurare un intervallo minimo e massimo di istanze di ruoli, coda hello e numero di coda messaggi tooprocess per ogni istanza e il numero di istanze tooscale su e giù per.</span><span class="sxs-lookup"><span data-stu-id="0a73b-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![Ridimensionare un ruolo del servizio cloud per coda di messaggi][queue_scale]

> [!TIP]
> <span data-ttu-id="0a73b-177">Ogni volta che viene visualizzato ![][tip_icon] spostare tooit il mouse ed è possibile ottenere la Guida sulle quali un'impostazione specifica.</span><span class="sxs-lookup"><span data-stu-id="0a73b-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="0a73b-178">Scalare risorse collegate</span><span class="sxs-lookup"><span data-stu-id="0a73b-178">Scale linked resources</span></span>
<span data-ttu-id="0a73b-179">Spesso quando si ridimensiona un ruolo, è utile tooscale i database di hello che utilizza anche l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0a73b-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="0a73b-180">Se si collega servizio cloud di hello database toohello, è possibile accedere hello scalabilità impostazioni per tale risorsa facendo clic sul collegamento appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="0a73b-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="0a73b-181">In hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **servizi Cloud**, quindi fare clic su nome hello del dashboard hello tooopen del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="0a73b-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0a73b-182">Se non viene visualizzato il servizio cloud, potrebbe essere necessario toochange da **produzione** troppo**gestione temporanea** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="0a73b-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="0a73b-183">Fare clic su **Scale**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-183">Click **Scale**.</span></span>
3. <span data-ttu-id="0a73b-184">Trovare hello **risorse collegate** sezione e fare clic su **gestire la scalabilità per questo database**.</span><span class="sxs-lookup"><span data-stu-id="0a73b-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0a73b-185">Se la sezione delle **risorse collegate** non viene visualizzata, è probabile che non sia presente alcuna risorsa.</span><span class="sxs-lookup"><span data-stu-id="0a73b-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
