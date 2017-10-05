---
title: Introduzione ad Azure Advisor | Microsoft Docs
description: Introduzione ad Azure Advisor.
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: a662841bebda460d4225e080f16705b3f16fdc46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="a8dfc-103">Introduzione ad Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="a8dfc-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="a8dfc-104">Informazioni su come accedere ad Advisor tramite il portale di Azure e ricevere, mettere in pratica, cercare consigli o chiedere consigli aggiornati.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="a8dfc-105">Ricevere consigli da Advisor</span><span class="sxs-lookup"><span data-stu-id="a8dfc-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="a8dfc-106">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a8dfc-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a8dfc-107">Nel riquadro sinistro selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-107">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="a8dfc-108">Nel riquadro del menu del servizio in **Monitoraggio e gestione** fare clic su **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="a8dfc-109">Verrà visualizzato il dashboard di Advisor.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-109">The Advisor dashboard is displayed.</span></span>

   ![Accedere ad Azure Advisor tramite il Portale di Azure](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="a8dfc-111">Nel dashboard di Advisor selezionare la sottoscrizione per cui si desidera ricevere consigli.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span></span>  
<span data-ttu-id="a8dfc-112">Nel dashboard di Advisor vengono visualizzati consigli personalizzati per la sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="a8dfc-113">Per ricevere consigli per una determinata categoria, fare clic su una delle schede: **Disponibilità elevata**, **Sicurezza**, **Prestazioni** o **Costo**.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="a8dfc-114">Per accedere ai consigli di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="a8dfc-115">Una sottoscrizione viene registrata quando il *proprietario della sottoscrizione* avvia il dashboard di Advisor e fa clic sul pulsante **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="a8dfc-116">Si tratta di un'*operazione una tantum*.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-116">This is a *one-time operation*.</span></span> <span data-ttu-id="a8dfc-117">Dopo aver registrato una sottoscrizione, è possibile accedere ai consigli di Advisor come *Proprietario*, *Collaboratore* o *Lettore* di una sottoscrizione, di un gruppo di risorse o di una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Dashboard di Azure Advisor](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="a8dfc-119">Ottenere i dettagli dei consigli di Advisor e implementare una soluzione</span><span class="sxs-lookup"><span data-stu-id="a8dfc-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="a8dfc-120">Il pannello **Raccomandazioni** in Advisor offre informazioni aggiuntive sui consigli.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span></span> 

1. <span data-ttu-id="a8dfc-121">Accedere al [portale di Azure](https://portal.azure.com) e quindi avviare [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="a8dfc-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="a8dfc-122">Nel dashboard **Raccomandazioni Advisor** fare clic su **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="a8dfc-123">Nell'elenco dei consigli fare clic su un consigli da esaminare nel dettaglio.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-123">In the list of recommendations, click a recommendation that you want to review in detail.</span></span>  
<span data-ttu-id="a8dfc-124">Verrà visualizzato il pannello **Raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-124">The **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="a8dfc-125">Nel pannello **Raccomandazioni** esaminare le informazioni sulle azioni che è possibile eseguire per risolvere un potenziale problema o sfruttare un'opportunità per ridurre i costi.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![Pannello dei consigli di Advisor](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="a8dfc-127">Cercare consigli di Advisor</span><span class="sxs-lookup"><span data-stu-id="a8dfc-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="a8dfc-128">È possibile cercare consigli per un determinato gruppo di risorse o una determinata sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="a8dfc-129">È anche possibile cercare consigli in base allo stato.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="a8dfc-130">Accedere al [portale di Azure](https://portal.azure.com) e quindi avviare [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="a8dfc-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="a8dfc-131">Cercare i consigli applicando un filtro in base a sottoscrizioni, gruppi di risorse e stato dei consigli (**Attivo** o **Posposto**).</span><span class="sxs-lookup"><span data-stu-id="a8dfc-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="a8dfc-132">Per visualizzare un elenco di consigli di Advisor in base ai criteri dei filtri di ricerca, fare clic su **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Criteri dei filtri di ricerca di Advisor](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="a8dfc-134">Posporre o ignorare i consigli di Advisor</span><span class="sxs-lookup"><span data-stu-id="a8dfc-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="a8dfc-135">Accedere al [portale di Azure](https://portal.azure.com) e quindi avviare [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="a8dfc-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="a8dfc-136">Fare clic su **Ottieni raccomandazioni** e quindi fare clic su un consiglio nell'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="a8dfc-137">Nel pannello **Consigli** fare clic su **Posponi**.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-137">On the **Recommendation** blade, click **Snooze**.</span></span>  

   ![Esempio di azione consigliata da Advisor](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="a8dfc-139">È possibile specificare il periodo di tempo in base al quale posporre il consiglio oppure selezionare **Mai** per ignorare il consiglio.</span><span class="sxs-lookup"><span data-stu-id="a8dfc-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a8dfc-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8dfc-140">Next steps</span></span>

<span data-ttu-id="a8dfc-141">Per altre informazioni su Advisor, vedere:</span><span class="sxs-lookup"><span data-stu-id="a8dfc-141">To learn more about Advisor, see:</span></span>
* <span data-ttu-id="a8dfc-142">[Introduction to Azure Advisor](advisor-overview.md) (Presentazione di Azure Advisor)</span><span class="sxs-lookup"><span data-stu-id="a8dfc-142">[Introduction to Azure Advisor](advisor-overview.md)</span></span>
* <span data-ttu-id="a8dfc-143">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)</span><span class="sxs-lookup"><span data-stu-id="a8dfc-143">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md)</span></span>
* <span data-ttu-id="a8dfc-144">[Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza)</span><span class="sxs-lookup"><span data-stu-id="a8dfc-144">[Advisor Security recommendations](advisor-security-recommendations.md)</span></span>
-  <span data-ttu-id="a8dfc-145">[Advisor Performance recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sulle prestazioni)</span><span class="sxs-lookup"><span data-stu-id="a8dfc-145">[Advisor Performance recommendations](advisor-performance-recommendations.md)</span></span>
* <span data-ttu-id="a8dfc-146">[Advisor Cost recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sui costi)</span><span class="sxs-lookup"><span data-stu-id="a8dfc-146">[Advisor Cost recommendations](advisor-performance-recommendations.md)</span></span>
