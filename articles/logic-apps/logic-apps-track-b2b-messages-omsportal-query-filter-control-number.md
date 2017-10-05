---
title: Query per i messaggi B2B in Operations Management Suite - App per la logica di Azure| Microsoft Docs
description: Creare query per tenere traccia dei messaggi AS2, X12 ed EDIFACT in Operations Management Suite
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2748d3d3daf7c13dca05f663a4a088598e1b3605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-the-microsoft-operations-management-suite-oms"></a><span data-ttu-id="11710-103">Query per i messaggi AS2, X12 ed EDIFACT in Microsoft Operations Management Suite, ovvero OMS</span><span class="sxs-lookup"><span data-stu-id="11710-103">Query for AS2, X12, and EDIFACT messages in the Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="11710-104">Per trovare i messaggi AS2, X12 o EDIFACT che si desidera monitorare con [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), è possibile creare query per filtrare le azioni in base a criteri specifici.</span><span class="sxs-lookup"><span data-stu-id="11710-104">To find the AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="11710-105">Ad esempio, è possibile trovare i messaggi in base a un numero di controllo interscambio specifico.</span><span class="sxs-lookup"><span data-stu-id="11710-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="11710-106">Requisiti</span><span class="sxs-lookup"><span data-stu-id="11710-106">Requirements</span></span>

* <span data-ttu-id="11710-107">Un'app per la logica configurata con la registrazione diagnostica.</span><span class="sxs-lookup"><span data-stu-id="11710-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="11710-108">Informazioni su [come creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) e [come configurare la registrazione per tale app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="11710-108">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="11710-109">Un account di integrazione configurato con il monitoraggio e la registrazione.</span><span class="sxs-lookup"><span data-stu-id="11710-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="11710-110">Informazioni su [come creare un account di integrazione](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [come configurare il monitoraggio e la registrazione per tale account](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="11710-110">Learn [how to create an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how to set up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="11710-111">Se non è già stato fatto, [pubblicare i dati di diagnostica in Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) e [configurare la verifica dei messaggi in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="11710-111">If you haven't already, [publish diagnostic data to Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11710-112">Dopo avere soddisfatto i requisiti precedenti, sarà presente un'area di lavoro in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11710-112">After you've met the previous requirements, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="11710-113">È consigliabile usare la stessa area di lavoro di OMS per tenere traccia delle comunicazioni B2B in OMS.</span><span class="sxs-lookup"><span data-stu-id="11710-113">You should use the same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="11710-114">Se non si ha un'area di lavoro OMS, vedere [come crearne una](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="11710-114">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-the-operations-management-suite-portal"></a><span data-ttu-id="11710-115">Creare query per i messaggi con i filtri nel portale di Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="11710-115">Create message queries with filters in the Operations Management Suite portal</span></span>

<span data-ttu-id="11710-116">Questo esempio illustra come trovare i messaggi in base a un numero di controllo interscambio.</span><span class="sxs-lookup"><span data-stu-id="11710-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="11710-117">Se si conosce il nome dell'area di lavoro OMS, passare alla home page dell'area di lavoro (`https://{your-workspace-name}.portal.mms.microsoft.com`) e iniziare dal passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="11710-117">If you know your OMS workspace name, go to your workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="11710-118">Altrimenti iniziare dal passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="11710-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="11710-119">Nel [portale di Azure](https://portal.azure.com) scegliere **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="11710-119">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="11710-120">Cercare "Log Analytics" e quindi scegliere **Log Analytics**, come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="11710-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Trovare Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="11710-122">In **Log Analytics** trovare e selezionare l'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="11710-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Selezionare l'area di lavoro di OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="11710-124">In **Gestione** scegliere **Portale di OMS**.</span><span class="sxs-lookup"><span data-stu-id="11710-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Scegliere Portale di OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="11710-126">Nella home page di OMS scegliere **Ricerca log**.</span><span class="sxs-lookup"><span data-stu-id="11710-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Nella home page di OMS scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="11710-128">-oppure-</span><span class="sxs-lookup"><span data-stu-id="11710-128">-or-</span></span>

   ![Dal menu di OMS scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="11710-130">Nella casella di ricerca inserire il campo che si vuole trovare e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="11710-130">In the search box, enter a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="11710-131">Quando si inizia a digitare, OMS mostra le corrispondenze e operazioni che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="11710-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="11710-132">Altre informazioni su [come trovare i dati in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="11710-132">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="11710-133">Questo esempio cerca gli eventi con **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="11710-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Iniziare a digitare una stringa di query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="11710-135">Nella barra a sinistra scegliere l'intervallo di tempo che si vuole visualizzare.</span><span class="sxs-lookup"><span data-stu-id="11710-135">In the left bar, choose the timeframe that you want to view.</span></span> <span data-ttu-id="11710-136">Per aggiungere un filtro alla query, scegliere **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="11710-136">To add a filter to your query, choose **+Add**.</span></span>

   ![Aggiungere un filtro alla query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="11710-138">In **Aggiungi filtri** immettere il nome del filtro per trovare quello desiderato.</span><span class="sxs-lookup"><span data-stu-id="11710-138">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="11710-139">Selezionare il filtro e scegliere **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="11710-139">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="11710-140">Per trovare il numero di controllo interscambio, questo esempio cerca la parola "interscambio" e seleziona **event_record_messageProperties_interchangeControlNumber_s** come filtro.</span><span class="sxs-lookup"><span data-stu-id="11710-140">To find the interchange control number, this example searches for the word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as the filter.</span></span>

   ![Selezionare il filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="11710-142">Nella barra a sinistra selezionare il valore del filtro che si vuole usare e scegliere **Applica**.</span><span class="sxs-lookup"><span data-stu-id="11710-142">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   <span data-ttu-id="11710-143">Questo esempio consente di selezionare il numero di controllo interscambio per i messaggi desiderati.</span><span class="sxs-lookup"><span data-stu-id="11710-143">This example selects the interchange control number for the messages we want.</span></span>

   ![Selezionare il valore del filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="11710-145">Tornare ora alla query che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="11710-145">Now return to the query that you're building.</span></span> <span data-ttu-id="11710-146">La query viene aggiornata con l'evento e il valore del filtro selezionati.</span><span class="sxs-lookup"><span data-stu-id="11710-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="11710-147">Vengono ora filtrati anche i risultati precedenti.</span><span class="sxs-lookup"><span data-stu-id="11710-147">Your previous results are now filtered too.</span></span>

    ![Tornare alla query con i risultati filtrati](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="11710-149">Per salvare la query per un uso futuro</span><span class="sxs-lookup"><span data-stu-id="11710-149">Save your query for future use</span></span>

1. <span data-ttu-id="11710-150">Dalla query nella pagina **Ricerca log** scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="11710-150">From your query on the **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="11710-151">Assegnare un nome alla query, selezionare una categoria e scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="11710-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Assegnare un nome e una categoria alla query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="11710-153">Per visualizzare la query, scegliere **Preferiti**.</span><span class="sxs-lookup"><span data-stu-id="11710-153">To view your query, choose **Favorites**.</span></span>

   ![Scegliere "Preferiti"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="11710-155">In **Ricerche salvate** selezionare la query per visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="11710-155">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="11710-156">Per aggiornare la query e trovare risultati diversi, modificare la query.</span><span class="sxs-lookup"><span data-stu-id="11710-156">To update the query so you can find different results, edit the query.</span></span>

   ![Selezionare la query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-the-operations-management-suite-portal"></a><span data-ttu-id="11710-158">Trovare ed eseguire le query nel portale di Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="11710-158">Find and run saved queries in the Operations Management Suite portal</span></span>

1. <span data-ttu-id="11710-159">Aprire la home page dell'area di lavoro OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) e scegliere **Ricerca log**.</span><span class="sxs-lookup"><span data-stu-id="11710-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Nella home page di OMS scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="11710-161">-oppure-</span><span class="sxs-lookup"><span data-stu-id="11710-161">-or-</span></span>

   ![Dal menu di OMS scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="11710-163">Nella home page **Ricerca log** scegliere **Preferiti**.</span><span class="sxs-lookup"><span data-stu-id="11710-163">On the **Log Search** home page, choose **Favorites**.</span></span>

   ![Scegliere "Preferiti"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="11710-165">In **Ricerche salvate** selezionare la query per visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="11710-165">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="11710-166">Per aggiornare la query e trovare risultati diversi, modificare la query.</span><span class="sxs-lookup"><span data-stu-id="11710-166">To update the query so you can find different results, edit the query.</span></span>

   ![Selezionare la query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="11710-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11710-168">Next steps</span></span>

* [<span data-ttu-id="11710-169">Schemi di rilevamento AS2</span><span class="sxs-lookup"><span data-stu-id="11710-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="11710-170">Schemi di rilevamento X12</span><span class="sxs-lookup"><span data-stu-id="11710-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="11710-171">Schemi di rilevamento personalizzati</span><span class="sxs-lookup"><span data-stu-id="11710-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)