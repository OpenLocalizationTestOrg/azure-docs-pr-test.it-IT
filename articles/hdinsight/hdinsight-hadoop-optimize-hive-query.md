---
title: esegue una query aaaOptimize Hive in HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toooptimize l'Hive esegue una query per Hadoop in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>Ottimizzare le query Hive in Azure HDInsight

Per impostazione predefinita, i cluster Hadoop non sono ottimizzati per le prestazioni. Questo articolo descrive alcuni metodi di ottimizzazione delle prestazioni Hive più comuni che è possibile applicare tooyour query.

## <a name="scale-out-worker-nodes"></a>Scalabilità orizzontale dei nodi di lavoro

Aumentare il numero di hello nodi di lavoro in un cluster, è possibile sfruttare più toobe di BizTalk Mapper e riduttori eseguite in parallelo. Esistono due modi per aumentare la scalabilità orizzontale in HDInsight:

* In fase di disposizione hello, è possibile specificare il numero di hello di nodi di lavoro utilizzando hello portale di Azure, Azure PowerShell o interfaccia della riga di comando multipiattaforma.  Per altre informazioni, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Hello schermata seguente mostra il lavoro hello configurazione del nodo nel portale di Azure hello:
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* In fase di esecuzione di hello, è anche possibile scalare orizzontalmente un cluster senza ricreare uno:

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

Per ulteriori informazioni sulle macchine virtuali diverse hello è supportato da HDInsight, vedere [prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="enable-tez"></a>Abilitare Tez

[Apache Tez](http://hortonworks.com/hadoop/tez/) è un motore di esecuzione alternativo motore toohello MapReduce:

![tez_1][image-hdi-optimize-hive-tez_1]

Tez è più veloce perché:

* **Eseguire indirizzate aciclico Graph (DAG) come un singolo processo di motore MapReduce hello**. Hello DAG richiede ogni set di BizTalk Mapper toobe seguita da una serie di riduttori. In questo modo toobe di processi MapReduce più rimosso per ogni query Hive. Tez non presenta questo vincolo e può elaborare DAG complessi con un unico processo, riducendo così il sovraccarico di avvio del processo.
* **Evita scritture non necessarie**. A causa di processi toomultiple viene ruotati per hello stessa query Hive nel motore MapReduce hello, output di hello di ogni processo viene scritto tooHDFS per i dati intermedi. Poiché Tez riduce al minimo numero di processi per ogni query Hive è in grado di tooavoid scrittura non necessari.
* **Riduce al minimo i ritardi di avvio**. Tez è migliore ritardo di avvio in grado di toominimize riducendo il numero di hello di BizTalk Mapper che è necessario toostart e anche migliorare di ottimizzazione in tutto.
* **Riusa i contenitori**. Ogni volta che Tez possibili è in grado di tooreuse contenitori tooensure tale latenza a causa di toostarting dei contenitori viene ridotto.
* **Usa tecniche di ottimizzazione continua**. In genere l'ottimizzazione viene eseguita durante la fase di compilazione. Tuttavia, sono disponibili ulteriori informazioni sugli input hello che consentono di migliore ottimizzazione in fase di esecuzione. Tez utilizza tecniche di ottimizzazione continua che consenta a tale piano di hello toooptimize ulteriormente in fase di runtime hello.

Per altre informazioni su questi concetti, vedere [Apache TEZ](http://hortonworks.com/hadoop/tez/).

È possibile apportare tutte le query Hive Tez abilitata aggiungendo il prefisso query hello con impostazione hello seguente:

    set hive.execution.engine=tez;

I cluster HDInsight basati su Linux hanno Tez abilitato per impostazione predefinita.


## <a name="hive-partitioning"></a>Partizionamento Hive

Operazione dei / o è hello principali collo di bottiglia per l'esecuzione di query Hive. possono migliorare le prestazioni di Hello se quantità hello di dati che devono essere toobe lettura può essere ridotto. Per impostazione predefinita, le query Hive analizzano intere tabelle Hive. Questa operazione è utile per query come le analisi di tabella, Tuttavia per le query che richiedono solo una piccola quantità di dati, ad esempio, le query con il filtro, tooscan, questo comportamento crea un inutile overhead. Partizionamento hive consente Hive query tooaccess solo hello necessarie quantità di dati nelle tabelle Hive.

Partizionamento hive viene implementato tramite la riorganizzazione di dati non elaborati hello in directory di nuovo a ciascuna partizione con una propria directory, in cui la partizione hello è definita da utente hello. Hello diagramma seguente illustra il partizionamento di una tabella Hive per colonna hello *anno*. Viene creata una nuova directory per ogni anno.

![partizionamento][image-hdi-optimize-hive-partitioning_1]

Alcune considerazioni sul partizionamento:

* **Non creare un numero eccessivamente ridotto di partizioni**: il partizionamento in colonne con pochi valori può causare un numero ridotto di partizioni. Ad esempio, solo il partizionamento in genere crea due toobe partizioni creato (maschio e femmina), pertanto solo ridurre la latenza di hello da un massimo di metà.
* **Eseguire non su una partizione** : nel hello altra estremità, creazione di una partizione in una colonna con un valore univoco (ad esempio, userid) fa sì che più partizioni. Sulla partizione impone quantità stress hello cluster namenode perché contiene numerosi hello toohandle delle directory.
* **Evitare lo sfasamento di dati** : scegliere la chiave di partizionamento con attenzione, in modo che tutte le partizioni siano di dimensioni pari. Un esempio è partizionamento in *stato* può causare il numero di hello di record in California toobe quasi 30 x che di Vermont a causa di differenza toohello popolazione.

toocreate una tabella di partizione, utilizzare hello *partizionata da* clausola:

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

Una volta creata la tabella partizionata hello, è possibile creare il partizionamento statico o il partizionamento dinamico.

* **Il partizionamento statico** significa che sono presenti dati già partizionati hello le directory appropriate che è possibile richiedere Hive partizioni manualmente in base alla posizione di directory hello. Hello frammento di codice seguente è riportato un esempio.
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **Partizionamento dinamico** significa che le partizioni toocreate Hive automaticamente per l'utente. Poiché sono già stati creati hello partizionamento tabella dalla tabella di gestione temporanea hello, è sufficiente toodo è insert dati partizionato toohello tabella:
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

Per ulteriori informazioni, vedere [Tabelle partizionate](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).

## <a name="use-hello-orcfile-format"></a>Utilizzare il formato ORCFile hello
Hive supporta diversi formati di file. ad esempio:

* **Testo**: questo è il formato di file predefinito hello e funziona con la maggior parte degli scenari
* **Avro**: funziona bene per scenari di interoperabilità
* **ORC/Parquet**: particolarmente indicato per le prestazioni

Il formato ORC (con ottimizzazione per la riga a colonne) è un toostore molto efficiente dati Hive. Formati tooother confrontati, ORC ha hello seguenti vantaggi:

* supporto per tipi complessi, inclusi i tipi complessi e semistrutturati e DateTime
* configurare la compressione % too70
* indici ogni 10.000 righe, che consentono di ignorare le righe
* significativa riduzione in fase di esecuzione

il formato ORC tooenable, creare innanzitutto una tabella con clausola hello *archiviati come ORC*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

Successivamente, si inserisce nella tabella dati toohello ORC dalla tabella di gestione temporanea hello. ad esempio:

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

Altre informazioni sul formato ORC hello [qui](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).

## <a name="vectorization"></a>Vettorizzazione

Consente di vettorizzazione Hive tooprocess un batch di 1024 righe insieme anziché l'elaborazione di una riga alla volta. Significa che le operazioni semplici vengono eseguite più velocemente perché meno codice interno deve essere toorun.

la vettorializzazione tooenable prefisso query Hive con hello seguente impostazione:

    set hive.vectorized.execution.enabled = true;

Per altre informazioni, vedere [Esecuzione di query vettorizzate](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).

## <a name="other-optimization-methods"></a>Altri metodi di ottimizzazione
Esistono altri metodi di ottimizzazione che è possibile considerare, ad esempio:

* **Hive bucket:** una tecnica che consente di segmento o toocluster grandi set di dati toooptimize le prestazioni delle query.
* **L'ottimizzazione del join:** ottimizzazione dell'esecuzione di query Hive pianificazione tooimprove hello l'efficienza di join e ridurre hello necessità per gli hint per utente. Per altre informazioni, vedere [Ottimizzazione join](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).
* **Aumento dei reducer**.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo sono stati illustrati vari metodi di ottimizzazione delle query comuni di Hive. toolearn informazioni, vedere hello seguenti articoli:

* [Usare Apache Hive in HDInsight](hdinsight-use-hive.md)
* [Analizzare i dati sui ritardi dei voli mediante Hive in HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Analizzare i dati Twitter mediante Hive in HDInsight](hdinsight-analyze-twitter-data.md)
* [Analizzare i dati del sensore utilizzando la Console di Query Hive hello in Hadoop in HDInsight](hdinsight-hive-analyze-sensor-data.md)
* [Usare l'Hive con log tooanalyze HDInsight da siti Web](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
