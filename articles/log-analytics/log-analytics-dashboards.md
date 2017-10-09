---
title: un dashboard personalizzato in Azure Log Analitica aaaCreate | Documenti Microsoft
description: Questa Guida consente di comprendere come i dashboard di Log Analitica possono visualizzare tutte le ricerche log salvate, offrendo una singola obiettivo tooview l'ambiente.
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
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="13f23-103">Creare un dashboard personalizzato da usare in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="13f23-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="13f23-104">Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi è possibile creare nuovi dashboard o modificare dashboard esistenti.</span><span class="sxs-lookup"><span data-stu-id="13f23-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="13f23-105">Questa Guida consente di comprendere come i dashboard di Log Analitica possono visualizzare tutte le ricerche log salvate, offrendo una singola obiettivo tooview l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="13f23-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![Dashboard di esempio](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="13f23-107">Tutti i dashboard personalizzati hello creati nel portale OMS hello sono disponibili anche in App per dispositivi mobili OMS hello.</span><span class="sxs-lookup"><span data-stu-id="13f23-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="13f23-108">Vedere hello seguenti pagine per altre informazioni sulle App hello.</span><span class="sxs-lookup"><span data-stu-id="13f23-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="13f23-109">App per dispositivi mobili OMS da hello Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="13f23-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="13f23-110">App OMS per dispositivi mobili in Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="13f23-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![dashboard mobile](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="13f23-112">Come si crea un dashboard?</span><span class="sxs-lookup"><span data-stu-id="13f23-112">How do I create my dashboard?</span></span>
<span data-ttu-id="13f23-113">toobegin, pagina Overview di OMS toohello passare.</span><span class="sxs-lookup"><span data-stu-id="13f23-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="13f23-114">Si noterà hello **My Dashboard** riquadro a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="13f23-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="13f23-115">Fare clic toodrill verso il basso nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="13f23-115">Click it toodrill down into your dashboard.</span></span>

![Panoramica](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="13f23-117">Aggiunta di un riquadro</span><span class="sxs-lookup"><span data-stu-id="13f23-117">Adding a tile</span></span>
<span data-ttu-id="13f23-118">I riquadri dei dashboard vengono compilati in base alle ricerche log salvate.</span><span class="sxs-lookup"><span data-stu-id="13f23-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="13f23-119">OMS offre diverse ricerche nei log salvate predefinite che ne consentono un utilizzo immediato.</span><span class="sxs-lookup"><span data-stu-id="13f23-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="13f23-120">Tale struttura i passaggi seguenti hello utilizzare come toobegin.</span><span class="sxs-lookup"><span data-stu-id="13f23-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="13f23-121">Nella visualizzazione My Dashboard hello, fare semplicemente clic **Personalizza** tooenter la modalità di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="13f23-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![Illustrazione](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="13f23-123">Pannello Hello visualizzato sul lato destro hello della pagina hello Mostra tutte le ricerche log salvate dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="13f23-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="13f23-124">toovisualize ricerca di un registro salvato come un riquadro, passare il mouse su una ricerca salvata e quindi fare clic su hello **più** simbolo.</span><span class="sxs-lookup"><span data-stu-id="13f23-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![Aggiunta di riquadri 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="13f23-126">Quando si fa clic su hello **più** symbol, un nuovo riquadro viene visualizzato nella visualizzazione My Dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="13f23-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![Aggiunta di riquadri 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="13f23-128">Modifica di un riquadro</span><span class="sxs-lookup"><span data-stu-id="13f23-128">Edit a tile</span></span>
<span data-ttu-id="13f23-129">Nella visualizzazione My Dashboard hello, fare semplicemente clic **Personalizza** tooenter la modalità di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="13f23-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="13f23-130">Fare clic su riquadro hello da tooedit.</span><span class="sxs-lookup"><span data-stu-id="13f23-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="13f23-131">riquadro di destra Hello diventa tooedit e fornisce diverse opzioni:</span><span class="sxs-lookup"><span data-stu-id="13f23-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![Modifica di un riquadro](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Modifica di un riquadro](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="13f23-134">Tipi di visualizzazione dei riquadri</span><span class="sxs-lookup"><span data-stu-id="13f23-134">Tile visualizations</span></span>
<span data-ttu-id="13f23-135">Esistono tre tipi di riquadro visualizzazioni toochoose da:</span><span class="sxs-lookup"><span data-stu-id="13f23-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="13f23-136">tipo di grafico</span><span class="sxs-lookup"><span data-stu-id="13f23-136">chart type</span></span> | <span data-ttu-id="13f23-137">funzione</span><span class="sxs-lookup"><span data-stu-id="13f23-137">what it does</span></span> |
| --- | --- |
| ![Grafico a barre](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="13f23-139">Visualizza una sequenza temporale dei risultati della ricerca log salvata sotto forma di grafico a barre o un elenco dei risultati per campo, a seconda che i risultati vengano aggregati o meno in base a un campo.</span><span class="sxs-lookup"><span data-stu-id="13f23-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![metrica](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="13f23-141">Il risultato totale della ricerca nei log viene visualizzato sotto forma di numero in un riquadro.</span><span class="sxs-lookup"><span data-stu-id="13f23-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="13f23-142">Metrica riquadri consentono di tooset una soglia che, quando viene raggiunta la soglia hello evidenziazione hello riquadro.</span><span class="sxs-lookup"><span data-stu-id="13f23-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="13f23-144">Visualizza una sequenza temporale dei risultati della ricerca log salvata con i relativi valori sotto forma di grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="13f23-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="13f23-145">Soglia</span><span class="sxs-lookup"><span data-stu-id="13f23-145">Threshold</span></span>
<span data-ttu-id="13f23-146">È possibile creare una soglia in un riquadro usando la visualizzazione Metrica hello.</span><span class="sxs-lookup"><span data-stu-id="13f23-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="13f23-147">Scegliere toocreate un valore di soglia nel riquadro di hello.</span><span class="sxs-lookup"><span data-stu-id="13f23-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="13f23-148">Scegliere se il riquadro hello toohighlight quando il valore di hello è sopra o sotto la soglia di hello scelto, quindi impostare valore soglia hello.</span><span class="sxs-lookup"><span data-stu-id="13f23-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="13f23-149">Organizzazione hello dashboard</span><span class="sxs-lookup"><span data-stu-id="13f23-149">Organizing hello dashboard</span></span>
<span data-ttu-id="13f23-150">tooorganize dashboard, passare a visualizzazione My Dashboard toohello e fare clic su **Personalizza** tooenter la modalità di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="13f23-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="13f23-151">Fare clic e trascinare riquadro hello desiderato toomove e spostarlo toowhere desiderato toobe del riquadro.</span><span class="sxs-lookup"><span data-stu-id="13f23-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![Organizzazione del dashboard](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="13f23-153">Rimozione di un riquadro</span><span class="sxs-lookup"><span data-stu-id="13f23-153">Remove a tile</span></span>
<span data-ttu-id="13f23-154">tooremove un riquadro, passare a visualizzazione My Dashboard toohello e fare clic su **Personalizza** tooenter la modalità di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="13f23-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="13f23-155">Riquadro hello selezionare tooremove desiderato, quindi nel riquadro di destra hello selezionare **Remove Tile**.</span><span class="sxs-lookup"><span data-stu-id="13f23-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![Rimozione di un riquadro](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="13f23-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13f23-157">Next steps</span></span>
* <span data-ttu-id="13f23-158">Creare [avvisi](log-analytics-alerts.md) notifiche toogenerate Log Analitica e tooremediate problemi.</span><span class="sxs-lookup"><span data-stu-id="13f23-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
