---
title: aaaAuto scalare un servizio cloud nel portale di hello | Documenti Microsoft
description: "Informazioni su come toouse hello tooconfigure portale regole di scalabilità automatica per un ruolo web del servizio cloud o un ruolo di lavoro in Azure."
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
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="72f46-103">Come tooconfigure auto scaling per un servizio Cloud nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="72f46-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72f46-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="72f46-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="72f46-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="72f46-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="72f46-106">È possibile impostare condizioni per un ruolo di lavoro del servizio cloud che attivano operazioni di scalabilità verticale o orizzontale.</span><span class="sxs-lookup"><span data-stu-id="72f46-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="72f46-107">le condizioni di Hello per ruolo hello possono essere basate su hello CPU, disco o il carico di rete del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="72f46-108">È inoltre possibile impostare una condizione in base a una metrica messaggio hello o coda di un'altra risorsa di Azure associata alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="72f46-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="72f46-109">Questo articolo è incentrato sui ruoli Web e di lavoro del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="72f46-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="72f46-110">Quando si crea una macchina virtuale (distribuzione classica) direttamente, questa viene ospitata in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="72f46-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="72f46-111">È possibile ridimensionare una macchina virtuale standard tramite l'associazione con un [set di disponibilità](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) e attivarla o disattivarla manualmente.</span><span class="sxs-lookup"><span data-stu-id="72f46-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="72f46-112">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="72f46-112">Considerations</span></span>
<span data-ttu-id="72f46-113">È necessario considerare le seguenti informazioni prima di configurare la scalabilità per l'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="72f46-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="72f46-114">La scalabilità è influenzata dall'utilizzo di core.</span><span class="sxs-lookup"><span data-stu-id="72f46-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="72f46-115">Le istanze del ruolo più ampie usano più core.</span><span class="sxs-lookup"><span data-stu-id="72f46-115">Larger role instances use more cores.</span></span> <span data-ttu-id="72f46-116">È possibile scalare un'applicazione solo entro il limite di hello di core per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="72f46-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="72f46-117">Si supponga, ad esempio, che la sottoscrizione abbia un limite di 20 core.</span><span class="sxs-lookup"><span data-stu-id="72f46-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="72f46-118">Se si esegue un'applicazione con i due servizi di cloud di medie dimensioni (un totale di 4 core), è possibile solo scalabilità verticale altre distribuzioni del servizio cloud nella sottoscrizione da 16 core hello rimanenti.</span><span class="sxs-lookup"><span data-stu-id="72f46-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="72f46-119">Per altre informazioni sulle dimensioni, vedere [Dimensioni dei servizi cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="72f46-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="72f46-120">È possibile eseguire la scalabilità in base a una soglia di messaggi in coda.</span><span class="sxs-lookup"><span data-stu-id="72f46-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="72f46-121">Per ulteriori informazioni su come toouse code, vedere [come toouse hello servizio di archiviazione code](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="72f46-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="72f46-122">È anche possibile ridimensionare altre risorse associate alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="72f46-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="72f46-123">tooenable la disponibilità elevata dell'applicazione, è necessario assicurarsi che venga distribuito con due o più istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="72f46-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="72f46-124">Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="72f46-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="72f46-125">Posizione della scalabilità</span><span class="sxs-lookup"><span data-stu-id="72f46-125">Where scale is located</span></span>
<span data-ttu-id="72f46-126">Dopo aver selezionato il servizio cloud, è necessario il pannello servizi di cloud hello è visibile.</span><span class="sxs-lookup"><span data-stu-id="72f46-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="72f46-127">Nel pannello del servizio cloud hello, su hello **ruoli e istanze** riquadro, nome selezionare hello del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="72f46-128">**IMPORTANTE**: rendere cloud di hello tooclick che servizio ruolo, non hello istanza del ruolo che si trova sotto il ruolo di hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="72f46-129">Seleziona hello **scala** riquadro.</span><span class="sxs-lookup"><span data-stu-id="72f46-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="72f46-130">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="72f46-130">Automatic scale</span></span>
<span data-ttu-id="72f46-131">È possibile configurare le impostazioni di scalabilità per un ruolo scegliendo tra due modalità **manuale** o **automatica**.</span><span class="sxs-lookup"><span data-stu-id="72f46-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="72f46-132">Manuale è come previsto, si imposta numero assoluto di hello delle istanze.</span><span class="sxs-lookup"><span data-stu-id="72f46-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="72f46-133">Automatica consente tuttavia tooset regole che determinano la modalità e in quale molto è consigliabile applicare la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="72f46-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="72f46-134">Set hello **scalare** opzione troppo**le regole di pianificazione e delle prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="72f46-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![Impostazioni di scalabilità dei servizi cloud con profilo e regola](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="72f46-136">Un profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="72f46-136">An existing profile.</span></span>
2. <span data-ttu-id="72f46-137">Aggiungere una regola per profilo padre hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="72f46-138">Aggiungere un altro profilo.</span><span class="sxs-lookup"><span data-stu-id="72f46-138">Add another profile.</span></span>

<span data-ttu-id="72f46-139">Selezionare **Aggiungi profilo**.</span><span class="sxs-lookup"><span data-stu-id="72f46-139">Select **Add Profile**.</span></span> <span data-ttu-id="72f46-140">profilo Hello determina la modalità desiderata toouse per scala hello: **sempre**, **ricorrenza**, **data fissa**.</span><span class="sxs-lookup"><span data-stu-id="72f46-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="72f46-141">Dopo aver configurato il profilo di hello e regole, selezionare hello **salvare** icona nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="72f46-142">Profilo</span><span class="sxs-lookup"><span data-stu-id="72f46-142">Profile</span></span>
<span data-ttu-id="72f46-143">profilo Hello imposta minimo e massimo di istanze per hello scalabilità anche quando l'intervallo di scala è attivo.</span><span class="sxs-lookup"><span data-stu-id="72f46-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="72f46-144">**Sempre**</span><span class="sxs-lookup"><span data-stu-id="72f46-144">**Always**</span></span>

    <span data-ttu-id="72f46-145">Consente di mantenere sempre disponibile questo intervallo di istanze.</span><span class="sxs-lookup"><span data-stu-id="72f46-145">Always keep this range of instances available.</span></span>  

    ![Servizio cloud che esegue sempre la scalabilità](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="72f46-147">**Ricorrenza**</span><span class="sxs-lookup"><span data-stu-id="72f46-147">**Recurrence**</span></span>

    <span data-ttu-id="72f46-148">Scegliere un set di giorni di hello settimana tooscale.</span><span class="sxs-lookup"><span data-stu-id="72f46-148">Choose a set of days of hello week tooscale.</span></span>

    ![Scalabilità del servizio cloud con pianificazione ricorrente](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="72f46-150">**Data fissa**</span><span class="sxs-lookup"><span data-stu-id="72f46-150">**Fixed Date**</span></span>

    <span data-ttu-id="72f46-151">Un ruolo di hello tooscale intervallo di date fisse.</span><span class="sxs-lookup"><span data-stu-id="72f46-151">A fixed date range tooscale hello role.</span></span>

    ![Scalabilità del servizio cloud con data fissa](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="72f46-153">Dopo aver configurato il profilo di hello, selezionare hello **OK** pulsante nella parte inferiore di hello del pannello profilo hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="72f46-154">Regola</span><span class="sxs-lookup"><span data-stu-id="72f46-154">Rule</span></span>
<span data-ttu-id="72f46-155">Le regole vengono aggiunti tooa profilo e rappresentano una condizione che attiva la scala hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="72f46-156">trigger della regola Hello è basato su una metrica di servizio cloud di hello (utilizzo della CPU, attività del disco o un'attività di rete) toowhich è possibile aggiungere un valore condizionale.</span><span class="sxs-lookup"><span data-stu-id="72f46-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="72f46-157">È inoltre possibile avere trigger hello in base a una metrica messaggio hello o coda di un'altra risorsa di Azure associata alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="72f46-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="72f46-158">Dopo aver configurato la regola hello, selezionare hello **OK** pulsante nella parte inferiore di hello del pannello regole hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="72f46-159">Scala toomanual indietro</span><span class="sxs-lookup"><span data-stu-id="72f46-159">Back toomanual scale</span></span>
<span data-ttu-id="72f46-160">Passare toohello [le impostazioni di scalabilità](#where-scale-is-located) e set hello **scalare** opzione troppo**un numero di istanze immesso manualmente**.</span><span class="sxs-lookup"><span data-stu-id="72f46-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![Impostazioni di scalabilità dei servizi cloud con profilo e regola](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="72f46-162">Questa impostazione consente di rimuovere il ridimensionamento automatico dal ruolo hello e quindi è possibile impostare il numero di istanze di hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="72f46-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="72f46-163">opzione della scala (manuali o automatizzati) Hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="72f46-164">Un ruolo istanza dispositivo di scorrimento tooset hello istanze tooscale per.</span><span class="sxs-lookup"><span data-stu-id="72f46-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="72f46-165">Istanze di hello ruolo tooscale per.</span><span class="sxs-lookup"><span data-stu-id="72f46-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="72f46-166">Dopo aver configurato le impostazioni di scalabilità di hello, selezionare hello **salvare** icona nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="72f46-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
