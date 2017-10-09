---
title: il foglio informativo language di aaaAzure Analitica Log query | Documenti Microsoft
description: "Questo articolo fornisce assistenza in fase di transizione toohello nuovo linguaggio di query per Analitica Log se si ha già familiarità con il linguaggio legacy hello."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>In fase di transizione tooAzure Log Analitica nuovo linguaggio di query

> [!NOTE]
> È possibile leggere ulteriori informazioni su hello Analitica Log nuovo linguaggio di query e ottenere hello procedure tooupgrade l'area di lavoro aggiornamento il [ricerca nei log di Azure Log Analitica dell'area di lavoro toonew](log-analytics-log-search-upgrade.md).

Questo articolo fornisce assistenza in fase di transizione toohello nuovo linguaggio di query per Analitica Log se si ha già familiarità con il linguaggio legacy hello.

## <a name="language-converter"></a>Convertitore di linguaggio

Se si ha familiarità con il linguaggio di query Log Analitica legacy hello, hello toocreate hello stessa query nella lingua nuova hello più semplice è toouse hello convertitore lingua installata nel portale di ricerca nei Log hello quando viene convertito nell'area di lavoro.  Usando il convertitore hello è semplice come immettere in una query nella casella di testo in alto hello legacy, quindi scegliere **convertire**.  È possibile fare clic su hello pulsante toorun hello ricerca o copia e Incolla toouse in un'altra posizione.

![Convertitore di linguaggio](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>Tabella di riepilogo

Hello nella tabella seguente fornisce un confronto tra un'ampia gamma di query comuni tooequivalent comandi tra il linguaggio di query di nuove e precedenti hello in Azure Log Analitica.

| Descrizione | Legacy | Nuovo |
|:--|:--|:--|
| Ricerca in tutte le tabelle      | error | ricerca di "error" (senza distinzione tra maiuscole/minuscole) |
| Selezione di dati da una tabella | Type=Event |  Event |
|                        | Type=Event &#124; select Source, EventLog, EventID | Event &#124; project Source, EventLog, EventID |
|                        | Type=Event &#124; top 100 | Event &#124; take 100 |
| Confronto di stringhe      | Type=Event Computer=srv01.contoso.com   | Event &#124; where Computer == "srv01.contoso.com" |
|                        | Type=Event Computer=contains("contoso") | Event &#124; where Computer contains "contoso" (senza distinzione tra maiuscole/minuscole)<br>Event &#124; where Computer contains_cs "Contoso" (con distinzione tra maiuscole/minuscole) |
|                        | Type=Event Computer=RegEx("@contoso@")  | Event &#124; where Computer matches regex ".*contoso*" |
| Confronto di date        | Type=Event TimeGenerated > NOW-1DAYS | Event &#124; where TimeGenerated > ago(1d) |
|                        | Type=Event TimeGenerated>2017-05-01 TimeGenerated<2017-05-31 | Event &#124; where TimeGenerated between (datetime(2017-05-01) .. datetime(2017-05-31)) |
| Confronto booleano     | Type=Heartbeat IsGatewayInstalled=false  | Heartbeat | where IsGatewayInstalled == false |
| Ordinamento                   | Type=Event &#124; sort Computer asc, EventLog desc, EventLevelName asc | Event \| sort by Computer asc, EventLog desc, EventLevelName asc |
| Distinzione               | Type=Event &#124; dedup Computer \| select Computer | Event &#124; summarize by Computer, EventLog |
| Estensione di colonne         | Type=Perf CounterName="% Processor Time" &#124; EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION | Perf &#124; where CounterName == "% Processor Time" \| extend Utilization = iff(CounterValue > 50, "HIGH", "LOW") |
| Aggregazione            | Type=Event &#124; measure count() as Count by Computer | Event &#124; summarize Count = count() by Computer |
|                                | Type=Perf ObjectName=Processor CounterName="% Processor Time" &#124; measure avg(CounterValue) by Computer interval 5minute | Perf &#124; where ObjectName=="Processor" and CounterName=="% Processor Time" &#124; summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min) |
| Aggregazione con limite | Type=Event &#124; measure count() by Computer &#124; top 10 | Event &#124; summarize AggregatedValue = count() by Computer &#124; limit 10 |
| Unione                  | Type=Event or Type=Syslog | union Event, Syslog |
| Join                   | Type=NetworkMonitoring &#124; join inner AgentIP (Type=Heartbeat) ComputerIP | NetworkMonitoring &#124; join kind=inner (search Type == "Heartbeat") on $left.AgentIP == $right.ComputerIP |



## <a name="next-steps"></a>Passaggi successivi
- Estrarre un [esercitazione sulla scrittura di query](https://go.microsoft.com/fwlink/?linkid=856078) utilizzando il nuovo linguaggio di query hello.
- Fare riferimento toohello [riferimenti al linguaggio di Query](https://go.microsoft.com/fwlink/?linkid=856079) per informazioni dettagliate su tutti i comandi, operatori e funzioni per il nuovo linguaggio di query hello.  
