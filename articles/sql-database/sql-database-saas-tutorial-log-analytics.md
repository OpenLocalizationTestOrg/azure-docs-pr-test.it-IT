---
title: aaaUse Log Analitica con un'applicazione multi-tenant di Database SQL | Documenti Microsoft
description: Configurare e usare Log Analitica (OMS) con app SaaS Wingtip esempio di hello Database SQL di Azure
keywords: esercitazione database SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>Configurare e usare Log Analitica (OMS) con app SaaS Wingtip hello

Questa esercitazione illustra come configurare e usare *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* per il monitoraggio di database e pool elastici. È basato su hello [esercitazione di gestione e monitoraggio delle prestazioni](sql-database-saas-tutorial-performance-monitoring.md)e viene illustrato come toouse *Log Analitica* tooaugment hello monitoraggio e avviso fornito nel portale di Azure hello. Log Analytics è una soluzione particolarmente adatta alla gestione del monitoraggio e degli avvisi su larga scala, perché supporta centinaia di pool e centinaia di migliaia di database. Si tratta inoltre di una soluzione di monitoraggio singola che supporta l'integrazione del monitoraggio di applicazioni e servizi di Azure diversi tra più sottoscrizioni di Azure.

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Installare e configurare Log Analytics (OMS)
> * Utilizzo di database e i pool di Log Analitica toomonitor

toocomplete completamento di questa esercitazione, assicurarsi che i hello seguenti prerequisiti:

* app SaaS Wingtip Hello viene distribuita. toodeploy in meno di cinque minuti, vedere [Distribuisci ed esplorare l'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell è installato. Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

Vedere hello [esercitazione di gestione e monitoraggio delle prestazioni](sql-database-saas-tutorial-performance-monitoring.md) per una discussione su scenari SaaS hello e modelli e gli effetti di requisiti hello in una soluzione di monitoraggio.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Monitoraggio e gestione delle prestazioni con Log Analytics (OMS)

Per il database SQL, il monitoraggio e gli avvisi sono disponibili per database e pool. Questo incorporati di monitoraggio e avviso sono specifico di risorsa ed è utile per un numero limitato di risorse, ma sono meno adatto toomonitoring installazioni di grandi dimensioni o per fornire una visualizzazione unificata tra le sottoscrizioni e le diverse risorse.

Per scenari con volumi elevati, è possibile usare Log Analytics. Questo è un servizio di Azure separato che offre analitica rispetto generato log di diagnostica e dati di telemetria raccolti in un'area di lavoro di analitica di log, che è possibile raccogliere dati di telemetria da molti servizi ed essere tooquery utilizzato e impostare gli avvisi. Log Analytics include un linguaggio di query predefinito e strumenti per la visualizzazione dei dati che consentono l'analisi e la visualizzazione di dati operativi. Ciao soluzione Analitica SQL vengono forniti diversi pool elastico predefiniti e monitoraggio e avviso viste e query di database e consente di aggiungere le query ad hoc e salvare queste esigenze. OMS offre anche una finestra di progettazione viste personalizzata.

Soluzioni di aree di lavoro e analitica Analitica log possono essere aperto in hello portale di Azure e in OMS. Hello portale di Azure è il punto di accesso più recente hello ma potrebbe trovarsi dietro il portale di OMS hello in alcune aree.

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>Avviare hello carico generatore toocreate dati tooanalyze

1. Aprire **Demo PerformanceMonitoringAndManagement.ps1** in hello **PowerShell ISE**. Mantenere questo script aperta quando si considera toorun alcuni degli scenari di generazione carico hello durante questa esercitazione.
1. Se si dispone di meno di cinque tenant, eseguire il provisioning di un batch di tenant tooprovide un contesto di monitoraggio più interessante:
   1. Impostare **$DemoScenario = 1,** **Effettuare il provisioning di un batch di tenant**
   1. Premere **F5** script hello toorun.

1. Impostare**$DemoScenario** = 2, **Generare un carico di intensità normale (circa 40 DTU)**.
1. Premere **F5** script hello toorun.

## <a name="get-hello-wingtip-application-scripts"></a>Ottenere script per l'applicazione hello Wingtip

Hello Wingtip ticket script e codice sorgente dell'applicazione sono disponibili in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repository github. File di script si trovano in hello [cartella Learning moduli](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules). Scaricare hello **moduli Learning** cartella tooyour computer locale, mantenendo la struttura di cartelle.

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>Installazione e configurazione di Log Analitica e hello soluzione Analitica SQL Azure

Log Analitica è un servizio distinto che deve toobe configurato. Log Analytics raccoglie dati di log, dati di telemetria e metriche in un'area di lavoro di Log Analytics. Un'area di lavoro è una risorsa, analogamente ad altre risorse in Azure, e deve essere creata. Durante l'area di lavoro hello non deve necessariamente toobe creato in hello stesso gruppo di risorse come applicazioni hello monitoraggio, in questo modo hello più appropriate. Nel caso di hello di app SaaS Wingtip hello, in questo modo hello dell'area di lavoro toobe facilmente eliminati con un'applicazione hello semplicemente eliminando il gruppo di risorse hello.

1. Apri... \\Moduli learning\\gestione e monitoraggio delle prestazioni\\Log Analitica\\*Demo LogAnalytics.ps1* in hello **PowerShell ISE**.
1. Premere **F5** script hello toorun.

A questo punto è necessario essere in grado di aprire Analitica di Log in portale di Azure hello (o il portale di OMS hello). Richiederà alcuni minuti per toobe di telemetria raccolti nell'area di lavoro Log Analitica hello e toobecome visibile. sarà Hello più che lasciare sistema hello di raccolta dati hello esperienza hello più interessante. Ora è utile toograb una bevanda - sufficiente Assicurarsi che il generatore di carico hello è ancora in esecuzione.


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>Utilizzare Log Analitica e hello database e i pool di toomonitor soluzione Analitica SQL


In questo esercizio, aprire Log Analitica e hello toolook portale di OMS in dati di telemetria hello raccolte per pool e i database hello.

1. Sfoglia toohello [portale di Azure](https://portal.azure.com) aprire Analitica Log facendo clic su più servizi, quindi cercare Analitica Log:

   ![aprire log analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. Selezionare l'area di lavoro hello denominato *wtploganalytics -&lt;utente&gt;*.

1. Selezionare **Panoramica** tooopen hello soluzione Analitica di Log in hello portale di Azure.
   ![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **IMPORTANTE**: potrebbe richiedere un paio di minuti prima che la soluzione hello è attiva. attivare la soluzione.

1. Fare clic su hello tooopen riquadro Analitica SQL Azure.

    ![panoramica](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![analisi](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. Hello visualizzazione hello soluzione blade scorre con rotazione laterale, con il proprio barra di scorrimento nella parte inferiore di hello (aggiornamento hello pannello se necessario).

1. Esplorare hello diverse visualizzazioni, fare clic su di essi o su singole risorse tooopen Esplora un drill-down in cui è possibile utilizzare hello-dispositivo di scorrimento tempo in hello in alto a sinistra oppure fare clic su un oggetto verticale barra toofocus in un intervallo di tempo più ristretto. Con questa visualizzazione, è possibile selezionare singoli toofocus database o i pool di risorse specifico:

    ![grafico](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. Nel Pannello di soluzione hello, se si scorre toohello estrema destra verrà visualizzato alcune query salvata che è possibile fare clic su tooopen ed esplorare. È possibile sperimentare modificandole e salvare eventuali query interessanti prodotte, in modo da poterle riaprire e usare con altre risorse.

1. Nel pannello dell'area di lavoro di hello Analitica di Log, selezionare non esiste soluzione di hello tooopen portale di OMS.

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. Nel portale OMS hello, è possibile configurare gli avvisi. Fare clic sulla parte di avviso hello di visualizzazione DTU del database hello.

1. Nella ricerca nei Log hello che appare si verrà visualizzato un grafico a barre di metriche di hello rappresentate.

    ![ricerca log](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. Se si fa clic su avviso nella barra degli strumenti hello sarà in grado di toosee configurazione degli avvisi hello e possibile modificarlo.

    ![aggiungi regola di avviso](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

Hello di monitoraggio e avviso nel Log Analitica e OMS è basato sulle query sui dati hello nell'area di lavoro hello, a differenza di hello alla visualizzazione di avvisi ogni pannello della risorsa, ovvero specifici delle risorse. È quindi possibile definire un avviso per monitorare tutti i database, ad esempio, invece di definirne uno per ogni database oppure scrivere un avviso che usa una query composita su più tipi di risorsa. Le query sono limitate solo dalle dati hello disponibili nell'area di lavoro hello.

Analitica di log per il Database SQL verrà addebitata in base hello volume di dati nell'area di lavoro hello. In questa esercitazione è creata un'area di lavoro disponibile, ovvero too500MB limitato al giorno. Una volta raggiunto tale limite dati non viene aggiunta toohello dell'area di lavoro.


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Installare e configurare Log Analytics (OMS)
> * Utilizzo di database e i pool di Log Analitica toomonitor

[Esercitazione sull'analisi dei tenant](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>Risorse aggiuntive

* [Altre esercitazioni che si basano su una distribuzione di applicazioni SaaS Wingtip iniziale hello](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Log Analytics di Azure](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
