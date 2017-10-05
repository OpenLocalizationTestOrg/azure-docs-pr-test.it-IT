---
title: Creare un dashboard personalizzato in Log Analytics di Azure | Documentazione Microsoft
description: Questa guida spiega in che modo i dashboard di Log Analytics visualizzano tutte le ricerche log salvate, offrendo un punto di vista unico su tutto l'ambiente.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a90d9c620221bffbb225fb060b997af2f5e90390
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="54c3a-103">Creare un dashboard personalizzato da usare in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="54c3a-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="54c3a-104">Se l'area di lavoro è stata aggiornata al [nuovo linguaggio di query di Log Analytics](log-analytics-log-search-upgrade.md), non è possibile creare nuovi dashboard o modificare i dashboard esistenti.</span><span class="sxs-lookup"><span data-stu-id="54c3a-104">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="54c3a-105">Questa guida spiega in che modo i dashboard di Log Analytics visualizzano tutte le ricerche log salvate, offrendo un punto di vista unico su tutto l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="54c3a-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span></span>

![Dashboard di esempio](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="54c3a-107">Tutti i dashboard personalizzati creati nel portale di OMS sono anche disponibili nell'app OMS per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="54c3a-107">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span></span> <span data-ttu-id="54c3a-108">Vedere le pagine seguenti per altre informazioni sulle app.</span><span class="sxs-lookup"><span data-stu-id="54c3a-108">See the following pages for more information about the apps.</span></span>

* [<span data-ttu-id="54c3a-109">App OMS per dispositivi mobili in Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="54c3a-109">OMS mobile app from the Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="54c3a-110">App OMS per dispositivi mobili in Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="54c3a-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![dashboard mobile](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="54c3a-112">Come si crea un dashboard?</span><span class="sxs-lookup"><span data-stu-id="54c3a-112">How do I create my dashboard?</span></span>
<span data-ttu-id="54c3a-113">Per iniziare, passare alla pagina di panoramica di OMS.</span><span class="sxs-lookup"><span data-stu-id="54c3a-113">To begin, go to the OMS Overview page.</span></span> <span data-ttu-id="54c3a-114">Sulla sinistra verrà visualizzato il riquadro **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="54c3a-114">You'll see the **My Dashboard** tile on the left.</span></span> <span data-ttu-id="54c3a-115">Fare clic per eseguire il drill-down nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="54c3a-115">Click it to drill down into your dashboard.</span></span>

![Panoramica](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="54c3a-117">Aggiunta di un riquadro</span><span class="sxs-lookup"><span data-stu-id="54c3a-117">Adding a tile</span></span>
<span data-ttu-id="54c3a-118">I riquadri dei dashboard vengono compilati in base alle ricerche log salvate.</span><span class="sxs-lookup"><span data-stu-id="54c3a-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="54c3a-119">OMS offre diverse ricerche nei log salvate predefinite che ne consentono un utilizzo immediato.</span><span class="sxs-lookup"><span data-stu-id="54c3a-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="54c3a-120">La procedura seguente descrive come iniziare.</span><span class="sxs-lookup"><span data-stu-id="54c3a-120">Use the following steps that outline how to begin.</span></span>

<span data-ttu-id="54c3a-121">Nella visualizzazione Dashboard fare semplicemente clic su **Personalizza** per passare alla modalità di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="54c3a-121">In the My Dashboard view, simply click **Customize** to enter customize mode.</span></span>

![Illustrazione](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="54c3a-123">Nel pannello visualizzato nella parte destra della pagina sono disponibili tutte le ricerche log salvate dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="54c3a-123">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="54c3a-124">Per visualizzare una ricerca log salvata sotto forma di riquadro, passare il mouse su una ricerca salvata e quindi fare clic sul simbolo **più**.</span><span class="sxs-lookup"><span data-stu-id="54c3a-124">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span></span>

![Aggiunta di riquadri 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="54c3a-126">Quando si fa clic sul segno **più** viene visualizzato un nuovo riquadro nella visualizzazione Dashboard.</span><span class="sxs-lookup"><span data-stu-id="54c3a-126">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span></span>

![Aggiunta di riquadri 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="54c3a-128">Modifica di un riquadro</span><span class="sxs-lookup"><span data-stu-id="54c3a-128">Edit a tile</span></span>
<span data-ttu-id="54c3a-129">Nella visualizzazione Dashboard fare semplicemente clic su **Personalizza** per passare alla modalità di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="54c3a-129">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span></span> <span data-ttu-id="54c3a-130">Fare clic sul riquadro che si desidera modificare.</span><span class="sxs-lookup"><span data-stu-id="54c3a-130">Click the tile you want to edit.</span></span> <span data-ttu-id="54c3a-131">Il pannello destro cambia per consentire la modifica e offre diverse opzioni:</span><span class="sxs-lookup"><span data-stu-id="54c3a-131">The right panel changes to edit, and gives a selection of options:</span></span>

![Modifica di un riquadro](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Modifica di un riquadro](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="54c3a-134">Tipi di visualizzazione dei riquadri</span><span class="sxs-lookup"><span data-stu-id="54c3a-134">Tile visualizations</span></span>
<span data-ttu-id="54c3a-135">È possibile scegliere tra tre tipi di visualizzazione dei riquadri:</span><span class="sxs-lookup"><span data-stu-id="54c3a-135">There are three kinds of tile visualizations to choose from:</span></span>

| <span data-ttu-id="54c3a-136">tipo di grafico</span><span class="sxs-lookup"><span data-stu-id="54c3a-136">chart type</span></span> | <span data-ttu-id="54c3a-137">funzione</span><span class="sxs-lookup"><span data-stu-id="54c3a-137">what it does</span></span> |
| --- | --- |
| ![Grafico a barre](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="54c3a-139">Visualizza una sequenza temporale dei risultati della ricerca log salvata sotto forma di grafico a barre o un elenco dei risultati per campo, a seconda che i risultati vengano aggregati o meno in base a un campo.</span><span class="sxs-lookup"><span data-stu-id="54c3a-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![metrica](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="54c3a-141">Il risultato totale della ricerca nei log viene visualizzato sotto forma di numero in un riquadro.</span><span class="sxs-lookup"><span data-stu-id="54c3a-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="54c3a-142">È possibile impostare un valore soglia che, quando viene raggiunto, determina l'evidenziazione del riquadro.</span><span class="sxs-lookup"><span data-stu-id="54c3a-142">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="54c3a-144">Visualizza una sequenza temporale dei risultati della ricerca log salvata con i relativi valori sotto forma di grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="54c3a-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="54c3a-145">Soglia</span><span class="sxs-lookup"><span data-stu-id="54c3a-145">Threshold</span></span>
<span data-ttu-id="54c3a-146">È possibile creare un valore soglia in un riquadro usando la visualizzazione Metrica.</span><span class="sxs-lookup"><span data-stu-id="54c3a-146">You can create a threshold on a tile using the Metric visualization.</span></span> <span data-ttu-id="54c3a-147">Selezionare le opzioni appropriate per creare un valore soglia nel riquadro.</span><span class="sxs-lookup"><span data-stu-id="54c3a-147">Select on to create a threshold value on the tile.</span></span> <span data-ttu-id="54c3a-148">Specificare se si desidera evidenziare il riquadro quando il valore è sopra o sotto la soglia selezionata e quindi immettere il valore soglia.</span><span class="sxs-lookup"><span data-stu-id="54c3a-148">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span></span>

## <a name="organizing-the-dashboard"></a><span data-ttu-id="54c3a-149">Organizzazione del dashboard</span><span class="sxs-lookup"><span data-stu-id="54c3a-149">Organizing the dashboard</span></span>
<span data-ttu-id="54c3a-150">Per organizzare il dashboard, passare alla visualizzazione Dashboard e fare clic su **Personalizza** per passare alla modalità di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="54c3a-150">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="54c3a-151">Fare clic e trascinare il riquadro nella posizione desiderata.</span><span class="sxs-lookup"><span data-stu-id="54c3a-151">Click and drag the tile you want to move, and move it to where you want your tile to be.</span></span>

![Organizzazione del dashboard](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="54c3a-153">Rimozione di un riquadro</span><span class="sxs-lookup"><span data-stu-id="54c3a-153">Remove a tile</span></span>
<span data-ttu-id="54c3a-154">Per rimuovere un riquadro, passare alla visualizzazione Dashboard e fare clic su **Personalizza** per passare alla modalità di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="54c3a-154">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="54c3a-155">Selezionare il riquadro che si vuole rimuovere e fare clic su **Rimuovi riquadro**nel pannello destro.</span><span class="sxs-lookup"><span data-stu-id="54c3a-155">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span></span>

![Rimozione di un riquadro](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="54c3a-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="54c3a-157">Next steps</span></span>
* <span data-ttu-id="54c3a-158">Creare [avvisi](log-analytics-alerts.md) in Log Analytics per generare notifiche e risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="54c3a-158">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span></span>
