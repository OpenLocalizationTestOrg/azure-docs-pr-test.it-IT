---
title: aaaMonitor e ottenere informazioni dettagliate sull'app logica viene eseguita mediante OMS - App Azure per la logica | Documenti Microsoft
description: "Monitorare l'esecuzione dell'applicazione logica con informazioni dettagliate tooget Log Analitica e Operations Management Suite (OMS) e le informazioni di debug più dettagliate per la risoluzione dei problemi e diagnostica"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>Monitorare e ottenere informazioni dettagliate sulle esecuzioni dell'app per la logica con Operations Management Suite (OMS) e Log Analytics

Per informazioni di debug più dettagliate e monitoraggio, è possibile attivare Analitica di Log in hello contemporaneamente quando si crea un'app di logica. Log Analitica fornisce Diagnostica registrazione e monitoraggio per l'app logica viene eseguita tramite il portale di Operations Management Suite (OMS) hello. Quando si aggiunge hello logica di gestione delle App soluzione tooOMS, si ottiene lo stato aggregato per la logica app viene eseguita e dettagli specifici, ad esempio lo stato, il tempo di esecuzione, lo stato di un nuovo invio e ID di correlazione.

Questo argomento viene illustrato come tooturn nel Log Analitica o installare hello soluzione logica di gestione delle App in OMS, in modo che è possibile visualizzare gli eventi di runtime e i dati per l'applicazione della logica di esecuzione.

 > [!TIP]
 > toomonitor logica App, seguire questi passaggi troppo [attivare la registrazione diagnostica e inviare la logica app runtime dati tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Requisiti

Prima di iniziare, è necessario toohave un'area di lavoro OMS. Informazioni su [come un'area di lavoro OMS toocreate](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Attivare la registrazione della diagnostica durante la creazione di app per la logica

1. Nel [portale di Azure](https://portal.azure.com) creare un'app per la logica. Scegliere **Nuovo** > **Enterprise Integration** > **App per la logica** > **Crea**.

   ![Creare un'app per la logica](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. In hello **crea la logica app** eseguire queste attività, come illustrato:

   1. Assegnare un nome all'app per la logica e selezionare la sottoscrizione di Azure personale. 
   2. Creare o selezionare un gruppo di risorse di Azure.
   3. Impostare **Log Analitica** troppo**su**. 
   Area di lavoro OMS selezionare hello in cui si desidera troppo invia dati per l'applicazione della logica di esecuzione. 
   4. Quando si è pronti, scegliere **Pin toodashboard** > **crea**.

      ![Creare l'app per la logica](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      Al termine di questo passaggio, Azure crea l'app per la logica, che ora è associata all'area di lavoro OMS personale. 
      Inoltre, questo passaggio installa automaticamente anche soluzioni di gestione delle App logica hello nell'area di lavoro OMS.

3. in OMS, l'esecuzione dell'app logica tooview [continuare con la procedura](#view-logic-app-runs-oms).

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>Installare una soluzione di gestione delle App logica hello in OMS

Se Log Analytics è già stato attivato al momento della creazione dell'app per la logica, ignorare questo passaggio. Si dispone già di soluzione di gestione delle app di logica di hello installato in OMS.

1. In hello [portale di Azure](https://portal.azure.com), scegliere **più servizi**. Digitare "Log Analytics" come filtro e scegliere **Log Analytics**, come illustrato di seguito:

   ![Scegliere "Log Analytics"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. In **Log Analytics** trovare e selezionare l'area di lavoro di OMS. 

   ![Selezionare l'area di lavoro di OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. In **Gestione** scegliere **Portale di OMS**.

   ![Scegliere "Portale di OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. Nella home page OMS, se viene visualizzata l'intestazione aggiornamento hello, scegliere il banner hello in modo che si aggiorna l'area di lavoro OMS prima. Scegliere quindi **Raccolta soluzioni**.

   ![Scegliere "Raccolta soluzioni"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. In **tutte le soluzioni**, trovare e scegliere il riquadro di hello per hello **logica di gestione delle app** soluzione.

   ![Scegliere "Logic Apps Management" ("Gestione delle app per la logica")](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. soluzione hello tooinstall nell'area di lavoro OMS, scegliere **Aggiungi**.

   ![Scegliere "Aggiungi" per "Logic Apps Management" ("Gestione delle app per la logica")](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>Visualizzare le esecuzioni dell'app per la logica nell'area di lavoro OMS

1. conteggio hello tooview e lo stato per l'app logica viene eseguito, pagina di panoramica passare toohello dell'area di lavoro OMS. Esaminare i dettagli di hello in hello **logica di gestione delle app** riquadro.

   ![Riquadro di panoramica con il numero e lo stato delle esecuzioni dell'app per la logica](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Se questo aggiornamento viene invece riquadro logica di gestione delle App hello, scegliere il banner hello in modo che si aggiorna l'area di lavoro OMS prima.
  
   > ![Aggiornare "l'area di lavoro di OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. tooview un riepilogo con ulteriori dettagli sull'esecuzione dell'applicazione logica, scegliere hello **logica di gestione delle app** riquadro.

   In questo riquadro le esecuzioni dell'app per la logica vengono raggruppate in base al nome o allo stato di esecuzione.

   ![Riepilogo dello stato per le esecuzioni dell'app per la logica](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. tooview che tutti hello viene eseguita per una logica specifica app o stato, riga hello selezionare per un'app di logica o lo stato.

   Di seguito è riportato un esempio che illustra tutte le esecuzioni di hello per un'applicazione una logica specifica:

   ![Visualizzare le esecuzioni per un'app per la logica o uno stato](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > Hello **nuovo invio** colonna viene visualizzato "Sì" per le operazioni risultanti da un'esecuzione inviata di nuovo.

4. toofilter questi risultati, è possibile eseguire il filtro sia sul lato client e lato server.

   * Filtro lato client: per ogni colonna, scegliere i filtri di hello desiderati. 
   Di seguito sono riportati alcuni esempi:

     ![Esempi di filtri di colonna](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Filtro lato server: toochoose un numero di hello finestra o toolimit ora specifica di esecuzione che vengono visualizzati, usare il controllo ambito hello nella parte superiore di hello della pagina hello. 
   Per impostazione predefinita, vengono visualizzati contemporaneamente solo 1.000 record. 
   
     ![Intervallo di tempo hello modifica](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. tooview tutti hello azioni e i relativi dettagli per un specifico, selezionare una riga, che verrà visualizzata la pagina di ricerca nei Log hello. 

   * tooview queste informazioni in una tabella, scegliere **tabella**.
   * query di hello toochange, è possibile modificare la stringa di query hello nella barra di ricerca hello. 
   Per un'esperienza migliore, scegliere **Analisi avanzata**.

     ![Visualizzare azioni e i dettagli per un'esecuzione dell'app per la logica](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     Nella pagina hello Azure Log Analitica qui è possibile aggiornare le query e visualizzare hello risultante dalla tabella hello. 
     Questa query utilizza [il linguaggio di query Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), che può essere modificato se si desidera tooview diversi risultati. 

     ![Azure Log Analytics - Visualizzazione Query](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Passaggi successivi

* [Monitorare i messaggi B2B](../logic-apps/logic-apps-monitor-b2b-message.md)
