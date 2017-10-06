---
title: soluzione di gestione in Operations Management Suite (OMS) aaaAlert | Documenti Microsoft
description: la soluzione Alert Management in Log Analitica Hello consente di analizzare tutti gli avvisi di hello nell'ambiente in uso.  In aggiunta tooconsolidating gli avvisi generati in OMS, Importa gli avvisi dai gruppi di gestione di System Center Operations Manager connessi in Log Analitica.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>La soluzione Gestione avvisi in Operations Management Suite (OMS)

![Icona di Alert Management](media/log-analytics-solution-alert-management/icon.png)

Hello soluzione Alert Management permette di analizzare tutti gli avvisi di hello nel repository Analitica di Log.  Questi avvisi possono provenire da diverse origini, incluse le fonti [create da Log Analytics](log-analytics-alerts.md) o [importate da Nagios o Zabbix](log-analytics-linux-agents.md).  Hello soluzione Importa anche gli avvisi da qualsiasi [gruppi di gestione di System Center Operations Manager connessi](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Prerequisiti
soluzione Hello funziona con i record nell'archivio di Log Analitica hello con un tipo di **avviso**, pertanto è necessario eseguire qualsiasi configurazione è necessario toocollect questi record.

- Per gli avvisi di Log Analitica, [creare regole di avviso](log-analytics-alerts.md) toocreate i record degli avvisi direttamente nel repository di hello.
- Per gli avvisi Nagios e Zabbix, [configurare tali server](log-analytics-linux-agents.md) toosend avvisi tooLog Analitica.
- Per gli avvisi di System Center Operations Manager, [collegare l'area di lavoro di Operations Manager Gestione gruppo tooyour Analitica Log](log-analytics-om-agents.md).  Tutti gli avvisi creati in System Center Operations Manager vengono importati in Log Analytics.  

## <a name="configuration"></a>Configurazione
Aggiungere tooyour soluzione di gestione degli avvisi hello all'area di lavoro OMS tramite il processo di hello [aggiungere soluzioni](log-analytics-add-solutions.md).  Non è richiesta alcuna ulteriore configurazione.

## <a name="management-packs"></a>Management Pack
Se il gruppo di gestione di System Center Operations Manager è l'area di lavoro OMS tooyour connesso, hello seguenti management pack viene installato in System Center Operations Manager quando si aggiunge questa soluzione.  Non è presente alcuna configurazione o manutenzione di hello management pack richiesti.  

* Alert Management di Microsoft System Center Advisor (Microsoft.IntelligencePacks.AlertManagement)

Per ulteriori informazioni sulla modalità di aggiornamento dei management pack di soluzione, vedere [tooLog connettere Operations Manager Analitica](log-analytics-om-agents.md).

## <a name="data-collection"></a>Raccolta dei dati
### <a name="agents"></a>Agents
Hello nella tabella seguente descrive hello connesso origini supportate da questa soluzione.

| Origine connessa | Supporto | Descrizione |
|:--- |:--- |:--- |
| [Agenti di Windows](log-analytics-windows-agents.md) | No |Gli agenti di Windows diretti non generano avvisi.  Gli avvisi di Log Analytics possono essere creati da eventi e dati sulle prestazioni raccolti dagli agenti di Windows. |
| [Agenti Linux](log-analytics-linux-agents.md) | No |Gli agenti di Linux diretti non generano avvisi.  Gli avvisi di Log Analytics possono essere creati da eventi e dati sulle prestazioni raccolti dagli agenti di Linux.  Avvisi Nagios e Zabbix vengono raccolti dai server che richiedono l'agente Linux di hello. |
| [Gruppo di gestione di System Center Operations Manager](log-analytics-om-agents.md) |Sì |Gli avvisi generati per gli agenti di Operations Manager sono recapitati toohello gruppo di gestione e quindi vengono inoltrati tooLog Analitica.<br><br>Una connessione diretta da tooLog gli agenti di Operations Manager non è necessario Analitica. Dati di avviso viene inoltrati dal repository di hello gestione gruppo toohello Analitica di Log. |


### <a name="collection-frequency"></a>Frequenza della raccolta
- I record degli avvisi sono soluzioni toohello disponibili non appena vengono archiviati nel repository di hello.
- Avviso dati vengono inviati da tooLog gruppo di gestione Operations Manager hello Analitica ogni tre minuti.  

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello
Quando si aggiunge l'area di lavoro OMS hello Alert Management soluzione tooyour, hello **Alert Management** riquadro viene aggiunto il dashboard OMS tooyour.  Questo riquadro Visualizza un numero e la rappresentazione grafica del numero di hello di avvisi attivi generati all'interno di hello ultime 24 ore.  Non è possibile modificare questo intervallo di tempo.

![Riquadro di Alert Management](media/log-analytics-solution-alert-management/tile.png)

Fare clic su hello **Alert Management** riquadro tooopen hello **Alert Management** dashboard.  dashboard Hello sono incluse colonne hello hello nella tabella seguente.  Ogni colonna sono elencati hello primi 10 avvisi associando conteggio che i criteri della colonna per hello specificato intervallo di ambito e tempo.  È possibile eseguire una ricerca di log che fornisce l'intero elenco hello facendo **tutti** nella parte inferiore di hello della colonna hello o facendo clic sull'intestazione di colonna hello.

| Colonna | Descrizione |
|:--- |:--- |
| Critical Alerts |Tutti gli avvisi con un livello di gravità Critico raggruppati per nome dell'avviso.  Fare clic su un nome dell'avviso di toorun una ricerca nei log la restituzione di tutti i record per tale avviso. |
| Warning Alerts |Tutti gli avvisi con una gravità Avviso per nome dell'avviso.  Fare clic su un nome dell'avviso di toorun una ricerca nei log la restituzione di tutti i record per tale avviso. |
| Avvisi SCOM attivi |Tutti gli avvisi raccolti da Operations Manager con qualsiasi stato diverso da *chiuso* raggruppati per origine avviso hello generato. |
| All Active Alerts |Tutti gli avvisi con qualsiasi gravità raggruppati per nome dell'avviso. Include solo gli avvisi Operations Manager con qualsiasi stato diverso da *Chiuso*. |

Se si scorre a destra toohello, dashboard hello Elenca diverse query comuni che è possibile fare clic su tooperform un [ricerca nei log](log-analytics-log-searches.md) per dati di avviso.

![Dashboard di Alert Management](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Record di Log Analytics
la soluzione Alert Management Hello analizza tutti i record con un tipo di **avviso**.  Gli avvisi creati Log Analitica o raccolte da Nagios o Zabbix non vengono raccolti dalla soluzione hello direttamente.

soluzione Hello importare gli avvisi di System Center Operations Manager e crea un record corrispondente per ognuno con un tipo di **avviso** e un SourceSystem di **Operations Manager**.  Tali record sono riportate le hello in hello nella tabella seguente:  

| Proprietà | Descrizione |
|:--- |:--- |
| Tipo |*Avviso* |
| SourceSystem |*OpsManager* |
| AlertContext |Dettagli dell'elemento di dati hello che ha causato toobe di hello avvisi generati in formato XML. |
| AlertDescription |Descrizione dettagliata dell'avviso hello. |
| AlertId |GUID dell'avviso hello. |
| AlertName |Nome dell'avviso hello. |
| AlertPriority |Livello di priorità dell'avviso hello. |
| AlertSeverity |Livello di gravità dell'avviso hello. |
| AlertState |Ultimo stato di risoluzione avviso hello. |
| LastModifiedBy |Nome dell'utente hello autore dell'ultima modifica avviso hello. |
| ManagementGroupName |Nome del gruppo di gestione di hello in cui è stato generato l'avviso hello. |
| RepeatCount |Numero di volte in cui hello stesso avviso è stato generato per hello che stessa un oggetto monitorato da risolvere. |
| ResolvedBy |Nome dell'utente hello hello avviso risolto. Vuoto se l'avviso hello non è ancora stato risolto. |
| SourceDisplayName |Nome visualizzato del monitoraggio di un oggetto che ha generato l'avviso hello hello. |
| SourceFullName |Nome completo del monitoraggio di un oggetto che ha generato l'avviso hello hello. |
| TicketId |ID ticket per l'avviso hello se ambiente System Center Operations Manager hello è integrato con un processo per l'assegnazione dei ticket per gli avvisi.  Vuoto se non è assegnato alcun ID ticket. |
| TimeGenerated |Data e ora di hello avviso è stato creato. |
| TimeLastModified |Data e ora di hello avviso ultima modifica. |
| TimeRaised |Data e ora di hello avviso è stato generato. |
| TimeResolved |Data e ora di hello avviso è stato risolto. Vuoto se l'avviso hello non è ancora stato risolto. |

## <a name="sample-log-searches"></a>Ricerche di log di esempio
Hello nella tabella seguente sono disponibili log di esempio cerca i record degli avvisi raccolti da questa soluzione: 

| Query | Descrizione |
|:--- |:--- |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR |Avvisi critici generati nelle hello nelle ultime 24 ore |
| Type=Alert AlertSeverity=warning TimeRaised>NOW-24HOUR |Avvisi generati durante hello nelle ultime 24 ore |
| Type=Alert SourceSystem=OpsManager AlertState!=Closed TimeRaised>NOW-24HOUR &#124; measure count() as Count by SourceDisplayName |Origini con avvisi attivi generati durante hello nelle ultime 24 ore |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR AlertState!=Closed |Avvisi critici generati nelle hello nelle ultime 24 ore ancora attivi |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-24HOUR AlertState=Closed |Avvisi generati durante hello nelle ultime 24 ore che sono stati chiusi |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; measure count() as Count by AlertSeverity |Avvisi generati durante il giorno 1 precedente raggruppato in base alla gravità hello |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; sort RepeatCount desc |Avvisi generati durante il giorno 1 precedente ordinato in base al valore del numero di ripetizioni hello |


>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello precedente query modificherebbe toohello seguenti:
>
>| Query | Descrizione |
|:---|:---|
| Avviso &#124; dove SourceSystem == "OpsManager" e AlertSeverity == "error" e TimeRaised > ago(24h) |Avvisi critici generati nelle hello nelle ultime 24 ore |
| Avviso &#124; dove AlertSeverity == "warning" e TimeRaised > ago(24h) |Avvisi generati durante hello nelle ultime 24 ore |
| Avviso &#124; dove SourceSystem == "OpsManager" e AlertState != "Closed" e TimeRaised > ago(24h) &#124; summarize Count = count() by SourceDisplayName |Origini con avvisi attivi generati durante hello nelle ultime 24 ore |
| Avviso &#124; dove SourceSystem == "OpsManager" e AlertSeverity == "error" e TimeRaised > ago(24h) e AlertState != "Closed" |Avvisi critici generati nelle hello nelle ultime 24 ore ancora attivi |
| Avviso &#124; dove SourceSystem == "OpsManager" e TimeRaised > ago(24h) e AlertState == "Closed" |Avvisi generati durante hello nelle ultime 24 ore che sono stati chiusi |
| Avviso &#124; dove SourceSystem == "OpsManager" e TimeRaised > ago(1d) &#124; summarize Count = count() by AlertSeverity |Avvisi generati durante il giorno 1 precedente raggruppato in base alla gravità hello |
| Avviso &#124; dove SourceSystem == "OpsManager" e TimeRaised > ago(1d) &#124; ordina per RepeatCount desc |Avvisi generati durante il giorno 1 precedente ordinato in base al valore del numero di ripetizioni hello |


## <a name="next-steps"></a>Passaggi successivi
* Leggere l'articolo [Avvisi in Log Analytics](log-analytics-alerts.md) per informazioni dettagliate sulla generazione di avvisi di Log Analytics.
