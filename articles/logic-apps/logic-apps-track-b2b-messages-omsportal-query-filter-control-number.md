---
title: aaaQuery per i messaggi B2B Operations Management Suite - App Azure per la logica | Documenti Microsoft
description: Creare query tootrack AS2, X12 e i messaggi EDIFACT in hello Operations Management Suite
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
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="77a2c-103">Eseguire una query per AS2, X12 ed EDIFACT messaggi hello Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="77a2c-103">Query for AS2, X12, and EDIFACT messages in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="77a2c-104">toofind hello AS2, X12 O messaggi EDIFACT che si desidera tenere traccia con [Azure Log Analitica](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), è possibile creare query per filtrare in base alle specifiche azioni criteri.</span><span class="sxs-lookup"><span data-stu-id="77a2c-104">toofind hello AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="77a2c-105">Ad esempio, è possibile trovare i messaggi in base a un numero di controllo interscambio specifico.</span><span class="sxs-lookup"><span data-stu-id="77a2c-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="77a2c-106">Requisiti</span><span class="sxs-lookup"><span data-stu-id="77a2c-106">Requirements</span></span>

* <span data-ttu-id="77a2c-107">Un'app per la logica configurata con la registrazione diagnostica.</span><span class="sxs-lookup"><span data-stu-id="77a2c-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="77a2c-108">Informazioni su [come toocreate un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md) e [come tooset il livello di registrazione per l'app logica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="77a2c-108">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="77a2c-109">Un account di integrazione configurato con il monitoraggio e la registrazione.</span><span class="sxs-lookup"><span data-stu-id="77a2c-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="77a2c-110">Informazioni su [come un account di integrazione toocreate](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [come tooset di monitoraggio e registrazione per l'account](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="77a2c-110">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="77a2c-111">Se hai già fatto, [pubblicare dati di diagnostica tooLog Analitica](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) e [impostare messaggio tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="77a2c-111">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="77a2c-112">Dopo che siano soddisfatti i requisiti precedenti hello, è necessario disporre di un'area di lavoro hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77a2c-112">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="77a2c-113">È consigliabile utilizzare hello stessa area di lavoro OMS per la gestione delle comunicazioni B2B in OMS.</span><span class="sxs-lookup"><span data-stu-id="77a2c-113">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="77a2c-114">Se non si dispone di un'area di lavoro OMS, informazioni su [come un'area di lavoro OMS toocreate](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="77a2c-114">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a><span data-ttu-id="77a2c-115">Creare query per i messaggi con i filtri nel portale di Operations Management Suite hello</span><span class="sxs-lookup"><span data-stu-id="77a2c-115">Create message queries with filters in hello Operations Management Suite portal</span></span>

<span data-ttu-id="77a2c-116">Questo esempio illustra come trovare i messaggi in base a un numero di controllo interscambio.</span><span class="sxs-lookup"><span data-stu-id="77a2c-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="77a2c-117">Se si conosce il nome dell'area di lavoro OMS, Vai a home page dell'area di lavoro di tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) e avviare nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="77a2c-117">If you know your OMS workspace name, go tooyour workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="77a2c-118">Altrimenti iniziare dal passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="77a2c-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="77a2c-119">In hello [portale di Azure](https://portal.azure.com), scegliere **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-119">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="77a2c-120">Cercare "Log Analytics" e quindi scegliere **Log Analytics**, come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="77a2c-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Trovare Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="77a2c-122">In **Log Analytics** trovare e selezionare l'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="77a2c-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Selezionare l'area di lavoro di OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="77a2c-124">In **Gestione** scegliere **Portale di OMS**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Scegliere Portale di OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="77a2c-126">Nella home page di OMS scegliere **Ricerca log**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Nella home page di OMS scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="77a2c-128">-oppure-</span><span class="sxs-lookup"><span data-stu-id="77a2c-128">-or-</span></span>

   ![Scegliere "Ricerca di Log" hello OMS menu](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="77a2c-130">Nella casella di ricerca hello, immettere un campo che si desidera toofind e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-130">In hello search box, enter a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="77a2c-131">Quando si inizia a digitare, OMS mostra le corrispondenze e operazioni che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="77a2c-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="77a2c-132">Altre informazioni, vedere [come toofind dati nel Log Analitica](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="77a2c-132">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="77a2c-133">Questo esempio cerca gli eventi con **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Iniziare a digitare una stringa di query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="77a2c-135">Nella barra sinistra hello, scegliere l'intervallo di tempo hello che si desidera tooview.</span><span class="sxs-lookup"><span data-stu-id="77a2c-135">In hello left bar, choose hello timeframe that you want tooview.</span></span> <span data-ttu-id="77a2c-136">Scegliere una query, tooyour filtro tooadd **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-136">tooadd a filter tooyour query, choose **+Add**.</span></span>

   ![Aggiungi filtro tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="77a2c-138">In **aggiungere filtri**, immettere il nome di filtro di hello, pertanto è possibile trovare il filtro di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="77a2c-138">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="77a2c-139">Selezionare il filtro hello e scegliere **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-139">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="77a2c-140">numero di controllo interscambio hello toofind, in questo esempio cerca la parola hello "interscambio" e seleziona **event_record_messageProperties_interchangeControlNumber_s** come filtro hello.</span><span class="sxs-lookup"><span data-stu-id="77a2c-140">toofind hello interchange control number, this example searches for hello word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as hello filter.</span></span>

   ![Selezionare il filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="77a2c-142">Nella barra sinistra hello, selezionare il valore del filtro hello che desidera toouse e scegliere **applica**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-142">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   <span data-ttu-id="77a2c-143">Questo esempio seleziona numero di controllo interscambio hello per i messaggi hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="77a2c-143">This example selects hello interchange control number for hello messages we want.</span></span>

   ![Selezionare il valore del filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="77a2c-145">Ora restituiscono toohello query che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="77a2c-145">Now return toohello query that you're building.</span></span> <span data-ttu-id="77a2c-146">La query viene aggiornata con l'evento e il valore del filtro selezionati.</span><span class="sxs-lookup"><span data-stu-id="77a2c-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="77a2c-147">Vengono ora filtrati anche i risultati precedenti.</span><span class="sxs-lookup"><span data-stu-id="77a2c-147">Your previous results are now filtered too.</span></span>

    ![Restituire tooyour query con risultati filtrati](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="77a2c-149">Per salvare la query per un uso futuro</span><span class="sxs-lookup"><span data-stu-id="77a2c-149">Save your query for future use</span></span>

1. <span data-ttu-id="77a2c-150">Dalla query in hello **ricerca nei Log** pagina, scegliere **salvare**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-150">From your query on hello **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="77a2c-151">Assegnare un nome alla query, selezionare una categoria e scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Assegnare un nome e una categoria alla query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="77a2c-153">tooview della query, scegliere **Preferiti**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-153">tooview your query, choose **Favorites**.</span></span>

   ![Scegliere "Preferiti"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="77a2c-155">In **ricerche salvate**, selezionare la query in modo che è possibile visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="77a2c-155">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="77a2c-156">query di hello tooupdate trovare, è possibile ottenere risultati diversi, modificare la query hello.</span><span class="sxs-lookup"><span data-stu-id="77a2c-156">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Selezionare la query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a><span data-ttu-id="77a2c-158">Trovare ed eseguire le query salvate nel portale di Operations Management Suite hello</span><span class="sxs-lookup"><span data-stu-id="77a2c-158">Find and run saved queries in hello Operations Management Suite portal</span></span>

1. <span data-ttu-id="77a2c-159">Aprire la home page dell'area di lavoro OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) e scegliere **Ricerca log**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Nella home page di OMS scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="77a2c-161">-oppure-</span><span class="sxs-lookup"><span data-stu-id="77a2c-161">-or-</span></span>

   ![Scegliere "Ricerca di Log" hello OMS menu](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="77a2c-163">In hello **ricerca nei Log** home page di scegliere **Preferiti**.</span><span class="sxs-lookup"><span data-stu-id="77a2c-163">On hello **Log Search** home page, choose **Favorites**.</span></span>

   ![Scegliere "Preferiti"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="77a2c-165">In **ricerche salvate**, selezionare la query in modo che è possibile visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="77a2c-165">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="77a2c-166">query di hello tooupdate trovare, è possibile ottenere risultati diversi, modificare la query hello.</span><span class="sxs-lookup"><span data-stu-id="77a2c-166">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Selezionare la query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="77a2c-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77a2c-168">Next steps</span></span>

* [<span data-ttu-id="77a2c-169">Schemi di rilevamento AS2</span><span class="sxs-lookup"><span data-stu-id="77a2c-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="77a2c-170">Schemi di rilevamento X12</span><span class="sxs-lookup"><span data-stu-id="77a2c-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="77a2c-171">Schemi di rilevamento personalizzati</span><span class="sxs-lookup"><span data-stu-id="77a2c-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)