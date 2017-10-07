---
title: le transazioni B2B aaaMonitor e impostare il livello di registrazione - App Azure per la logica | Documenti Microsoft
description: Monitorare i messaggi AS2, X12 ed EDIFACT, avviare la registrazione diagnostica per l'account di integrazione
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
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="aa0f9-103">Monitorare e configurare la registrazione diagnostica per la comunicazione B2B negli account di integrazione</span><span class="sxs-lookup"><span data-stu-id="aa0f9-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="aa0f9-104">Dopo avere configurato la comunicazione B2B tra due processi o applicazioni aziendali in esecuzione usando l'account di integrazione, tali entità possono scambiarsi messaggi.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="aa0f9-105">Questa comunicazione tooconfirm funziona come previsto, è possibile impostare il monitoraggio per AS2, X12, e i messaggi EDIFACT, con la registrazione diagnostica per l'account di integrazione tramite hello [Azure Log Analitica](../log-analytics/log-analytics-overview.md) servizio.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-105">tooconfirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="aa0f9-106">Questo servizio di [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) consente di monitorare il cloud e gli ambienti locali, di gestirne la disponibilità e le prestazioni e di raccogliere dettagli ed eventi di runtime per ottimizzare il debug.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="aa0f9-107">È anche possibile [usare i dati diagnostici con altri servizi](#extend-diagnostic-data), ad esempio Archiviazione di Azure e Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="aa0f9-108">Requisiti</span><span class="sxs-lookup"><span data-stu-id="aa0f9-108">Requirements</span></span>

* <span data-ttu-id="aa0f9-109">Un'app per la logica configurata con la registrazione diagnostica.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="aa0f9-110">Informazioni su [come tooset il livello di registrazione per l'app logica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="aa0f9-110">Learn [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="aa0f9-111">Dopo che hai rispettato il requisito, è necessario disporre di un'area di lavoro hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa0f9-111">After you've met this requirement, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="aa0f9-112">È consigliabile utilizzare hello stessa area di lavoro OMS quando si configura la registrazione per l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-112">You should use hello same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="aa0f9-113">Se non si dispone di un'area di lavoro OMS, informazioni su [come un'area di lavoro OMS toocreate](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aa0f9-113">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="aa0f9-114">Un account di integrazione che è collegato tooyour logica app.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-114">An integration account that's linked tooyour logic app.</span></span> <span data-ttu-id="aa0f9-115">Informazioni su [come account di toocreate un'integrazione con un'applicazione di logica tooyour collegamento](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="aa0f9-115">Learn [how toocreate an integration account with a link tooyour logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="aa0f9-116">Attivare la registrazione diagnostica per l'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="aa0f9-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="aa0f9-117">È possibile attivare la registrazione direttamente dall'account di integrazione o [tramite servizio di monitoraggio di Azure hello](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="aa0f9-117">You can turn on logging either directly from your integration account or [through hello Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="aa0f9-118">Monitoraggio di Azure offre il monitoraggio di base con dati a livello di infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="aa0f9-119">Altre informazioni su [Monitoraggio di Azure](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="aa0f9-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="aa0f9-120">Attivare la registrazione diagnostica direttamente dall'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="aa0f9-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="aa0f9-121">In hello [portale di Azure](https://portal.azure.com), trovare e selezionare l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-121">In hello [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="aa0f9-122">In **Monitoraggio** scegliere **Log di diagnostica** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="aa0f9-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Trovare e selezionare l'account di integrazione, quindi scegliere "Log di diagnostica"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="aa0f9-124">Dopo aver selezionato l'account di integrazione, hello seguente i valori viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-124">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="aa0f9-125">Se questi valori sono corretti, scegliere **Abilita diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="aa0f9-126">In caso contrario, selezionare i valori hello che si desidera:</span><span class="sxs-lookup"><span data-stu-id="aa0f9-126">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="aa0f9-127">In **sottoscrizione**, selezionare hello sottoscrizione di Azure che si utilizza con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-127">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="aa0f9-128">In **gruppo di risorse**selezionare gruppo di risorse hello utilizzati con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-128">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="aa0f9-129">In **Tipo di risorsa** selezionare **Account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="aa0f9-130">In **Risorsa** selezionare il proprio account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="aa0f9-131">Scegliere **Abilita diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-131">Choose **Turn on diagnostics**.</span></span>

   ![Configurare la diagnostica per l'account di integrazione](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="aa0f9-133">In **Impostazioni di diagnostica** scegliere **Sì** sotto **Stato**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Attivare la diagnostica di Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="aa0f9-135">A questo punto selezionare toouse hello OMS dell'area di lavoro e i dati per la registrazione come illustrato:</span><span class="sxs-lookup"><span data-stu-id="aa0f9-135">Now select hello OMS workspace and data toouse for logging as shown:</span></span>

   1. <span data-ttu-id="aa0f9-136">Selezionare **inviare tooLog Analitica**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-136">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="aa0f9-137">In **Log Analytics** scegliere **Configura**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="aa0f9-138">In **aree di lavoro OMS**, selezionare hello OMS workspace toouse per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-138">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="aa0f9-139">In **Log**selezionare hello **IntegrationAccountTrackingEvents** categoria.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-139">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="aa0f9-140">Scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-140">Choose **Save**.</span></span>

   ![Impostare Analitica di Log in modo è possibile inviare i log tooa dati di diagnostica](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="aa0f9-142">[Impostare la registrazione per i messaggi B2B in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="aa0f9-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="aa0f9-143">Attivare la registrazione diagnostica con Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="aa0f9-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="aa0f9-144">In hello [portale di Azure](https://portal.azure.com), in hello menu principale di Azure, scegliere **monitoraggio**, **log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-144">In hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="aa0f9-145">Selezionare quindi il proprio account di integrazione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="aa0f9-145">Then select your integration account as shown here:</span></span>

   ![Scegliere "Monitoraggio", "Log di diagnostica", selezionare l'account di integrazione](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="aa0f9-147">Dopo aver selezionato l'account di integrazione, hello seguente i valori viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-147">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="aa0f9-148">Se questi valori sono corretti, scegliere **Abilita diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="aa0f9-149">In caso contrario, selezionare i valori hello che si desidera:</span><span class="sxs-lookup"><span data-stu-id="aa0f9-149">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="aa0f9-150">In **sottoscrizione**, selezionare hello sottoscrizione di Azure che si utilizza con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-150">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="aa0f9-151">In **gruppo di risorse**selezionare gruppo di risorse hello utilizzati con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-151">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="aa0f9-152">In **Tipo di risorsa** selezionare **Account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="aa0f9-153">In **Risorsa** selezionare il proprio account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="aa0f9-154">Scegliere **Abilita diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-154">Choose **Turn on diagnostics**.</span></span>

   ![Configurare la diagnostica per l'account di integrazione](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="aa0f9-156">In **Impostazioni di diagnostica** scegliere **Sì**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Attivare la diagnostica di Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="aa0f9-158">A questo punto selezionare categoria hello OMS area di lavoro e l'evento per la registrazione come illustrato:</span><span class="sxs-lookup"><span data-stu-id="aa0f9-158">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="aa0f9-159">Selezionare **inviare tooLog Analitica**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-159">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="aa0f9-160">In **Log Analytics** scegliere **Configura**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="aa0f9-161">In **aree di lavoro OMS**, selezionare hello OMS workspace toouse per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-161">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="aa0f9-162">In **Log**selezionare hello **IntegrationAccountTrackingEvents** categoria.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-162">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="aa0f9-163">Al termine dell'operazione, scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-163">When you're done, choose **Save**.</span></span>

   ![Impostare Analitica di Log in modo è possibile inviare i log tooa dati di diagnostica](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="aa0f9-165">[Impostare la registrazione per i messaggi B2B in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="aa0f9-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="aa0f9-166">Estendere l'uso dei dati di diagnostica con altri servizi</span><span class="sxs-lookup"><span data-stu-id="aa0f9-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="aa0f9-167">Con Azure Log Analytics, è possibile usare in modo diverso i dati di diagnostica dell'app per la logica con altri servizi di Azure, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="aa0f9-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="aa0f9-168">Archiviare i log di diagnostica di Azure in Archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="aa0f9-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="aa0f9-169">I log di diagnostica Azure tooAzure hub eventi del flusso</span><span class="sxs-lookup"><span data-stu-id="aa0f9-169">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="aa0f9-170">È quindi possibile eseguire il monitoraggio in tempo reale usando i dati di telemetria e l'analisi da altri servizi, ad esempio [Analisi di flusso di Azure](../stream-analytics/stream-analytics-introduction.md) e [Power BI](../log-analytics/log-analytics-powerbi.md),</span><span class="sxs-lookup"><span data-stu-id="aa0f9-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="aa0f9-171">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="aa0f9-171">For example:</span></span>

* [<span data-ttu-id="aa0f9-172">Dati di flusso da hub eventi tooStream Analitica</span><span class="sxs-lookup"><span data-stu-id="aa0f9-172">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="aa0f9-173">Analizzare i dati di streaming con Analisi di flusso e creare un dashboard di analisi in tempo reale in Power BI</span><span class="sxs-lookup"><span data-stu-id="aa0f9-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="aa0f9-174">In base alle opzioni di hello che si desidera configurare, assicurarsi che è primo [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md) o [creare un hub eventi Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="aa0f9-174">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="aa0f9-175">Selezionare quindi le opzioni di hello per cui si desidera toosend dati di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="aa0f9-175">Then select hello options for where you want toosend diagnostic data:</span></span>

![Inviare dati tooAzure storage account o l'evento hub](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="aa0f9-177">Periodi di memorizzazione si applicano solo quando si sceglie toouse un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-177">Retention periods apply only when you choose toouse a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="aa0f9-178">Schemi di rilevamento supportati</span><span class="sxs-lookup"><span data-stu-id="aa0f9-178">Supported tracking schemas</span></span>

<span data-ttu-id="aa0f9-179">Azure supporta questi tipi di schema, che sono corretti schemi ad eccezione del fatto hello tipo personalizzato di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="aa0f9-179">Azure supports these tracking schema types, which all have fixed schemas except hello Custom type.</span></span>

* [<span data-ttu-id="aa0f9-180">Schema di rilevamento AS2</span><span class="sxs-lookup"><span data-stu-id="aa0f9-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="aa0f9-181">Schema di rilevamento X12</span><span class="sxs-lookup"><span data-stu-id="aa0f9-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="aa0f9-182">Schema di rilevamento personalizzato</span><span class="sxs-lookup"><span data-stu-id="aa0f9-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="aa0f9-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aa0f9-183">Next steps</span></span>

* [<span data-ttu-id="aa0f9-184">Tenere traccia dei messaggi B2B in OMS</span><span class="sxs-lookup"><span data-stu-id="aa0f9-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Tenere traccia dei messaggi B2B in OMS")
* [<span data-ttu-id="aa0f9-185">Altre informazioni su Enterprise Integration Pack hello</span><span class="sxs-lookup"><span data-stu-id="aa0f9-185">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")

