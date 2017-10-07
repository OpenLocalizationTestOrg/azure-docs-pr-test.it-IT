---
title: "funzionalità aaaCreate per i dati in un cluster Hadoop usano query Hive | Documenti Microsoft"
description: "Esempi di query Hive che generano funzionalità nei dati archiviati in un cluster HDInsight Hadoop di Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Creare funzionalità per i dati in un cluster Hadoop mediante le query Hive
Questo documento illustra come toocreate funzionalità per i dati archiviati in un cluster Azure HDInsight Hadoop usano query Hive. Queste query Hive usano incorporato Hive funzioni definite dall'utente (UDF), hello per i quali sono i seguenti.

funzionalità di toocreate Hello operazioni necessarie possono essere con utilizzo intensivo della memoria. prestazioni di Hello delle query Hive diventano più importanti in questi casi e possono migliorare tramite l'ottimizzazione di determinati parametri. Hello ottimizzazione di questi parametri è descritta nella sezione finale di hello.

Esempi di query di hello presentati sono specifico toohello [NYC Taxi viaggi dati](http://chriswhong.com/open-data/foil_nyc_taxi/) scenari vengono inoltre forniti [repository GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Queste query già uno schema di dati specificato e sono pronti toobe inviato toorun. Nella sezione finale hello, vengono descritte anche i parametri che gli utenti possono ottimizzare in modo che sia possano migliorare le prestazioni di hello di query Hive.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Questo **menu** collegamenti tootopics che descrivono come toocreate funzionalità per i dati in vari ambienti. Questa attività è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone che l'utente abbia:

* Creato un account di archiviazione di Azure. Per istruzioni, vedere [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Il provisioning di un cluster Hadoop personalizzato con hello servizio HDInsight.  Per istruzioni, vedere [Personalizzazione di cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md).
* dati Hello sono stato caricato tooHive tabelle cluster Azure HDInsight Hadoop. In caso contrario, seguire [carico e creare tabelle di dati tooHive](machine-learning-data-science-move-hive-tables.md) tooupload dati tooHive tabelle prima.
* Cluster toohello di accesso remoto abilitato. Se sono necessarie istruzioni, vedere [hello accesso nodo Head del Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="hive-featureengineering"></a>Creazione di funzionalità
In questa sezione vengono descritti alcuni esempi di modalità hello in cui è possano generare funzionalità usano query Hive. Dopo aver creato le funzionalità aggiuntive, è possibile aggiungerli come tabella di colonne toohello esistente o creare una nuova tabella con le funzionalità aggiuntive di hello e chiave primaria, che quindi può essere unita con la tabella originale hello. Ecco alcuni esempi di hello presentati:

1. [Creazione di funzionalità basata sulla frequenza](#hive-frequencyfeature)
2. [Rischi di variabili di categoria nella classificazione binaria](#hive-riskfeature)
3. [Estrazione delle funzionalità dal campo Datetime](#hive-datefeatures)
4. [Estrazione delle funzionalità dal campo Text](#hive-textfeatures)
5. [Calcolo della distanza tra le coordinate GPS](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>Creazione di funzionalità basata sulla frequenza
È spesso utile toocalculate frequenze di hello di hello livelli di una variabile per categoria o frequenze hello di alcune combinazioni di livelli da più variabili di categoria. Gli utenti possono usare queste frequenze di hello toocalculate script seguenti:

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>Rischi di variabili di categoria nella classificazione binaria
Nella classificazione binaria, è necessario tooconvert le variabili di categoria non numerico in funzioni numeriche in cui viene utilizzati solo i modelli di hello funzioni numeriche. È possibile eseguire questa operazione sostituendo tutti i livelli non numerici con un rischio numerico. In questa sezione vengono illustrati alcuni query Hive generiche che consentono di calcolare valori hello (log-odds) di una variabile per categoria.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

In questo esempio, le variabili `smooth_param1` e `smooth_param2` sono set toosmooth hello rischio valori calcolati dai dati di hello. Rischi devono essere compresi in un intervallo di -Inf e Inf. Rischi > 0 indica che probabilità hello che hello la destinazione sia uguale too1 è maggiore di 0,5.

Dopo aver calcolata la tabella dei rischi hello, gli utenti possono assegnare tabella tooa dei valori di rischio creando un join con la tabella di rischio hello. query di unione Hive Hello è stato specificato nella sezione precedente.

### <a name="hive-datefeatures"></a>Estrazione delle funzionalità dal campo Datetime
In Hive è disponibile un set di funzioni definite dall'utente per elaborare i campi Datetime. Nell'Hive, formato di data/ora predefinito hello è ' aaaa-MM-GG 00:00:00 ' ('1970-01-01-12:21:32 ', ad esempio). In questa sezione vengono indicati esempi in cui estrarre hello giorno del mese, il mese di hello da un campo datetime e altri esempi che converte una stringa di data/ora in un formato diverso di formato predefinita hello predefinito formato tooa datetime della stringa.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

Questa query Hive presuppone che hello *&#60; campo datetime >* è nel formato di datetime hello predefinito.

Se un campo datetime non è nel formato predefinito di hello, è necessario innanzitutto campo datetime di tooconvert hello in indicatore data e ora di Unix e quindi convertire hello Unix ora datetime tooa indicatore di stringa che è predefinita hello formato. Quando hello datetime è predefinita, gli utenti possono applicare le funzionalità di tooextract hello incorporato datetime funzioni definite dall'utente.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

In questa query, se hello *&#60; campo datetime >* ha modello hello like *26/03/2015 12:04:39*, hello *' &#60; modello di campo datetime hello >'* deve essere `'MM/dd/yyyy HH:mm:ss'`. tootest, gli utenti possono eseguire

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

Hello *hivesampletable* in questa query è preinstallato in tutti i cluster di Azure HDInsight Hadoop per impostazione predefinita quando viene effettuato il provisioning di cluster hello.

### <a name="hive-textfeatures"></a>Estrazione delle funzionalità dal campo Text
Quando tabella Hive hello dispone di un campo di testo che contiene una stringa di parole che sono delimitate da spazi, hello nella query seguente estrae lunghezza hello di stringa hello e hello numero di parole nella stringa hello.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>Calcolo della distanza tra le coordinate GPS
query Hello descritte in questa sezione possono essere applicato direttamente toohello NYC Taxi viaggi dati. scopo di Hello di questa query è tooshow come tooapply incorporato funzioni matematiche in Hive toogenerate funzionalità.

campi che vengono utilizzati in questa query Hello vengono coordinate GPS hello prelievo e dropoff percorsi, denominato *prelievo\_longitudine*, *prelievo\_latitudine*,  *dropoff\_longitudine*, e *dropoff\_latitudine*. le query di Hello che calcola hello distanza diretta tra le coordinate di ritiro e dropoff hello sono:

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

equazioni matematiche Hello che consentono di calcolare la distanza hello tra due coordinate GPS possono trovarsi in hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">gli script di tipo mobile</a> sito, creato da Peter Lapisu. In sua Javascript, hello funzione `toRad()` è solo *lat_or_lon*pi/180 *, che converte i gradi tooradians. In questo caso, *lat_or_lon* è longitudine o latitudine hello. Poiché non fornisce la funzione hello Hive `atan2`, ma fornisce la funzione hello `atan`, hello `atan2` viene implementata da `atan` funzione hello sopra query Hive usando fornito nella definizione di hello <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.

![Creare un'area di lavoro](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Un elenco completo delle funzioni definite dall'utente incorporati sono reperibili hello Hive **funzioni predefinite** sezione hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).  

## <a name="tuning"></a>Argomenti avanzati: tooImprove parametri Hive ottimizzazione della velocità delle Query
Hello parametro predefinito delle impostazioni di Hive cluster potrebbero non essere adatte per le query Hive hello e hello di elaborazione query hello. In questa sezione viene illustrato il alcuni parametri che è possono ottimizzare gli utenti che consentono di migliorare le prestazioni di hello delle query Hive. Gli utenti devono parametro hello tooadd ottimizzazione delle query prima di eseguire query hello di elaborazione dei dati.

1. **Lo spazio dell'heap Java**: per le query che includono join grandi set di dati o l'elaborazione di record lunghi, **sta esaurendo lo spazio dell'heap** è un errore comune hello. Questo è possibile ottimizzare l'impostazione dei parametri *mapreduce.map.java.opts* e *mapreduce.task.io.sort.mb* toodesired valori. Di seguito è fornito un esempio:
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    Questo parametro alloca lo spazio dell'heap tooJava memoria 4GB e consente inoltre di ordinamento più efficiente tramite l'allocazione di memoria per tale. Se sono presenti spazi processo errore errori correlati tooheap è tooplay una buona idea con queste allocazioni.

1. **Dimensioni del blocco DFS** : questo parametro imposta hello più piccola unità di dati che hello archivi di sistema di file. Ad esempio, se hello DFS blocco è 128MB, tutti i dati di dimensioni inferiori e backup too128MB vengono quindi archiviati in un unico blocco, mentre i dati che sono maggiori di 128MB assegnata blocchi aggiuntivi. Se si sceglie una dimensione del blocco molto piccolo, sovraccarico di grandi dimensioni in Hadoop poiché hello nome nodo dispone di molte altre richieste toofind hello rilevanti blocco relativi file toohello tooprocess. Un'impostazione consigliata per dati con dimensioni in gigabyte (o più grandi) è:
   
        set dfs.block.size=128m;
2. **Ottimizzare l'operazione di join nell'Hive** : durante le operazioni di join nel framework di riduzione/mappe hello vengono in genere eseguite in hello ridurre fase, in alcuni casi, enormi vantaggi possono essere ottenuti pianificazione join in fase di mapping hello (detto anche "mapjoins"). toodirect Hive toodo questo laddove possibile, è possibile impostare:
   
        set hive.auto.convert.join=true;
3. **Specifica il numero di hello di BizTalk Mapper tooHive** : mentre Hadoop consente di hello tooset hello utente numero riduttori hello di, BizTalk Mapper è in genere non è impostata dall'utente hello. Un espediente che consente un certo grado di controllo a questo numero è variabili Hadoop hello toochoose *mapred.min.split.size* e *mapred.max.split.size* come dimensione hello di ogni mappa attività è determinato da:
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    Hello in genere, il valore predefinito di *mapred.min.split.size* è 0, che di *mapred.max.split.size* è **Long.MAX** e quello di *dfs.block.size* è di 64MB. Come possiamo vedere, dimensioni dei dati specificato hello ottimizzazione questi parametri, "configurazione" li consente numero hello tootune di BizTalk Mapper utilizzato.
4. Di seguito, sono riportate altre **opzioni avanzate** che consentono di ottimizzare le prestazioni di Hive. Questi consentono di toomap di memoria allocata tooset hello e ridurre le attività e può essere utili per regolare le prestazioni. Tenere presente che hello *MapReduce* non può essere maggiore di dimensioni della memoria fisica di ogni nodo di lavoro in un cluster Hadoop hello hello.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

