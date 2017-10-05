---
title: "Eseguire l'aggiornamento del cluster HDInsight a una versione più recente: Azure | Microsoft Docs"
description: "Informazioni su come eseguire l'aggiornamento del cluster HDInsight a una versione più recente"
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: fa2e37bd922690322ccc3d8f68128180d013b701
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="a5933-103">Eseguire l'aggiornamento del cluster HDInsight a una versione più recente</span><span class="sxs-lookup"><span data-stu-id="a5933-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="a5933-104">Per poter sfruttare le funzionalità più recenti di HDInsight, è consigliabile che i cluster HDInsight siano aggiornati alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="a5933-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="a5933-105">Seguire le linee guida per aggiornare le versioni dei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a5933-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="a5933-106">Le versioni 3.2 e 3.3 dei cluster HDInsight sono prossime alla data di ritiro.</span><span class="sxs-lookup"><span data-stu-id="a5933-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="a5933-107">Per altre informazioni sulle versioni di HDInsight vedere [Versioni del componente HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="a5933-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="a5933-108">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="a5933-108">Upgrade tasks</span></span>
<span data-ttu-id="a5933-109">Il flusso di lavoro per eseguire l'aggiornamento del cluster HDInsight è il seguente.</span><span class="sxs-lookup"><span data-stu-id="a5933-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![Diagramma del flusso di lavoro di aggiornamento](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="a5933-111">Leggere interamente questo documento per comprendere le modifiche che potrebbero essere necessarie durante l'aggiornamento del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a5933-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="a5933-112">Creare un cluster come ambiente di test/controllo qualità.</span><span class="sxs-lookup"><span data-stu-id="a5933-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="a5933-113">Per altre informazioni sulla creazione di un cluster, vedere [Informazioni su come creare cluster HDInsight basati su Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a5933-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="a5933-114">Copiare processi esistenti, origini dati e sink nel nuovo ambiente.</span><span class="sxs-lookup"><span data-stu-id="a5933-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="a5933-115">Per altri dettagli vedere la sezione [Copiare i dati nell'ambiente di test](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment).</span><span class="sxs-lookup"><span data-stu-id="a5933-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="a5933-116">Eseguire il test di convalida per assicurarsi che i processi funzionino come previsto nel nuovo cluster.</span><span class="sxs-lookup"><span data-stu-id="a5933-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="a5933-117">Dopo avere verificato che tutto funzioni come previsto, pianificare i tempi di inattività per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="a5933-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="a5933-118">Durante questo periodo di inattività, eseguire le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="a5933-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="a5933-119">Eseguire il backup tutti i dati temporanei archiviati localmente sui nodi del cluster,</span><span class="sxs-lookup"><span data-stu-id="a5933-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="a5933-120">ad esempio se i dati sono archiviati direttamente in un nodo head.</span><span class="sxs-lookup"><span data-stu-id="a5933-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="a5933-121">Eliminare il cluster esistente.</span><span class="sxs-lookup"><span data-stu-id="a5933-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="a5933-122">Creare un cluster nella stessa subnet di rete virtuale con la versione più recente supportata di HDI, usando lo stesso archivio dati predefinito usato dal cluster precedente.</span><span class="sxs-lookup"><span data-stu-id="a5933-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="a5933-123">In questo modo il nuovo cluster continuerà a lavorare con i dati di produzione esistenti.</span><span class="sxs-lookup"><span data-stu-id="a5933-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="a5933-124">Importare i dati temporanei di cui è stata eseguita una copia di backup.</span><span class="sxs-lookup"><span data-stu-id="a5933-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="a5933-125">Avviare processi/continuare l'elaborazione con il nuovo cluster.</span><span class="sxs-lookup"><span data-stu-id="a5933-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5933-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5933-126">Next Steps</span></span>
* [<span data-ttu-id="a5933-127">Informazioni su come creare cluster HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="a5933-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="a5933-128">Connettersi a HDInsight tramite SSH</span><span class="sxs-lookup"><span data-stu-id="a5933-128">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="a5933-129">Gestire un cluster basato su Linux tramite Ambari</span><span class="sxs-lookup"><span data-stu-id="a5933-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

