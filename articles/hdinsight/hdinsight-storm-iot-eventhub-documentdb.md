---
title: dati del sensore veicolo aaaProcess con Apache Storm in HDInsight | Documenti Microsoft
description: Informazioni su come dati del sensore veicolo tooprocess dagli hub di eventi utilizzando Apache Storm in HDInsight. Aggiungere dati del modello dal database di Azure Cosmos e archiviare toostorage di output.
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Elaborare i dati del sensore veicolo dagli hub eventi di Azure usando Apache Storm in HDInsight

Informazioni su come dati del sensore veicolo tooprocess dagli hub di eventi di Azure usando Apache Storm in HDInsight. In questo esempio legge i dati del sensore dagli hub di eventi di Azure, arricchisce dati hello facendo riferimento a dati archiviati nel database di Azure Cosmos. Hello dati vengono archiviati in archiviazione di Azure usando hello del File System di Hadoop (HDFS).

![HDInsight e hello diagramma dell'architettura di Internet delle cose (IoT)](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Panoramica

Aggiunta di sensori toovehicles consente problemi attrezzature toopredict in base alle tendenze dei dati cronologici. Consente inoltre toomake miglioramenti versioni toofuture basate su Analisi utilizzo del modello. È necessario essere in grado di tooquickly e caricare in modo efficiente i dati di hello da tutti i veicoli in Hadoop prima di poter eseguire l'elaborazione di MapReduce. Inoltre, è preferibile toodo analisi per i percorsi di errore critico (temperatura del motore, freni, e così via) in tempo reale.

Hub eventi di Azure è compilato in volume di grande hello toohandle dei dati generati dai sensori. Apache Storm può essere utilizzato tooload e hello elaborare i dati prima di essere archiviati in HDFS.

## <a name="solution"></a>Soluzione

I dati di telemetria relativi a temperatura del motore, temperatura ambiente e velocità del veicolo vengono registrati dai sensori. Dati vengono quindi inviati hub tooEvent insieme veicolo identificazione numero (VPN dell'automobile hello) e un timestamp. Da qui, una topologia di Storm in esecuzione in un elevato numero di Apache nel cluster HDInsight legge i dati di hello, elabora e archivia in HDFS.

Durante l'elaborazione, hello VPN è informazioni relative al modello tooretrieve utilizzato dal database Cosmos. Questi dati viene aggiunto il flusso di dati toohello prima che venga archiviata.

componenti di Hello utilizzati nella topologia Storm hello sono:

* **EventHubSpout** : legge i dati dagli hub eventi di Azure
* **TypeConversionBolt** -converte hello stringa JSON da hub eventi in una tupla contenente hello sensore dati seguenti:
    * engineTemperature
    * Temperatura ambiente
    * speed
    * vin
    * Timestamp
* **DataReferencBolt** -Cerca modello hello da DB Cosmos tramite VPN hello
* **WasbStoreBolt** -archivi hello tooHDFS dati (archiviazione di Azure)

Hello seguente immagine è un diagramma di questa soluzione:

![topologia storm](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Implementazione

Una completa soluzione automatizzata per questo scenario è disponibile come parte di hello [esempi di Storm HDInsight](https://github.com/hdinsight/hdinsight-storm-examples) repository in GitHub. toouse in questo esempio, seguire la procedura seguente hello in hello [IoTExample README. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Passaggi successivi

Per altri esempi di topologie Storm, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).

