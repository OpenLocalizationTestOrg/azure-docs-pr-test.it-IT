---
title: esempi di aaaQuery per i modelli di utilizzo comune in flusso Analitica | Documenti Microsoft
description: Modelli di query comuni di Analisi di flusso di Azure
keywords: esempi di query
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>Esempi di query per modelli di uso comune di Analisi di flusso
## <a name="introduction"></a>Introduzione
Le query in Analisi di flusso di Azure sono espresse in un linguaggio di query di tipo SQL. Queste query sono documentate in hello [flusso Analitica riferimenti al linguaggio di query](https://msdn.microsoft.com/library/azure/dn834998.aspx) Guida. Questo articolo vengono illustrati soluzioni tooseveral comuni modelli di query, in base a scenari reali. È un lavoro in corso e continua toobe aggiornato con nuovi modelli in maniera continuativa.

## <a name="query-example-convert-data-types"></a>Esempio di query: convertire tipi di dati
**Descrizione**: definire i tipi di hello di proprietà nel flusso di input hello.
Ad esempio, peso car hello proviene nel flusso di input hello come stringhe e deve toobe convertito è troppo**INT** tooperform **somma** , configurarlo.

**Input**:

| Casa automobilistica | Tempo | Peso |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |"1000" |
| Honda |2015-01-01T00:00:02.0000000Z |"2000" |

**Output**:

| Casa automobilistica | Peso |
| --- | --- |
| Honda |3000 |

**Soluzione**:

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**SPIEGAZIONE**: utilizzare un **CAST** istruzione hello **peso** campo toospecify il tipo di dati. Vedere hello elenco dei tipi di dati supportati in [tipi di dati (Analitica del flusso di Azure)](https://msdn.microsoft.com/library/azure/dn835065.aspx).

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a>Esempio di query: utilizzare Like o Not like toodo criteri di ricerca
**Descrizione**: verificare che il valore di un campo evento hello corrisponde a un determinato modello.
Ad esempio, verificare che il risultato di hello restituisca targa che iniziare con una lettera e terminare con 9.

**Input**:

| Casa automobilistica | Targa | Tempo |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Output**:

| Casa automobilistica | Targa | Tempo |
| --- | --- | --- |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Soluzione**:

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

**SPIEGAZIONE**: hello utilizzare **come** hello toocheck istruzione **LicensePlate** valore del campo. inizi con la lettera A, contenga una stringa di zeri o altri caratteri e termini con 9. 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>Esempio di query: Specificare la logica per i diversi casi/valori (istruzioni CASE)
**Descrizione**: fornire un calcolo diverso per un campo in base un determinato criterio.
Ad esempio, fornire una descrizione della stringa per automobili quanti di hello stesso rendere passato, con un caso speciale di 1.

**Input**:

| Casa automobilistica | Tempo |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output**:

| Auto passate | Tempo |
| --- | --- | --- |
| 1 Honda |2015-01-01T00:00:10.0000000Z |
| 2 Toyota |2015-01-01T00:00:10.0000000Z |

**Soluzione**:

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**SPIEGAZIONE**: hello **CASE** clausola consente tooprovide un calcolo diversi, in base ad alcuni criteri (in questo caso, il conteggio di hello di automobili hello nella finestra di aggregazione hello).

## <a name="query-example-send-data-toomultiple-outputs"></a>Esempio di query: inviare dati toomultiple restituisce
**Descrizione**: trasmissione dati toomultiple output destinazioni da un singolo processo.
Ad esempio, analizzare i dati per un avviso in base a soglie e spazio di archiviazione di tooblob tutti gli eventi.

**Input**:

| Casa automobilistica | Tempo |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output1**:

| Casa automobilistica | Tempo |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output2**:

| Casa automobilistica | Tempo | Conteggio |
| --- | --- | --- |
| Toyota |2015-01-01T00:00:10.0000000Z |3 |

**Soluzione**:

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

**SPIEGAZIONE**: hello **INTO** clausola indica Analitica flusso quali hello restituisce toowrite hello dati toofrom questa istruzione.
Hello prima query è pass-through dei dati di hello è pervenuta tooan output è denominato **ArchiveOutput**.
funzionamento di una query secondo Hello alcune semplici aggregazioni e il filtro, quindi invia i risultati di hello tooa sistema di avvisi a valle.

Si noti che è anche possibile riutilizzare i risultati di hello delle espressioni di tabella comuni hello (CTE) (ad esempio **WITH** istruzioni) in più istruzioni di output. Questa opzione è hello ulteriore vantaggio di apertura di un numero inferiore lettori toohello l'origine di input.
ad esempio: 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a>Esempio di query: contare valori univoci
**Descrizione**: contare il numero di hello di valori di campo univoco che vengono visualizzati nel flusso di hello all'interno di un intervallo di tempo.
Ad esempio, il numero univoco consente di automobili passate casello hello in una finestra di 2 secondi?

**Input**:

| Casa automobilistica | Tempo |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output:**

| Conteggio | Tempo |
| --- | --- |
| 2 |2015-01-01T00:00:02.000Z |
| 1 |2015-01-01T00:00:04.000Z |

**Soluzione:**

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


**Spiegazione:**
**COUNT (DISTINCT rendere)** restituisce hello numero di valori distinct in hello **rendere** colonna all'interno di un intervallo di tempo.

## <a name="query-example-determine-if-a-value-has-changed"></a>Esempio di query: Determinare la potenziale variazione di un valore
**Descrizione**: esaminare un toodetermine valore precedente se è diverso dal valore corrente di hello.
Ad esempio, è Auto precedente hello in hello di strada casello hello che stesso rendere car corrente hello?

**Input**:

| Casa automobilistica | Tempo |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Output**:

| Casa automobilistica | Tempo |
| --- | --- |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Soluzione**:

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

**SPIEGAZIONE**: utilizzare **LAG** toopeek in hello nuovamente un evento flusso di input e ottenere hello **rendere** valore. Confrontare quindi toohello **rendere** valore hello corrente ed evento output hello se sono diversi.

## <a name="query-example-find-hello-first-event-in-a-window"></a>Esempio di query: primo evento hello trova in una finestra
**Descrizione**: auto prima di trovare hello in ogni intervallo di 10 minuti.

**Input**:

| Targa | Casa automobilistica | Tempo |
| --- | --- | --- |
| DXE 5291 |Honda |27-07-2015T00:00:05.0000000Z |
| YZK 5704 |Ford |27-07-2015T00:02:17.0000000Z |
| RMV 8282 |Honda |27-07-2015T00:05:01.0000000Z |
| YHN 6970 |Toyota |27-07-2015T00:06:00.0000000Z |
| VFE 1616 |Toyota |27-07-2015T00:09:31.0000000Z |
| QYF 9358 |Honda |27-07-2015T00:12:02.0000000Z |
| MDR 6128 |BMW |27-07-2015T00:13:45.0000000Z |

**Output**:

| Targa | Casa automobilistica | Tempo |
| --- | --- | --- |
| DXE 5291 |Honda |27-07-2015T00:00:05.0000000Z |
| QYF 9358 |Honda |27-07-2015T00:12:02.0000000Z |

**Soluzione**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

Ora verifichiamo modifica hello problema e individuare hello prima Auto di un particolare in ogni intervallo di 10 minuti.

| Targa | Casa automobilistica | Tempo |
| --- | --- | --- |
| DXE 5291 |Honda |27-07-2015T00:00:05.0000000Z |
| YZK 5704 |Ford |27-07-2015T00:02:17.0000000Z |
| YHN 6970 |Toyota |27-07-2015T00:06:00.0000000Z |
| QYF 9358 |Honda |27-07-2015T00:12:02.0000000Z |
| MDR 6128 |BMW |27-07-2015T00:13:45.0000000Z |

**Soluzione**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a>Esempio di query: ultimo evento hello trova in una finestra
**Descrizione**: auto ultima ricerca di hello in ogni intervallo di 10 minuti.

**Input**:

| Targa | Casa automobilistica | Tempo |
| --- | --- | --- |
| DXE 5291 |Honda |27-07-2015T00:00:05.0000000Z |
| YZK 5704 |Ford |27-07-2015T00:02:17.0000000Z |
| RMV 8282 |Honda |27-07-2015T00:05:01.0000000Z |
| YHN 6970 |Toyota |27-07-2015T00:06:00.0000000Z |
| VFE 1616 |Toyota |27-07-2015T00:09:31.0000000Z |
| QYF 9358 |Honda |27-07-2015T00:12:02.0000000Z |
| MDR 6128 |BMW |27-07-2015T00:13:45.0000000Z |

**Output**:

| Targa | Casa automobilistica | Tempo |
| --- | --- | --- |
| VFE 1616 |Toyota |27-07-2015T00:09:31.0000000Z |
| MDR 6128 |BMW |27-07-2015T00:13:45.0000000Z |

**Soluzione**:

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

**SPIEGAZIONE**: sono disponibili due passaggi nella query hello. Hello prima rileva uno hello più recente timestamp in windows 10 minuti. join di Hello secondo passaggio hello risultati di query prima di hello con hello originale flusso toofind hello eventi che corrispondono ultimo timestamp hello in ogni finestra. 

## <a name="query-example-detect-hello-absence-of-events"></a>Esempio di query: rilevare l'assenza di hello di eventi
**Descrizione**: verificare che un flusso non abbia un valore corrispondente a determinati criteri.
Ad esempio, 2 automobili consecutive da hello che stesso rendere immesse road casello hello all'interno di hello 90 secondi ultimo?

**Input**:

| Casa automobilistica | Targa | Tempo |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Honda |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Toyota |DEF-987 |2015-01-01T00:00:03.0000000Z |
| Honda |GHI-345 |2015-01-01T00:00:04.0000000Z |

**Output**:

| Casa automobilistica | Tempo | Targa auto corrente | Targa prima auto | Tempo prima auto |
| --- | --- | --- | --- | --- |
| Honda |2015-01-01T00:00:02.0000000Z |AAA-999 |ABC-123 |2015-01-01T00:00:01.0000000Z |

**Soluzione**:

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

**SPIEGAZIONE**: utilizzare **LAG** toopeek in hello nuovamente un evento flusso di input e ottenere hello **rendere** valore. Confrontarlo toohello **rendere** hello corrente eventi e output hello se essi sono hello stesso valore. È inoltre possibile utilizzare **LAG** dati tooget su Auto precedente hello.

## <a name="query-example-detect-hello-duration-between-events"></a>Esempio di query: rilevare la durata di hello tra gli eventi
**Descrizione**: trovare hello durata di un determinato evento. Ad esempio, dato un clickstream web, determinare tempo hello dedicato a una funzionalità.

**Input**:  

| Utente | Funzionalità | Evento | Tempo |
| --- | --- | --- | --- |
| user@location.com |RightMenu |Inizia |2015-01-01T00:00:01.0000000Z |
| user@location.com |RightMenu |End |2015-01-01T00:00:08.0000000Z |

**Output**:  

| Utente | Funzionalità | Durata |
| --- | --- | --- |
| user@location.com |RightMenu |7 |

**Soluzione**:

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

**SPIEGAZIONE**: hello utilizzare **ultimo** funzione hello tooretrieve ultima **ora** valore quando il tipo di evento hello **avviare**. Hello **ultimo** funzione Usa **PARTITION BY [user]** tooindicate che hello risultato viene calcolato per ogni utente univoco. query Hello dispone di una soglia massima di 1 ora per la differenza di orario hello tra **avviare** e **arrestare** eventi, ma può essere configurato in base alle esigenze **(limite DURATION(hour, 1)**.

## <a name="query-example-detect-hello-duration-of-a-condition"></a>Esempio di query: rilevare la durata di hello di una condizione
**Descrizione**: individuare la durata di una condizione.
Si supponga, ad esempio, che un bug abbia generato un peso errato per tutte le automobili (oltre 20.000 libbre, pari a 9 tonnellate) Si vuole che la durata di hello toocompute bug hello.

**Input**:

| Casa automobilistica | Tempo | Peso |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |2000 |
| Toyota |2015-01-01T00:00:02.0000000Z |25000 |
| Honda |2015-01-01T00:00:03.0000000Z |26000 |
| Toyota |2015-01-01T00:00:04.0000000Z |25000 |
| Honda |2015-01-01T00:00:05.0000000Z |26000 |
| Toyota |2015-01-01T00:00:06.0000000Z |25000 |
| Honda |2015-01-01T00:00:07.0000000Z |26000 |
| Toyota |2015-01-01T00:00:08.0000000Z |2000 |

**Output**:

| Inizio errore | Fine errore |
| --- | --- |
| 2015-01-01T00:00:02.000Z |2015-01-01T00:00:07.000Z |

**Soluzione**:

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

**SPIEGAZIONE**: utilizzare **LAG** flusso di input hello tooview per 24 ore e cercare istanze where **StartFault** e **StopFault** sono occupati da hello peso < 20000.

## <a name="query-example-fill-missing-values"></a>Esempio di query: immettere i valori mancanti
**Descrizione**: per il flusso di hello di eventi con i valori mancanti, generare un flusso di eventi con intervalli regolari.
Ad esempio, generare un evento ogni 5 secondi che segnala punto dati hello visualizzato più di recente.

**Input**:

| t | value |
| --- | --- |
| "2014-01-01T06:01:00" |1 |
| "2014-01-01T06:01:05" |2 |
| "2014-01-01T06:01:10" |3 |
| "2014-01-01T06:01:15" |4 |
| "2014-01-01T06:01:30" |5 |
| "2014-01-01T06:01:35" |6 |

**Output (prime 10 righe)**:

| windowend | lastevent.t | lastevent.value |
| --- | --- | --- |
| 2014-01-01T14:01:00.000Z |2014-01-01T14:01:00.000Z |1 |
| 2014-01-01T14:01:05.000Z |2014-01-01T14:01:05.000Z |2 |
| 2014-01-01T14:01:10.000Z |2014-01-01T14:01:10.000Z |3 |
| 2014-01-01T14:01:15.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:20.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:25.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:30.000Z |2014-01-01T14:01:30.000Z |5 |
| 2014-01-01T14:01:35.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:40.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:45.000Z |2014-01-01T14:01:35.000Z |6 |

**Soluzione**:

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


**SPIEGAZIONE**: la query seguente genera gli eventi ogni 5 secondi e l'output di hello ultimo evento ricevuto in precedenza. Hello [finestra Hopping](https://msdn.microsoft.com/library/dn835041.aspx "finestra Hopping - Azure flusso Analitica") durata determina la distanza query hello Indietro Cerca toofind evento più recente di hello (300 secondi in questo esempio).

## <a name="get-help"></a>Ottenere aiuto
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

