---
title: Soluzione Azure SQL Analytics in Log Analytics | Microsoft Docs
description: La soluzione Azure SQL Analytics consente di gestire i database SQL di Azure.
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
ms.openlocfilehash: cab45cc6dd621eb4a95ef5f1842ec38c25e980b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Monitorare un database SQL di Azure usando Azure SQL Analytics (anteprima) in Log Analytics

![Simbolo di Analisi SQL di Azure](./media/log-analytics-azure-sql/azure-sql-symbol.png)

La soluzione Analisi SQL di Azure in Azure Log Analytics raccoglie e visualizza importanti metriche sulle prestazioni di SQL Azure. Usando le metriche raccolte con la soluzione, è possibile creare regole e avvisi di monitoraggio personalizzati. È anche possibile monitorare il database SQL di Azure e le metriche dei pool elastici in più sottoscrizioni e pool elastici di Azure e visualizzarli. La soluzione consente anche di identificare i problemi a ogni livello dello stack di applicazioni.  Usa le [metriche di Diagnostica di Azure](log-analytics-azure-storage.md) con le viste di Log Analytics per presentare i dati su tutti i database SQL di Azure e i pool elastici in un'unica area di lavoro di Log Analytics.

Questa soluzione in anteprima supporta attualmente fino a 150.000 database SQL di Azure e 5.000 pool elastici SQL per area di lavoro.

La soluzione Analisi SQL di Azure, come altre disponibili per Log Analytics, consente di monitorare e ricevere notifiche sull'integrità delle risorse di Azure, in questo caso il database SQL di Azure. Il database SQL di Microsoft Azure è un servizio di database relazionale scalabile che fornisce le comuni funzionalità di tipo SQL Server alle applicazioni in esecuzione nel cloud di Azure. Log Analytics consente di raccogliere, correlare e visualizzare dati strutturati e non strutturati.

## <a name="connected-sources"></a>Origini connesse

La soluzione Analisi SQL di Azure non usa agenti per connettersi al servizio Log Analytics.

La tabella seguente descrive le origini connesse che sono supportate da questa soluzione.

| Origine connessa | Supporto | Descrizione |
| --- | --- | --- |
| [Agenti di Windows](log-analytics-windows-agents.md) | No | Gli agenti Windows diretti non vengono usati dalla soluzione. |
| [Agenti Linux](log-analytics-linux-agents.md) | No | Gli agenti Linux diretti non vengono usati dalla soluzione. |
| [Gruppo di gestione SCOM](log-analytics-om-agents.md) | No | Una connessione diretta dall'agente SCOM a Log Analytics non viene usata dalla soluzione. |
| [Account di archiviazione di Azure](log-analytics-azure-storage.md) | No | Log Analytics non legge i dati da un account di archiviazione. |
| [Diagnostica di Azure](log-analytics-azure-storage.md) | Sì | I dati relativi alle metriche di Azure vengono inviati a Log Analytics direttamente da Azure. |

## <a name="prerequisites"></a>Prerequisiti

- Una sottoscrizione di Azure. Se non si ha una sottoscrizione, è possibile crearne una [gratuitamente](https://azure.microsoft.com/free/).
- Un'area di lavoro di Log Analytics. È possibile usarne una esistente o [crearne una nuova](log-analytics-get-started.md) prima di iniziare a usare questa soluzione.
- Abilitare Diagnostica di Azure per i database SQL di Azure SQL e i pool elastici e [configurarli per l'invio dei dati a Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Configurazione

Eseguire questa procedura per aggiungere la soluzione Analisi SQL di Azure all'area di lavoro.

1. Aggiungere la soluzione Azure SQL Analytics da [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) o seguendo la procedura illustrata in [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md).
2. Nel portale di Azure fare clic su **Nuovo** (il simbolo +), quindi nell'elenco di risorse selezionare **Monitoraggio e gestione**.  
    ![Monitoraggio e gestione](./media/log-analytics-azure-sql/monitoring-management.png)
3. Nell'elenco **Monitoraggio e gestione** fare clic su **Visualizza tutto**.
4. Nell'elenco **Consigliati** fare clic su **Altro** e quindi nel nuovo elenco trovare **Azure SQL Analytics (anteprima)** e selezionarlo.  
    ![Soluzione Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. Nel pannello **Azure SQL Analytics (anteprima)** fare clic su **Crea**.  
    ![Creare](./media/log-analytics-azure-sql/portal-create.png)
6. Nel pannello **Crea nuova soluzione** selezionare l'area di lavoro che si vuole aggiungere alla soluzione e quindi fare clic su **Crea**.  
    ![Aggiunta all'area di lavoro](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="to-configure-multiple-azure-subscriptions"></a>Per configurare più sottoscrizioni di Azure

Per supportare più sottoscrizioni, usare lo script di PowerShell contenuto in [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/) (Abilitare la registrazione delle metriche sulle risorse di Azure usando PowerShell). Specificare l'ID risorsa dell'area di lavoro come parametro quando si esegue lo script per inviare i dati di diagnostica dalle risorse in una sottoscrizione di Azure a un'area di lavoro in un'altra sottoscrizione di Azure.

**Esempio**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-the-solution"></a>Uso della soluzione

Quando si aggiunge la soluzione all'area di lavoro, il riquadro Azure SQL Analytics viene aggiunto all'area di lavoro e visualizzato in Panoramica. Il riquadro mostra il numero di database SQL di Azure e di pool elastici SQL a cui la soluzione è connessa.

![Riquadro Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Visualizzazione dei dati di Analisi SQL di Azure

Fare clic sul riquadro **Analisi SQL di Azure** per aprire il dashboard Analisi SQL di Azure. Il dashboard include i pannelli definiti di seguito. Ogni pannello elenca un massimo di 15 risorse (sottoscrizione, server, pool elastico e database). Fare clic su una delle risorse per aprire il dashboard per una risorsa specifica. Pool elastico o Database contengono i grafici con le metriche per una risorsa selezionata. Fare clic su un grafico per aprire la finestra di dialogo Ricerca log.

| Pannello | Descrizione |
|---|---|
| Sottoscrizioni | Elenco delle sottoscrizioni con numero di server, pool e database connessi. |
| Server | Elenco dei server con numero di pool e database connessi. |
| Pool elastici | Elenco di pool elastici connessi con numero massimo di GB ed eDTU nel periodo osservato. |
|Database | Elenco di database connessi con numero massimo di GB e DTU nel periodo osservato.|


### <a name="analyze-data-and-create-alerts"></a>Analizzare i dati e creare avvisi

È possibile creare facilmente avvisi con i dati provenienti dalle risorse del database SQL di Azure. Di seguito sono riportati due query utili di [ricerca nei log](log-analytics-log-searches.md) che è possibile usare per gli avvisi:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*Elevato utilizzo di DTU nel database SQL di Azure*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*Elevato utilizzo di DTU nel pool elastico del database SQL di Azure*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

È possibile usare queste query basate su avvisi per creare avvisi per soglie specifiche sia per i database SQL di Azure che per i pool elastici. Per configurare un avviso per l'area di lavoro OMS:

#### <a name="to-configure-an-alert-for-your-workspace"></a>Per configurare un avviso per l'area di lavoro

1. Aprire il [portale di OMS](http://mms.microsoft.com/) e accedere.
2. Aprire l'area di lavoro configurata per la soluzione.
3. Nella pagina Panoramica fare clic sul riquadro **Azure SQL Analytics (anteprima)**.
4. Eseguire una delle query di esempio.
5. In Ricerca log fare clic su **Avviso**.  
![Creare un avviso nella ricerca](./media/log-analytics-azure-sql/create-alert01.png)
6. Nella pagina **Aggiungi regola di avviso** configurare le proprietà necessarie e le soglie specifiche desiderate e quindi fare clic su **Salva**.  
![Aggiungere una regola di avviso](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Agire sui dati di Analisi SQL di Azure

Ad esempio, una delle query più utili che è possibile eseguire è confrontare l'utilizzo DTU per tutti i pool elastici SQL di Azure in tutte le sottoscrizioni di Azure. L'unità elaborata di database (DTU, Database Throughput Unit) consente di descrivere la capacità relativa di un livello delle prestazioni dei database e dei pool Basic, Standard e Premium. Le unità DTU sono basate su una misura combinata di CPU, memoria, operazioni di lettura e di scrittura. Quando le unità DTU aumentano, aumenta anche la potenza offerta dal livello delle prestazioni. Un livello delle prestazioni con 5 DTU, ad esempio, ha cinque volte la potenza di un livello delle prestazioni con 1 DTU. A ogni server e pool elastico viene applicata una quota massima di DTU.

Eseguendo la query di ricerca log seguente, è possibile capire facilmente se si sta sottoutilizzando o sovrautilizzando i pool elastici SQL Azure.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Se l'area di lavoro è stata aggiornata al [nuovo linguaggio di query di Log Analytics](log-analytics-log-search-upgrade.md), la query precedente verrà sostituita dalla seguente.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

Nell'esempio seguente è possibile osservare che un pool elastico ha un utilizzo elevato, prossimo al 100% dell'unità DTU, mentre gli altri hanno un utilizzo molto basso. È possibile eseguire un'indagine più approfondita per risolvere i problemi delle potenziali modifiche recenti dell'ambiente usando i log attività di Azure.

![Risultati della ricerca log: utilizzo elevato](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>Vedere anche

- Usare le [ricerche log](log-analytics-log-searches.md) in Log Analytics per visualizzare i dati dettagliati per Azure SQL.
- [Creare dashboard personalizzati](log-analytics-dashboards.md) che mostrino i dati per Azure SQL.
- [Creare avvisi](log-analytics-alerts.md) quando si verificano eventi specifici relativi ad Azure SQL.
