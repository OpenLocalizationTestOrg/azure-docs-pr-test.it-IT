---
title: esegue la ricerca in OMS Log Analitica aaaLog | Documenti Microsoft
description: "È necessario un tooretrieve di ricerca di log di tutti i dati dal Log Analitica.  Questo articolo descrive come nuovo log ricerche vengono utilizzate nel Log Analitica e vengono forniti i concetti che è necessario toounderstand prima di crearne uno nuovo."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Informazioni sulle ricerche log in Log Analytics

> [!NOTE]
> Questo articolo descrive ricerche nei log in Analitica di Log di Azure utilizzando il nuovo linguaggio di query hello.  È possibile acquisire familiarità con il nuovo linguaggio di hello e ottenere hello procedure tooupgrade l'area di lavoro in [aggiornare la ricerca di log di Azure Log Analitica dell'area di lavoro toonew](log-analytics-log-search-upgrade.md).  
>
> Se l'area di lavoro non è stato aggiornato toohello nuovo linguaggio di query, è consigliabile consultare troppo[trovare i dati tramite ricerche nei log nel Log Analitica](log-analytics-log-searches.md).

È necessario un tooretrieve di ricerca di log di tutti i dati dal Log Analitica.  Se si sta analizzando i dati nel portale di hello, toobe una regola di avviso di configurazione una notifica di una determinata condizione, o il recupero dei dati utilizzando hello Log Analitica API, si utilizzerà un registro ricerca toospecify hello dati.  Questo articolo descrive come vengono usate le ricerche log in Log Analytics e illustra i concetti con cui occorre avere familiarità prima di crearne una. Vedere hello [passaggi successivi](#next-steps) sezione per informazioni dettagliate sulla creazione e modifica ricerche nei log e per i riferimenti nel linguaggio di query hello.

## <a name="where-log-searches-are-used"></a>Possibili usi delle ricerche log

Hello modi diversi che si utilizzeranno ricerche nei log in Analitica Log includono hello informazioni seguenti:

- **Portali.** È possibile eseguire un'analisi interattiva dei dati nel repository di hello con hello [portale ricerca nei Log](log-analytics-log-search-log-search-portal.md) o hello [portale avanzate Analitica](https://go.microsoft.com/fwlink/?linkid=856587).  In questo modo si tooedit le query e analizzare i risultati di hello in una vasta gamma di formati e le visualizzazioni.  La maggior parte delle query create verrà avviato in uno dei portali hello e quindi copiate dopo aver verificato che funziona come previsto.
- **Regole di avviso.** Le [regole di avviso](log-analytics-alerts.md) consentono di identificare in modo proattivo i problemi dai dati nell'area di lavoro.  Ogni regola di avviso è basata su una ricerca log che viene eseguita automaticamente a intervalli regolari.  risultati di Hello sono toodetermine ispezionata se è necessario creare un avviso.
- **Visualizzazioni.**  È possibile creare visualizzazioni di dati toobe inclusi nel dashboard di utente con [Visualizza finestra di progettazione](log-analytics-view-designer.md).  Ricerche nei log forniscono dati hello utilizzati da [riquadri](log-analytics-view-designer-tiles.md) e [parti visualizzazione](log-analytics-view-designer-parts.md) di ogni visualizzazione.  È possibile scorrere verso il basso dalle parti di visualizzazione hello un'ulteriore analisi portale tooperform ricerca dei registri dati hello.
- **Esportazione.**  Quando si esportano dati da hello Analitica di Log dell'area di lavoro tooExcel o [Power BI](log-analytics-powerbi.md), si crea un tooexport di dati di registro ricerca toodefine hello.
- **PowerShell.** È possibile eseguire uno script di PowerShell da una riga di comando o un runbook di automazione di Azure che utilizza [Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve dati dal Log Analitica.  Questo cmdlet richiede un tooretrieve di dati di query toodetermine hello.
- **API di Log Analytics.**  Hello [API di ricerca di log Log Analitica](log-analytics-log-search-api.md) consente a qualsiasi client dell'API REST tooretrieve dati dall'area di lavoro hello.  richiesta di API Hello include una query che viene eseguita su un Log Analitica toodetermine hello dati tooretrieve.

![Ricerche log](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Organizzazione dei dati di Log Analytics
Quando si compila una query, è necessario innanzitutto determinare quali tabelle presentano dati hello che si sta cercando. Ogni [origine dati](log-analytics-data-sources.md) e [soluzione](../operations-management-suite/operations-management-suite-solutions.md) archivia i dati in tabelle dedicate nell'area di lavoro Log Analitica hello.  Documentazione per ogni origine dati e la soluzione include hello nome del tipo di dati hello che crea e una descrizione di ciascuna delle relative proprietà.     Molte query saranno necessari solo i dati dalle tabelle di un singolo, ma altri utenti possono utilizzare un'ampia gamma di opzioni tooinclude dati da più tabelle.

![Tabelle](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>Scrittura di una query
Hello nucleo del log delle ricerche nel Log Analitica è [un linguaggio di query completo](https://docs.loganalytics.io/) che consente di recuperare e analizzare dati dal repository hello in diversi modi.  Si tratta dello stesso linguaggio di query usato per [Application Insights](../application-insights/app-insights-analytics.md).  Apprendere come toowrite una query è critica toocreating ricerche nei log nel Log Analitica.  In genere si inizierà con query di base e quindi lo stato di avanzamento toouse più funzioni avanzate come esigenze diventano più complessi.

struttura di base di una query Hello è una tabella di origine seguita da una serie di operatori separati da un carattere barra verticale `|`.  È possibile concatenare i dati di più operatori toorefine hello ed eseguire funzioni avanzate.

Si supponga, ad esempio, che si desiderava toofind hello prime dieci computer con hello la maggior parte degli eventi di errore su hello giorno precedente.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

O forse si desidera toofind computer che non hanno avuto un heartbeat nell'ultimo giorno hello.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

Su un grafico a linee con utilizzo del processore hello per ogni computer dall'ultima settimana?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

È possibile visualizzare gli esempi rapidi che indipendentemente dal tipo di hello di dati che si sta lavorando, hello di struttura di query hello è simile.  È possibile suddividerla in passaggi distinti in cui i dati risultanti di hello da un comando viene inviati tramite comando successivo di hello pipeline toohello.

Per una documentazione completa sul linguaggio di query Azure Log Analitica hello inclusi riferimenti al linguaggio ed esercitazioni, vedere hello [la documentazione del linguaggio di query Azure Log Analitica](https://docs.loganalytics.io/).

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su hello [portali utilizzare toocreate e ricerche nei log di modifica](log-analytics-log-search-portals.md).
- Estrarre un [esercitazione sulla scrittura di query](https://go.microsoft.com/fwlink/?linkid=856078) utilizzando il nuovo linguaggio di query hello.
