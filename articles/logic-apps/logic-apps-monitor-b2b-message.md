---
title: Monitorare e configurare la registrazione per le transazioni B2B - App per la logica di Azure | Microsoft Docs
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
ms.openlocfilehash: f717dae9a70a96944b623f22b90cf8c5a943f382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="190af-103">Monitorare e configurare la registrazione diagnostica per la comunicazione B2B negli account di integrazione</span><span class="sxs-lookup"><span data-stu-id="190af-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="190af-104">Dopo avere configurato la comunicazione B2B tra due processi o applicazioni aziendali in esecuzione usando l'account di integrazione, tali entità possono scambiarsi messaggi.</span><span class="sxs-lookup"><span data-stu-id="190af-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="190af-105">Per verificare che la comunicazione funziona come previsto, è possibile impostare il monitoraggio per i messaggi AS2, X12 ed EDIFACT, nonché la registrazione diagnostica per l'account di integrazione attraverso il servizio [Log Analytics di Azure](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="190af-105">To confirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through the [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="190af-106">Questo servizio di [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) consente di monitorare il cloud e gli ambienti locali, di gestirne la disponibilità e le prestazioni e di raccogliere dettagli ed eventi di runtime per ottimizzare il debug.</span><span class="sxs-lookup"><span data-stu-id="190af-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="190af-107">È anche possibile [usare i dati diagnostici con altri servizi](#extend-diagnostic-data), ad esempio Archiviazione di Azure e Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="190af-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="190af-108">Requisiti</span><span class="sxs-lookup"><span data-stu-id="190af-108">Requirements</span></span>

* <span data-ttu-id="190af-109">Un'app per la logica configurata con la registrazione diagnostica.</span><span class="sxs-lookup"><span data-stu-id="190af-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="190af-110">Informazioni su [come configurare la registrazione per l'app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="190af-110">Learn [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="190af-111">Soddisfatto questo requisito, sarà disponibile un'area di lavoro in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="190af-111">After you've met this requirement, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="190af-112">Quando si configura la registrazione per l'account di integrazione è consigliabile usare la stessa area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="190af-112">You should use the same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="190af-113">Se non si ha un'area di lavoro di OMS, vedere [come crearne una](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="190af-113">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="190af-114">Un account di integrazione collegato all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="190af-114">An integration account that's linked to your logic app.</span></span> <span data-ttu-id="190af-115">Informazioni su [come creare un account di integrazione con un collegamento all'app per la logica](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="190af-115">Learn [how to create an integration account with a link to your logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="190af-116">Attivare la registrazione diagnostica per l'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="190af-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="190af-117">È possibile attivare la registrazione direttamente dall'account di integrazione o [usando il servizio Monitoraggio di Azure](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="190af-117">You can turn on logging either directly from your integration account or [through the Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="190af-118">Monitoraggio di Azure offre il monitoraggio di base con dati a livello di infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="190af-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="190af-119">Altre informazioni su [Monitoraggio di Azure](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="190af-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="190af-120">Attivare la registrazione diagnostica direttamente dall'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="190af-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="190af-121">Nel [portale di Azure](https://portal.azure.com) trovare e selezionare l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="190af-121">In the [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="190af-122">In **Monitoraggio** scegliere **Log di diagnostica** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="190af-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Trovare e selezionare l'account di integrazione, quindi scegliere "Log di diagnostica"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="190af-124">Dopo aver selezionato l'account di integrazione, i valori riportati di seguito vengono selezionati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="190af-124">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="190af-125">Se questi valori sono corretti, scegliere **Abilita diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="190af-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="190af-126">In caso contrario, selezionare valori specifici:</span><span class="sxs-lookup"><span data-stu-id="190af-126">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="190af-127">In **Sottoscrizione** selezionare la sottoscrizione di Azure da usare con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="190af-127">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="190af-128">In **Gruppo di risorse** selezionare il gruppo di risorse da usare con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="190af-128">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="190af-129">In **Tipo di risorsa** selezionare **Account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="190af-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="190af-130">In **Risorsa** selezionare il proprio account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="190af-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="190af-131">Scegliere **Abilita diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="190af-131">Choose **Turn on diagnostics**.</span></span>

   ![Configurare la diagnostica per l'account di integrazione](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="190af-133">In **Impostazioni di diagnostica** scegliere **Sì** sotto **Stato**.</span><span class="sxs-lookup"><span data-stu-id="190af-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Attivare la diagnostica di Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="190af-135">Selezionare ora l'area di lavoro di OMS e i dati da usare per la registrazione, come indicato:</span><span class="sxs-lookup"><span data-stu-id="190af-135">Now select the OMS workspace and data to use for logging as shown:</span></span>

   1. <span data-ttu-id="190af-136">Selezionare **Invia a Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="190af-136">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="190af-137">In **Log Analytics** scegliere **Configura**.</span><span class="sxs-lookup"><span data-stu-id="190af-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="190af-138">In **Aree di lavoro OMS** selezionare l'area di lavoro di OMS da usare per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="190af-138">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="190af-139">In **Log** selezionare la categoria **IntegrationAccountTrackingEvents**.</span><span class="sxs-lookup"><span data-stu-id="190af-139">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="190af-140">Scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="190af-140">Choose **Save**.</span></span>

   ![Impostare Log Analytics in modo da inviare i dati di diagnostica a un log](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="190af-142">[Impostare la registrazione per i messaggi B2B in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="190af-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="190af-143">Attivare la registrazione diagnostica con Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="190af-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="190af-144">Nel menu principale di Azure del [portale di Azure](https://portal.azure.com) scegliere **Monitoraggio**, **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="190af-144">In the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="190af-145">Selezionare quindi il proprio account di integrazione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="190af-145">Then select your integration account as shown here:</span></span>

   ![Scegliere "Monitoraggio", "Log di diagnostica", selezionare l'account di integrazione](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="190af-147">Dopo aver selezionato l'account di integrazione, i valori riportati di seguito vengono selezionati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="190af-147">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="190af-148">Se questi valori sono corretti, scegliere **Abilita diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="190af-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="190af-149">In caso contrario, selezionare valori specifici:</span><span class="sxs-lookup"><span data-stu-id="190af-149">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="190af-150">In **Sottoscrizione** selezionare la sottoscrizione di Azure da usare con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="190af-150">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="190af-151">In **Gruppo di risorse** selezionare il gruppo di risorse da usare con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="190af-151">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="190af-152">In **Tipo di risorsa** selezionare **Account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="190af-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="190af-153">In **Risorsa** selezionare il proprio account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="190af-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="190af-154">Scegliere **Abilita diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="190af-154">Choose **Turn on diagnostics**.</span></span>

   ![Configurare la diagnostica per l'account di integrazione](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="190af-156">In **Impostazioni di diagnostica** scegliere **Sì**.</span><span class="sxs-lookup"><span data-stu-id="190af-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Attivare la diagnostica di Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="190af-158">Selezionare ora l'area di lavoro di OMS e la categoria di eventi per la registrazione, come indicato:</span><span class="sxs-lookup"><span data-stu-id="190af-158">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="190af-159">Selezionare **Invia a Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="190af-159">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="190af-160">In **Log Analytics** scegliere **Configura**.</span><span class="sxs-lookup"><span data-stu-id="190af-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="190af-161">In **Aree di lavoro OMS** selezionare l'area di lavoro di OMS da usare per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="190af-161">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="190af-162">In **Log** selezionare la categoria **IntegrationAccountTrackingEvents**.</span><span class="sxs-lookup"><span data-stu-id="190af-162">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="190af-163">Al termine dell'operazione, scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="190af-163">When you're done, choose **Save**.</span></span>

   ![Impostare Log Analytics in modo da inviare i dati di diagnostica a un log](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="190af-165">[Impostare la registrazione per i messaggi B2B in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="190af-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="190af-166">Estendere l'uso dei dati di diagnostica con altri servizi</span><span class="sxs-lookup"><span data-stu-id="190af-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="190af-167">Con Azure Log Analytics, è possibile usare in modo diverso i dati di diagnostica dell'app per la logica con altri servizi di Azure, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="190af-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="190af-168">Archiviare i log di diagnostica di Azure in Archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="190af-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="190af-169">Trasmettere i log di diagnostica di Azure a Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="190af-169">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="190af-170">È quindi possibile eseguire il monitoraggio in tempo reale usando i dati di telemetria e l'analisi da altri servizi, ad esempio [Analisi di flusso di Azure](../stream-analytics/stream-analytics-introduction.md) e [Power BI](../log-analytics/log-analytics-powerbi.md),</span><span class="sxs-lookup"><span data-stu-id="190af-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="190af-171">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="190af-171">For example:</span></span>

* [<span data-ttu-id="190af-172">Trasmettere i dati da Hub eventi ad Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="190af-172">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="190af-173">Analizzare i dati di streaming con Analisi di flusso e creare un dashboard di analisi in tempo reale in Power BI</span><span class="sxs-lookup"><span data-stu-id="190af-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="190af-174">In base alle opzioni che si vuole configurare, assicurarsi prima di tutto di [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md) o di [creare un hub eventi di Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="190af-174">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="190af-175">Selezionare quindi le opzioni per la posizione a cui si vogliono inviare i dati di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="190af-175">Then select the options for where you want to send diagnostic data:</span></span>

![Inviare i dati all'hub di eventi o all'account di archiviazione di Azure](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="190af-177">I periodi di conservazione si applicano solo quando si sceglie di usare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="190af-177">Retention periods apply only when you choose to use a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="190af-178">Schemi di rilevamento supportati</span><span class="sxs-lookup"><span data-stu-id="190af-178">Supported tracking schemas</span></span>

<span data-ttu-id="190af-179">Azure supporta questi tipi di schemi di rilevamento, che sono tutti fissi ad eccezione del tipo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="190af-179">Azure supports these tracking schema types, which all have fixed schemas except the Custom type.</span></span>

* [<span data-ttu-id="190af-180">Schema di rilevamento AS2</span><span class="sxs-lookup"><span data-stu-id="190af-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="190af-181">Schema di rilevamento X12</span><span class="sxs-lookup"><span data-stu-id="190af-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="190af-182">Schema di rilevamento personalizzato</span><span class="sxs-lookup"><span data-stu-id="190af-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="190af-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="190af-183">Next steps</span></span>

* [<span data-ttu-id="190af-184">Tenere traccia dei messaggi B2B in OMS</span><span class="sxs-lookup"><span data-stu-id="190af-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Tenere traccia dei messaggi B2B in OMS")
* [<span data-ttu-id="190af-185">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="190af-185">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack")

