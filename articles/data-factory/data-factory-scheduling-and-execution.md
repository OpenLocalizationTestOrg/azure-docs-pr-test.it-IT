---
title: aaaScheduling e l'esecuzione con Data Factory | Documenti Microsoft
description: Informazioni sugli aspetti di pianificazione ed esecuzione del modello applicativo di Azure Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Pianificazione ed esecuzione con Data Factory
Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di hello Azure Data Factory. L'articolo presuppone la conoscenza dei concetti di base del modello applicativo di Data Factory: attività, pipeline, servizi collegati e set di dati. Per concetti di base di Azure Data Factory, vedere hello seguenti articoli:

* [Introduzione tooData Factory](data-factory-introduction.md)
* [Pipeline](data-factory-create-pipelines.md)
* [Set di dati](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>Ora di inizio e ora di fine della pipeline
Una pipeline è attiva solo tra l'ora di **inizio** e l'ora di **fine**. Non viene eseguita prima dell'ora di inizio hello o dopo l'ora di fine hello. Se la pipeline di hello è sospesa, non viene eseguito indipendentemente dal relativo ora di inizio e fine. Per toorun una pipeline, consigliabile non sospesa. Queste impostazioni (inizio, fine, in pausa) disponibili nella definizione di pipeline hello: 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

Per altre informazioni su queste proprietà, vedere l'articolo [Creare pipeline](data-factory-create-pipelines.md). 


## <a name="specify-schedule-for-an-activity"></a>Pianificare l'esecuzione di un'attività
Non è pipeline hello che viene eseguita. Si tratta di attività hello nella pipeline hello che vengono eseguite in hello contesto complessivo della pipeline hello. È possibile specificare una pianificazione ricorrente per un'attività tramite hello **dell'utilità di pianificazione** sezione del formato JSON dell'attività. Ad esempio, è possibile pianificare un toorun attività ogni ora come indicato di seguito:  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Come illustrato nel seguente diagramma hello, che specifica che una pianificazione per un'attività crea una serie di finestre a cascata con in hello della pipeline di inizio e di fine. Le finestre a cascata sono costituite da una serie di intervalli temporali di dimensioni fisse, contigui e non sovrapposti. Queste finestre logiche a cascata per un'attività vengono denominate **finestre attività**.

![Esempio di utilità di pianificazione delle attività](media/data-factory-scheduling-and-execution/scheduler-example.png)

Hello **dell'utilità di pianificazione** proprietà per un'attività è facoltativa. Se si specifica questa proprietà, deve corrispondere a cadenza hello specificate nella definizione di hello del set di dati di output per l'attività hello. Set di dati di output è attualmente, quali unità hello pianificazione. Pertanto, è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output. 

## <a name="specify-schedule-for-a-dataset"></a>Specificare una pianificazione per un set di dati
Un'attività in una pipeline di Data Factory può non avere alcun **set di dati** di input o può averne più di uno e generare uno o più set di dati di output. Per un'attività, è possibile specificare una frequenza di hello quali hello dati di input sono disponibili o dati di output di hello viene generati utilizzando hello **disponibilità** sezione nelle definizioni di set di dati hello. 

**Frequenza** in hello **disponibilità** sezione specifica di unità di tempo hello. Hello i valori consentiti per la frequenza sono: minuto, ora, giorno, settimana e mese. Hello **intervallo** proprietà nella sezione di disponibilità hello consente di specificare un moltiplicatore di frequenza. Ad esempio: se la frequenza di hello è impostata tooDay e l'intervallo è impostato too1 per un set di dati di output, i dati di output di hello viene prodotta ogni giorno. Se si specifica la frequenza di hello minuto, è consigliabile impostare hello intervallo toono inferiore a 15. 

Nell'esempio seguente di hello, dati di input hello sono disponibili ogni ora e dati di output di hello viene generati ogni ora (`"frequency": "Hour", "interval": 1`). 

**Set di dati di input:** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


**Set di dati di output**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Attualmente, **pianificazione hello unità set di dati di output**. In altre parole, pianificazione hello specificata per il set di dati di hello output è toorun usato un'attività in fase di esecuzione. Pertanto, è necessario creare un set di dati di output, anche se l'attività hello non genera alcun output. Se l'attività hello non accetta alcun input, è possibile ignorare i set di dati input hello creazione. 

In seguito hello pipeline definizione, hello **dell'utilità di pianificazione** proprietà è pianificazione toospecify utilizzati per attività hello. Questa proprietà è facoltativa. Attualmente, pianificazione hello per attività hello deve corrispondere pianificazione hello specificata per il set di dati di hello output.
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

In questo esempio viene eseguito ogni ora di hello attività tra hello inizio e di fine della pipeline hello. per windows a tre ore (8 AM - 09 AM, 09: 00:10:00 e AM 10-11 AM), dati di output di Hello viene prodotta ogni ora. 

Ogni unità di dati usata o prodotta da un'esecuzione di attività prende il nome di **sezione di dati**. Hello seguente diagramma viene illustrato un esempio di un'attività con un set di dati di input e un set di dati di output: 

![Utilità di pianificazione della disponibilità](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

diagramma di Hello Mostra hello ogni ora per hello sezioni di dati di input e output di set di dati. diagramma di Hello mostra tre intervalli di input che sono pronti per l'elaborazione. attività 10: 11 AM Hello è in corso, producendo una sezione di output di hello 10 11 AM. 

È possibile accedere a intervallo di tempo hello associata utilizzando variabili di intervallo corrente di hello hello set di dati JSON: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) e [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables). Analogamente, è possibile accedere intervallo di tempo hello associata a una finestra attività utilizzando hello WindowStart e WindowEnd. pianificazione di Hello di un'attività deve corrispondere pianificazione hello del set di dati per l'attività hello output di hello. Pertanto, hello SliceStart e SliceEnd valori sono hello stesso come valori WindowStart e WindowEnd rispettivamente. Per altre informazioni su queste variabili, vedere gli articoli [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md#data-factory-system-variables).  

È possibile usare queste variabili per scopi diversi nel file JSON dell'attività. Ad esempio, è possibile utilizzare tali dati tooselect di input e output set di dati che rappresenta dati della serie temporale (ad esempio: 8 AM too9 AM). Questo esempio Usa anche **WindowStart** e **WindowEnd** tooselect dati rilevanti per un'attività Esegui e copiarlo tooa blob con hello appropriato **folderPath**. Hello **folderPath** è toohave con parametri di una cartella separata per ogni ora.  

In hello sopra riportato, pianificazione hello specificata per il set di dati di input e output è hello stesso (ogni ora). Se il set di dati input hello per attività hello è disponibile una frequenza diversa, ad esempio ogni 15 minuti, attività hello che produce questo set di dati di output esegue ancora una volta all'ora come set di dati output hello quali unità hello pianificazione dell'attività. Per altre informazioni, vedere [Modellare i set di dati con frequenze diverse](#model-datasets-with-different-frequencies).

## <a name="dataset-availability-and-policies"></a>Disponibilità e criteri dei set di dati
È stato illustrato l'utilizzo di hello di frequenza e l'intervallo di proprietà nella sezione di disponibilità hello della definizione di set di dati. Esistono alcune altre proprietà che influiscono sulla pianificazione hello e l'esecuzione di un'attività. 

### <a name="dataset-availability"></a>Disponibilità dei set di dati 
Hello nella tabella seguente vengono descritte le proprietà è possibile utilizzare in hello **disponibilità** sezione:

| Proprietà | Descrizione | Obbligatorio | Default |
| --- | --- | --- | --- |
| frequency |Specifica l'unità di tempo hello per la produzione di sezione set di dati.<br/><br/><b>Frequenza supportata</b>: minuto, ora, giorno, settimana, mese |Sì |ND |
| interval |Specifica un moltiplicatore per la frequenza.<br/><br/>"Intervallo di frequenza x" determina la frequenza con cui hello sezione viene prodotta.<br/><br/>Se è necessario hello toobe dataset sezionati su base oraria, impostare <b>frequenza</b> troppo<b>ora</b>, e <b>intervallo</b> troppo<b>1</b>.<br/><br/><b>Nota</b>: se si specifica Frequency come Minute, si consiglia di impostare hello intervallo toono inferiore a 15 |Sì |ND |
| style |Specifica se la sezione hello deve essere prodotta all'hello inizio/fine dell'intervallo "hello".<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Se Frequency è impostato tooMonth e style è impostato tooEndOfInterval, hello sezione viene prodotta hello ultimo giorno del mese. Se lo stile di hello è impostato tooStartOfInterval, hello sezione viene prodotta hello primo giorno del mese.<br/><br/>Se Frequency è impostato tooDay e style è impostato tooEndOfInterval, sezione hello viene prodotta nell'ultima ora del giorno hello hello.<br/><br/>Se Frequency è impostato tooHour e style è impostato tooEndOfInterval, sezione hello viene prodotta alla fine hello ora hello. Ad esempio, per una sezione per periodo 1 PM – 2 PM, sezione di hello viene prodotta alle 14.00. |No |EndOfInterval |
| anchorDateTime |Definisce una posizione assoluta di hello in utilizzata dai limiti di sezione dell'utilità di pianificazione toocompute set di dati. <br/><br/><b>Nota</b>: se hello AnchorDateTime ha parti di date più granulari frequenza hello in hello parti più granulari verranno ignorate. <br/><br/>Ad esempio, se hello <b>intervallo</b> è <b>oraria</b> (frequenza: ora e intervallo: 1) e hello <b>AnchorDateTime</b> contiene <b>minuti e secondi</b>, quindi hello <b>minuti e secondi</b> parti di hello AnchorDateTime verranno ignorate. |No |01/01/0001 |
| offset |Intervallo di tempo da cui hello iniziale e finale di tutte le sezioni di set di dati vengono spostati. <br/><br/><b>Nota</b>: se vengono specificati sia anchorDateTime che offset, il risultato di hello è MAIUSC hello combinato. |No |ND |

### <a name="offset-example"></a>Esempio di offset
Per impostazione predefinita, le sezioni giornaliere (`"frequency": "Day", "interval": 1`) iniziano alle 00:00, mezzanotte, ora UTC. Se si desidera hello inizio ora toobe 6: 00 UTC ora invece, impostare hello offset come illustrato nel seguente frammento di codice hello: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Esempio di anchorDateTime
Nell'esempio seguente di hello, hello set di dati viene prodotta una volta ogni 23 ore. Hello prima sezione viene avviata in fase di hello specificato da anchorDateTime hello, che è stato impostato troppo`2017-04-19T08:00:00` (ora UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Esempio di offset/style
è un set di dati mensili Hello seguente set di dati e viene prodotta 3 ° di ogni mese alle ore 8:00 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>Criteri di set di dati
Un set di dati è stato definito un criterio di convalida che specifica come dati hello generati dall'esecuzione di una sezione possono essere convalidati prima che sia pronto per l'utilizzo. In questi casi, al termine dell'esecuzione, sezione hello hello output sezione stato viene modificato troppo**in attesa** con uno stato secondario di **convalida**. Una volta convalidate sezioni hello, lo stato della sezione hello modificato anche**pronto**. Se una sezione di dati è stato prodotto ma non ha superato la convalida di hello, esecuzioni di attività per sezioni downstream che dipendono da questa sezione non vengono elaborati. [Monitorare e gestire le pipeline](data-factory-monitor-manage-pipelines.md) copre hello vari stati di sezioni di dati in Data Factory.

Hello **criteri** sezione nella definizione di set di dati definisce i criteri di hello o condizione hello hello sezioni di set di dati è necessario soddisfare. Hello nella tabella seguente vengono descritte le proprietà è possibile utilizzare in hello **criteri** sezione:

| Nome criterio | Descrizione | Troppo applicato| Obbligatorio | Default |
| --- | --- | --- | --- | --- |
| minimumSizeMB | Convalida i dati di hello un **blob di Azure** hello di soddisfa i requisiti di dimensioni minime (in megabyte). |BLOB Azure |No |ND |
| minimumRows | Convalida i dati di hello un **database SQL di Azure** o **tabella Azure** contiene hello numero minimo di righe. |<ul><li>Database SQL di Azure</li><li>tabella di Azure</li></ul> |No |ND |

#### <a name="examples"></a>esempi
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

Per altre informazioni sulle proprietà e gli esempi precedenti, vedere l'articolo [Creare i set di dati](data-factory-create-datasets.md). 

## <a name="activity-policies"></a>Criteri di attività
Criteri influiscono sul comportamento di hello in fase di esecuzione di un'attività, in particolare quando viene elaborata la sezione hello di una tabella. Hello nella tabella seguente fornisce dettagli hello.

| Proprietà | Valori consentiti | Valore predefinito | Descrizione |
| --- | --- | --- | --- |
| Concorrenza |Integer  <br/><br/>Valore massimo: 10 |1 |Numero di esecuzioni simultanee dell'attività hello.<br/><br/>Determina il numero di hello di esecuzioni di attività parallele che possono verificarsi in sezioni diverse. Ad esempio, se un'attività deve toogo tramite un ampio set di dati disponibili, un valore maggiore di concorrenza di velocizzare l'elaborazione dati hello. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Determina hello ordinamento delle sezioni di dati che vengono elaborate.<br/><br/>Ad esempio nel caso in cui si abbiano 2 sezioni, una alle 16.00 e l'altra alle 17.00, ed entrambe siano in attesa di esecuzione. Se si imposta executionPriorityOrder di hello toobe NewestFirst, slice hello 17: 00 viene elaborata per prima. Allo stesso modo se si imposta executionPriorityORder di hello toobe OldestFIrst, viene elaborato sezione hello 4 ore. |
| retry |Integer <br/><br/>Valore massimo: 10 |0 |Numero di tentativi prima dell'elaborazione dei dati di hello per sezione hello è contrassegnato come errore. Esecuzione di attività per una sezione di dati viene ripetuta backup toohello specificato numero di tentativi. Riprova Hello viene eseguito appena possibile dopo l'errore hello. |
| timeout |TimeSpan |00:00:00 |Timeout per l'attività hello. Esempio: 00:10:00 (implica un timeout di 10 minuti)<br/><br/>Se un valore viene omesso o è 0, hello timeout è infinito.<br/><br/>Se il tempo di elaborazione di dati hello in una sezione supera il valore di timeout di hello, viene annullata e sistema hello tenta l'elaborazione di hello tooretry. numero di tentativi di Hello dipende dalla proprietà retry hello. Quando si verifica il timeout, hello stato tooTimedOut. |
| delay |TimeSpan |00:00:00 |Specificare il ritardo di hello prima dell'elaborazione di dati di hello sezione inizia.<br/><br/>esecuzione di Hello dell'attività per una sezione di dati viene avviata dopo hello ritardo passato hello previsto tempo di esecuzione.<br/><br/>Esempio: 00:10:00 (implica un ritardo di 10 minuti) |
| longRetry |Integer <br/><br/>Valore massimo: 10 |1 |numero di Hello di long tentativi prima dell'esecuzione della sezione hello è non è riuscito.<br/><br/>I tentativi longRetry sono distanziati da longRetryInterval. Pertanto, se è necessario toospecify un intervallo tra tentativi, usare quindi longRetry. Se vengono specificati Retry e longRetry, ogni tentativo longRetry include nuovi tentativi e numero massimo di tentativi di hello è Riprova * longRetry.<br/><br/>Ad esempio, se si dispone delle seguenti impostazioni in criteri attività hello hello:<br/>Retry: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Si supponga che sia presente solo una sezione tooexecute (lo stato è in attesa) e l'esecuzione dell'attività hello ha esito negativo di ogni volta. All’inizio vi saranno tre tentativi di esecuzione consecutivi. Dopo ogni tentativo, lo stato della sezione hello sarà Retry. Dopo aver innanzitutto 3 tentativi di failover, lo stato della sezione hello sarebbe LongRetry.<br/><br/>Dopo un'ora (vale a dire il valore di longRetryInteval), verrà eseguita un'altra serie di 3 tentativi di esecuzione consecutivi. Successivamente, lo stato della sezione hello sarà Failed e non più necessario tentativi. Quindi, sono stati eseguiti 6 tentativi.<br/><br/>Se qualsiasi esecuzione ha esito positivo, lo stato della sezione hello sarà Ready e non più tentativi.<br/><br/>longRetry possono essere utilizzati in situazioni in cui dipendenti dati arrivano a volte non deterministica o hello ambiente generale non è affidabile in cui l'elaborazione dei dati si verifica. In questi casi, potrebbe non aiutare eseguire tentativi uno dopo l'altro e in questo modo, dopo un intervallo di risultati in fase di hello desiderato output.<br/><br/>Attenzione: non impostare valori elevati per longRetry o longRetryInterval. In genere, valori più elevati comportano altri problemi sistemici. |
| longRetryInterval |TimeSpan |00:00:00 |ritardo Hello tra nuovi tentativi lunghi |

Per altre informazioni, vedere l'articolo [Pipeline](data-factory-create-pipelines.md). 

## <a name="parallel-processing-of-data-slices"></a>Elaborazione parallela delle sezioni di dati
È possibile impostare la data di inizio hello per pipeline hello in hello precedente. Quando si esegue questa operazione, Data Factory Calcola (riempimenti indietro) tutte le sezioni di dati in hello ultimi automaticamente e inizia l'elaborazione. Ad esempio: se si crea una pipeline con data di inizio 2017-04-01 e hello data corrente è 2017-04-10. Se l'output ritmo hello di hello set di dati è ogni giorno, Data Factory avvia l'elaborazione di tutte le sezioni di hello da 2017-04-01 too2017-04-09 immediatamente perché hello data di inizio è hello precedente. Hello sezione da 2017-04-10 non viene elaborata ancora perché il valore di hello della proprietà di stile nella sezione di disponibilità hello EndOfInterval per impostazione predefinita. Hello sezione meno recente viene elaborato per primo come valore predefinito di hello valore executionPriorityOrder è OldestFirst. Per una descrizione della proprietà di stile hello, vedere [disponibilità dataset](#dataset-availability) sezione. Per una descrizione della sezione executionPriorityOrder hello, vedere hello [criteri attività](#activity-policies) sezione. 

È possibile configurare toobe sezioni di dati riempito back elaborati in parallelo da hello impostazione **concorrenza** proprietà hello **criteri** sezione del formato JSON dell'attività hello. Questa proprietà determina il numero di hello di esecuzioni di attività parallele che possono verificarsi in sezioni diverse. il valore predefinito Hello per la proprietà di concorrenza hello è 1. Pertanto, per impostazione predefinita viene elaborata una sola sezione alla volta. valore massimo Hello è 10. Quando una pipeline deve toogo tramite un ampio set di dati disponibili, un valore maggiore di concorrenza di velocizzare l'elaborazione dati hello. 

## <a name="rerun-a-failed-data-slice"></a>Nuova esecuzione di una sezione di dati non riuscita
Quando si verifica un errore durante l'elaborazione di una sezione di dati, è possibile scoprire perché non è riuscita l'elaborazione di hello di una sezione utilizzando pannelli portali Azure o i Monitor e gestire App. Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline con i pannelli del portale di Azure](data-factory-monitor-manage-pipelines.md) o [App di monitoraggio e gestione](data-factory-monitor-manage-app.md).

Prendere in considerazione hello seguente esempio, due attività. Activity1 e Activity 2. Activity1 utilizza una sezione di Dataset1 e produce una sezione del set di dati 2, che viene utilizzata come input dal Activity2 tooproduce una sezione di hello set di dati finale.

![Sezione non riuscita](./media/data-factory-scheduling-and-execution/failed-slice.png)

Hello diagramma viene mostrato che da tre sezioni di recente, si è verificato una sezione di 9 10 AM errore produzione hello per Dataset2. Data Factory rileva automaticamente le dipendenze per set di dati serie hello ora. Di conseguenza, non viene avviato per intervallo di hello AM 9-10 a valle di esecuzione dell'attività hello.

Strumenti di gestione e monitoraggio di Factory dati consentono di organizzare toodrill in log di diagnostica hello per la radice hello hello sezione tooeasily trova causare per problema hello e risolvere il problema. Dopo avere risolto il problema di hello, è possibile avviare facilmente attività hello eseguire tooproduce hello sezione. Per ulteriori informazioni su come toorerun e comprendere le transizioni di stato per le sezioni di dati, vedere [monitoraggio e gestione delle pipeline utilizzando pannelli portali Azure](data-factory-monitor-manage-pipelines.md) o [monitoraggio e gestione di app](data-factory-monitor-manage-app.md).

Dopo che si esegue nuovamente hello 9 10 AM sezionare per **Dataset2**, Data Factory avvia hello eseguita per sezione di hello AM 9 10 dipendenti hello set di dati finale.

![Nuova esecuzione di una sezione non riuscita](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>Attività multiple in una pipeline
È possibile avere più di un'attività in una pipeline. Se si dispone di più attività in una pipeline e output di hello di un'attività non è un input di un'altra attività, le attività di hello possono essere eseguite in parallelo se gli intervalli di dati di input per le attività di hello pronti.

È possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. è possibile l'attività di Hello in hello stessa pipeline o in una pipeline diverse. seconda attività Hello viene eseguita solo quando hello prima uno completata correttamente.

Si consideri ad esempio hello caso in cui una pipeline ha due attività seguenti:

1. L'attività A1, che richiede il set di dati di input esterno D1 e produce il set di dati di output D2.
2. L'attività A2, che richiede l'input del set di dati D2 e produce il set di dati di output D3.

In questo scenario, l'attività A1 e A2 sono in hello stessa pipeline. attività Hello che a1 viene eseguito quando sono disponibili dati esterni hello e frequenza disponibilità hello pianificata viene raggiunto. Hello attività A2 viene eseguito quando hello intervalli pianificati da D2 diventano disponibili e hello frequenza disponibilità pianificata viene raggiunto. Se si verifica un errore in uno degli intervalli di hello nel set di dati D2, A2 non viene eseguito per tale sezione finché diventa disponibile.

Hello vista diagramma con entrambe le attività in hello stessa pipeline avrà un aspetto analogo hello seguente diagramma:

![Concatenamento di attività in hello stessa pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

Come accennato in precedenza, potrebbe essere attività hello nella pipeline diverse. In tale scenario, vista diagramma hello sarebbe simile hello seguente diagramma:

![Concatenamento di attività in due pipeline](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

Vedere hello [copiare in sequenza](#copy-sequentially) sezione Appendice hello per un esempio.

## <a name="model-datasets-with-different-frequencies"></a>Modellare i set di dati con frequenze diverse
Negli esempi di hello, le frequenze di hello per input e output set di dati e hello attività periodi pianificati sono stati hello stesso. Alcuni scenari richiedono l'output di tooproduce hello possibilità a una frequenza diversa da frequenze hello di uno o più input. Data Factory supporta la modellazione di questi scenari.

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>Esempio 1: Generazione di un report di output giornaliero per i dati di input, disponibile ogni ora
Si consideri uno scenario in cui i dati delle misurazioni di input dei sensori sono disponibili ogni ora nell'archiviazione BLOB di Azure. Si desidera tooproduce un report giornaliero di aggregazione con statistiche, ad esempio Media, massimo e minimo per il giorno hello con [attività hive di Data Factory](data-factory-hive-activity.md).

Ecco come modellare questo scenario con Data Factory:

**Set di dati di input**

Hello input ogni ora vengono eliminati i file nella cartella hello hello giorno specificato. Il valore di disponibilità per l'input è impostato su **Hour** (frequency: Hour, interval: 1).

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Set di dati di output**

Viene creato ogni giorno di un file di output nella cartella hello del giorno. Il valore di disponibilità per l'output è impostato su **Day** (frequency: Day, interval: 1).

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Attività: attività Hive in una pipeline**

script hive Hello riceve hello appropriato *DateTime* informazioni come parametri che utilizzano hello **WindowStart** variabile, come illustrato nel seguente frammento di codice hello. script hive Hello utilizza questi dati di hello tooload variabile dalla cartella corretta hello per giorno hello ed eseguire l'output di hello aggregazione toogenerate hello.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

Hello diagramma seguente illustra uno scenario di hello da un punto di vista di dipendenza dei dati.

![Dipendenza dei dati](./media/data-factory-scheduling-and-execution/data-dependency.png)

sezione di output di Hello per ogni giorno dipende da 24 orarie sezioni da un set di dati di input. Data Factory calcola queste dipendenze automaticamente, immaginando hello porzioni di dati di input che rientrano in hello stesso periodo di tempo come hello toobe sezione output generato. Se una delle sezioni di input hello 24 non è disponibile, Data Factory attende hello sezione input toobe pronto prima di avviare l'esecuzione dell'attività giornaliera hello.

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>Esempio 2: Definizione di una dipendenza con espressioni e funzioni di Data Factory
Si consideri ora un altro scenario Si supponga di avere un'attività Hive che elabora i due set di dati di input. Uno di questi dispone di nuovi dati ogni giorno, mentre l'altro li riceve ogni settimana. Si supponga che si desiderava toodo un join tra due input hello e produrre un output di ogni giorno.

un approccio di Hello in cui Data Factory automaticamente fascicolazione input di destra hello seziona tooprocess allineando output toohello periodo tempo della sezione di dati non funziona.

È necessario specificare che per ogni esecuzione dell'attività, hello Data Factory deve usare la sezione di dati della settimana scorsa per hello settimanale input set di dati. Si utilizzano funzioni di Data Factory di Azure, come illustrato nel seguente frammento di codice tooimplement hello questo comportamento.

**Input1: BLOB di Azure**

Hello primo input del blob di Azure hello viene aggiornata ogni giorno.

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Input2: BLOB di Azure**

Input2 è hello blob di Azure viene aggiornato settimanalmente.

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**Output: BLOB di Azure**

Ogni giorno viene creato un file di output nella cartella hello per giorno hello. Disponibilità di output è troppo**giorno** (frequenza: Day, intervallo: 1).

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Attività: attività Hive in una pipeline**

attività hive Hello accetta hello due input e produce una sezione di output ogni giorno. È possibile specificare toodepend sezione output di ogni giorno in hello porzione di input della settimana precedente per l'input settimanale, come indicato di seguito.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

Per un elenco di funzioni e variabili di sistema supportate da Data Factory, vedere l'articolo [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md) .

## <a name="appendix"></a>Appendice

### <a name="example-copy-sequentially"></a>Esempio: copiare in sequenza
È possibile toorun più operazioni di copia uno dopo l'altro in modo sequenziale o ordinato. Ad esempio, potrebbe essere due copia le attività di input in una pipeline (CopyActivity1 e CopyActivity2) con hello seguente dati output set di dati:   

CopyActivity1

Input: Dataset. Output: Dataset2.

CopyActivity2

Input: Dataset2.  Output: Dataset3.

CopyActivity2 viene eseguito solo se è stata eseguita correttamente hello CopyActivity1 e Dataset2 è disponibile.

Di seguito è riportata la pipeline di esempio hello JSON:

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

Si noti che nell'esempio hello, il set di dati di hello output di hello prima attività di copia (Dataset2) è specificato come input per la seconda attività hello. Pertanto, hello seconda attività viene eseguita solo quando il set di dati di hello output dalla prima attività hello è pronto.  

Nell'esempio hello CopyActivity2 può avere un input diverso, ad esempio Dataset3, ma è specificare Dataset2 come un input tooCopyActivity2, in modo attività hello non viene eseguito fino al completamento CopyActivity1. ad esempio:

CopyActivity1

Input: Dataset1. Output: Dataset2.

CopyActivity2

Input: Dataset3, Dataset2. Output: Dataset4.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

Si noti che nell'esempio hello, due set di dati di input specificati per attività di copia secondo hello. Quando vengono specificate più input, viene utilizzato solo hello primo input set di dati per la copia dei dati, ma altri set di dati vengono utilizzati come dipendenze. CopyActivity2 inizi solo dopo hello seguenti condizioni:

* L’esecuzione di CopyActivity1 è riuscita e Dataset2 è disponibile. Questo set di dati non viene utilizzato quando si copiano dati tooDataset4. La sua funzione è semplicemente quella di pianificare la dipendenza per CopyActivity2.   
* Dataset3 è disponibile. Questo set di dati rappresenta dati hello destinazione toohello copiato. 
