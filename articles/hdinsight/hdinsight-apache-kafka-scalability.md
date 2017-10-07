---
title: aaaApache Kafka aumentare scale - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su modalità di gestione di dischi di cluster Apache Kafka sulla scalabilità di Azure HDInsight tooincrease tooconfigure."
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
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>Configurare l'archiviazione e la scalabilità per Apache Kafka in HDInsight

Informazioni sull'utilizzo numero hello tooconfigure di dischi gestiti da Apache Kafka in HDInsight.

Kafka in HDInsight Usa disco locale di hello delle macchine virtuali hello nel cluster HDInsight hello. I/o molto elevato, poiché Kafka [dischi gestiti di Azure](../virtual-machines/windows/managed-disks-overview.md) è la velocità effettiva elevata tooprovide utilizzato e fornire maggiore spazio di archiviazione per ogni nodo. Se tradizionali dischi rigidi virtuali (VHD) sono stati utilizzati per Kafka, ogni nodo è limitato too1 TB. Con i dischi gestiti, è possibile utilizzare più dischi tooachieve 16 TB per ogni nodo nel cluster hello.

Hello diagramma seguente offre un confronto tra Kafka in HDInsight prima di dischi gestiti e Kafka in HDInsight con dischi gestiti:

![Diagramma che mostra Kafka in HDInsight con un singolo disco rigido virtuale per ogni macchina virtuale e con più dischi gestiti per ogni macchina virtuale](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>Configurare i dischi gestiti: portale di Azure

1. Seguire i passaggi hello hello [creare un cluster HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello comune passaggi toocreate un cluster tramite il portale di hello. Non completare il processo di creazione del portale hello.

2. Da hello __dimensioni del Cluster__ blade, utilizzare hello __dischi per ogni nodo del lavoro__ tooconfigure hello numero di dischi del campo.

    > [!NOTE]
    > Hello tipo di disco gestito può essere __Standard__ (HDD) o __Premium__ (unità SSD). I dischi Premium sono usati con le macchine virtuali serie DS e GS. Tutti gli altri tipi di macchine virtuali usano dischi Standard.

    ![Immagine del Pannello di dimensioni di cluster hello con dischi hello per ogni nodo di lavoro evidenziato](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>Configurare i dischi gestiti: modello di Resource Manager

numero di hello toocontrol di dischi utilizzato da nodi di lavoro hello in un cluster Kafka, utilizzare hello seguente sezione del modello di hello:

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

È possibile trovare un modello completo che illustra una modalità di gestione di dischi tooconfigure [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'utilizzo di Kafka in HDInsight, vedere hello seguenti documenti:

* [Utilizzare MirrorMaker toocreate una replica di Kafka in HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Usare Apache Storm (anteprima) con Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)
* [Connettersi tooKafka tramite una rete virtuale di Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [Blog di HDInsight sui dischi gestiti con Kafka](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)