---
title: introduzione di aaaAn tooApache Kafka in HDInsight - Azure | Documenti Microsoft
description: "Informazioni su Apache Kafka in HDInsight: che cos'è, descrizione e in cui toofind esempi e ottenere le informazioni introduttive."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>Introduzione ad Apache Kafka in HDInsight (anteprima)

[Apache Kafka](https://kafka.apache.org) è una piattaforma streaming distribuita open source che può essere utilizzato toobuild in tempo reale streaming pipeline di dati e applicazioni. Kafka fornisce inoltre broker messaggi funzionalità simili tooa coda di messaggi, in cui è possibile pubblicare e sottoscrivere toonamed flussi di dati. Kafka in HDInsight offre un servizio gestito, estremamente scalabile e a disponibilità elevata nel cloud di Microsoft Azure hello.

## <a name="why-use-kafka-on-hdinsight"></a>Perché usare Kafka in HDInsight?

Kafka fornisce hello seguenti caratteristiche:

* Modello di messaggistica di pubblicazione-sottoscrizione: Kafka fornisce un'API di produzione per la pubblicazione di record tooa argomento Kafka. Hello API Consumer viene utilizzato quando si sottoscrive tooa argomento.

* Elaborazione dei flussi: Kafka viene usato spesso con Apache Storm o Spark per l'elaborazione dei flussi in tempo reale. Kafka 0.10.0.0 (HDInsight versione 3.5) introdotta un'API di flusso che consente di toobuild streaming soluzioni senza Storm o Spark.

* Scalabilità orizzontale: Kafka flussi vengono partizionati tra i nodi nel cluster HDInsight hello hello. È possibile associati singole partizioni tooprovide bilanciamento del carico quando si utilizzano i record dei processi del consumer.

* Recapito nell'ordine: in ogni partizione, i record vengono archiviati nel flusso di hello in ordine di hello che sono stati ricevuti. Associando un processo consumer per partizione, è possibile garantire che i record vengano elaborati in ordine.

* A tolleranza di errore: Le partizioni possono essere replicate tra la tolleranza di errore tooprovide nodi.

* Integrazione con i dischi gestiti di Azure: dischi gestito offre maggiore scalabilità e velocità effettiva per hello dischi utilizzati dalle macchine virtuali hello in cluster di HDInsight hello.

    Dischi gestiti sono abilitati per impostazione predefinita per Kafka in HDInsight e il numero di hello di dischi utilizzato per ogni nodo può essere configurato durante la creazione di HDInsight. Per altre informazioni sui dischi gestiti, vedere [Panoramica di Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).

    Per informazioni sulla configurazione di dischi gestiti con Kafka in HDInsight, vedere [Configurare l'archiviazione e la scalabilità per Apache Kafka in HDInsight](hdinsight-apache-kafka-scalability.md).

## <a name="use-cases"></a>Casi d'uso

* **Messaggistica**: poiché hello supporta il modello di messaggio di pubblicazione-sottoscrizione, Kafka viene spesso usato come broker di messaggi.

* **Rilevamento di attività**: Kafka poiché fornisce la registrazione nell'ordine dei record, può essere utilizzato tootrack e ricreare le attività. Ad esempio, le azioni dell'utente in un sito Web o in un'applicazione.

* **Aggregazione**: utilizza l'elaborazione del flusso, è possibile aggregare informazioni da flussi diversi toocombine e centralizzare le informazioni di hello in dati operativi.

* **Trasformazione**: usando l'elaborazione dei flussi, è possibile combinare e arricchire dati da più argomenti di input in uno o più argomenti di output.

## <a name="next-steps"></a>Passaggi successivi

Seguente hello utilizzare collegamenti toolearn come toouse Kafka Apache in HDInsight:

* [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) (Introduzione a Kafka in HDInsight)

* [Utilizzare MirrorMaker toocreate una replica di Kafka in HDInsight](hdinsight-apache-kafka-mirroring.md)

* [Usare Apache Storm (anteprima) con Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)

* [Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)

* [Connettersi tooKafka tramite una rete virtuale di Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
