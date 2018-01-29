---
title: Usare Log Analytics con un'app multi-tenant del database SQL | Microsoft Docs
description: Configurare e usare Log Analytics (OMS) con un'app SaaS multi-tenant del database SQL di Azure
keywords: esercitazione database SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: billgib; sstein
ms.openlocfilehash: 48e8eb91a5febcc1109bee3404bb534bd0391f88
ms.sourcegitcommit: f847fcbf7f89405c1e2d327702cbd3f2399c4bc2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2017
---
# <a name="set-up-and-use-log-analytics-oms-with-a-multi-tenant-azure-sql-database-saas-app"></a>Configurare e usare Log Analytics (OMS) con un'app SaaS multi-tenant del database SQL di Azure

Questa esercitazione illustra come configurare e usare *Log Analytics ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* per il monitoraggio di database e pool elastici. Questa esercitazione si basa sull'[esercitazione sul monitoraggio e la gestione delle prestazioni](saas-dbpertenant-performance-monitoring.md) e mostra come usare *Log Analytics* per estendere le funzionalità di monitoraggio e avviso disponibili nel portale di Azure. Log Analytics è una soluzione adatta alla gestione del monitoraggio e degli avvisi su larga scala, perché supporta centinaia di pool e centinaia di migliaia di database. Si tratta inoltre di una soluzione di monitoraggio singola che supporta l'integrazione del monitoraggio di applicazioni e servizi di Azure diversi tra più sottoscrizioni di Azure.

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Installare e configurare Log Analytics (OMS)
> * Usare Log Analytics per monitorare i pool e i database

Per completare questa esercitazione, verificare che siano soddisfatti i prerequisiti seguenti:

* È stata distribuita l'app del database per tenant SaaS Wingtip Tickets. Per eseguire la distribuzione in meno di cinque minuti, vedere [Deploy and explore the Wingtip Tickets SaaS Database Per Tenant application](saas-dbpertenant-get-started-deploy.md) (Distribuire ed esplorare l'applicazione del database per tenant SaaS Wingtip Tickets)
* Azure PowerShell è installato. Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

Vedere l'[esercitazione sul monitoraggio e la gestione delle prestazioni](saas-dbpertenant-performance-monitoring.md) per una presentazione degli scenari e dei modelli SaaS, nonché dei loro effetti sui requisiti per una soluzione di monitoraggio.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Monitoraggio e gestione delle prestazioni con Log Analytics (OMS)

Per il database SQL, il monitoraggio e gli avvisi sono disponibili per database e pool. Queste funzionalità predefinite di gestione del monitoraggio e degli avvisi sono destinate a risorse specifiche e risultano comode per un numero limitato di risorse. Sono invece meno efficaci per il monitoraggio di installazioni di grandi dimensioni o per ottenere una vista unificata su sottoscrizioni e risorse diverse.

Per scenari con volumi elevati, è possibile usare Log Analytics. Si tratta di un servizio di Azure separato che fornisce funzionalità di analisi per log di diagnostica e dati di telemetria raccolti in un'area di lavoro di Log Analytics, che consente di raccogliere dati di telemetria da molti servizi e supporta l'esecuzione di query e l'impostazione di avvisi. Log Analytics include un linguaggio di query predefinito e strumenti per la visualizzazione dei dati che consentono l'analisi e la visualizzazione di dati operativi. La soluzione Analisi SQL include varie viste e query predefinite per il monitoraggio e gli avvisi per pool elastici e database, oltre a consentire l'aggiunta e il salvataggio di query ad hoc all'occorrenza. OMS offre anche una finestra di progettazione viste personalizzata.

Le aree di lavoro e le soluzioni di analisi di Log Analytics possono essere aperte sia nel portale di Azure che in OMS. Il portale di Azure è il punto di accesso più recente, ma potrebbe trovarsi dietro il portale OMS in alcune aree.

### <a name="create-data-by-starting-the-load-generator"></a>Creare dati avviando il generatore di carico 

1. Aprire **Demo-PerformanceMonitoringAndManagement.ps1** in **PowerShell ISE**. Mantenere lo script aperto perché potrebbe essere necessario eseguire vari scenari di generazione del carico durante l'esercitazione.
1. Se sono disponibili meno di cinque tenant, effettuare il provisioning di un batch di tenant per ottenere un contesto di monitoraggio più interessante:
   1. Impostare **$DemoScenario = 1,** **Effettuare il provisioning di un batch di tenant**
   1. Premere **F5** per eseguire lo script.

1. Impostare **$DemoScenario** = 2, **Generare un carico di intensità normale (circa 40 DTU)**.
1. Premere **F5** per eseguire lo script.

## <a name="get-the-wingtip-tickets-saas-database-per-tenant-application-scripts"></a>Ottenere gli script dell'applicazione del database per tenant SaaS Wingtip Tickets

Gli script e il codice sorgente dell'applicazione SaaS di database multi-tenant Wingtip Tickets sono disponibili nel repository [WingtipTicketsSaaS-DbPerTenant](https://github.com/Microsoft/WingtipTicketsSaaS-DbPerTenant) di GitHub. Leggere le [linee guida generali](saas-tenancy-wingtip-app-guidance-tips.md) per i passaggi da seguire per scaricare e sbloccare gli script dell'app SaaS Wingtip Tickets.

## <a name="installing-and-configuring-log-analytics-and-the-azure-sql-analytics-solution"></a>Installazione e configurazione di Log Analytics e della soluzione Analisi SQL di Azure

Log Analytics è un servizio separato che deve essere configurato. Log Analytics raccoglie dati di log, dati di telemetria e metriche in un'area di lavoro di Log Analytics. Un'area di lavoro è una risorsa, analogamente ad altre risorse in Azure, e deve essere creata. Anche se l'area di lavoro non deve essere necessariamente creata nello stesso gruppo di risorse delle applicazioni da monitorare, questa è in genere la scelta più sensata. Per l'app del database per tenant SaaS Wingtip Tickets, ciò permette di eliminare facilmente l'area di lavoro con l'applicazione, eliminando il gruppo di risorse.

1. Aprire ...**Learning Modules**Performance Monitoring and Management\\Log Analytics\\\\Demo-LogAnalytics.ps1\\ in *PowerShell ISE*.
1. Premere **F5** per eseguire lo script.

A questo punto, dovrebbe essere possibile aprire Log Analytics nel portale di Azure (o nel portale OMS). Sono necessari alcuni minuti per raccogliere i dati di telemetria e visualizzarli nell'area di lavoro di Log Analytics. L'esperienza diventa più interessante raccogliendo una maggiore quantità di dati dal sistema, quindi si consiglia di lasciare in esecuzione il generatore di carico per un po' di tempo.


## <a name="use-log-analytics-and-the-sql-analytics-solution-to-monitor-pools-and-databases"></a>Usare Log Analytics e la soluzione Analisi SQL per monitorare i pool e i database


Per questo esercizio, aprire Log Analytics e il portale OMS per esaminare i dati di telemetria raccolti per i database e i pool.

1. Passare al [portale di Azure](https://portal.azure.com) e aprire Log Analytics facendo clic su Altri servizi e cercando Log Analytics:

   ![aprire log analytics](media/saas-dbpertenant-log-analytics/log-analytics-open.png)

1. Selezionare l'area di lavoro denominata *wtploganalytics-&lt;UTENTE&gt;*.

1. Selezionare **Panoramica** per aprire la soluzione Log Analytics nel portale di Azure.
   ![overview-link](media/saas-dbpertenant-log-analytics/click-overview.png)

    > [!IMPORTANT]
    > Attendere perché potrebbe essere necessario qualche minuto per attivare la soluzione.

1. Fare clic sul riquadro Analisi SQL di Azure per aprirlo.

    ![panoramica](media/saas-dbpertenant-log-analytics/overview.png)

    ![analisi](media/saas-dbpertenant-log-analytics/analytics.png)

1. La visualizzazione nel pannello della soluzione scorre lateralmente ed è disponibile una barra di scorrimento apposita nella parte inferiore (aggiornare il pannello se necessario).

1. Esplorare le diverse visualizzazioni, fare clic su di esse o sulle singole risorse per aprire una finestra di esplorazione di drill-down, in cui è possibile usare il dispositivo di scorrimento del tempo in alto a sinistra o fare clic su una barra verticale per concentrarsi su un intervallo di tempo più ristretto. Con questa visualizzazione è possibile selezionare singoli database o pool per concentrarsi su risorse specifiche:

    ![grafico](media/saas-dbpertenant-log-analytics/chart.png)

1. Tornando al pannello della soluzione, se si scorre fino all'estrema destra verranno visualizzate alcune query salvate su cui è possibile fare clic per aprirle ed esplorarle. È possibile sperimentare modificandole e salvare eventuali query interessanti prodotte, in modo da poterle riaprire e usarle con altre risorse.

1. Tornare al pannello dell'area di lavoro di Log Analytics e selezionare il portale OMS per aprire la soluzione in questo portale.

    ![oms](media/saas-dbpertenant-log-analytics/oms.png)

1. Nel portale OMS è possibile configurare gli avvisi. Fare clic nella parte relativa agli avvisi della visualizzazione DTU dei database.

1. Nella visualizzazione Ricerca log che viene aperta si vedrà un grafico a barre delle metriche rappresentate.

    ![ricerca log](media/saas-dbpertenant-log-analytics/log-search.png)

1. Se fa clic su Avviso sulla barra degli strumenti verrà visualizzata la configurazione dell'avviso ed è possibile modificarla.

    ![aggiungi regola di avviso](media/saas-dbpertenant-log-analytics/add-alert.png)

Le funzionalità di monitoraggio e avviso in Log Analytics e in OMS si basano sull'esecuzione di query sui dati nell'area di lavoro, diversamente dagli avvisi per ogni pannello di risorse, specifici per le risorse. È quindi possibile definire un avviso per monitorare tutti i database, ad esempio, invece di definirne uno per ogni database oppure scrivere un avviso che usa una query composita su più tipi di risorsa. Le query sono limitate solo dai dati disponibili nell'area di lavoro.

Gli addebiti relativi a Log Analytics per database SQL sono basati sul volume di dati nell'area di lavoro. In questa esercitazione viene creata un'area di lavoro gratuita, limitata a 500 MB al giorno. Una volta raggiunto tale limite, non vengono aggiunti altri dati all'area di lavoro.


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Installare e configurare Log Analytics (OMS)
> * Usare Log Analytics per monitorare i pool e i database

[Esercitazione sull'analisi dei tenant](saas-dbpertenant-log-analytics.md)

## <a name="additional-resources"></a>Risorse aggiuntive

* [Altre esercitazioni basate sulla distribuzione iniziale dell'applicazione del database per tenant SaaS Wingtip Tickets](saas-dbpertenant-wingtip-app-overview.md#sql-database-wingtip-saas-tutorials)
* [Log Analytics di Azure](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
