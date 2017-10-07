---
title: "aaaWhat è HBase in HDInsight di Azure? | Microsoft Docs"
description: Un'introduzione tooApache HBase in HDInsight, un database NoSQL di compilazione in Hadoop. Informazioni sui casi di utilizzo e confrontare i cluster Hadoop di HBase tooother.
keywords: BigTable, NoSQL, informazioni su HBase, Apache HBase, HBase, panoramica di HBbase,
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>Informazioni su HBase in HDInsight: un database NoSQL che fornisce funzionalità di tipo BigTable per Hadoop
Apache HBase è un database NoSQL open source basato su Hadoop e modellato su Google BigTable. HBase fornisce accesso casuale e coerenza assoluta per quantità elevate di dati non strutturati e semistrutturati in un database privo di schema organizzato per famiglie di colonne.

Dati vengono archiviati in righe hello di una tabella e del raggruppamento dei dati all'interno di una riga dalla famiglia di colonna. HBase è un database schemaless nel senso hello che nessuna delle due hello colonne né il tipo di hello dei dati archiviati al loro interno necessario toobe definito prima di usarli. codice open source Hello viene ridimensionata in modo lineare toohandle petabyte di dati migliaia di nodi. È possibile basarsi sulla ridondanza dei dati, l'elaborazione batch e altre funzionalità fornite dalle applicazioni distribuite nell'ecosistema Hadoop hello.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>Modalità di implementazione di HBase in Azure HDInsight
HDInsight HBase viene offerto come un cluster gestito è integrato in hello ambiente Azure. cluster di Hello sono configurati toostore dati direttamente in [di archiviazione di Azure](./hdinsight-hadoop-use-blob-storage.md) o [archivio Azure Data Lake](./hdinsight-hadoop-use-data-lake-store.md), che fornisce bassa latenza e una maggiore elasticità nelle opzioni di prestazioni e costi. In questo modo i clienti toobuild interattivo i siti Web che funzionano con grandi set di dati, servizi toobuild che archiviano i dati di telemetria e sensore da milioni di punti di fine e tooanalyze questi dati con i processi di Hadoop. HBase e Hadoop sono un buon punto di partenza per il progetto di dati in Azure; in particolare, consentono toowork applicazioni in tempo reale con grandi set di dati.

implementazione di HDInsight Hello sfrutta l'architettura di scalabilità orizzontale hello di HBase tooprovide automatica partizionamento delle tabelle, la coerenza assoluta per letture e scritture e il failover automatico. Le prestazioni sono ottimizzate dalla cache in memoria per le operazioni di lettura e da flussi a velocità effettiva elevata per quelle di scrittura. È possibile creare un cluster HBase in una rete virtuale. Per informazioni dettagliate, vedere [Creare cluster HDInsight nella rete virtuale di Azure][hbase-provision-vnet].

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>Modalità di gestione dei dati in HBase di HDInsight
Possono essere gestiti i dati in HBase tramite hello `create`, `get`, `put`, e `scan` comandi dalla shell di HBase hello. Dati vengono scritti toohello database mediante `put` e leggere usando `get`. Hello `scan` comando è tooobtain utilizzati dati da più righe in una tabella. Dati possono essere gestiti tramite hello HBase API c#, che fornisce una libreria client sopra hello API REST HBase. È anche possibile eseguire query in un database di HBase tramite Hive. Per un toothese introduzione modelli di programmazione, vedere [informazioni introduttive sull'utilizzo di HBase con Hadoop in HDInsight][hbase-get-started]. CO-processori sono inoltre disponibili, che consente l'elaborazione dei dati nei nodi hello database hello host.

> [!NOTE]
> Thrift non è supportato da HBase in HDInsight.
>

## <a name="scenarios-use-cases-for-hbase"></a>Scenari: casi di utilizzo per HBase
Hello caso d'uso canonico per i quali BigTable (e, di conseguenza, HBase) è stato creato è stato ricerca sul web. Motori di ricerca compila indici che eseguono il mapping delle condizioni toohello le pagine web che li contengono. Tuttavia, HBase è adatto a molti altri casi di utilizzo, alcuni dei quali sono descritti in dettaglio in questa sezione.

* Archivio chiave-valore
  
    HBase può essere usato come archivio di tipo chiave-valore ed è adatto alla gestione di sistemi di messaggistica. Facebook usa HBase per il proprio sistema di messaggistica ed è ideale per l'archiviazione e la gestione di comunicazioni Internet. Tabella Web Usa toosearch HBase per e gestire le tabelle che vengono estratti dalle pagine Web.
* Dati di sensori
  
    HBase è utile per l'acquisizione di dati raccolti in modo incrementale da varie origini, incluse analisi di social media e serie temporali, e permette di mantenere aggiornati i dashboard interattivi con tendenze e contatori e di gestire i sistemi di log di controllo. Operatore Bloomberg terminal sono esempi e aprire Database di serie di tempo (OpenTSDB), che archivia e offre accesso toometrics hello raccolti sull'integrità hello dei sistemi server.
* Query in tempo reale
  
    [Phoenix](http://phoenix.apache.org/) è un motore di query SQL per Apache HBase. Vi si accede come un'unità JDBC e permette di eseguire query e di gestire le tabelle HBase tramite SQL.
* HBase come piattaforma
  
    Le applicazioni possono essere eseguite su HBase, usato come un archivio dati. Alcuni esempi sono Phoenix, OpenTSDB, Kiji e Titan. Le applicazioni possono anche essere integrate con HBase, ad esempio Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia e Drill.

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione all'uso di HBase con Hadoop in HDInsight][hbase-get-started]
* [Creare cluster HDInsight nella rete virtuale di Azure][hbase-provision-vnet]
* [Configurare la replica di HBase in HDInsight](hdinsight-hbase-replication.md)
* [Analizzare i sentimenti Twitter con HBase in HDInsight][hbase-twitter-sentiment]
* [Utilizzare le applicazioni Java di Maven toobuild che utilizzano HBase di HDInsight (Hadoop)][hbase-build-java-maven]

## <a name="see-also"></a>Vedere anche
* [Apache HBase](https://hbase.apache.org/)
* [Bigtable:un sistema di archiviazione distribuita per dati strutturati](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
