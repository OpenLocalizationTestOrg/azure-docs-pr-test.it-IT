---
title: soluzione Analitica SQL in Log Analitica aaaAzure | Documenti Microsoft
description: Hello soluzione Analitica SQL Azure consente di gestire i database SQL di Azure.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Monitorare un database SQL di Azure usando Azure SQL Analytics (anteprima) in Log Analytics

![Simbolo di Analisi SQL di Azure](./media/log-analytics-azure-sql/azure-sql-symbol.png)

Hello soluzione Analitica SQL Azure in Azure Log Analitica raccoglie e visualizza le metriche delle prestazioni di SQL Azure importanti. Utilizzando le metriche di hello raccolti con soluzione hello, è possibile creare avvisi e le regole di monitoraggio personalizzate. È anche possibile monitorare il database SQL di Azure e le metriche dei pool elastici in più sottoscrizioni e pool elastici di Azure e visualizzarli. soluzione Hello consente inoltre di problemi di tooidentify a ogni livello dello stack applicazione.  Usa [metriche di diagnostica Azure](log-analytics-azure-storage.md) insieme Log Analitica Visualizza i dati di toopresent su tutti i database SQL di Azure e i pool elastici in un'area di lavoro Log Analitica.

Attualmente, questa soluzione di anteprima supporta backup too150, 000 i database di SQL Azure e 5.000 pool elastico SQL per ogni area di lavoro.

Hello soluzione Analitica SQL Azure, come altri disponibili per i Log Analitica, consente di monitorare e ricevere notifiche sull'integrità hello di risorse di Azure, in questo caso, il Database SQL di Azure. Database SQL di Microsoft Azure è un servizio di database relazionale scalabile che offre familiarità tooapplications di funzionalità simile a SQL Server in esecuzione in hello cloud di Azure. Log Analitica consente toocollect, correlare e visualizzare i dati strutturati.

## <a name="connected-sources"></a>Origini connesse

Hello soluzione Analitica SQL Azure non usa gli agenti tooconnect toohello servizio Analitica di Log.

Hello nella tabella seguente descrive hello connesso origini supportate da questa soluzione.

| Origine connessa | Supporto | Descrizione |
| --- | --- | --- |
| [Agenti di Windows](log-analytics-windows-agents.md) | No | Diretta degli agenti di Windows non vengono utilizzati dalla soluzione hello. |
| [Agenti Linux](log-analytics-linux-agents.md) | No | Gli agenti Linux diretti non vengono utilizzati dalla soluzione hello. |
| [Gruppo di gestione SCOM](log-analytics-om-agents.md) | No | Una connessione diretta da hello SCOM agente tooLog Analitica non è utilizzata dalla soluzione hello. |
| [Account di archiviazione di Azure](log-analytics-azure-storage.md) | No | Log Analitica leggere hello dati da un account di archiviazione. |
| [Diagnostica di Azure](log-analytics-azure-storage.md) | Sì | Dati di metrica Azure vengono inviati tooLog Analitica direttamente da Azure. |

## <a name="prerequisites"></a>Prerequisiti

- Una sottoscrizione di Azure. Se non si ha una sottoscrizione, è possibile crearne una [gratuitamente](https://azure.microsoft.com/free/).
- Un'area di lavoro di Log Analytics. È possibile usarne una esistente o [crearne una nuova](log-analytics-get-started.md) prima di iniziare a usare questa soluzione.
- Abilitare la diagnostica di Azure per i database di SQL Azure e i pool elastici e [configurarli toosend loro tooLog dati Analitica](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Configurazione

Eseguire hello seguendo i passaggi tooadd hello Azure SQL Analitica soluzione tooyour dell'area di lavoro.

1. Aggiungere hello Azure SQL Analitica soluzione tooyour area di lavoro da [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).
2. Nel portale di Azure hello, fare clic su **New** (hello simbolo +), quindi hello seleziona nell'elenco di risorse, **monitoraggio + gestione**.  
    ![Monitoraggio e gestione](./media/log-analytics-azure-sql/monitoring-management.png)
3. In hello **monitoraggio + gestione** fare clic su elenco **tutti**.
4. In hello **consigliato** elenco, fare clic su **più** e quindi nell'elenco nuovo hello individuare **Analitica di SQL Azure (anteprima)** e selezionarlo.  
    ![Soluzione Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. In hello **Analitica di SQL Azure (anteprima)** pannello, fare clic su **crea**.  
    ![Creare](./media/log-analytics-azure-sql/portal-create.png)
6. In hello **Crea nuova soluzione** blade, dell'area di lavoro selezionare hello che desidera tooadd hello soluzione tooand, quindi fare clic su **crea**.  
    ![aggiungere tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure più sottoscrizioni di Azure

toosupport più sottoscrizioni, usare uno script di PowerShell hello da [registrazione metriche di risorsa abilitare Azure tramite PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/). Fornire l'ID risorsa dell'area di lavoro di hello come parametro durante l'esecuzione di dati di diagnostica di hello script toosend dalle risorse nell'area di lavoro tooa una sottoscrizione di Azure in un'altra sottoscrizione di Azure.

**Esempio**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello

Quando si aggiunge l'area di lavoro tooyour soluzione hello, hello riquadro Analitica SQL Azure viene aggiunto tooyour dell'area di lavoro e viene visualizzato nella panoramica. riquadro Hello Mostra il numero di hello di database SQL di Azure e i pool elastici SQL di Azure connessa a soluzione hello.

![Riquadro Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Visualizzazione dei dati di Analisi SQL di Azure

Fare clic su hello **Analitica SQL Azure** riquadro tooopen hello Azure SQL Analitica dashboard. dashboard Hello include pannelli hello definiti di seguito. Ogni pannello elenca le risorse too15 (sottoscrizione server, il pool elastico e database). Fare clic su uno qualsiasi dei dashboard di hello risorse tooopen hello per tale risorsa specifica. Elastico Pool o il Database contiene grafici hello con le metriche per una risorsa selezionata. Fare clic su una finestra di dialogo ricerca nei Log di hello tooopen di grafico.

| Pannello | Descrizione |
|---|---|
| Sottoscrizioni | Elenco delle sottoscrizioni con numero di server, pool e database connessi. |
| Server | Elenco dei server con numero di pool e database connessi. |
| Pool elastici | Elenco di pool elastico connesso con hello osservato di eDTU e GB massimo di periodo. |
|Database | Elenco di database connessi con DTU e GB massimo osservati hello periodo.|


### <a name="analyze-data-and-create-alerts"></a>Analizzare i dati e creare avvisi

È possibile creare facilmente avvisi con dati hello provenienti dalle risorse di Database SQL di Azure. Di seguito sono riportati due query utili di [ricerca nei log](log-analytics-log-searches.md) che è possibile usare per gli avvisi:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*Elevato utilizzo di DTU nel database SQL di Azure*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*Elevato utilizzo di DTU nel pool elastico del database SQL di Azure*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

È possibile utilizzare questi tooalert le query basate su avviso sulle soglie specifiche per i Database di SQL Azure e il pool elastico. un avviso per l'area di lavoro OMS tooconfigure:

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>tooconfigure un avviso per l'area di lavoro

1. Passare toohello [portale OMS](http://mms.microsoft.com/) ed eseguire l'accesso.
2. Aprire l'area di lavoro di hello che è stato configurato per la soluzione hello.
3. Nella pagina di panoramica hello, fare clic su hello **Analitica di SQL Azure (anteprima)** riquadro.
4. Eseguire una delle query di esempio hello.
5. In Ricerca log fare clic su **Avviso**.  
![Creare un avviso nella ricerca](./media/log-analytics-azure-sql/create-alert01.png)
6. In hello **Aggiungi regola di avviso** pagina, configurare le proprietà appropriate hello e hello soglie specifiche che si desidera e quindi fare clic su **salvare**.  
![Aggiungere una regola di avviso](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Agire sui dati di Analisi SQL di Azure

Ad esempio, una delle query più utili di hello che è possibile eseguire è l'utilizzo di DTU toocompare hello per tutti i pool elastico di SQL Azure per tutte le sottoscrizioni di Azure. Unità di velocità effettiva database (DTU) fornisce un modo toodescribe hello capacità relativa di un livello di prestazioni di database Basic, Standard e Premium e pool. Le unità DTU sono basate su una misura combinata di CPU, memoria, operazioni di lettura e di scrittura. Aumentare delle Dtu hello potenza offerto da Aumenta livello di prestazioni hello. Un livello delle prestazioni con 5 DTU, ad esempio, ha cinque volte la potenza di un livello delle prestazioni con 1 DTU. Quota massima di DTU si applica il pool di server ed elastica tooeach.

Eseguendo hello seguenti query di ricerca di Log, è possibile stabilire facilmente se si sottoutilizzano o oltre che utilizzano il pool elastico SQL Azure.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

Nell'esempio seguente di hello, si noterà che un pool elastico ha un utilizzo elevato prossimo al 100% DTU mentre altri hanno un utilizzo minimo. È possibile esaminare ulteriori modifiche recenti potenziali tootroubleshoot nel proprio ambiente usando i log attività di Azure.

![Risultati della ricerca log: utilizzo elevato](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>Vedere anche

- Utilizzare [ricerche nei Log](log-analytics-log-searches.md) nel Log Analitica tooview in dettaglio i dati di SQL Azure.
- [Creare dashboard personalizzati](log-analytics-dashboards.md) che mostrino i dati per Azure SQL.
- [Creare avvisi](log-analytics-alerts.md) quando si verificano eventi specifici relativi ad Azure SQL.
