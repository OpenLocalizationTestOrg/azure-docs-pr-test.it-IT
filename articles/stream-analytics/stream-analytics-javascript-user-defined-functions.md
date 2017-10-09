---
title: le funzioni definite dall'utente flusso Analitica JavaScript aaaAzure | Documenti Microsoft
description: Eseguire i meccanismi di query avanzate con funzioni JavaScript definite dall'utente
keywords: javascript, funzioni definite dall'utente, udf
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Funzioni JavaScript definite dall'utente in Analisi di flusso di Azure
L'Analisi di flusso di Azure supporta le funzioni definite dall'utente nel linguaggio JavaScript. Ampia gamma di hello di **stringa**, **RegExp**, **matematiche**, **matrice**, e **data** metodi che JavaScript fornisce, le trasformazioni di dati complessi con i processi di flusso Analitica diventano toocreate più semplice.

## <a name="javascript-user-defined-functions"></a>Funzioni JavaScript definite dall'utente
Le funzioni JavaScript definite dall'utente supportano funzioni senza stato e di solo calcolo che non richiedono connettività esterna. Hello restituiscono valore di una funzione può essere solo un valore scalare (singolo). Dopo aver aggiunto un processo di tooa JavaScript funzione definita dall'utente, è possibile utilizzare la funzione hello in qualsiasi punto nella query hello, ad esempio una funzione scalare predefinita.

Ecco alcuni scenari in cui potrebbero essere utili le funzioni JavaScript definite dall'utente:
* Analisi e manipolazione delle stringhe con funzioni di espressione regolare, ad esempio **Regexp_Replace()** e **Regexp_Extract()**
* Decodifica e codifica dati, ad esempio conversione dal formato binario al formato esadecimale
* Esecuzione di calcoli matematici con funzioni JavaScript **Math**
* Esecuzione di operazioni di matrice come ordinamento, aggiunta, ricerca e riempimento

Ecco alcune operazioni non eseguibili con una funzione JavaScript definita dall'utente in Analisi di flusso:
* Chiamate agli endpoint REST esterni, ad esempio per l'esecuzione di una ricerca inversa degli indirizzi IP o per la raccolta di dati di riferimento da un'origine esterna
* Esecuzione della serializzazione o deserializzazione negli input e output di un formato evento personalizzato
* Creazione di aggregazioni personalizzate

Sebbene le funzioni come **Date.GetDate()** o **Math.random()** non sono bloccate nella definizione di funzioni hello, è consigliabile evitare di utilizzarle. Queste funzioni **non** hello restituito stesso risultato ogni volta che vengono chiamati e hello servizio Analitica di flusso di Azure non mantiene una registrazione di chiamate di funzione e ha restituito risultati. Se una funzione restituisce risultati diversi in hello stessi eventi, ripetibilità non è garantito quando un processo viene riavviato dall'utente o dal servizio di flusso Analitica hello.

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>Aggiungere una funzione definita dall'utente di JavaScript nel portale di Azure hello
toocreate una funzione definita dall'utente JavaScript semplice in un processo di flusso Analitica esistente, eseguire questi passaggi:

1.  Nel portale di Azure hello, trovare il processo di flusso Analitica.
2.  In **TOPOLOGIA PROCESSO** selezionare la funzione. Viene visualizzato un elenco vuoto di funzioni.
3.  Selezionare una nuova funzione definita dall'utente, toocreate **Aggiungi**.
4.  In hello **nuova funzione** pannello per **tipo di funzione**selezionare **JavaScript**. Un modello di funzione predefinita viene visualizzata nell'editor di hello.
5.  Per hello **alias funzione definita dall'utente**, immettere **hex2Int**e modifica di implementazione della funzione hello come segue:

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  Selezionare **Salva**. La funzione viene visualizzato nell'elenco di hello di funzioni.
7.  Seleziona hello nuovo **hex2Int** funzione e controllare la definizione di funzione hello. Tutte le funzioni hanno un **funzione definita dall'utente** alias di funzione di prefisso toohello aggiunto. È necessario troppo*includere il prefisso hello* quando si chiama la funzione hello nella query Analitica di flusso. In questo caso, si chiama **UDF.hex2Int**.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>Chiamare una funzione JavaScript definita dall'utente nella query

1. In hello editor di query, in **processo TOPOLOGIA**selezionare **Query**.
2.  Modificare la query e quindi chiamare hello-funzione definita dall'utente, simile al seguente:

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  file di dati di esempio hello tooupload, rapida hello processo input.
4.  tootest della query, seleziona **Test**.


## <a name="supported-javascript-objects"></a>Oggetti JavaScript supportati
Le funzioni JavaScript definite dall'utente in Analisi di flusso di Azure supportano oggetti JavaScript standard e incorporati. Per un elenco di questi oggetti, vedere [Oggetti globali](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).

### <a name="stream-analytics-and-javascript-type-conversion"></a>Conversione dei tipi di Analisi di flusso e JavaScript

Esistono differenze nei tipi di hello che supportano il linguaggio di query flusso Analitica hello e JavaScript. Questa tabella elenca i mapping di conversione hello tra hello due:

Analisi di flusso | JavaScript
--- | ---
bigint | Numero (JavaScript possono rappresentare solo valori interi di tooprecisely 2 ^ 53)
DateTime | Data (JavaScript supporta solo millisecondi)
double | Number
nvarchar(MAX) | string
Record | Oggetto
Array | Array
NULL | Null


Ecco le conversioni da JavaScript ad Analisi di flusso:


JavaScript | Analisi dei flussi
--- | ---
Number | Bigint (se il numero di hello è arrotondamento e tra long. MinValue e long. MaxValue; in caso contrario, viene applicato il doppio)
Date | DateTime
String | nvarchar(MAX)
Oggetto | Record
Array | Array
Null, Undefined | NULL
Qualsiasi altro tipo (ad esempio, una funzione o un errore) | Non supportato (risultati nell'errore di runtime)

## <a name="troubleshooting"></a>Risoluzione dei problemi
Errori di runtime di JavaScript sono considerati irreversibili e resi visibili tramite log attività hello. log hello tooretrieve, nel portale di Azure hello, andare tooyour processo e scegliere **log attività**.


## <a name="other-javascript-user-defined-function-patterns"></a>Altri modelli della funzione JavaScript definita dall'utente

### <a name="write-nested-json-toooutput"></a>Scrivere toooutput JSON nidificata
Se si dispone di un passaggio di completamento di elaborazione che utilizza un processo Analitica di flusso di output come input, ed è necessario un formato JSON, è possibile scrivere un toooutput stringa JSON. esempio Hello chiama hello **JSON.stringify()** funzione toopack tutte le coppie nome/valore di hello di input e quindi li scrivono come un singolo valore stringa nell'output.

**Definizione della funzione JavaScript definita dall'utente:**

```
function main(x) {
return JSON.stringify(x);
}
```

**Query di esempio:**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>Ottenere aiuto
Per ulteriore assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
