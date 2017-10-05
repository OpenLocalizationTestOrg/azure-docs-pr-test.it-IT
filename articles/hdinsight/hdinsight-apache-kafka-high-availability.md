---
title: "Disponibilità elevata con Apache Kafka: Azure HDInsight| Microsoft Docs"
description: "Informazioni su come garantire disponibilità elevata con Apache Kafka in Azure HDInsight. Questo articolo illustra come ribilanciare le repliche di partizione in Kafka in modo che siano incluse in domini di errore diversi all'interno dell'area di Azure contenente HDInsight."
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
ms.openlocfilehash: f8164d1c3483b28e5f2abcc8035da78880daec1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="aee51-104">Disponibilità elevata dei dati con Apache Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="aee51-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="aee51-105">Questo articolo illustra come configurare le repliche di partizione per gli argomenti Kafka in modo da sfruttare la configurazione rack hardware sottostante,</span><span class="sxs-lookup"><span data-stu-id="aee51-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="aee51-106">che garantisce la disponibilità dei dati archiviati in Apache Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aee51-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="aee51-107">Domini di errore e di aggiornamento con Kafka</span><span class="sxs-lookup"><span data-stu-id="aee51-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="aee51-108">Un dominio di errore è un raggruppamento logico dell'hardware sottostante in un data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="aee51-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="aee51-109">Ogni dominio di errore condivide una fonte di alimentazione e un commutatore di rete comuni.</span><span class="sxs-lookup"><span data-stu-id="aee51-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="aee51-110">Le macchine virtuali e i dischi gestiti che implementano i nodi in un cluster HDInsight sono distribuiti tra i domini di errore.</span><span class="sxs-lookup"><span data-stu-id="aee51-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="aee51-111">Questa architettura limita il potenziale impatto dei guasti dell'hardware fisico.</span><span class="sxs-lookup"><span data-stu-id="aee51-111">This architecture limits the potential impact of physical hardware failures.</span></span>

<span data-ttu-id="aee51-112">Ogni area di Azure include un numero specifico di domini di errore.</span><span class="sxs-lookup"><span data-stu-id="aee51-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="aee51-113">Per un elenco dei domini e il numero dei domini di errore in essi contenuti, vedere la documentazione relativa ai [set di disponibilità](../virtual-machines/linux/regions-and-availability.md#availability-sets).</span><span class="sxs-lookup"><span data-stu-id="aee51-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aee51-114">Kafka non rileva i domini di errore.</span><span class="sxs-lookup"><span data-stu-id="aee51-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="aee51-115">Quando si crea un argomento in Kafka, tutte le partizioni di replica potrebbero essere archiviate nello stesso dominio di errore.</span><span class="sxs-lookup"><span data-stu-id="aee51-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span></span> <span data-ttu-id="aee51-116">Per risolvere il problema, è disponibile uno [strumento per il ribilanciamento delle partizioni Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="aee51-116">To solve this problem, we provide the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-to-rebalance-partition-replicas"></a><span data-ttu-id="aee51-117">Quando ribilanciare le repliche di partizione</span><span class="sxs-lookup"><span data-stu-id="aee51-117">When to rebalance partition replicas</span></span>

<span data-ttu-id="aee51-118">Per garantire la massima disponibilità dei dati Kafka, è consigliabile ribilanciare le repliche di partizione per l'argomento nei momenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aee51-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span></span>

* <span data-ttu-id="aee51-119">Quando viene creato un nuovo argomento o una nuova partizione</span><span class="sxs-lookup"><span data-stu-id="aee51-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="aee51-120">Quando si aumentano le prestazioni di un cluster</span><span class="sxs-lookup"><span data-stu-id="aee51-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="aee51-121">Fattore di replica</span><span class="sxs-lookup"><span data-stu-id="aee51-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aee51-122">È consigliabile usare un'area di Azure contenente tre domini di errore e un fattore di replica di 3.</span><span class="sxs-lookup"><span data-stu-id="aee51-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="aee51-123">Se si deve usare un'area che contiene solo due domini di errore, usare un fattore di replica di 4 per distribuire uniformemente le repliche tra i due domini di errore.</span><span class="sxs-lookup"><span data-stu-id="aee51-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span></span>

<span data-ttu-id="aee51-124">Per un esempio della creazione di argomenti e dell'impostazione del fattore di replica, vedere il documento su come [iniziare a usare Kafka in HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aee51-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-to-rebalance-partition-replicas"></a><span data-ttu-id="aee51-125">Come ribilanciare le repliche di partizione</span><span class="sxs-lookup"><span data-stu-id="aee51-125">How to rebalance partition replicas</span></span>

<span data-ttu-id="aee51-126">Usare lo [strumento per il ribilanciamento delle partizioni Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) per ribilanciare gli argomenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="aee51-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span></span> <span data-ttu-id="aee51-127">Questo strumento deve essere eseguito da una sessione SSH al nodo head del cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="aee51-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span></span>

<span data-ttu-id="aee51-128">Per altre informazioni sulla connessione a HDInsight con SSH, vedere il documento su come [usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aee51-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aee51-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aee51-129">Next steps</span></span>

* [<span data-ttu-id="aee51-130">Scalabilità di Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="aee51-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="aee51-131">Mirroring con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="aee51-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)