---
title: Informazioni su HBase in Azure HDInsight | Microsoft Docs
description: Introduzione ad Apache HBase in HDInsight, un database NoSQL basato su Hadoop. Informazioni sui casi di utilizzo e confronto di HBase con altri cluster Hadoop.
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
ms.openlocfilehash: 6823633bfdb07ce649083804ba211709519cb6da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>Informazioni su HBase in HDInsight: un database NoSQL che fornisce funzionalità di tipo BigTable per Hadoop
Apache HBase è un database NoSQL open source basato su Hadoop e modellato su Google BigTable. HBase fornisce accesso casuale e coerenza assoluta per quantità elevate di dati non strutturati e semistrutturati in un database privo di schema organizzato per famiglie di colonne.

I dati sono archiviati nelle righe di una tabella e i dati di ogni riga sono raggruppati in base al tipo di colonna. HBase è un database privo di schema, poiché non è necessario definire le colonne o i tipi di dati archiviati nelle colonne prima dell'uso. Il codice open source offre scalabilità lineare, in modo da gestire petabyte di dati in migliaia di nodi. Può contare su ridondanza dei dati, elaborazione batch e altre funzionalità offerte dalle applicazioni distribuite nell'ecosistema di Hadoop.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>Modalità di implementazione di HBase in Azure HDInsight
HBase di HDInsight è offerto come cluster gestito integrato nell'ambiente di Azure. I cluster sono configurati per archiviare i dati direttamente in [Archiviazione di Azure](./hdinsight-hadoop-use-blob-storage.md) o [Azure Data Lake Store](./hdinsight-hadoop-use-data-lake-store.md), che offre bassa latenza e maggiore flessibilità nelle opzioni relative a prestazioni e costi. Ciò permette ai clienti di creare siti Web interattivi da usare con grandi set di dati, per creare servizi che archiviano dati di sensori e telemetria da milioni di endpoint e per analizzare questi dati tramite processi Hadoop. HBase e Hadoop sono punti di partenza ottimali per progetti Big Data in Azure. In particolare, possono permettere alle applicazioni in tempo reale di usare set di dati di grandi dimensioni.

L'implementazione di HDInsight usa l'architettura di scalabilità orizzontale di HBase per fornire il partizionamento orizzontale delle tabelle, la coerenza assoluta di letture e scritture e il failover automatico. Le prestazioni sono ottimizzate dalla cache in memoria per le operazioni di lettura e da flussi a velocità effettiva elevata per quelle di scrittura. È possibile creare un cluster HBase in una rete virtuale. Per informazioni dettagliate, vedere [Creare cluster HDInsight nella rete virtuale di Azure][hbase-provision-vnet].

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>Modalità di gestione dei dati in HBase di HDInsight
I dati possono essere gestiti in HBase tramite i comandi `create`, `get`, `put` e `scan` dalla shell di HBase. I dati vengono scritti nel database tramite `put` e letti tramite `get`. Il comando `scan` viene usato per ottenere i dati da più righe in una tabella. I dati possono essere gestiti anche tramite l'API C# di HBase, che offre una libreria client, oltre all'API REST di HBase. È anche possibile eseguire query in un database di HBase tramite Hive. Per informazioni introduttive su questi modelli di programmazione, vedere [Introduzione a HBase con Hadoop in HDInsight][hbase-get-started]. Sono anche disponibili coprocessori che consentono l'elaborazione dei dati nei nodi che ospitano il database.

> [!NOTE]
> Thrift non è supportato da HBase in HDInsight.
>

## <a name="scenarios-use-cases-for-hbase"></a>Scenari: casi di utilizzo per HBase
Il caso di utilizzo tipico per cui è stato creato BigTable, e per estensione HBase, è stata la ricerca sul Web. I motori di ricerca costruiscono indici per il mapping di termini alle pagine Web che li contengono. Tuttavia, HBase è adatto a molti altri casi di utilizzo, alcuni dei quali sono descritti in dettaglio in questa sezione.

* Archivio chiave-valore
  
    HBase può essere usato come archivio di tipo chiave-valore ed è adatto alla gestione di sistemi di messaggistica. Facebook usa HBase per il proprio sistema di messaggistica ed è ideale per l'archiviazione e la gestione di comunicazioni Internet. WebTable usa HBase per eseguire ricerche e gestire tabelle estratte da pagine Web.
* Dati di sensori
  
    HBase è utile per l'acquisizione di dati raccolti in modo incrementale da varie origini, incluse analisi di social media e serie temporali, e permette di mantenere aggiornati i dashboard interattivi con tendenze e contatori e di gestire i sistemi di log di controllo. Alcuni esempi includono il terminale dei trader di Bloomberg e il database OpenTSDB (Open Time Series Database), che archivia e fornisce l'accesso alle metriche raccolte sull'integrità dei sistemi di server.
* Query in tempo reale
  
    [Phoenix](http://phoenix.apache.org/) è un motore di query SQL per Apache HBase. Vi si accede come un'unità JDBC e permette di eseguire query e di gestire le tabelle HBase tramite SQL.
* HBase come piattaforma
  
    Le applicazioni possono essere eseguite su HBase, usato come un archivio dati. Alcuni esempi sono Phoenix, OpenTSDB, Kiji e Titan. Le applicazioni possono anche essere integrate con HBase, ad esempio Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia e Drill.

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione all'uso di HBase con Hadoop in HDInsight][hbase-get-started]
* [Creare cluster HDInsight nella rete virtuale di Azure][hbase-provision-vnet]
* [Configurare la replica di HBase in HDInsight](hdinsight-hbase-replication.md)
* [Analizzare i sentimenti Twitter con HBase in HDInsight][hbase-twitter-sentiment]
* [Usare Maven per compilare applicazioni Java che usano HBase con HDInsight (Hadoop)][hbase-build-java-maven]

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
