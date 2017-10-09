---
title: avvisi aaaUnderstanding Analitica di Log di Azure | Documenti Microsoft
description: Gli avvisi nel registro Analitica identificare importanti informazioni nel repository OMS e in modo proattivo ricevere una notifica di problemi o richiamare azioni tooattempt toocorrect li.  In questo articolo descrive hello diversi tipi di regole di avviso e come vengono definite.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>Informazioni sugli avvisi in Log Analytics

Gli avvisi in Log Analytics identificano informazioni importanti nel repository di Log Analytics.  In questo articolo vengono fornite informazioni dettagliate, come regole di avviso in un Log Analitica e vengono descritte le differenze di hello tra diversi tipi di regole di avviso.

Per processo hello di Creazione regole di avviso, vedere hello seguenti articoli:

- Creare regole di avviso tramite il [portale di Azure](log-analytics-alerts-creating.md)
- Creare regole di avviso tramite il [modello di Resource Manager](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
- Creare regole di avviso tramite l'[API REST](log-analytics-api-alerts.md)


## <a name="alert-rules"></a>Regole di avviso

Gli avvisi vengono creati da regole di avviso che eseguono automaticamente ricerche log a intervalli regolari.  Se hello risultati della ricerca log hello corrispondono a determinati criteri, viene creato un record di avviso.  regola Hello quindi eseguire automaticamente uno o più azioni tooproactively ricevere una notifica di avviso hello o richiamare un altro processo.  Diversi tipi di regole di avviso utilizzano una logica diversa tooperform questa analisi.

![Avvisi Log Analytics](media/log-analytics-alerts/overview.png)

Le regole di avviso vengono definite da hello seguenti dettagli:

- **Ricerca log**.  query Hello che viene eseguito ogni volta che viene attivata la regola di avviso hello.  record Hello restituiti da questa query è toodetermine utilizzato se viene creato un avviso.
- **Intervallo di tempo**.  Specifica l'intervallo di tempo hello per query hello.  Hello query restituisce solo i record che sono stati creati all'interno dell'intervallo di hello ora corrente.  Può essere un valore qualsiasi compreso tra 5 minuti e 24 ore. Ad esempio, se hello finestra è impostata too60 minuti e query hello esecuzione 1:15 PM, viene restituito solo i record creati tra 12:15 PM e 1:15 PM.
- **Frequenza**.  Specifica la frequenza con cui hello è necessario eseguire query. Può essere un valore qualsiasi compreso tra 5 minuti e 24 ore. Deve essere uguale tooor minore di intervallo di tempo hello.  Se il valore di hello è maggiore di intervallo di tempo hello, si rischia record viene ignorato.<br>Si considerino ad esempio un intervallo di tempo di 30 minuti e una frequenza pari a 60 minuti.  Se l'esecuzione di query di hello 1:00, restituisce i record compresi tra 12:30 e 1:00 PM.  Hello successivo hello verrebbe eseguita è 2:00 quando il risultato restituito sarebbe i record compresi tra 1:30 alle 2:00.  Qualsiasi record creato tra le 13:00 e 13:30 non verrà mai valutato.
- **Soglia**.  risultati di Hello della ricerca log hello sono valutate toodetermine se un avviso deve essere creato.  soglia di Hello è diverso per tipi diversi di hello delle regole di avviso.

Ogni regola di avviso di Log Analytics è di uno fra due tipi.  Ognuno di questi tipi è descritte dettagliatamente nelle sezioni hello che seguono.

- **[Numero di risultati](#number-of-results-alert-rules)**. Singolo avviso creato quando i record di numero hello restituiti dalla ricerca log hello supera un numero specificato.
- **[Unità di misura della metrica](#metric-measurement-alert-rules)**.  Avviso creato per ogni oggetto nei risultati di hello della ricerca log hello con i valori che superano la soglia specificata.

differenze di Hello tra tipi di regola di avviso sono i seguenti.

- **Numero di risultati** regola di avviso creerà sempre un po' di tempo di avviso singolo **misura metrico** regola di avviso crea un avviso per ogni oggetto che supera la soglia di hello.
- **Numero di risultati** le regole di avviso creano un avviso quando viene superata la soglia di hello una sola volta. **Misura metrico** le regole di avviso è possono creare un avviso quando viene superata la soglia di hello un certo numero di volte in un intervallo di tempo specifico.

## <a name="number-of-results-alert-rules"></a>Regole di avviso Numero di risultati
**Numero di risultati** le regole di avviso creano un avviso solo quando il numero di hello di record restituiti dalla query di ricerca hello supera la soglia specificata di hello.

### <a name="threshold"></a>Soglia
soglia di Hello per un **numero di risultati** regola di avviso è semplicemente maggiore o minore di un particolare valore.  Se il numero di hello di record restituiti dalla ricerca nei log hello corrisponde questo criterio, viene creato un avviso.

### <a name="scenarios"></a>Scenari

#### <a name="events"></a>Eventi
Questo tipo di regola di avviso è adatto per l'uso con eventi come quelli dei log eventi di Windows, Syslog e log personalizzati.  È consigliabile toocreate un avviso quando viene creato un evento di errore specifico oppure quando vengono creati più eventi di errore all'interno di un intervallo di tempo specifico.

tooalert su un singolo evento, il numero di hello set di risultati toogreater tra 0 e la frequenza di hello e minuti di tempo finestra too5.  Che esegue query hello ogni 5 minuti e il controllo per l'occorrenza hello di un singolo evento che è stato creato dall'esecuzione di query di hello hello ultima ora.  Una frequenza maggiore può ritardare il tempo di hello tra hello being di eventi raccolti e di avviso hello viene creato.

Alcune applicazioni possono registrare un errore occasionale che non deve necessariamente generare un avviso.  Ad esempio, un'applicazione hello può ripetere l'elaborazione di hello che ha creato l'evento di errore hello e quindi esito positivo hello successivo.  In questo caso, si consiglia di non avviso hello toocreate a meno che non vengono creati più eventi all'interno di un intervallo di tempo specifico.  

In alcuni casi, è consigliabile toocreate un avviso in assenza di hello di un evento.  Ad esempio, un processo può registrare eventi regolari tooindicate che funzioni correttamente.  Se non viene registrato uno di questi eventi in un intervallo di tempo specifico, dovrà essere creato un avviso.  In questo caso impostare soglia hello troppo**inferiore a 1**.

#### <a name="performance-alerts"></a>Avvisi di prestazioni
[I dati sulle prestazioni](log-analytics-data-sources-performance-counters.md) viene archiviato come record hello tooevents simile di repository OMS.  Se si desidera tooalert quando un contatore delle prestazioni supera una determinata soglia, nella query hello è necessario includere tale soglia.

Ad esempio, se si desidera tooalert quando hello processore viene eseguito su 90%, utilizzare una query come hello seguenti soglia hello per regola di avviso hello **maggiore di 0**.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

Se si desidera tooalert quando processore hello Media oltre il 90% per un intervallo di tempo specifico, utilizzare una query utilizzando hello [misurare comando](log-analytics-search-reference.md#commands) simile hello seguente con la soglia di hello per regola di avviso hello **maggiore di 0** .

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguenti:`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>Regole di avviso Unità di misura della metrica

>[!NOTE]
> Le regole di avviso Unità di misura della metrica sono attualmente disponibili in anteprima pubblica.

Le regole di avviso **Unità di misura della metrica** creano un avviso per ogni oggetto in una query con un valore che supera una soglia specificata.  Hanno hello seguenti differenze distinte da **numero di risultati** regole di avviso.

#### <a name="log-search"></a>Ricerca log
Sebbene sia possibile utilizzare qualsiasi query per un **numero di risultati** regola di avviso, sono presenti query hello requisiti specifici per una regola di avviso di metriche di misurazione.  Deve includere un [misurare comando](log-analytics-search-reference.md#commands) risultati hello toogroup su un particolare campo. Questo comando deve includere hello seguenti elementi.

- **Funzione di aggregazione**.  Determina il calcolo hello che viene eseguito e potenzialmente tooaggregate un campo numerico.  Ad esempio, **Count ()** verrà restituito il numero di hello di record nella query hello **avg(CounterValue)** restituirà Media hello del campo CounterValue hello su intervallo "hello".
- **Campo Gruppo**.  Viene creato un record con un valore aggregato per ogni istanza di questo campo e può essere generato un avviso per ognuno di essi.  Ad esempio, se si desidera toogenerate un avviso per ogni computer, utilizzare **dal Computer**.   
- **Intervallo**.  Definisce l'intervallo di tempo hello in cui vengono aggregati i dati di hello.  Ad esempio, se è stato specificato **5 minuti**, verrebbe creato un record per ogni istanza del campo gruppo hello aggregato a intervalli di 5 minuti in intervallo di tempo hello specificato per l'avviso hello.

#### <a name="threshold"></a>Soglia
soglia di Hello per le regole di avviso di metriche di misurazione viene definita da un valore di aggregazione e un numero di violazioni della sicurezza.  Se un punto dati nella ricerca nei log hello supera questo valore, è considerata una violazione di sicurezza.  Se il numero di hello di violazioni della sicurezza in qualsiasi oggetto nei risultati di hello supera hello valore specificato, quindi viene creato un avviso per l'oggetto.

#### <a name="example"></a>Esempio
Si consideri uno scenario in cui si desidera creare un avviso se l'uso del processo di un computer supera il 90% tre volte in 30 minuti.  È necessario creare una regola di avviso con hello seguenti dettagli.  

**Query:** Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer Interval 5minute<br>
**Intervallo di tempo:** 30 minuti<br>
**Frequenza di avviso:** 5 minuti<br>
**Valore di aggregazione:** maggiore di 90<br>
**Attiva l'avviso in base a:** violazioni totali maggiori di 5<br>

query Hello creerebbe un valore medio per ogni computer a intervalli di 5 minuti.  La query verrebbe eseguita ogni 5 minuti per i dati raccolti tramite hello 30 minuti precedenti.  Di seguito sono illustrati dati di esempio per tre computer.

![Risultati della query di esempio](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

In questo esempio, verrebbero creati avvisi separati per srv02 e srv03 poiché essi violazione soglia 90% di hello 3 volte in intervallo di tempo hello.  Se hello **avviso Trigger in base a:** sono state modificate troppo**pieghevole** quindi verrebbe creato un avviso solo per srv03 poiché è verificata una violazione di soglia hello per 3 campioni consecutivi.

## <a name="alert-records"></a>Record di avvisi
I record degli avvisi creati dalle regole di avviso in Log Analytics hanno un **Tipo** impostato su **Avviso** e **SourceSystem** impostato su **OMS**.  Presentano proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| Tipo |*Avviso* |
| SourceSystem |*OMS* |
| *Object*  | [Gli avvisi di metriche di misurazione](#metric-measurement-alert-rules) avrà una proprietà per il campo gruppo hello.  Ad esempio, se la ricerca dei registri di hello gruppi nel Computer, hello avviso con il record dispone di un campo del Computer con nome hello del computer di hello come valore di hello.
| AlertName |Nome dell'avviso hello. |
| AlertSeverity |Livello di gravità dell'avviso hello. |
| LinkToSearchResults |Collegamento tooLog Analitica Registro ricerca che restituisce i record di hello dalla query hello hello avviso creato. |
| Query |Testo della query hello che è stata eseguita. |
| QueryExecutionEndTime |Fine dell'intervallo di tempo hello per query hello. |
| QueryExecutionStartTime |Inizio dell'intervallo di tempo hello per query hello. |
| ThresholdOperator | Operatore utilizzato dalla regola di avviso hello. |
| ThresholdValue | Valore utilizzato dalla regola di avviso hello. |
| TimeGenerated |Data e ora avviso hello è stato creato. |

Sono disponibili altri tipi di record degli avvisi creati da hello [soluzione Alert Management](log-analytics-solution-alert-management.md) e da [Power BI Esporta](log-analytics-powerbi.md).  Questi record hanno un **Tipo** impostato su **Avviso** ma vengono distinti da relativo **SourceSystem**.


## <a name="next-steps"></a>Passaggi successivi
* Installare hello [soluzione Alert Management](log-analytics-solution-alert-management.md) raccolti gli avvisi tooanalyze creati in Log Analitica con gli avvisi da System Center Operations Manager.
* Altre informazioni sulle [ricerche nei log](log-analytics-log-searches.md) che possono generare avvisi.
* Completare una procedura dettagliata per la [configurazione di un webhook](log-analytics-alerts-webhooks.md) con una regola di avviso.  
* Informazioni su come toowrite [i runbook in automazione di Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate problemi identificati tramite gli avvisi.
