---
title: portale di ricerca nei Log aaaUsing hello in Azure Log Analitica | Documenti Microsoft
description: In questo articolo include un'esercitazione che illustra come toocreate log ricerche e analisi dei dati memorizzati nell'area di lavoro Analitica Log tramite il portale di ricerca nei Log hello.  esercitazione di Hello include eseguire alcune semplici query tooreturn diversi tipi di dati e analizzare i risultati.
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
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>Creare ricerche nei log in Analitica di Log di Azure tramite il portale di ricerca nei Log hello

> [!NOTE]
> Questo articolo descrive il portale di ricerca nei Log hello in Analitica di Log di Azure utilizzando il nuovo linguaggio di query hello.  È possibile acquisire familiarità con il nuovo linguaggio di hello e ottenere hello procedure tooupgrade l'area di lavoro in [aggiornare la ricerca di log di Azure Log Analitica dell'area di lavoro toonew](log-analytics-log-search-upgrade.md).  
>
> Se l'area di lavoro non è stato aggiornato toohello nuovo linguaggio di query, è consigliabile consultare troppo[trovare i dati tramite ricerche nei log nel Log Analitica](log-analytics-log-searches.md) per informazioni sulla versione corrente di hello del portale di ricerca nei Log hello.

In questo articolo include un'esercitazione che illustra come toocreate log ricerche e analisi dei dati memorizzati nell'area di lavoro Analitica Log tramite il portale di ricerca nei Log hello.  esercitazione di Hello include eseguire alcune semplici query tooreturn diversi tipi di dati e analizzare i risultati.  Si concentra sulle funzionalità nel portale di ricerca nei Log hello per modificare la query hello anziché modificarlo direttamente.  Per informazioni dettagliate sulla modifica direttamente la query hello, vedere hello [riferimenti al linguaggio di Query](https://go.microsoft.com/fwlink/?linkid=856079).

vedere toocreate ricerche nel portale di Advanced Analitica hello anziché portale ricerca nei Log di hello [Introduzione al portale Analitica hello](https://go.microsoft.com/fwlink/?linkid=856587).  Entrambi i portali utilizzano hello stessa query language tooaccess hello stessi dati nell'area di lavoro Log Analitica hello.

## <a name="prerequisites"></a>Prerequisiti
In questa esercitazione si presuppone che si disponga già di un'area di lavoro Log Analitica con almeno un'origine connessa che genera i dati per tooanalyze query hello.  

- Se non si dispone di un'area di lavoro, è possibile creare uno disponibile nella procedura hello in [Introduzione a un'area di lavoro Log Analitica](log-analytics-get-started.md).
- Connettere almeno una [dell'agente di Windows](log-analytics-windows-agents.md) o uno [agente Linux](log-analytics-linux-agents.md) toohello dell'area di lavoro.  

## <a name="open-hello-log-search-portal"></a>Portale di hello aprire ricerca dei registri
Avvia aprendo il portale di ricerca nei Log hello.  È possibile accedervi in hello portale di Azure o il portale di OMS hello.

1. Hello aprirlo portale di Azure.
2. Passare tooLog Analitica e selezionare l'area di lavoro.
3. Selezionare **ricerca nei Log** toostay in hello Azure portal o avviare hello portale OMS selezionando **portale OMS** e quindi fare clic sul pulsante ricerca dei registri hello.

![Pulsante di ricerca log](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>Creare una ricerca semplice
tooretrieve modo più rapido Hello toowork alcuni dati con è una query semplice che restituisce tutti i record nella tabella.  Se si dispone di qualsiasi area di tooyour connessi i client Windows o Linux, quindi sarà necessario dati hello di eventi (Windows) o una tabella Syslog (Linux).

Digitare uno hello seguente query nella casella di ricerca hello e fare clic sul pulsante ricerca hello.  

```
Event
```
```
Syslog
```

Vengono restituiti dati nella visualizzazione elenco predefinito di hello ed è possibile visualizzare il numero totale di record sono stati restituiti.

![Query semplice](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

Solo hello prima alcune proprietà di ogni record vengono visualizzate.  Fare clic su **Mostra altre** toodisplay tutte le proprietà per un record specifico.

![Dettagli sui record](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>Impostare l'ambito di hello ora
Ogni record raccolti da Log Analitica con un **TimeGenerated** proprietà contenente hello data e ora in cui è stato creato il record di hello.  Una query nel portale di ricerca nei Log hello restituisce solo i record con un **TimeGenerated** ambito hello ora che viene visualizzato sul lato sinistro di schermata Ciao hello.  

È possibile modificare filtro temporale hello selezionando l'elenco a discesa hello o modificando il dispositivo di scorrimento hello.  dispositivo di scorrimento Hello Visualizza un grafico a barre che mostra i numero di record per ogni segmento di tempo compreso hello relativo hello.  Questo segmento dipenderà dall'intervallo hello.

ambito di tempo predefinito Hello è **1 giorno**.  Modificare questo valore troppo**7 giorni**, e hello il numero totale di record aumenta.

![Intervallo temporale](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>Filtrare i risultati della query hello
In hello lato sinistro dello schermo hello è riquadro filtri hello consente tooadd filtro query toohello senza modificarlo direttamente.  Diverse proprietà di hello record restituiti vengono visualizzate con i relativi dieci valori superiore al numero di record.

Se si lavora con **evento**, selezionare hello casella di controllo accanto troppo**errore** in **EVENTLEVELNAME**.   Se si lavora con **Syslog**, selezionare hello casella di controllo accanto troppo**err** in **SEVERITYLEVEL**.  In questo caso query hello tooone di hello seguente hello toolimit risultati tooerror eventi.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

Aggiungi riquadro filtro toohello di proprietà selezionando **aggiungere toofilters** dal menu di proprietà hello in uno dei record di hello.

![Aggiungere menu toofilter](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

È possibile impostare hello allo stesso filtro selezionando **filtro** dal menu di proprietà hello per un record con valore hello desiderato toofilter.  

È sufficiente hello **filtro** opzione per le proprietà con il relativo nome in blu.  Si tratta di campi *disponibili per la ricerca* che vengono indicizzati per le condizioni di ricerca.  I campi in grigio sono *disponibile per la ricerca di testo libero* campi che dispongono solo delle hello **Mostra riferimenti** opzione.  Questa opzione restituisce i record con il valore specificato in qualsiasi proprietà.

![Menu di filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

È possibile raggruppare i risultati di hello in una singola proprietà selezionando hello **raggruppare** opzione nel menu record hello.  Verrà aggiunta una [riepilogare](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) query tooyour operatore che visualizza i risultati di hello in un grafico.  È possibile raggruppare in più di una proprietà, ma è necessario query hello tooedit direttamente.  Selezionare prova menu record successivo hello prova **Computer** proprietà e selezionare **Group by 'Computer'**.  

![Raggruppare in base alla proprietà Computer](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>Usare i risultati
portale di ricerca nei Log Hello dispone di una serie di funzionalità per l'utilizzo dei risultati di hello di una query.  È possibile ordinare, filtrare e raggruppare dati hello tooanalyze dei risultati senza modificare la query effettiva hello.  I risultati di una query non sono ordinati per impostazione predefinita.

dati hello tooview in forma di tabella che fornisce ulteriori opzioni di filtro e ordinamento, fare clic su **tabella**.  

![Visualizzazione tabella](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

Fare clic sulla freccia di hello da un dettagli hello tooview record per tale record.

![Ordinare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

È possibile ordinare i risultati in base a qualsiasi campo facendo clic sulla relativa intestazione di colonna.

![Ordinare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

Filtrare i risultati di hello su un valore specifico nella colonna hello facendo clic sul pulsante filtro hello e fornendo una condizione di filtro.

![Filtrare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

Raggruppare in una colonna, trascinare la parte superiore toohello di intestazione di colonna dei risultati di hello.  È possibile raggruppare in più campi mediante il trascinamento di più colonne toohello dall'alto.

![Raggruppare i risultati](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>Utilizzare i dati sulle prestazioni
Dati sulle prestazioni per Windows e Linux gli agenti vengono archiviati nell'area di lavoro Log Analitica hello in hello **prestazioni** tabella.  I record sulle prestazioni hanno lo stesso aspetto di qualsiasi altro record ed è possibile scrivere una query semplice che restituisce tutti i record sulle prestazioni esattamente come per gli eventi.

```
Perf
```

![Dati sulle prestazioni](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

La restituzione di milioni di record per tutti i contatori e gli oggetti prestazioni non è molto utile.  È possibile utilizzare hello è utilizzato in precedenza dati hello toofilter o semplicemente digitare hello seguente stessi metodi di query direttamente nella casella di ricerca log hello.  Vengono restituiti solo i record relativi all'utilizzo del processore per i computer Windows e Linux.

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilizzo del processore](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

Questo limita particolare contatore tooa dati hello, ma ancora non inserirlo in un form che risulta particolarmente utile.  È possibile visualizzare i dati di hello in un grafico a linee, ma prima di tutto necessario toogroup da Computer e TimeGenerated.  toogroup in più campi, è necessario query hello toomodify modificare direttamente, pertanto seguente toohello di hello query.  Questo metodo utilizza hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) funzione su hello **CounterValue** valore medio hello toocalculate della proprietà di ogni ora.

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Grafico dei dati sulle prestazioni](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

Ora che i dati di hello adeguatamente raggruppati, è possibile visualizzarlo in un grafico visual aggiungendo hello [rendering](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operatore.  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Grafico a linee](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sul linguaggio di query Log Analitica hello in [Introduzione al portale Analitica hello](https://go.microsoft.com/fwlink/?linkid=856079).
- Scorrere un'esercitazione utilizzando hello [portale avanzate Analitica](https://go.microsoft.com/fwlink/?linkid=856587) che consentono di hello toorun stessa query e accesso hello portale ricerca nei Log hello stessi dati.
