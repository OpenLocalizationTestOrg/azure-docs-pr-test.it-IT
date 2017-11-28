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
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="3903a-103">Configurare l'archiviazione e la scalabilità per Apache Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3903a-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="3903a-104">Informazioni sull'utilizzo numero hello tooconfigure di dischi gestiti da Apache Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3903a-104">Learn how tooconfigure hello number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="3903a-105">Kafka in HDInsight Usa disco locale di hello delle macchine virtuali hello nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="3903a-105">Kafka on HDInsight uses hello local disk of hello virtual machines in hello HDInsight cluster.</span></span> <span data-ttu-id="3903a-106">I/o molto elevato, poiché Kafka [dischi gestiti di Azure](../virtual-machines/windows/managed-disks-overview.md) è la velocità effettiva elevata tooprovide utilizzato e fornire maggiore spazio di archiviazione per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="3903a-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used tooprovide high throughput and provide more storage per node.</span></span> <span data-ttu-id="3903a-107">Se tradizionali dischi rigidi virtuali (VHD) sono stati utilizzati per Kafka, ogni nodo è limitato too1 TB.</span><span class="sxs-lookup"><span data-stu-id="3903a-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited too1 TB.</span></span> <span data-ttu-id="3903a-108">Con i dischi gestiti, è possibile utilizzare più dischi tooachieve 16 TB per ogni nodo nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3903a-108">With managed disks, you can use multiple disks tooachieve 16 TB for each node in hello cluster.</span></span>

<span data-ttu-id="3903a-109">Hello diagramma seguente offre un confronto tra Kafka in HDInsight prima di dischi gestiti e Kafka in HDInsight con dischi gestiti:</span><span class="sxs-lookup"><span data-stu-id="3903a-109">hello following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagramma che mostra Kafka in HDInsight con un singolo disco rigido virtuale per ogni macchina virtuale e con più dischi gestiti per ogni macchina virtuale](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="3903a-111">Configurare i dischi gestiti: portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3903a-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="3903a-112">Seguire i passaggi hello hello [creare un cluster HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello comune passaggi toocreate un cluster tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="3903a-112">Follow hello steps in hello [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello common steps toocreate a cluster using hello portal.</span></span> <span data-ttu-id="3903a-113">Non completare il processo di creazione del portale hello.</span><span class="sxs-lookup"><span data-stu-id="3903a-113">Do not complete hello portal creation process.</span></span>

2. <span data-ttu-id="3903a-114">Da hello __dimensioni del Cluster__ blade, utilizzare hello __dischi per ogni nodo del lavoro__ tooconfigure hello numero di dischi del campo.</span><span class="sxs-lookup"><span data-stu-id="3903a-114">From hello __Cluster size__ blade, use hello __Disks per worker node__ field tooconfigure hello number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3903a-115">Hello tipo di disco gestito può essere __Standard__ (HDD) o __Premium__ (unità SSD).</span><span class="sxs-lookup"><span data-stu-id="3903a-115">hello type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="3903a-116">I dischi Premium sono usati con le macchine virtuali serie DS e GS.</span><span class="sxs-lookup"><span data-stu-id="3903a-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="3903a-117">Tutti gli altri tipi di macchine virtuali usano dischi Standard.</span><span class="sxs-lookup"><span data-stu-id="3903a-117">All other VM types use standard.</span></span>

    ![Immagine del Pannello di dimensioni di cluster hello con dischi hello per ogni nodo di lavoro evidenziato](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="3903a-119">Configurare i dischi gestiti: modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3903a-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="3903a-120">numero di hello toocontrol di dischi utilizzato da nodi di lavoro hello in un cluster Kafka, utilizzare hello seguente sezione del modello di hello:</span><span class="sxs-lookup"><span data-stu-id="3903a-120">toocontrol hello number of disks used by hello worker nodes in a Kafka cluster, use hello following section of hello template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="3903a-121">È possibile trovare un modello completo che illustra una modalità di gestione di dischi tooconfigure [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="3903a-121">You can find a complete template that demonstrates how tooconfigure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3903a-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3903a-122">Next steps</span></span>

<span data-ttu-id="3903a-123">Per ulteriori informazioni sull'utilizzo di Kafka in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="3903a-123">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="3903a-124">Utilizzare MirrorMaker toocreate una replica di Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3903a-124">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="3903a-125">Usare Apache Storm (anteprima) con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3903a-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* <span data-ttu-id="3903a-126">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="3903a-126">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>
* [<span data-ttu-id="3903a-127">Connettersi tooKafka tramite una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="3903a-127">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="3903a-128">Blog di HDInsight sui dischi gestiti con Kafka</span><span class="sxs-lookup"><span data-stu-id="3903a-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)