---
title: aaaSample dati nelle tabelle di Azure HDInsight Hive | Documenti Microsoft
description: Esecuzione del sotto-campionamento dei dati nelle tabelle Hive (Hadoop) di Azure HDInsight
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Dati di esempio nelle tabelle Hive di Azure HDInsight
In questo articolo vengono descritte come toodown-esempio dati archiviati nelle tabelle di Azure HDInsight Hive usano query Hive. Vengono trattati i tre metodi di campionamento utilizzati più frequentemente:

* Campionamento casuale uniforme
* Campionamento casuale per gruppi
* Campionamento stratificato

esempio Hello **menu** collegamenti tootopics che descrivono come toosample dati da diversi ambienti di archiviazione.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Perché campionare i dati?**
Se si prevede di tooanalyze set di dati hello è grande, è in genere un tooreduce di dati di buona toodown esempio hello è tooa più piccolo ma rappresentativo e gestibile dimensioni. Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità. Il relativo ruolo nel processo di analisi scientifica dei dati di Team hello è tooenable rapida la creazione di prototipi di funzioni di elaborazione dei dati hello e modelli di machine learning.

Questa attività di campionamento è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-toosubmit-hive-queries"></a>La modalità query Hive toosubmit
È possibile inviare query hive dalla console di riga di comando Hadoop hello nel nodo head di hello del cluster Hadoop hello. toodo questa operazione, accedere al nodo head di hello del cluster Hadoop hello, aprire console della riga di comando Hadoop hello e inviare query Hive hello da qui. Per istruzioni sull'invio di query Hive nella console della riga di comando Hadoop hello, vedere [come tooSubmit query Hive](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a> Campionamento casuale uniforme
Campionamento casuale Uniform significa che ogni riga nel set di dati hello stessa probabilità di in fase di campionamento. Questo può essere implementata tramite l'aggiunta di un set di dati campo aggiuntivo toohello rand () in query "select" interna hello e hello query "select" esterna tale condizione su quel campo casuale.

Di seguito è fornito un esempio di query:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

In questo caso, `<sample rate, 0-1>` specifica la proporzione di hello di record che gli utenti di hello desiderano toosample.

## <a name="group"></a> Campionamento casuale per gruppi
Quando i dati di campionamento per categoria, è opportuno tooeither includere o escludere tutte le istanze di hello di un valore specifico di una variabile per categoria. Questo è il significato di "campionamento per gruppi".
Ad esempio, se si dispone di una variabile categorica, "Stato", che ha valori NY AG, Canada, NJ, PA, e così via, che si desidera record di hello stesso stato sempre essere insieme, se vengono campionate o non.

Di seguito è presentata una query di esempio che consente di eseguire il campionamento per gruppi:

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a> Campionamento stratificato
Campionamento casuale è stratificato con riguardo tooa categorico variabile quando i valori di categoria che devono di esempi di hello ottenuti in hello stesso rapporto come popolamento padre hello ottenuti dal quale hello esempi. Utilizzando hello stesso esempio precedente, si supponga che i dati con popolazioni secondario gli stati, ad esempio NJ ha 100 osservazioni, NY è 60 osservazioni, e WA con 300 osservazioni. Se la frequenza di hello di campionamento toobe 0,5 stratificata, quindi hello ottenuto deve essere circa 50, 30 e 150 osservazioni di NJ NY e WA rispettivamente.

Di seguito è fornito un esempio di query:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


Per informazioni su metodi di campionamento più avanzati disponibili in Hive, vedere [Campionamento di LanguageManual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).

