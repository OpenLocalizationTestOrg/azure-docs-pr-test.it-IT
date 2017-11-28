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
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="368f8-104">Disponibilità elevata dei dati con Apache Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="368f8-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="368f8-105">Informazioni su come le repliche delle partizioni tooconfigure per Kafka argomenti tootake sfruttare hardware sottostante rack configurazione.</span><span class="sxs-lookup"><span data-stu-id="368f8-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="368f8-106">Questa configurazione assicura la disponibilità di hello dei dati archiviati in Apache Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="368f8-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="368f8-107">Domini di errore e di aggiornamento con Kafka</span><span class="sxs-lookup"><span data-stu-id="368f8-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="368f8-108">Un dominio di errore è un raggruppamento logico dell'hardware sottostante in un data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="368f8-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="368f8-109">Ogni dominio di errore condivide una fonte di alimentazione e un commutatore di rete comuni.</span><span class="sxs-lookup"><span data-stu-id="368f8-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="368f8-110">Hello le macchine virtuali e dischi gestiti che implementano i nodi di hello all'interno di un cluster HDInsight vengono distribuiti tra i domini di errore.</span><span class="sxs-lookup"><span data-stu-id="368f8-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="368f8-111">Questa architettura limita l'impatto potenziale di hello dei guasti hardware fisico.</span><span class="sxs-lookup"><span data-stu-id="368f8-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="368f8-112">Ogni area di Azure include un numero specifico di domini di errore.</span><span class="sxs-lookup"><span data-stu-id="368f8-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="368f8-113">Per un elenco di domini e il numero di hello di domini di errore contengono, vedere hello [set di disponibilità](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentazione.</span><span class="sxs-lookup"><span data-stu-id="368f8-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="368f8-114">Kafka non rileva i domini di errore.</span><span class="sxs-lookup"><span data-stu-id="368f8-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="368f8-115">Quando si crea un argomento in Kafka, è possibile archiviare tutte le repliche di partizione in hello stesso dominio di errore.</span><span class="sxs-lookup"><span data-stu-id="368f8-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="368f8-116">toosolve questo problema, forniamo hello [strumento ribilanciamento delle partizioni Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="368f8-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="368f8-117">Quando toorebalance partizione repliche</span><span class="sxs-lookup"><span data-stu-id="368f8-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="368f8-118">tooensure hello massima disponibilità dei dati Kafka, è necessario ribilanciare le repliche delle partizioni hello per l'argomento in seguito volte hello:</span><span class="sxs-lookup"><span data-stu-id="368f8-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="368f8-119">Quando viene creato un nuovo argomento o una nuova partizione</span><span class="sxs-lookup"><span data-stu-id="368f8-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="368f8-120">Quando si aumentano le prestazioni di un cluster</span><span class="sxs-lookup"><span data-stu-id="368f8-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="368f8-121">Fattore di replica</span><span class="sxs-lookup"><span data-stu-id="368f8-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="368f8-122">È consigliabile usare un'area di Azure contenente tre domini di errore e un fattore di replica di 3.</span><span class="sxs-lookup"><span data-stu-id="368f8-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="368f8-123">Se è necessario utilizzare un'area che contiene solo due domini di errore, utilizzare un fattore di replica delle repliche di hello toospread 4 in modo uniforme tra i due domini di errore hello.</span><span class="sxs-lookup"><span data-stu-id="368f8-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="368f8-124">Per un esempio di creazione di argomenti e fattore di replica hello impostazione, vedere hello [iniziano con Kafka in HDInsight](hdinsight-apache-kafka-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="368f8-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="368f8-125">Le repliche delle partizioni toorebalance</span><span class="sxs-lookup"><span data-stu-id="368f8-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="368f8-126">Hello utilizzare [strumento ribilanciamento delle partizioni Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selezionato argomenti.</span><span class="sxs-lookup"><span data-stu-id="368f8-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="368f8-127">Questo strumento deve essere eseguito da un nodo head di toohello sessione SSH del cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="368f8-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="368f8-128">Per ulteriori informazioni sulla connessione tooHDInsight tramite SSH, vedere il [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="368f8-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="368f8-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="368f8-129">Next steps</span></span>

* [<span data-ttu-id="368f8-130">Scalabilità di Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="368f8-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="368f8-131">Mirroring con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="368f8-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)