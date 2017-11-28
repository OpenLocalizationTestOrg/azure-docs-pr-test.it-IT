---
title: "Configurazione della scalabilità automatica di un servizio cloud nel portale | Documentazione Microsoft"
description: "Informazioni su come usare il portale per configurare le regole di scalabilità automatica per un ruolo Web o un ruolo di lavoro del servizio cloud in Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: e9683d4c5779450fd67fa42ab13095c7f201b4cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-portal"></a><span data-ttu-id="537c2-103">Come configurare la scalabilità automatica per un servizio cloud nel portale</span><span class="sxs-lookup"><span data-stu-id="537c2-103">How to configure auto scaling for a Cloud Service in the portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="537c2-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="537c2-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="537c2-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="537c2-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="537c2-106">È possibile impostare condizioni per un ruolo di lavoro del servizio cloud che attivano operazioni di scalabilità verticale o orizzontale.</span><span class="sxs-lookup"><span data-stu-id="537c2-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="537c2-107">Le condizioni per il ruolo possono essere basate sulla CPU, sul disco o sul carico di rete del ruolo.</span><span class="sxs-lookup"><span data-stu-id="537c2-107">The conditions for the role can be based on the CPU, disk, or network load of the role.</span></span> <span data-ttu-id="537c2-108">È anche possibile impostare una condizione in base a una coda di messaggi o alla metrica di un'altra risorsa di Azure associata alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="537c2-108">You can also set a condition based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="537c2-109">Questo articolo è incentrato sui ruoli Web e di lavoro del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="537c2-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="537c2-110">Quando si crea una macchina virtuale (distribuzione classica) direttamente, questa viene ospitata in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="537c2-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="537c2-111">È possibile ridimensionare una macchina virtuale standard tramite l'associazione con un [set di disponibilità](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) e attivarla o disattivarla manualmente.</span><span class="sxs-lookup"><span data-stu-id="537c2-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="537c2-112">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="537c2-112">Considerations</span></span>
<span data-ttu-id="537c2-113">Prima di configurare la scalabilità per l'applicazione, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="537c2-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="537c2-114">La scalabilità è influenzata dall'utilizzo di core.</span><span class="sxs-lookup"><span data-stu-id="537c2-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="537c2-115">Le istanze del ruolo più ampie usano più core.</span><span class="sxs-lookup"><span data-stu-id="537c2-115">Larger role instances use more cores.</span></span> <span data-ttu-id="537c2-116">È possibile ridimensionare il numero di istanze di un'applicazione solo entro i limiti di core previsti dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="537c2-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="537c2-117">Si supponga, ad esempio, che la sottoscrizione abbia un limite di 20 core.</span><span class="sxs-lookup"><span data-stu-id="537c2-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="537c2-118">Se si esegue un'applicazione con due servizi cloud di medie dimensioni (per un totale di 4 core), l'aumento di altre distribuzioni del servizio cloud nella sottoscrizione è limitata ai 16 core rimanenti.</span><span class="sxs-lookup"><span data-stu-id="537c2-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="537c2-119">Per altre informazioni sulle dimensioni, vedere [Dimensioni dei servizi cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="537c2-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="537c2-120">È possibile eseguire la scalabilità in base a una soglia di messaggi in coda.</span><span class="sxs-lookup"><span data-stu-id="537c2-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="537c2-121">Per altre informazioni sull'uso delle code, vedere l'articolo relativo all' [uso del servizio di archiviazione code](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="537c2-121">For more information about how to use queues, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="537c2-122">È anche possibile ridimensionare altre risorse associate alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="537c2-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="537c2-123">Per abilitare la disponibilità elevata dell'applicazione, è necessario accertarsi che sia distribuita con due o più istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="537c2-123">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="537c2-124">Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="537c2-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="537c2-125">Posizione della scalabilità</span><span class="sxs-lookup"><span data-stu-id="537c2-125">Where scale is located</span></span>
<span data-ttu-id="537c2-126">Dopo aver selezionato il servizio cloud, viene visualizzato il pannello del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="537c2-126">After you select your cloud service, you should have the cloud service blade visible.</span></span>

1. <span data-ttu-id="537c2-127">Nel pannello del servizio cloud, nel riquadro **Ruoli e istanze** , selezionare il nome del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="537c2-127">On the cloud service blade, on the **Roles and Instances** tile, select the name of the cloud service.</span></span>   
   <span data-ttu-id="537c2-128">**IMPORTANTE**: assicurarsi di selezionare il ruolo del servizio cloud, non l'istanza del ruolo che si trova sotto il ruolo.</span><span class="sxs-lookup"><span data-stu-id="537c2-128">**IMPORTANT**: Make sure to click the cloud service role, not the role instance that is below the role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="537c2-129">Selezionare il riquadro **Ridimensiona** .</span><span class="sxs-lookup"><span data-stu-id="537c2-129">Select the **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="537c2-130">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="537c2-130">Automatic scale</span></span>
<span data-ttu-id="537c2-131">È possibile configurare le impostazioni di scalabilità per un ruolo scegliendo tra due modalità **manuale** o **automatica**.</span><span class="sxs-lookup"><span data-stu-id="537c2-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="537c2-132">Con la modalità manuale, come si può immaginare, si imposta il numero assoluto di istanze.</span><span class="sxs-lookup"><span data-stu-id="537c2-132">Manual is as you would expect, you set the absolute count of instances.</span></span> <span data-ttu-id="537c2-133">La modalità automatica consente tuttavia di impostare regole che determinano il modo e la dimensione della scalabilità.</span><span class="sxs-lookup"><span data-stu-id="537c2-133">Automatic however allows you to set rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="537c2-134">Impostare l'opzione **Ridimensiona di** su **regole per la pianificazione e le prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="537c2-134">Set the **Scale by** option to **schedule and performance rules**.</span></span>

![Impostazioni di scalabilità dei servizi cloud con profilo e regola](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="537c2-136">Un profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="537c2-136">An existing profile.</span></span>
2. <span data-ttu-id="537c2-137">Aggiungere una regola per il profilo padre.</span><span class="sxs-lookup"><span data-stu-id="537c2-137">Add a rule for the parent profile.</span></span>
3. <span data-ttu-id="537c2-138">Aggiungere un altro profilo.</span><span class="sxs-lookup"><span data-stu-id="537c2-138">Add another profile.</span></span>

<span data-ttu-id="537c2-139">Selezionare **Aggiungi profilo**.</span><span class="sxs-lookup"><span data-stu-id="537c2-139">Select **Add Profile**.</span></span> <span data-ttu-id="537c2-140">Il profilo determina la modalità da usare per la scalabilità: **sempre**, **ricorrenza**, **data fissa**.</span><span class="sxs-lookup"><span data-stu-id="537c2-140">The profile determines which mode you want to use for the scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="537c2-141">Dopo aver configurato il profilo e le regole, selezionare l'icona **Salva** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="537c2-141">After you have configured the profile and rules, select the **Save** icon at the top.</span></span>

#### <a name="profile"></a><span data-ttu-id="537c2-142">Profilo</span><span class="sxs-lookup"><span data-stu-id="537c2-142">Profile</span></span>
<span data-ttu-id="537c2-143">Il profilo imposta istanze minime e massime per la scalabilità, anche quando è attivo questo intervallo di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="537c2-143">The profile sets minimum and maximum instances for the scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="537c2-144">**Sempre**</span><span class="sxs-lookup"><span data-stu-id="537c2-144">**Always**</span></span>

    <span data-ttu-id="537c2-145">Consente di mantenere sempre disponibile questo intervallo di istanze.</span><span class="sxs-lookup"><span data-stu-id="537c2-145">Always keep this range of instances available.</span></span>  

    ![Servizio cloud che esegue sempre la scalabilità](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="537c2-147">**Ricorrenza**</span><span class="sxs-lookup"><span data-stu-id="537c2-147">**Recurrence**</span></span>

    <span data-ttu-id="537c2-148">Consente di scegliere un set di giorni della settimana per la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="537c2-148">Choose a set of days of the week to scale.</span></span>

    ![Scalabilità del servizio cloud con pianificazione ricorrente](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="537c2-150">**Data fissa**</span><span class="sxs-lookup"><span data-stu-id="537c2-150">**Fixed Date**</span></span>

    <span data-ttu-id="537c2-151">Un intervallo di date fisso per eseguire la scalabilità del ruolo.</span><span class="sxs-lookup"><span data-stu-id="537c2-151">A fixed date range to scale the role.</span></span>

    ![Scalabilità del servizio cloud con data fissa](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="537c2-153">Dopo aver configurato il profilo, selezionare il pulsante **OK** nella parte inferiore del pannello del profilo.</span><span class="sxs-lookup"><span data-stu-id="537c2-153">After you have configured the profile, select the **OK** button at the bottom of the profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="537c2-154">Regola</span><span class="sxs-lookup"><span data-stu-id="537c2-154">Rule</span></span>
<span data-ttu-id="537c2-155">Le regole vengono aggiunte al profilo e rappresentano la condizione che attiva la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="537c2-155">Rules are added to a profile and represent a condition that triggers the scale.</span></span>

<span data-ttu-id="537c2-156">Il trigger della regola è basato su una metrica del servizio cloud (uso della CPU, attività del disco o attività di rete) a cui è possibile aggiungere un valore condizionale.</span><span class="sxs-lookup"><span data-stu-id="537c2-156">The rule trigger is based on a metric of the cloud service (CPU usage, disk activity, or network activity) to which you can add a conditional value.</span></span> <span data-ttu-id="537c2-157">È anche possibile impostare il trigger in base a una coda di messaggi o alla metrica di un'altra risorsa di Azure associata alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="537c2-157">Additionally you can have the trigger based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="537c2-158">Dopo aver configurato la regola, selezionare il pulsante **OK** nella parte inferiore del pannello della regola.</span><span class="sxs-lookup"><span data-stu-id="537c2-158">After you have configured the rule, select the **OK** button at the bottom of the rule blade.</span></span>

## <a name="back-to-manual-scale"></a><span data-ttu-id="537c2-159">Ritorno alla scalabilità manuale</span><span class="sxs-lookup"><span data-stu-id="537c2-159">Back to manual scale</span></span>
<span data-ttu-id="537c2-160">Accedere a [Impostazioni scalabilità](#where-scale-is-located) e impostare l'opzione **Ridimensiona di** su **numero di istanze immesso manualmente**.</span><span class="sxs-lookup"><span data-stu-id="537c2-160">Navigate to the [scale settings](#where-scale-is-located) and set the **Scale by** option to **an instance count that I enter manually**.</span></span>

![Impostazioni di scalabilità dei servizi cloud con profilo e regola](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="537c2-162">Questa impostazione rimuove la scalabilità automatica dal ruolo e quindi è possibile impostare direttamente il numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="537c2-162">This setting removes automated scaling from the role and then you can set the instance count directly.</span></span>

1. <span data-ttu-id="537c2-163">L'opzione di scalabilità (manuale o automatica).</span><span class="sxs-lookup"><span data-stu-id="537c2-163">The scale (manual or automated) option.</span></span>
2. <span data-ttu-id="537c2-164">Un dispositivo di scorrimento delle istanze del ruolo per impostare le istanze da ridimensionare.</span><span class="sxs-lookup"><span data-stu-id="537c2-164">A role instance slider to set the instances to scale to.</span></span>
3. <span data-ttu-id="537c2-165">Istanze del ruolo da ridimensionare.</span><span class="sxs-lookup"><span data-stu-id="537c2-165">Instances of the role to scale to.</span></span>

<span data-ttu-id="537c2-166">Dopo aver configurato il profilo e le regole, selezionare l'icona **Salva** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="537c2-166">After you have configured the scale settings, select the **Save** icon at the top.</span></span>
