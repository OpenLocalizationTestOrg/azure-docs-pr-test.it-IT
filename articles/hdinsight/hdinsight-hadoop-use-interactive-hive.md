---
title: aaaUse interattivo Hive in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse interattivo (Hive nel LLAP) Hive in HDInsight.
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="0f771-103">Usare Interactive Hive in HDInsight (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="0f771-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="0f771-104">Interactive Hive (o</span><span class="sxs-lookup"><span data-stu-id="0f771-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="0f771-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) è un nuovo [tipo di cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f771-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="0f771-106">Interactive Hive consente il caching delle query Hive, rendendo le stesse molto più interattive e veloci.</span><span class="sxs-lookup"><span data-stu-id="0f771-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="0f771-107">Questa nuova funzionalità rende HDInsight uno di hello la maggior parte delle ad alte prestazioni, flessibile e aperta Big Data le soluzioni del mondo nel cloud hello delle cache in memoria (tramite Hive e Spark) e la gestione avanzata analitica tramite una stretta integrazione con R Services.</span><span class="sxs-lookup"><span data-stu-id="0f771-107">This new feature makes HDInsight one of hello world’s most performant, flexible, and open Big Data solutions on hello cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="0f771-108">cluster Hive interattivo Hello è diverso da un cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="0f771-108">hello Interactive Hive cluster is different from hello Hadoop cluster.</span></span> <span data-ttu-id="0f771-109">Contiene solo il servizio di Hive hello.</span><span class="sxs-lookup"><span data-stu-id="0f771-109">It only contains hello Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f771-110">MapReduce, Pig, Sqoop, Oozie e altri servizi saranno presto rimossi da questo cluster.</span><span class="sxs-lookup"><span data-stu-id="0f771-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="0f771-111">servizio Hive nel cluster Hive interattivo hello Hello è accessibile solo tramite hello vista Ambari Hive, Beeline e Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="0f771-111">hello Hive service in hello Interactive Hive cluster is only accessible via hello Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="0f771-112">Non è possibile accedervi tramite console Hive, Templeton, interfaccia della riga di comando di Azure e Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f771-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="0f771-113">Creare un cluster Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="0f771-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="0f771-114">Il cluster Interactive Hive è supportato solo dai cluster basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="0f771-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="0f771-115">Per informazioni sulla creazione di cluster HDInsight, vedere [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0f771-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="0f771-116">Eseguire Hive da Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="0f771-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="0f771-117">Sono disponibili diverse opzioni per eseguire query Hive:</span><span class="sxs-lookup"><span data-stu-id="0f771-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="0f771-118">Eseguire Hive utilizzando hello Ambari Hive visualizzazione</span><span class="sxs-lookup"><span data-stu-id="0f771-118">Run Hive using hello Ambari Hive view</span></span>
  
    <span data-ttu-id="0f771-119">Per informazioni di hello sull'utilizzo di hello Hive visualizzazione, vedere [hello utilizzare Vista Hive con Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="0f771-119">For hello information about using hello Hive View, see [Use hello Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="0f771-120">Eseguire Hive tramite Beeline</span><span class="sxs-lookup"><span data-stu-id="0f771-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="0f771-121">Per informazioni di hello sull'utilizzo di Beeline in HDInsight, vedere [utilizzare Hive con Hadoop in HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="0f771-121">For hello information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="0f771-122">Utilizzare Beeline dal nodo head hello o un nodo del bordo vuoto.</span><span class="sxs-lookup"><span data-stu-id="0f771-122">You use Beeline from either hello headnode or an empty edge node.</span></span>  <span data-ttu-id="0f771-123">È consigliabile usare Beeline da un nodo perimetrale vuoto.</span><span class="sxs-lookup"><span data-stu-id="0f771-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="0f771-124">Per informazioni sulla creazione di un cluster HDInsight con un nodo perimetrale vuoto, vedere [Usare nodi perimetrali vuoti in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="0f771-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="0f771-125">Eseguire Hive tramite Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="0f771-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="0f771-126">Per informazioni di hello sull'utilizzo di ODBC Hive, vedere [tooHadoop connessione Excel con il driver ODBC di Microsoft Hive hello](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="0f771-126">For hello information on using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="0f771-127">**hello toofind stringa di connessione JDBC:**</span><span class="sxs-lookup"><span data-stu-id="0f771-127">**toofind hello JDBC connection string:**</span></span>

1. <span data-ttu-id="0f771-128">Accedere utilizzando l'URL seguente hello tooAmbari: https://<ClusterName>. Cluster>.azurehdinsight.NET.</span><span class="sxs-lookup"><span data-stu-id="0f771-128">Sign on tooAmbari using hello following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="0f771-129">Fare clic su **Hive** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="0f771-129">Click **Hive** from hello left menu.</span></span>
3. <span data-ttu-id="0f771-130">Fare clic su hello evidenziato icona toocopy hello URL:</span><span class="sxs-lookup"><span data-stu-id="0f771-130">Click hello highlighted icon toocopy hello URL:</span></span>
   
   ![JDBC di HDInsight Hadoop Interactive Hive LLAP](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="0f771-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0f771-132">See also</span></span>
* <span data-ttu-id="0f771-133">[Creare i cluster basati su Linux, Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informazioni su come i cluster toocreate interattivo Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f771-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how toocreate Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="0f771-134">[Usare l'Hive con Hadoop in HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md): informazioni su come le query Hive di toouse Beeline toosubmit.</span><span class="sxs-lookup"><span data-stu-id="0f771-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how toouse Beeline toosubmit Hive queries.</span></span>
* <span data-ttu-id="0f771-135">[Connettere Excel tooHadoop con hello Hive di Microsoft ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): informazioni su come tooconnect tooHive di Excel.</span><span class="sxs-lookup"><span data-stu-id="0f771-135">[Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how tooconnect Excel tooHive.</span></span>

