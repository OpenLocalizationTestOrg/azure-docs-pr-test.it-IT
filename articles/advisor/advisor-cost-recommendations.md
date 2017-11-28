---
title: raccomandazioni di Advisor costo aaaAzure | Documenti Microsoft
description: Utilizzare Advisor Azure toooptimize hello costo delle distribuzioni di Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="c7a0c-103">Consigli di Advisor sui costi</span><span class="sxs-lookup"><span data-stu-id="c7a0c-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="c7a0c-104">Advisor aiuta a ottimizzare e ridurre la spesa complessiva legata ad Azure identificando le risorse inattive e sottoutilizzate.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="c7a0c-105">È possibile Ottieni suggerimenti di hello **costo** scheda nel dashboard di Advisor hello.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Scheda Costo di Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="c7a0c-107">Ottimizzare la spesa correlata alle macchine virtuali ridimensionando le istanze sottoutilizzate</span><span class="sxs-lookup"><span data-stu-id="c7a0c-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="c7a0c-108">Sebbene alcuni scenari di applicazione possono comportare un utilizzo ridotto in base alla progettazione, è possibile salvare spesso money gestendo hello dimensioni e il numero di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="c7a0c-109">Advisor monitora l'utilizzo delle macchine virtuali per 14 giorni, in modo da identificare le macchine virtuali il cui utilizzo è ridotto.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="c7a0c-110">Le macchine virtuali con un utilizzo della CPU pari al 5% o inferiore e un utilizzo di rete pari a 7 MB o inferiore per quattro o più giorni sono considerate macchine virtuali il cui utilizzo è ridotto.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="c7a0c-111">Mostra Advisor hello costo stimato di continuare toorun la macchina virtuale, in modo da poter scegliere tooshut verso il basso oppure ridimensionarlo.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![Consigli di Advisor sui costi per il ridimensionamento delle macchine virtuali](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="c7a0c-113">Utilizzare obiettivi di prestazioni toomanage una soluzione a costi contenuti di più database SQL</span><span class="sxs-lookup"><span data-stu-id="c7a0c-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="c7a0c-114">Advisor identifica le istanze di SQL Server che possono trarre vantaggio dalla creazione di pool di database elastici.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="c7a0c-115">Pool di database elastici forniscono toomanage una soluzione semplice e conveniente obiettivi di prestazioni hello di più database con diversi modelli di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="c7a0c-116">Per altre informazioni sui pool elastici di Azure, vedere [Cos'è un pool elastico di Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="c7a0c-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Consigli di Advisor sui costi per pool di database elastici](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="c7a0c-118">Come tooaccess costo indicazioni in preparazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c7a0c-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="c7a0c-119">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c7a0c-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c7a0c-120">Nel riquadro di sinistra hello, fare clic su **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="c7a0c-121">Hello servizio dei menu, in **monitoraggio e gestione**, fare clic su **Advisor Azure**.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="c7a0c-122">Hello Advisor dashboard viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="c7a0c-123">Nel dashboard di Advisor hello, fare clic su hello **costo** scheda.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="c7a0c-124">Selezionare hello sottoscrizione per il quale desidera tooreceive indicazioni e quindi fare clic su **consigli**.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="c7a0c-125">tooaccess raccomandazioni di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="c7a0c-126">Una sottoscrizione viene registrata quando un *sottoscrizione proprietario* avvia hello hello di dashboard e fa clic su Advisor **consigli** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="c7a0c-127">Si tratta di un'*operazione una tantum*.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-127">This is a *one-time operation*.</span></span> <span data-ttu-id="c7a0c-128">Dopo la sottoscrizione hello è registrata, è possibile accedere raccomandazioni di Advisor come *proprietario*, *collaboratore*, o *lettore* per una sottoscrizione, un gruppo di risorse, o risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="c7a0c-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7a0c-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7a0c-129">Next steps</span></span>

<span data-ttu-id="c7a0c-130">toolearn sulle raccomandazioni di Advisor, vedere:</span><span class="sxs-lookup"><span data-stu-id="c7a0c-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="c7a0c-131">Introduzione tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="c7a0c-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="c7a0c-132">esercitazione introduttiva</span><span class="sxs-lookup"><span data-stu-id="c7a0c-132">Get Started</span></span>](advisor-get-started.md)
* <span data-ttu-id="c7a0c-133">[Advisor Performance recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sulle prestazioni)</span><span class="sxs-lookup"><span data-stu-id="c7a0c-133">[Advisor Performance recommendations](advisor-cost-recommendations.md)</span></span>
* <span data-ttu-id="c7a0c-134">[Advisor High Availability recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)</span><span class="sxs-lookup"><span data-stu-id="c7a0c-134">[Advisor High Availability recommendations](advisor-cost-recommendations.md)</span></span>
* <span data-ttu-id="c7a0c-135">[Advisor Security recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sulla sicurezza)</span><span class="sxs-lookup"><span data-stu-id="c7a0c-135">[Advisor Security recommendations](advisor-cost-recommendations.md)</span></span>
