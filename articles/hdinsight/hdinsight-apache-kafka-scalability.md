---
title: "Aumento della scalabilità in Apache Kafka - Azure HDInsight | Microsoft Docs"
description: "Informazioni su come configurare i dischi gestiti per i cluster di Apache Kafka in Azure HDInsight per aumentare la scalabilità."
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
ms.openlocfilehash: 880a186a3d9a23b013294b0121e8265270d160cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="b6fff-103">Configurare l'archiviazione e la scalabilità per Apache Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6fff-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="b6fff-104">Questo articolo spiega come configurare il numero di dischi gestiti usati da Apache Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6fff-104">Learn how to configure the number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="b6fff-105">Kafka in HDInsight usa il disco locale delle macchine virtuali nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6fff-105">Kafka on HDInsight uses the local disk of the virtual machines in the HDInsight cluster.</span></span> <span data-ttu-id="b6fff-106">Dal momento che in Kafka i processi I/O sono intensivi, viene usata la funzionalità [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) per assicurare una velocità effettiva elevata e fornire maggiore spazio di archiviazione per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="b6fff-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used to provide high throughput and provide more storage per node.</span></span> <span data-ttu-id="b6fff-107">Se si usano le tradizionali unità disco rigido virtuali (VHD) per Kafka, ogni nodo è limitato a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="b6fff-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited to 1 TB.</span></span> <span data-ttu-id="b6fff-108">Con i dischi gestiti, è possibile usare più dischi per ottenere 16 TB per ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="b6fff-108">With managed disks, you can use multiple disks to achieve 16 TB for each node in the cluster.</span></span>

<span data-ttu-id="b6fff-109">Il diagramma seguente offre un confronto tra Kafka in HDInsight prima dei dischi gestiti e Kafka in HDInsight con i dischi gestiti:</span><span class="sxs-lookup"><span data-stu-id="b6fff-109">The following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagramma che mostra Kafka in HDInsight con un singolo disco rigido virtuale per ogni macchina virtuale e con più dischi gestiti per ogni macchina virtuale](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="b6fff-111">Configurare i dischi gestiti: portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b6fff-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="b6fff-112">Seguire i passaggi riportati in [Creare un cluster HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) per comprendere le operazioni principali per creare un cluster tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="b6fff-112">Follow the steps in the [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) to understand the common steps to create a cluster using the portal.</span></span> <span data-ttu-id="b6fff-113">Non completare il processo di creazione del portale.</span><span class="sxs-lookup"><span data-stu-id="b6fff-113">Do not complete the portal creation process.</span></span>

2. <span data-ttu-id="b6fff-114">Nel pannello __Dimensioni del cluster__ usare il campo dei __dischi per nodo del ruolo di lavoro__ per configurare il numero di dischi.</span><span class="sxs-lookup"><span data-stu-id="b6fff-114">From the __Cluster size__ blade, use the __Disks per worker node__ field to configure the number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6fff-115">Il tipo di disco gestito può essere __Standard__ (HDD) o __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="b6fff-115">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="b6fff-116">I dischi Premium sono usati con le macchine virtuali serie DS e GS.</span><span class="sxs-lookup"><span data-stu-id="b6fff-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="b6fff-117">Tutti gli altri tipi di macchine virtuali usano dischi Standard.</span><span class="sxs-lookup"><span data-stu-id="b6fff-117">All other VM types use standard.</span></span>

    ![Immagine del pannello Dimensioni del cluster con i dischi per nodo del ruolo di lavoro evidenziati](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="b6fff-119">Configurare i dischi gestiti: modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b6fff-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="b6fff-120">Per controllare il numero di dischi usati dai nodi del ruolo di lavoro in un cluster Kafka, usare la sezione seguente del modello:</span><span class="sxs-lookup"><span data-stu-id="b6fff-120">To control the number of disks used by the worker nodes in a Kafka cluster, use the following section of the template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="b6fff-121">È possibile trovare un modello completo che illustra come configurare i dischi gestiti all'indirizzo [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="b6fff-121">You can find a complete template that demonstrates how to configure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6fff-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6fff-122">Next steps</span></span>

<span data-ttu-id="b6fff-123">Per altre informazioni sull'uso della gestione di Kafka in HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6fff-123">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="b6fff-124">Usare MirrorMaker per creare una replica di Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6fff-124">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="b6fff-125">Usare Apache Storm (anteprima) con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6fff-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* <span data-ttu-id="b6fff-126">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b6fff-126">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>
* <span data-ttu-id="b6fff-127">[Connect to Kafka through an Azure Virtual Network](hdinsight-apache-kafka-connect-vpn-gateway.md) (Connettersi a Kafka tramite una rete virtuale di Azure)</span><span class="sxs-lookup"><span data-stu-id="b6fff-127">[Connect to Kafka through an Azure Virtual Network](hdinsight-apache-kafka-connect-vpn-gateway.md)</span></span>

* [<span data-ttu-id="b6fff-128">Blog di HDInsight sui dischi gestiti con Kafka</span><span class="sxs-lookup"><span data-stu-id="b6fff-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)