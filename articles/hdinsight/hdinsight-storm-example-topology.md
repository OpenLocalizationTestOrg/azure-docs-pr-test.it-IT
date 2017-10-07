---
title: topologie di Apache Storm aaaExample in HDInsight | Documenti Microsoft
description: Un elenco di esempi di topologie Storm create e testate con Apache Storm in HDInsight, incluse le topologie C# e Java di base per l'utilizzo di hub eventi.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>Esempi di topologie e componenti Storm per Apache Storm in HDInsight

di seguito Hello è un elenco di esempi creati e gestiti da Microsoft per l'utilizzo con Apache Storm in HDInsight. Questi esempi illustrano una varietà di argomenti, dalla creazione di base in c# e Java topologie tooworking con servizi di Azure, ad esempio gli hub di eventi, DB Cosmos, Power BI, Database SQL, di HBase in HDInsight e archiviazione di Azure. Alcuni esempi illustrano anche come toowork con tecnologie diverse da Azure o anche non Microsoft, ad esempio SignalR e Socket.IO.

| Descrizione | Dimostra | Linguaggio/framework |
|:--- |:--- |:--- |
| [Scrivere archivio Data Lake di tooAzure da Apache Storm](hdinsight-storm-write-data-lake-store.md) |Scrittura di archivio tooAzure Data Lake |Java |
| [Origine per Spout e Bolt dell'hub eventi](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |Origine per hello Spout Hub eventi e fulmine |Java |
| [Sviluppare topologie basate su Java per Apache Storm in HDInsight][5797064f] |Maven |Java |
| [Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio][16fce2d1] |HDInsight Tools per Visual Studio |C#, Java |
| [Creare più flussi di dati in una topologia Storm C#][ec5a4064] |Più flussi |C# |
| [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (C#)][844d1d81] |Hub eventi |C# e Java |
| [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md) |Hub eventi |Java |
| [Utilizzare i dati di Power Bi toovisualize da una topologia di Storm][94d15238] |Power BI |C# |
| [Analisi dei dati dei sensori con Storm e HBase in HDInsight][ab894747] |Hub eventi, HBase, Socket.IO, dashboard Web |C#, Java, JavaScript, HTML |
| [Elaborare i dati del sensore veicolo dall'hub di eventi usando Storm in HDInsight][246ee964] |Hub eventi, Cosmos DB, BLOB del servizio di archiviazione di Azure (WASB) |C#, Java |
| [Estrazione, trasformazione e caricamento (ETL) da tooHBase hub eventi di Azure, utilizzando Storm in HDInsight][b4b68194] |Hub eventi, HBase |C# |
| [Progetto di topologia Storm C# modello per l'uso dei servizi Azure da Storm in HDInsight][ce0c02a2] |Hub eventi, Cosmos DB, database SQL, HBase, SignalR |C#, Java |
| [Benchmark di scalabilità per la lettura da hub eventi di Azure con Storm in HDInsight][d6c540e3] |Velocità effettiva dei messaggi, hub di eventi, database SQL |C#, Java |
| [Correlare gli eventi  con Storm e HBase in HDInsight](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [Introduzione a Python con Storm in HDInsight](hdinsight-storm-develop-python-topology.md) |Componenti Python con una topologia Flux |Python |
| [Usare Kafka con Storm in HDInsight](hdinsight-apache-storm-with-kafka.md) | Lettura di Apache Storm e la scrittura tooApache Kafka | Java |

### <a name="next-steps"></a>Passaggi successivi

* [Introduzione ad Apache Storm in HDInsight][2b8c3488]
* [Informazioni su come toodeploy e gestire le topologie di Storm con Storm in HDInsight][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "Informazioni su come un elevato numero di cluster HDInsight e l'utilizzo di toocreate hello topologie di esempio toodeploy Storm Dashboard."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "Informazioni su come toodeploy e gestire le topologie tramite hello Dashboard Storm basato su web e interfaccia utente di Storm o hello HDInsight Tools per Visual Studio."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Informazioni su come le topologie di c# Storm toocreate utilizzando hello strumenti HDInsight per Visual Studio."
[5797064f]: hdinsight-storm-develop-java-topology.md "Informazioni su come le topologie di Storm toocreate in Java, utilizzando Maven, tramite la creazione di una topologia di base wordcount."
[94d15238]: hdinsight-storm-power-bi-topology.md "Di seguito viene illustrato come toowrite dati tooPower BI da una topologia c#, quindi creare un dashboard e un grafico da dati hello."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "Illustra una topologia Storm di base che esegue un conteggio di parole, implementata in C#, Illustra inoltre come toocreate flussi di dati più all'interno di una topologia c#."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "Informazioni su come tooread e scrittura dati dall'hub di eventi di Azure con Storm in HDInsight."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Informazioni su come visualizzarla D3.js toouse Apache Storm HDInsight tooprocess dei dati del sensore di hub di eventi di Azure e (facoltativamente), archiviarlo tooHBase."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "Informazioni su come toouse una tempesta topologia tooread messaggi dall'hub di eventi di Azure, leggere documenti dal database di Azure Cosmos per fare riferimento a dati e salvare dati tooAzure archiviazione."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "Diverse topologie toodemonstrate velocità effettiva durante la lettura dagli hub di eventi di Azure e l'archiviazione tooSQL Database usando Apache Storm in HDInsight."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Informazioni su come dati tooread da hub di eventi di Azure, aggregazione e trasforma hello dati, quindi archiviano tooHBase in HDInsight."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "Questo progetto contiene modelli per toointeract spouts, dadi e topologie con diversi servizi di Azure come hub eventi, DB Cosmos e Database SQL."

