---
title: Consigli di Azure Advisor sui costi | Microsoft Docs
description: Usare Azure Advisor per ottimizzare il costo delle distribuzioni di Azure.
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
ms.openlocfilehash: 5eef2116f238b477fa8de46ce7b25728c393739c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="0aa49-103">Consigli di Advisor sui costi</span><span class="sxs-lookup"><span data-stu-id="0aa49-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="0aa49-104">Advisor aiuta a ottimizzare e ridurre la spesa complessiva legata ad Azure identificando le risorse inattive e sottoutilizzate.</span><span class="sxs-lookup"><span data-stu-id="0aa49-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="0aa49-105">È possibile ottenere consigli sui costi nella scheda **Costo** del dashboard di Advisor.</span><span class="sxs-lookup"><span data-stu-id="0aa49-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

![Scheda Costo di Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="0aa49-107">Ottimizzare la spesa correlata alle macchine virtuali ridimensionando le istanze sottoutilizzate</span><span class="sxs-lookup"><span data-stu-id="0aa49-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="0aa49-108">Sebbene in alcuni scenari applicativi possa verificarsi un utilizzo ridotto legato alla progettazione, è comunque possibile risparmiare denaro mediante la gestione delle dimensioni e del numero delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0aa49-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="0aa49-109">Advisor monitora l'utilizzo delle macchine virtuali per 14 giorni, in modo da identificare le macchine virtuali il cui utilizzo è ridotto.</span><span class="sxs-lookup"><span data-stu-id="0aa49-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="0aa49-110">Le macchine virtuali con un utilizzo della CPU pari al 5% o inferiore e un utilizzo di rete pari a 7 MB o inferiore per quattro o più giorni sono considerate macchine virtuali il cui utilizzo è ridotto.</span><span class="sxs-lookup"><span data-stu-id="0aa49-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="0aa49-111">Advisor mostra il costo stimato qualora si continui a eseguire la macchina virtuale, consentendo pertanto di scegliere se arrestarla o ridimensionarla.</span><span class="sxs-lookup"><span data-stu-id="0aa49-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>  

![Consigli di Advisor sui costi per il ridimensionamento delle macchine virtuali](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-to-manage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="0aa49-113">Usare una soluzione conveniente per gestire gli obiettivi di prestazioni di più database SQL</span><span class="sxs-lookup"><span data-stu-id="0aa49-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="0aa49-114">Advisor identifica le istanze di SQL Server che possono trarre vantaggio dalla creazione di pool di database elastici.</span><span class="sxs-lookup"><span data-stu-id="0aa49-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="0aa49-115">I pool di database elastici offrono una soluzione semplice e conveniente per gestire gli obiettivi di prestazioni per più database con modelli di utilizzo mutevoli.</span><span class="sxs-lookup"><span data-stu-id="0aa49-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="0aa49-116">Per altre informazioni sui pool elastici di Azure, vedere [Cos'è un pool elastico di Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="0aa49-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Consigli di Advisor sui costi per pool di database elastici](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="0aa49-118">Come accedere ai consigli sui costi in Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="0aa49-118">How to access cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="0aa49-119">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0aa49-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0aa49-120">Nel riquadro sinistro selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="0aa49-120">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="0aa49-121">Nel riquadro del menu del servizio in **Monitoraggio e gestione** fare clic su **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="0aa49-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="0aa49-122">Verrà visualizzato il dashboard di Advisor.</span><span class="sxs-lookup"><span data-stu-id="0aa49-122">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="0aa49-123">Nel dashboard di Advisor fare clic sulla scheda **Costo**.</span><span class="sxs-lookup"><span data-stu-id="0aa49-123">On the Advisor dashboard, click the **Cost** tab.</span></span>

5. <span data-ttu-id="0aa49-124">Selezionare la sottoscrizione per cui si desidera ricevere consigli e quindi fare clic su **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="0aa49-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="0aa49-125">Per accedere ai consigli di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor.</span><span class="sxs-lookup"><span data-stu-id="0aa49-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="0aa49-126">Una sottoscrizione viene registrata quando il *proprietario della sottoscrizione* avvia il dashboard di Advisor e fa clic sul pulsante **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="0aa49-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="0aa49-127">Si tratta di un'*operazione una tantum*.</span><span class="sxs-lookup"><span data-stu-id="0aa49-127">This is a *one-time operation*.</span></span> <span data-ttu-id="0aa49-128">Dopo aver registrato una sottoscrizione, è possibile accedere ai consigli di Advisor come *Proprietario*, *Collaboratore* o *Lettore* di una sottoscrizione, di un gruppo di risorse o di una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="0aa49-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0aa49-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0aa49-129">Next steps</span></span>

<span data-ttu-id="0aa49-130">Per altre informazioni sui consigli di Advisor, vedere:</span><span class="sxs-lookup"><span data-stu-id="0aa49-130">To learn more about Advisor recommendations, see:</span></span>
* <span data-ttu-id="0aa49-131">[Introduction to Advisor](advisor-overview.md) (Presentazione di Azure Advisor)</span><span class="sxs-lookup"><span data-stu-id="0aa49-131">[Introduction to Advisor](advisor-overview.md)</span></span>
* [<span data-ttu-id="0aa49-132">esercitazione introduttiva</span><span class="sxs-lookup"><span data-stu-id="0aa49-132">Get Started</span></span>](advisor-get-started.md)
* <span data-ttu-id="0aa49-133">[Advisor Performance recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sulle prestazioni)</span><span class="sxs-lookup"><span data-stu-id="0aa49-133">[Advisor Performance recommendations](advisor-cost-recommendations.md)</span></span>
* <span data-ttu-id="0aa49-134">[Advisor High Availability recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)</span><span class="sxs-lookup"><span data-stu-id="0aa49-134">[Advisor High Availability recommendations](advisor-cost-recommendations.md)</span></span>
* <span data-ttu-id="0aa49-135">[Advisor Security recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sulla sicurezza)</span><span class="sxs-lookup"><span data-stu-id="0aa49-135">[Advisor Security recommendations](advisor-cost-recommendations.md)</span></span>
