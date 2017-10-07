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
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a>Monitorare e configurare la registrazione diagnostica per la comunicazione B2B negli account di integrazione

Dopo avere configurato la comunicazione B2B tra due processi o applicazioni aziendali in esecuzione usando l'account di integrazione, tali entità possono scambiarsi messaggi. Questa comunicazione tooconfirm funziona come previsto, è possibile impostare il monitoraggio per AS2, X12, e i messaggi EDIFACT, con la registrazione diagnostica per l'account di integrazione tramite hello [Azure Log Analitica](../log-analytics/log-analytics-overview.md) servizio. Questo servizio di [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) consente di monitorare il cloud e gli ambienti locali, di gestirne la disponibilità e le prestazioni e di raccogliere dettagli ed eventi di runtime per ottimizzare il debug. È anche possibile [usare i dati diagnostici con altri servizi](#extend-diagnostic-data), ad esempio Archiviazione di Azure e Hub eventi di Azure.

## <a name="requirements"></a>Requisiti

* Un'app per la logica configurata con la registrazione diagnostica. Informazioni su [come tooset il livello di registrazione per l'app logica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

  > [!NOTE]
  > Dopo che hai rispettato il requisito, è necessario disporre di un'area di lavoro hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). È consigliabile utilizzare hello stessa area di lavoro OMS quando si configura la registrazione per l'account di integrazione. Se non si dispone di un'area di lavoro OMS, informazioni su [come un'area di lavoro OMS toocreate](../log-analytics/log-analytics-get-started.md).

* Un account di integrazione che è collegato tooyour logica app. Informazioni su [come account di toocreate un'integrazione con un'applicazione di logica tooyour collegamento](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a>Attivare la registrazione diagnostica per l'account di integrazione

È possibile attivare la registrazione direttamente dall'account di integrazione o [tramite servizio di monitoraggio di Azure hello](#azure-monitor-service). Monitoraggio di Azure offre il monitoraggio di base con dati a livello di infrastruttura. Altre informazioni su [Monitoraggio di Azure](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a>Attivare la registrazione diagnostica direttamente dall'account di integrazione

1. In hello [portale di Azure](https://portal.azure.com), trovare e selezionare l'account di integrazione. In **Monitoraggio** scegliere **Log di diagnostica** come illustrato di seguito:

   ![Trovare e selezionare l'account di integrazione, quindi scegliere "Log di diagnostica"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. Dopo aver selezionato l'account di integrazione, hello seguente i valori viene selezionato automaticamente. Se questi valori sono corretti, scegliere **Abilita diagnostica**. In caso contrario, selezionare i valori hello che si desidera:

   1. In **sottoscrizione**, selezionare hello sottoscrizione di Azure che si utilizza con l'account di integrazione.
   2. In **gruppo di risorse**selezionare gruppo di risorse hello utilizzati con l'account di integrazione.
   3. In **Tipo di risorsa** selezionare **Account di integrazione**. 
   4. In **Risorsa** selezionare il proprio account di integrazione. 
   5. Scegliere **Abilita diagnostica**.

   ![Configurare la diagnostica per l'account di integrazione](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. In **Impostazioni di diagnostica** scegliere **Sì** sotto **Stato**.

   ![Attivare la diagnostica di Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. A questo punto selezionare toouse hello OMS dell'area di lavoro e i dati per la registrazione come illustrato:

   1. Selezionare **inviare tooLog Analitica**. 
   2. In **Log Analytics** scegliere **Configura**. 
   3. In **aree di lavoro OMS**, selezionare hello OMS workspace toouse per la registrazione.
   4. In **Log**selezionare hello **IntegrationAccountTrackingEvents** categoria.
   5. Scegliere **Salva**.

   ![Impostare Analitica di Log in modo è possibile inviare i log tooa dati di diagnostica](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. [Impostare la registrazione per i messaggi B2B in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a>Attivare la registrazione diagnostica con Monitoraggio di Azure

1. In hello [portale di Azure](https://portal.azure.com), in hello menu principale di Azure, scegliere **monitoraggio**, **log di diagnostica**. Selezionare quindi il proprio account di integrazione come indicato di seguito:

   ![Scegliere "Monitoraggio", "Log di diagnostica", selezionare l'account di integrazione](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. Dopo aver selezionato l'account di integrazione, hello seguente i valori viene selezionato automaticamente. Se questi valori sono corretti, scegliere **Abilita diagnostica**. In caso contrario, selezionare i valori hello che si desidera:

   1. In **sottoscrizione**, selezionare hello sottoscrizione di Azure che si utilizza con l'account di integrazione.
   2. In **gruppo di risorse**selezionare gruppo di risorse hello utilizzati con l'account di integrazione.
   3. In **Tipo di risorsa** selezionare **Account di integrazione**.
   4. In **Risorsa** selezionare il proprio account di integrazione.
   5. Scegliere **Abilita diagnostica**.

   ![Configurare la diagnostica per l'account di integrazione](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. In **Impostazioni di diagnostica** scegliere **Sì**.

   ![Attivare la diagnostica di Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. A questo punto selezionare categoria hello OMS area di lavoro e l'evento per la registrazione come illustrato:

   1. Selezionare **inviare tooLog Analitica**. 
   2. In **Log Analytics** scegliere **Configura**. 
   3. In **aree di lavoro OMS**, selezionare hello OMS workspace toouse per la registrazione.
   4. In **Log**selezionare hello **IntegrationAccountTrackingEvents** categoria.
   5. Al termine dell'operazione, scegliere **Salva**.

   ![Impostare Analitica di Log in modo è possibile inviare i log tooa dati di diagnostica](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. [Impostare la registrazione per i messaggi B2B in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Estendere l'uso dei dati di diagnostica con altri servizi

Con Azure Log Analytics, è possibile usare in modo diverso i dati di diagnostica dell'app per la logica con altri servizi di Azure, ad esempio: 

* [Archiviare i log di diagnostica di Azure in Archiviazione di Microsoft Azure](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [I log di diagnostica Azure tooAzure hub eventi del flusso](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

È quindi possibile eseguire il monitoraggio in tempo reale usando i dati di telemetria e l'analisi da altri servizi, ad esempio [Analisi di flusso di Azure](../stream-analytics/stream-analytics-introduction.md) e [Power BI](../log-analytics/log-analytics-powerbi.md), ad esempio:

* [Dati di flusso da hub eventi tooStream Analitica](../stream-analytics/stream-analytics-define-inputs.md)
* [Analizzare i dati di streaming con Analisi di flusso e creare un dashboard di analisi in tempo reale in Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)

In base alle opzioni di hello che si desidera configurare, assicurarsi che è primo [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md) o [creare un hub eventi Azure](../event-hubs/event-hubs-create.md). Selezionare quindi le opzioni di hello per cui si desidera toosend dati di diagnostica:

![Inviare dati tooAzure storage account o l'evento hub](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> Periodi di memorizzazione si applicano solo quando si sceglie toouse un account di archiviazione.

## <a name="supported-tracking-schemas"></a>Schemi di rilevamento supportati

Azure supporta questi tipi di schema, che sono corretti schemi ad eccezione del fatto hello tipo personalizzato di rilevamento.

* [Schema di rilevamento AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Schema di rilevamento X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Schema di rilevamento personalizzato](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a>Passaggi successivi

* [Tenere traccia dei messaggi B2B in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Tenere traccia dei messaggi B2B in OMS")
* [Altre informazioni su Enterprise Integration Pack hello](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")

