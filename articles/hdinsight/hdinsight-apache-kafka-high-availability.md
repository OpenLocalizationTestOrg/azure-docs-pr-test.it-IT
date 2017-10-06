---
title: "disponibilità aaaHigh con Apache Kafka - HDInsight di Azure | Documenti Microsoft"
description: "Informazioni su come la disponibilità elevata tooensure con Apache Kafka in Azure HDInsight. Informazioni su come toorebalance partizionare le repliche Kafka in modo che siano in diversi domini di errore all'interno di hello area che contiene HDInsight di Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>Disponibilità elevata dei dati con Apache Kafka (anteprima) in HDInsight

Informazioni su come le repliche delle partizioni tooconfigure per Kafka argomenti tootake sfruttare hardware sottostante rack configurazione. Questa configurazione assicura la disponibilità di hello dei dati archiviati in Apache Kafka in HDInsight.

## <a name="fault-and-update-domains-with-kafka"></a>Domini di errore e di aggiornamento con Kafka

Un dominio di errore è un raggruppamento logico dell'hardware sottostante in un data center di Azure. Ogni dominio di errore condivide una fonte di alimentazione e un commutatore di rete comuni. Hello le macchine virtuali e dischi gestiti che implementano i nodi di hello all'interno di un cluster HDInsight vengono distribuiti tra i domini di errore. Questa architettura limita l'impatto potenziale di hello dei guasti hardware fisico.

Ogni area di Azure include un numero specifico di domini di errore. Per un elenco di domini e il numero di hello di domini di errore contengono, vedere hello [set di disponibilità](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentazione.

> [!IMPORTANT]
> Kafka non rileva i domini di errore. Quando si crea un argomento in Kafka, è possibile archiviare tutte le repliche di partizione in hello stesso dominio di errore. toosolve questo problema, forniamo hello [strumento ribilanciamento delle partizioni Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).

## <a name="when-toorebalance-partition-replicas"></a>Quando toorebalance partizione repliche

tooensure hello massima disponibilità dei dati Kafka, è necessario ribilanciare le repliche delle partizioni hello per l'argomento in seguito volte hello:

* Quando viene creato un nuovo argomento o una nuova partizione

* Quando si aumentano le prestazioni di un cluster

## <a name="replication-factor"></a>Fattore di replica

> [!IMPORTANT]
> È consigliabile usare un'area di Azure contenente tre domini di errore e un fattore di replica di 3.

Se è necessario utilizzare un'area che contiene solo due domini di errore, utilizzare un fattore di replica delle repliche di hello toospread 4 in modo uniforme tra i due domini di errore hello.

Per un esempio di creazione di argomenti e fattore di replica hello impostazione, vedere hello [iniziano con Kafka in HDInsight](hdinsight-apache-kafka-get-started.md) documento.

## <a name="how-toorebalance-partition-replicas"></a>Le repliche delle partizioni toorebalance

Hello utilizzare [strumento ribilanciamento delle partizioni Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selezionato argomenti. Questo strumento deve essere eseguito da un nodo head di toohello sessione SSH del cluster Kafka.

Per ulteriori informazioni sulla connessione tooHDInsight tramite SSH, vedere il [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

## <a name="next-steps"></a>Passaggi successivi

* [Scalabilità di Kafka in HDInsight](hdinsight-apache-kafka-scalability.md)
* [Mirroring con Kafka in HDInsight](hdinsight-apache-kafka-mirroring.md)