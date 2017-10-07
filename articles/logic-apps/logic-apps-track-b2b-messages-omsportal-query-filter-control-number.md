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
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a>Eseguire una query per AS2, X12 ed EDIFACT messaggi hello Microsoft Operations Management Suite (OMS)

toofind hello AS2, X12 O messaggi EDIFACT che si desidera tenere traccia con [Azure Log Analitica](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), è possibile creare query per filtrare in base alle specifiche azioni criteri. Ad esempio, è possibile trovare i messaggi in base a un numero di controllo interscambio specifico.

## <a name="requirements"></a>Requisiti

* Un'app per la logica configurata con la registrazione diagnostica. Informazioni su [come toocreate un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md) e [come tooset il livello di registrazione per l'app logica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Un account di integrazione configurato con il monitoraggio e la registrazione. Informazioni su [come un account di integrazione toocreate](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [come tooset di monitoraggio e registrazione per l'account](../logic-apps/logic-apps-monitor-b2b-message.md).

* Se hai già fatto, [pubblicare dati di diagnostica tooLog Analitica](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) e [impostare messaggio tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

> [!NOTE]
> Dopo che siano soddisfatti i requisiti precedenti hello, è necessario disporre di un'area di lavoro hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). È consigliabile utilizzare hello stessa area di lavoro OMS per la gestione delle comunicazioni B2B in OMS. 
>  
> Se non si dispone di un'area di lavoro OMS, informazioni su [come un'area di lavoro OMS toocreate](../log-analytics/log-analytics-get-started.md).

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a>Creare query per i messaggi con i filtri nel portale di Operations Management Suite hello

Questo esempio illustra come trovare i messaggi in base a un numero di controllo interscambio.

> [!TIP] 
> Se si conosce il nome dell'area di lavoro OMS, Vai a home page dell'area di lavoro di tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) e avviare nel passaggio 4. Altrimenti iniziare dal passaggio 1.

1. In hello [portale di Azure](https://portal.azure.com), scegliere **più servizi**. Cercare "Log Analytics" e quindi scegliere **Log Analytics**, come illustrato qui:

   ![Trovare Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. In **Log Analytics** trovare e selezionare l'area di lavoro di OMS.

   ![Selezionare l'area di lavoro di OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. In **Gestione** scegliere **Portale di OMS**.

   ![Scegliere Portale di OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. Nella home page di OMS scegliere **Ricerca log**.

   ![Nella home page di OMS scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -oppure-

   ![Scegliere "Ricerca di Log" hello OMS menu](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. Nella casella di ricerca hello, immettere un campo che si desidera toofind e premere **invio**. Quando si inizia a digitare, OMS mostra le corrispondenze e operazioni che è possibile usare. Altre informazioni, vedere [come toofind dati nel Log Analitica](../log-analytics/log-analytics-log-searches.md).

   Questo esempio cerca gli eventi con **Type=AzureDiagnostics**.

   ![Iniziare a digitare una stringa di query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. Nella barra sinistra hello, scegliere l'intervallo di tempo hello che si desidera tooview. Scegliere una query, tooyour filtro tooadd **+ Aggiungi**.

   ![Aggiungi filtro tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. In **aggiungere filtri**, immettere il nome di filtro di hello, pertanto è possibile trovare il filtro di hello desiderato. Selezionare il filtro hello e scegliere **+ Aggiungi**.

   numero di controllo interscambio hello toofind, in questo esempio cerca la parola hello "interscambio" e seleziona **event_record_messageProperties_interchangeControlNumber_s** come filtro hello.

   ![Selezionare il filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. Nella barra sinistra hello, selezionare il valore del filtro hello che desidera toouse e scegliere **applica**.

   Questo esempio seleziona numero di controllo interscambio hello per i messaggi hello desiderato.

   ![Selezionare il valore del filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. Ora restituiscono toohello query che si sta creando. La query viene aggiornata con l'evento e il valore del filtro selezionati. Vengono ora filtrati anche i risultati precedenti.

    ![Restituire tooyour query con risultati filtrati](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>Per salvare la query per un uso futuro

1. Dalla query in hello **ricerca nei Log** pagina, scegliere **salvare**. Assegnare un nome alla query, selezionare una categoria e scegliere **Salva**.

   ![Assegnare un nome e una categoria alla query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. tooview della query, scegliere **Preferiti**.

   ![Scegliere "Preferiti"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. In **ricerche salvate**, selezionare la query in modo che è possibile visualizzare i risultati di hello. query di hello tooupdate trovare, è possibile ottenere risultati diversi, modificare la query hello.

   ![Selezionare la query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a>Trovare ed eseguire le query salvate nel portale di Operations Management Suite hello

1. Aprire la home page dell'area di lavoro OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) e scegliere **Ricerca log**.

   ![Nella home page di OMS scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -oppure-

   ![Scegliere "Ricerca di Log" hello OMS menu](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. In hello **ricerca nei Log** home page di scegliere **Preferiti**.

   ![Scegliere "Preferiti"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. In **ricerche salvate**, selezionare la query in modo che è possibile visualizzare i risultati di hello. query di hello tooupdate trovare, è possibile ottenere risultati diversi, modificare la query hello.

   ![Selezionare la query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>Passaggi successivi

* [Schemi di rilevamento AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Schemi di rilevamento X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Schemi di rilevamento personalizzati](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)