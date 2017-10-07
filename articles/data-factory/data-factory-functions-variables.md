---
title: aaaData Factory funzioni e variabili di sistema | Documenti Microsoft
description: Fornisce un elenco delle funzioni e delle variabili di sistema di Azure Data Factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a>Azure Data Factory - Funzioni e variabili di sistema
In questo articolo vengono fornite informazioni sulle funzioni e le variabili supportate da Azure Data Factory.

## <a name="data-factory-system-variables"></a>Variabili di sistema di Data Factory
| Nome variabile | Descrizione | Ambito dell'oggetto | Ambito JSON e casi d'uso |
| --- | --- | --- | --- |
| WindowStart |Inizio dell'intervallo di tempo relativo alla finestra di esecuzione dell'attività |attività |<ol><li>Definizione delle query di selezione dei dati. Vedere connettore articoli a cui fa riferimento in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo.</li> |
| WindowEnd |Fine dell'intervallo di tempo relativo alla finestra di esecuzione dell'attività |attività |uguale a WindowStart. |
| SliceStart |Inizio dell'intervallo di tempo relativo alla sezione di dati in fase di produzione |attività<br/>attività |<ol><li>Definizione di nomi di file e percorsi di cartelle dinamici durante l'uso dell'[archivio BLOB di Azure](data-factory-azure-blob-connector.md) e dei [set di dati del file system](data-factory-onprem-file-system-connector.md).</li><li>Definizione delle dipendenze di input con le funzioni della data factory nella raccolta di input dell'attività.</li></ol> |
| SliceEnd |Fine dell'intervallo di tempo relativo alla sezione di dati corrente. |attività<br/>dataset |uguale a SliceStart. |

> [!NOTE]
> Attualmente è necessario tale hello pianificare hello specificato nella data factory di attività corrisponde esattamente alla pianificazione di hello specificata nella disponibilità di dataset di output di hello. Pertanto, WindowStart, WindowEnd e SliceStart e SliceEnd sempre eseguito il mapping toohello stesso tempo periodo e una sezione singolo output.
> 

### <a name="example-for-using-a-system-variable"></a>Esempio di uso di una variabile di sistema
Nel seguente esempio, anno, mese, giorno e ora di hello **SliceStart** vengono estratti in variabili distinte che vengono utilizzate da **folderPath** e **fileName** proprietà.

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a>Funzioni di Data Factory
È possibile utilizzare funzioni nella data factory e le variabili di sistema per hello seguenti scopi:

1. Specifica di query di selezione dei dati (vedere connettore articoli a cui fa riferimento hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo.
   
   Hello tooinvoke sintassi è una funzione di data factory:  **$$ <function>**  per query di selezione dei dati e altre proprietà in attività hello e set di dati.  
2. Definizione delle dipendenze di input con le funzioni della data factory nella raccolta di input dell'attività.
   
    La sintassi $$ non è necessaria per definire le espressioni delle dipendenze di input.     

Nel seguente esempio, hello **sqlReaderQuery** proprietà in un file JSON viene assegnato il valore di tooa restituito da hello `Text.Format` (funzione). In questo esempio utilizza inoltre una variabile di sistema denominata **WindowStart**, che rappresenta l'ora di inizio hello della finestra di esecuzione dell'attività hello.

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

Vedere l'argomento [Stringhe di formato di data e ora personalizzato](https://msdn.microsoft.com/library/8kb3ddd4.aspx) che descrive diverse opzioni di formattazione che è possibile usare, ad esempio: aa e aaaa. 

### <a name="functions"></a>Funzioni
le tabelle seguenti Hello Elenca tutte le funzioni hello nella Data Factory di Azure:

| Categoria | Funzione | Parametri | Descrizione |
| --- | --- | --- | --- |
| Time |AddHours(X,Y) |X: DateTime  <br/><br/>Y: int |Aggiunge Y ore toohello momento X. <br/><br/>Esempio: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM` |
| Time |AddMinutes(X,Y) |X: DateTime  <br/><br/>Y: int |Aggiunge Y minuti tooX.<br/><br/>Esempio: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM` |
| Time |StartOfHour(X) |X: DateTime  |Ottiene hello avvio per ora hello rappresentato dal componente di ora hello di X. <br/><br/>Esempio: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM` |
| Data |AddDays(X,Y) |X: DateTime <br/><br/>Y: int |Aggiunge Y giorni tooX. <br/><br/>Esempio: 9/15/2013 12:00:00 PM + 2 giorni = 9/17/2013 12:00:00 PM.<br/><br/>È possibile anche sottrarre giorni specificando Y come un numero negativo.<br/><br/>Esempio: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`. |
| Data |AddMonths(X,Y) |X: DateTime <br/><br/>Y: int |Aggiunge Y mesi tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.<br/><br/>È possibile anche sottrarre mesi specificando Y come un numero negativo.<br/><br/>Esempio: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.|
| Data |AddQuarters(X,Y) |X: DateTime  <br/><br/>Y: int |Aggiunge Y * 3 mesi tooX.<br/><br/>Esempio: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM` |
| Data |AddWeeks(X,Y) |X: DateTime <br/><br/>Y: int |Aggiunge Y * 7 giorni tooX<br/><br/>Esempio: 15/09/2013 12:00:00 + 1 settimana = 22/09/2013 12:00:00<br/><br/>È possibile anche sottrarre settimane specificando Y come un numero negativo.<br/><br/>Esempio: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`. |
| Data |AddYears(X,Y) |X: DateTime <br/><br/>Y: int |Aggiunge Y anni tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/>È possibile anche sottrarre anni specificando Y come un numero negativo.<br/><br/>Esempio: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`. |
| Data |Day(X) |X: DateTime |Ottiene il componente giorno hello di X.<br/><br/>Esempio: `Day of 9/15/2013 12:00:00 PM is 9`. |
| Data |DayOfWeek(X) |X: DateTime |Ottiene hello componente giorno della settimana di X.<br/><br/>Esempio: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`. |
| Data |DayOfYear(X) |X: DateTime |Ottiene il giorno hello nell'anno hello rappresentato dal componente anno hello di X.<br/><br/>Esempi:<br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| Data |DaysInMonth(X) |X: DateTime |Ottiene i giorni hello nel mese di hello rappresentato dal componente di mese di hello del parametro X.<br/><br/>Esempio: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`. |
| Data |EndOfDay(X) |X: DateTime |Ottiene data e ora di hello che rappresenta la fine del giorno hello (componente giorno) x hello.<br/><br/>Esempio: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`. |
| Data |EndOfMonth(X) |X: DateTime |Ottiene hello fine del mese hello rappresentato dal componente di mese del parametro X. <br/><br/>Esempio: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (data e ora che rappresenta la fine del mese di settembre hello) |
| Date |StartOfDay(X) |X: DateTime |Ottiene l'inizio di hello del giorno hello rappresentato dal componente giorno hello del parametro X.<br/><br/>Esempio: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`. |
| DateTime |From(X) |X: String |Analizzare la stringa X tooa data ora. |
| DateTime |Ticks(X) |X: DateTime |Ottiene i segni di graduazione hello proprietà del parametro hello X. Un tick è uguale a 100 nanosecondi. il valore di Hello di questa proprietà rappresenta il numero di hello di segni di graduazione che sono trascorsi dalla mezzanotte 12:00:00 del 1 ° gennaio 0001. |
| Text |Format(X) |X: variabile stringa |Formati di testo di hello (utilizzare `\\'` tooescape combinazione `'` carattere).|

> [!IMPORTANT]
> Quando si utilizza una funzione all'interno di un'altra funzione, non è necessario toouse  **$$**  prefisso per la funzione interna hello. Ad esempio: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)). In questo esempio, si noti che  **$$**  prefisso non viene utilizzato per hello **Time.AddHours** (funzione). 

#### <a name="example"></a>Esempio
In hello vengono determinati i seguenti parametri di esempio di input e output per l'attività Hive hello utilizzando hello `Text.Format` SliceStart variabili di sistema e di funzione. 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a>Esempio 2

Nell'esempio seguente di hello, hello parametro DateTime per l'attività Stored Procedure viene determinato tramite hello testo hello. Formattare la funzione e hello SliceStart variabile. 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a>Esempio 3
dati tooread dal giorno precedente anziché giorno rappresentato dal hello SliceStart, funzione hello AddDays come illustrato nell'esempio seguente hello: 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
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

Vedere l'argomento [Stringhe di formato di data e ora personalizzato](https://msdn.microsoft.com/library/8kb3ddd4.aspx) che descrive diverse opzioni di formattazione che è possibile usare, ad esempio: AA e aaaa. 

