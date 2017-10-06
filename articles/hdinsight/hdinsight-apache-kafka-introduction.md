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
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="06221-103">Introduzione ad Apache Kafka in HDInsight (anteprima)</span><span class="sxs-lookup"><span data-stu-id="06221-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="06221-104">[Apache Kafka](https://kafka.apache.org) è una piattaforma streaming distribuita open source che può essere utilizzato toobuild in tempo reale streaming pipeline di dati e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="06221-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="06221-105">Kafka fornisce inoltre broker messaggi funzionalità simili tooa coda di messaggi, in cui è possibile pubblicare e sottoscrivere toonamed flussi di dati.</span><span class="sxs-lookup"><span data-stu-id="06221-105">Kafka also provides message broker functionality similar tooa message queue, where you can publish and subscribe toonamed data streams.</span></span> <span data-ttu-id="06221-106">Kafka in HDInsight offre un servizio gestito, estremamente scalabile e a disponibilità elevata nel cloud di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="06221-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in hello Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="06221-107">Perché usare Kafka in HDInsight?</span><span class="sxs-lookup"><span data-stu-id="06221-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="06221-108">Kafka fornisce hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="06221-108">Kafka provides hello following features:</span></span>

* <span data-ttu-id="06221-109">Modello di messaggistica di pubblicazione-sottoscrizione: Kafka fornisce un'API di produzione per la pubblicazione di record tooa argomento Kafka.</span><span class="sxs-lookup"><span data-stu-id="06221-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records tooa Kafka topic.</span></span> <span data-ttu-id="06221-110">Hello API Consumer viene utilizzato quando si sottoscrive tooa argomento.</span><span class="sxs-lookup"><span data-stu-id="06221-110">hello Consumer API is used when subscribing tooa topic.</span></span>

* <span data-ttu-id="06221-111">Elaborazione dei flussi: Kafka viene usato spesso con Apache Storm o Spark per l'elaborazione dei flussi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="06221-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="06221-112">Kafka 0.10.0.0 (HDInsight versione 3.5) introdotta un'API di flusso che consente di toobuild streaming soluzioni senza Storm o Spark.</span><span class="sxs-lookup"><span data-stu-id="06221-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you toobuild streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="06221-113">Scalabilità orizzontale: Kafka flussi vengono partizionati tra i nodi nel cluster HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="06221-113">Horizontal scale: Kafka partitions streams across hello nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="06221-114">È possibile associati singole partizioni tooprovide bilanciamento del carico quando si utilizzano i record dei processi del consumer.</span><span class="sxs-lookup"><span data-stu-id="06221-114">Consumer processes can be associated with individual partitions tooprovide load balancing when consuming records.</span></span>

* <span data-ttu-id="06221-115">Recapito nell'ordine: in ogni partizione, i record vengono archiviati nel flusso di hello in ordine di hello che sono stati ricevuti.</span><span class="sxs-lookup"><span data-stu-id="06221-115">In-order delivery: Within each partition, records are stored in hello stream in hello order that they were received.</span></span> <span data-ttu-id="06221-116">Associando un processo consumer per partizione, è possibile garantire che i record vengano elaborati in ordine.</span><span class="sxs-lookup"><span data-stu-id="06221-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="06221-117">A tolleranza di errore: Le partizioni possono essere replicate tra la tolleranza di errore tooprovide nodi.</span><span class="sxs-lookup"><span data-stu-id="06221-117">Fault-tolerant: Partitions can be replicated between nodes tooprovide fault tolerance.</span></span>

* <span data-ttu-id="06221-118">Integrazione con i dischi gestiti di Azure: dischi gestito offre maggiore scalabilità e velocità effettiva per hello dischi utilizzati dalle macchine virtuali hello in cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="06221-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for hello disks used by hello virtual machines in hello HDInsight cluster.</span></span>

    <span data-ttu-id="06221-119">Dischi gestiti sono abilitati per impostazione predefinita per Kafka in HDInsight e il numero di hello di dischi utilizzato per ogni nodo può essere configurato durante la creazione di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06221-119">Managed disks are enabled by default for Kafka on HDInsight, and hello number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="06221-120">Per altre informazioni sui dischi gestiti, vedere [Panoramica di Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="06221-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="06221-121">Per informazioni sulla configurazione di dischi gestiti con Kafka in HDInsight, vedere [Configurare l'archiviazione e la scalabilità per Apache Kafka in HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="06221-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="06221-122">Casi d'uso</span><span class="sxs-lookup"><span data-stu-id="06221-122">Use cases</span></span>

* <span data-ttu-id="06221-123">**Messaggistica**: poiché hello supporta il modello di messaggio di pubblicazione-sottoscrizione, Kafka viene spesso usato come broker di messaggi.</span><span class="sxs-lookup"><span data-stu-id="06221-123">**Messaging**: Since it supports hello publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="06221-124">**Rilevamento di attività**: Kafka poiché fornisce la registrazione nell'ordine dei record, può essere utilizzato tootrack e ricreare le attività.</span><span class="sxs-lookup"><span data-stu-id="06221-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used tootrack and re-create activities.</span></span> <span data-ttu-id="06221-125">Ad esempio, le azioni dell'utente in un sito Web o in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06221-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="06221-126">**Aggregazione**: utilizza l'elaborazione del flusso, è possibile aggregare informazioni da flussi diversi toocombine e centralizzare le informazioni di hello in dati operativi.</span><span class="sxs-lookup"><span data-stu-id="06221-126">**Aggregation**: Using stream processing, you can aggregate information from different streams toocombine and centralize hello information into operational data.</span></span>

* <span data-ttu-id="06221-127">**Trasformazione**: usando l'elaborazione dei flussi, è possibile combinare e arricchire dati da più argomenti di input in uno o più argomenti di output.</span><span class="sxs-lookup"><span data-stu-id="06221-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06221-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06221-128">Next steps</span></span>

<span data-ttu-id="06221-129">Seguente hello utilizzare collegamenti toolearn come toouse Kafka Apache in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="06221-129">Use hello following links toolearn how toouse Apache Kafka on HDInsight:</span></span>

* <span data-ttu-id="06221-130">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) (Introduzione a Kafka in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="06221-130">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>

* [<span data-ttu-id="06221-131">Utilizzare MirrorMaker toocreate una replica di Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="06221-131">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="06221-132">Usare Apache Storm (anteprima) con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="06221-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* <span data-ttu-id="06221-133">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="06221-133">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>

* [<span data-ttu-id="06221-134">Connettersi tooKafka tramite una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="06221-134">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
