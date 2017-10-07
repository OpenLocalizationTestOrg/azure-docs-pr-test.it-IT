---
title: aaaCollect e analizzare i contatori delle prestazioni in Azure Log Analitica | Documenti Microsoft
description: I contatori delle prestazioni vengono raccolti dalle prestazioni tooanalyze Log Analitica su Windows e Linux gli agenti.  Questo articolo viene descritto come i contatori tooconfigure raccolta delle prestazioni per Windows e Linux gli agenti, i dettagli di cui vengono archiviati nel repository OMS hello e come tooanalyze nel portale di OMS hello.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>Origini dati per le prestazioni di Windows e Linux in Log Analytics
I contatori delle prestazioni di Windows e Linux forniscono informazioni dettagliate sulle prestazioni di hello di componenti hardware, sistemi operativi e applicazioni.  Log Analitica può raccogliere i contatori delle prestazioni a intervalli frequenti per l'analisi quasi in tempo reale (NRT) in dati sulle prestazioni di addizione tooaggregating per analisi di più lungo termine e i report.

![Contatori delle prestazioni](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>Configurazione dei contatori delle prestazioni
Configurare i contatori delle prestazioni nel portale OMS hello da hello [menu dati nelle impostazioni di registro Analitica](log-analytics-data-sources.md#configuring-data-sources).

Durante la prima configurazione di Windows oppure contatori delle prestazioni di Linux per una nuova area di lavoro OMS, è possibile hello opzione tooquickly creare diversi contatori comuni.  Sono elencati con un tooeach Avanti casella di controllo.  Assicurarsi di creare contatori di cui si desidera tooinitially vengono controllate e quindi fare clic su **Aggiungi hello selezionato i contatori delle prestazioni**.

Per i contatori delle prestazioni di Windows è possibile scegliere un'istanza specifica per ogni contatore delle prestazioni. Per i contatori delle prestazioni di Linux, istanza hello di ogni contatore prescelto si applica tooall i contatori figlio del contatore padre hello. Hello nella tabella seguente mostra le istanze comuni hello tooboth disponibili Linux e Windows contatori delle prestazioni.

| Nome dell'istanza | Descrizione |
| --- | --- |
| \_Totale |Totale di tutte le istanze di hello |
| \* |Tutte le istanze |
| (/&#124;/var) |Corrisponde alle istanze denominate / oppure /var |

### <a name="windows-performance-counters"></a>Contatori delle prestazioni di Windows

![Configurare i contatori delle prestazioni di Windows](media/log-analytics-data-sources-performance-counters/configure-windows.png)

Seguire questa tooadd procedure un nuovo toocollect contatore delle prestazioni di Windows.

1. Nome del tipo hello del contatore hello nella casella di testo hello in formato hello *\counter oggetto (istanza)*.  Quando si inizia a digitare, viene visualizzato un elenco di contatori comuni corrispondenti.  È possibile selezionare un contatore dall'elenco hello o digitarne uno proprio.  Per restituire tutte le istanze per un contatore specifico, specificare *oggetto\contatore*.  

    Quando si raccolgono i contatori delle prestazioni di SQL Server da istanze denominate, tutti un nome istanza contatori iniziano con *MSSQL$* e aggiungendo il nome dell'istanza di hello hello.  Ad esempio, hello toocollect percentuale riscontri Cache Log contatore per l'istanza di tutti i database dall'oggetto delle prestazioni di Database hello per SQL denominata INST2, specificare `MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`.

2. Fare clic su  **+**  o premere **invio** elenco toohello di tooadd hello contatore.
3. Quando si aggiunge un contatore, Usa predefinito hello è 10 secondi per il relativo **intervallo di campionamento**.  Se si desidera che i requisiti di archiviazione hello tooreduce di hello raccolti i dati sulle prestazioni, è possibile modificare questo valore più alto tooa di backup too1800 secondi (30 minuti).
4. Una volta terminato l'aggiunta di contatori, fare clic su hello **salvare** pulsante nella parte superiore di hello della configurazione di hello toosave schermata hello.

### <a name="linux-performance-counters"></a>Contatori delle prestazioni di Linux

![Configurare i contatori delle prestazioni di Linux](media/log-analytics-data-sources-performance-counters/configure-linux.png)

Seguire questa tooadd procedure un nuovo toocollect contatore delle prestazioni di Linux.

1. Per impostazione predefinita, tutte le modifiche di configurazione vengono automaticamente spostate tooall agenti.  Per gli agenti Linux, un file di configurazione viene inviato l'agente di raccolta dati Fluentd toohello.  Se si desidera toomodify questo file manualmente in ogni agente Linux, quindi deselezionare la casella di hello *Apply below macchine Linux di configurazione toomy* e seguire le guide di hello indicate di seguito.
2. Nome del tipo hello del contatore hello nella casella di testo hello in formato hello *\counter oggetto (istanza)*.  Quando si inizia a digitare, viene visualizzato un elenco di contatori comuni corrispondenti.  È possibile selezionare un contatore dall'elenco hello o digitarne uno proprio.  
3. Fare clic su  **+**  o premere **invio** tooadd hello contatore toohello elenco di altri contatori per oggetto hello.
4. Tutti i contatori per un utilizzo dell'oggetto hello stesso **intervallo di campionamento**.  valore predefinito di Hello è 10 secondi.  È modificare il valore più alto tooa di backup too1800 secondi (30 minuti) se si desidera che i requisiti di archiviazione di hello tooreduce dei dati sulle prestazioni raccolti hello.
5. Una volta terminato l'aggiunta di contatori, fare clic su hello **salvare** pulsante nella parte superiore di hello della configurazione di hello toosave schermata hello.

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>Configurare i contatori delle prestazioni di Linux nel file di configurazione
Anziché configurare i contatori delle prestazioni di Linux tramite il portale di OMS hello, è possibile hello di modifica dei file di configurazione nell'agente Linux di hello.  Toocollect le metriche delle prestazioni sono controllate dalla configurazione hello in **/e così via/rifiutare/microsoft/omsagent/\<id area di lavoro\>/conf/omsagent.conf**.

Ogni oggetto, o categoria, delle prestazioni metriche toocollect deve essere definito nel file di configurazione hello come una singola `<source>` elemento. sintassi di Hello seguito è descritto hello.

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


in hello nella tabella seguente sono descritti i parametri Hello in questo elemento.

| parameters | Descrizione |
|:--|:--|
| object\_name | Nome dell'oggetto per la raccolta di hello. |
| instance\_regex |  Oggetto *espressione regolare* toocollect quali istanze di definizione. valore di Hello: `.*` specifica tutte le istanze. le metriche del processore toocollect per solo hello \_istanza totale, è possibile specificare `_Total`. per dati metrici sui processi toocollect hello solo le istanze crond o sshd, è possibile specificare: ' (crond\|sshd)`. |
| counter\_name\_regex | Oggetto *espressione regolare* definizione toocollect quali contatori (per oggetto hello). specificare tutti i contatori per l'oggetto hello, toocollect: `.*`. toocollect solo i contatori di spazio di swapping per l'oggetto memoria hello, ad esempio, è possibile specificare:`.+Swap.+` |
| interval | Frequenza di raccolta contatori dell'oggetto cui hello. |


Hello nella tabella seguente vengono elencati oggetti hello e contatori che è possibile specificare nel file di configurazione hello.  Per alcune applicazioni sono disponibili contatori aggiuntivi, come descritto in [Collect performance counters for Linux applications in Log Analytics](log-analytics-data-sources-linux-applications.md) (Raccogliere contatori delle prestazioni per applicazioni Linux in Log Analytics).

| Nome oggetto | Nome contatore |
|:--|:--|
| Logical Disk | % Free Inodes |
| Logical Disk | % Free Space |
| Logical Disk | % Used Inodes |
| Logical Disk | % Used Space |
| Logical Disk | Byte letti da disco/sec  |
| Logical Disk | Letture disco/sec  |
| Logical Disk | Disk Transfers/sec |
| Logical Disk | Byte scritti su disco/sec |
| Logical Disk | Scritture disco/sec |
| Logical Disk | Free Megabytes |
| Logical Disk | Logical Disk Bytes/sec |
| Memoria | % Available Memory |
| Memoria | % Available Swap Space |
| Memoria | % Used Memory |
| Memoria | % Used Swap Space |
| Memoria | Available MBytes Memory |
| Memoria | Available MBytes Swap |
| Memoria | Page Reads/sec |
| Memoria | Page Writes/sec |
| Memoria | Pages/sec |
| Memoria | Used MBytes Swap Space |
| Memoria | Used Memory MBytes |
| Rete | Total Bytes Transmitted |
| Rete | Total Bytes Received |
| Rete | Total Bytes |
| Rete | Total Packets Transmitted |
| Rete | Total Packets Received |
| Rete | Total Rx Errors |
| Rete | Total Tx Errors |
| Rete | Total Collisions |
| Physical Disk | Avg. Disk sec/Read |
| Physical Disk | Avg. Disk sec/Transfer |
| Physical Disk | Avg. Disk sec/Write |
| Physical Disk | Physical Disk Bytes/sec |
| Process | Pct Privileged Time |
| Process | Pct User Time |
| Process | Used Memory kBytes |
| Process | Virtual Shared Memory |
| Processore | % DPC Time |
| Processore | % Idle Time |
| Processore | % Interrupt Time |
| Processore | % IO Wait Time |
| Processore | % Nice Time |
| Processore | % Privileged Time |
| Processore | % di tempo processore |
| Processore | % User Time |
| Sistema | Free Physical Memory |
| Sistema | Free Space in Paging Files |
| Sistema | Free Virtual Memory |
| Sistema | Processi |
| Sistema | Size Stored In Paging Files |
| Sistema | Uptime |
| Sistema | Utenti |


Di seguito è una configurazione predefinita di hello per le metriche delle prestazioni.

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>Raccolta dei dati
Log Analytics raccoglierà tutti i contatori delle prestazioni specificati in base all'intervallo di campionamento definito in tutti gli agenti in cui è installato il contatore.  non vengono aggregati i dati di Hello e dati non elaborati hello sono disponibili in tutte le visualizzazioni di ricerca di log per durata hello specificata dalla sottoscrizione OMS.

## <a name="performance-record-properties"></a>Proprietà dei record delle prestazioni
Record di prestazioni sono un tipo di **prestazioni** e dispone di proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| Computer |Computer in cui hello eventi raccolti da. |
| CounterName |Nome del contatore delle prestazioni hello |
| CounterPath |Percorso completo del contatore hello nel modulo hello \\ \\ \<Computer >\\oggetto (istanza)\\contatore. |
| CounterValue |Valore numerico del contatore hello. |
| InstanceName |Nome dell'istanza dell'evento hello.  Vuoto se l'istanza non è presente. |
| ObjectName |Nome dell'oggetto prestazione hello |
| SourceSystem |Tipo di agente hello dati raccolti da. <br><br>OpsManager: agente Windows, con connessione diretta o SCOM <br> Linux – Tutti gli agenti Linux  <br> AzureStorage: Diagnostica di Azure |
| TimeGenerated |Data e ora dati hello è stati campionati. |

## <a name="sizing-estimates"></a>Stime di dimensionamento
 Secondo una stima approssimativa per la raccolta di un determinato contatore a intervalli di 10 secondi, le dimensioni equivalgono a circa 1 MB al giorno per istanza.  È possibile stimare i requisiti di archiviazione hello di un particolare contatore con hello formula seguente.

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>Ricerche di record delle prestazioni nei log
Hello nella tabella seguente vengono forniti esempi di ricerche nei log che recuperano i record delle prestazioni.

| Query | Descrizione |
|:--- |:--- |
| Type=Perf |Tutti i dati sulle prestazioni |
| Type=Perf Computer="Computer" |Tutti i dati sulle prestazioni da un computer specifico |
| Type=Perf CounterName="Lunghezza corrente coda del disco" |Tutti i dati sulle prestazioni da un contatore specifico |
| Type=Perf (ObjectName=Processor) CounterName="% tempo processore" InstanceName=_Total &#124; measure Avg(Average) as AVGCPU  by Computer |Utilizzo medio della CPU per tutti i computer |
| Type=Perf (CounterName="% tempo processore") &#124;  measure max(Max) by Computer |Utilizzo massimo della CPU per tutti i computer |
| Type=Perf ObjectName=LogicalDisk CounterName="Lunghezza corrente coda del disco" Computer="Nome computer" &#124; measure Avg(Average) by InstanceName |Media lunghezza corrente coda del disco in tutte le istanze di hello di un computer specifico |
| Type=Perf CounterName="Trasferimenti disco/sec" &#124; measure percentile95(Average) by Computer |95° percentile di trasferimenti disco al secondo per tutti i computer |
| Type=Perf CounterName="% tempo processore" InstanceName="_Total"  &#124; measure avg(CounterValue) by Computer Interval 1HOUR |Utilizzo orario medio della CPU per tutti i computer |
| Type=Perf Computer="MyComputer" CounterName=%* InstanceName=_Total &#124; measure percentile70(CounterValue) by CounterName Interval 1HOUR |70° percentile orario di ogni contatore percentuale % per un computer specifico |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total"  (Computer="MyComputer") &#124; measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR |Utilizzo CPU orario medio, minimo, massimo e 75° percentile per un computer specifico |
| Type=Perf ObjectName="MSSQL$INST2:Databases" InstanceName=master | Tutti i dati sulle prestazioni delle prestazioni del Database hello dell'oggetto per il database master hello dall'istanza di SQL Server INST2 denominata hello.  

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.

> | Query | Descrizione |
|:--- |:--- |
| Perf |Tutti i dati sulle prestazioni |
| Perf &#124; where Computer == "MyComputer" |Tutti i dati sulle prestazioni da un computer specifico |
| Perf &#124; where CounterName == "Current Disk Queue Length" |Tutti i dati sulle prestazioni da un contatore specifico |
| Perf &#124; where ObjectName == "Processor" and CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AVGCPU = avg(Average) by Computer |Utilizzo medio della CPU per tutti i computer |
| Perf &#124; where CounterName == "% Processor Time" &#124; summarize AggregatedValue = max(Max) by Computer |Utilizzo massimo della CPU per tutti i computer |
| Perf &#124; where ObjectName == "LogicalDisk" and CounterName == "Current Disk Queue Length" and Computer == "MyComputerName" &#124; summarize AggregatedValue = avg(Average) by InstanceName |Media lunghezza corrente coda del disco in tutte le istanze di hello di un computer specifico |
| Perf &#124; where CounterName == "DiskTransfers/sec" &#124; summarize AggregatedValue = percentile(Average, 95) by Computer |95° percentile di trasferimenti disco al secondo per tutti i computer |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), Computer |Utilizzo orario medio della CPU per tutti i computer |
| Perf &#124; where Computer == "MyComputer" and CounterName startswith_cs "%" and InstanceName == "_Total" &#124; summarize AggregatedValue = percentile(CounterValue, 70) by bin(TimeGenerated, 1h), CounterName | 70° percentile orario di ogni contatore percentuale % per un computer specifico |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" and Computer == "MyComputer" &#124; summarize ["min(CounterValue)"] = min(CounterValue), ["avg(CounterValue)"] = avg(CounterValue), ["percentile75(CounterValue)"] = percentile(CounterValue, 75), ["max(CounterValue)"] = max(CounterValue) by bin(TimeGenerated, 1h), Computer |Utilizzo CPU orario medio, minimo, massimo e 75° percentile per un computer specifico |
| Perf &#124; where ObjectName == "MSSQL$INST2:Databases" and InstanceName == "master" | Tutti i dati sulle prestazioni delle prestazioni del Database hello dell'oggetto per il database master hello dall'istanza di SQL Server INST2 denominata hello.  

## <a name="viewing-performance-data"></a>Visualizzazione dei dati sulle prestazioni
Quando si esegue una ricerca di log per i dati sulle prestazioni, hello **elenco** viene visualizzato per impostazione predefinita.  tooview hello dati sotto forma di grafico, fare clic su **metriche**.  Per una visualizzazione grafica dettagliata, fare clic su hello  **+**  contatore tooa successivo.  

![Visualizzazione Metriche compressa](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

dati sulle prestazioni tooaggregate in una ricerca di log, vedere [aggregazione metrica su richiesta e la visualizzazione in OMS](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/).


## <a name="next-steps"></a>Passaggi successivi
* [Raccogliere i contatori delle prestazioni da applicazioni Linux](log-analytics-data-sources-linux-applications.md) come il server HTTP Apache e MySQL.
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.  
* Esportare i dati raccolti troppo[Power BI](log-analytics-powerbi.md) per l'analisi e visualizzazioni aggiuntive.
