---
title: Consente di generare script U-SQL aaaExtend con Python in Azure Data Lake Analitica | Documenti Microsoft
description: Informazioni su come codice toorun Python script U-SQL
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Esercitazione: Introduzione all'estensione di U-SQL con Python

Le estensioni di Python per U-SQL consentono agli sviluppatori tooperform massiva l'esecuzione parallela di codice Python. Hello di esempio seguente illustra i passaggi di base hello:

* Hello utilizzare `REFERENCE ASSEMBLY` istruzione tooenable Python estensioni hello Script U-SQL
* Utilizzo di hello `REDUCE` hello toopartition operazione dati su una chiave di input
* le estensioni di Python per U-SQL Hello includono un riduttore incorporato (`Extension.Python.Reducer`) che esegue codice Python in ogni riduttore toohello vertice assegnato
* Hello script U-SQL contiene codice Python incorporato hello che dispone di una funzione denominata `usqlml_main` che accetta un pandas frame di dati come input e restituisce un pandas frame di dati come output.

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a>Come Python si integra con U-SQL

### <a name="datatypes"></a>Tipi di dati

* Le colonne stringa e numeriche di U-SQL vengono convertite come sono tra Pandas e U-SQL
* I valori null U-SQL vengono convertiti tooand da Pandas `NA` valori

### <a name="schemas"></a>Schemi

* I vettori indice di Pandas non sono supportati in U-SQL. Tutti i frame di dati di input nella funzione di Python hello hanno sempre un indice numerico a 64 bit compreso tra 0 e il numero di hello di righe meno 1. 
* I set di dati di U-SQL non possono avere nomi di colonna duplicati.
* Nomi di colonna dei set di dati di U-SQL che non sono stringhe. 

### <a name="python-versions"></a>Versioni di Python
È supportato solo Python 3.5.1 (compilato per Windows). 

### <a name="standard-python-modules"></a>Moduli standard di Python
Tutti i moduli Python standard hello sono inclusi.

### <a name="additional-python-modules"></a>Altri moduli di Python
Oltre alle librerie standard di Python di hello, sono incluse varie librerie python comunemente usate:

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Messaggi di eccezione
Attualmente un'eccezione nel codice Python viene visualizzata come errore di vertice generico. I messaggi di errore di hello processo U-SQL verranno visualizzati hello future, messaggio di eccezione hello Python.

### <a name="input-and-output-size-limitations"></a>Limitazioni delle dimensioni di input e output
Ogni vertice ha una quantità limitata di memoria assegnata tooit. che attualmente corrisponde a 6 GB per AU. Poiché hello frame di dati di input e output devono essere presenti in memoria nel codice Python hello, dimensione totale di hello per hello input e output non può superare 6 GB.

## <a name="see-also"></a>Vedere anche
* [Panoramica di Analisi Data Lake di Microsoft Azure](data-lake-analytics-overview.md)
* [Sviluppare script U-SQL mediante Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Uso delle funzioni finestra di U-SQL per i processi di Analisi Azure Data Lake](data-lake-analytics-use-window-functions.md)

