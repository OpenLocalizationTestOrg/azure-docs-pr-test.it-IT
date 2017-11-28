---
title: aaaUse Apache Phoenix & esce con HBase - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse Phoenix Apache in HDInsight e come tooinstall e configurare esce sul cluster workstation tooconnect tooan HBase in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="ddf58-103">Usare Apache Phoenix con cluster HBase basati su Linux in HDinsight</span><span class="sxs-lookup"><span data-stu-id="ddf58-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="ddf58-104">Informazioni su come toouse [Phoenix Apache](http://phoenix.apache.org/) in HDInsight e come toouse SQLLine.</span><span class="sxs-lookup"><span data-stu-id="ddf58-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="ddf58-105">Per altre informazioni su Phoenix, vedere la [breve panoramica su Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="ddf58-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="ddf58-106">Per hello grammatica Phoenix, vedere [grammatica Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="ddf58-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="ddf58-107">Per informazioni sulla versione Phoenix in HDInsight hello, vedere [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ddf58-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="ddf58-108">Usare SQLLine</span><span class="sxs-lookup"><span data-stu-id="ddf58-108">Use SQLLine</span></span>
<span data-ttu-id="ddf58-109">[SQLLine](http://sqlline.sourceforge.net/) è tooexecute un'utilità della riga di comando SQL.</span><span class="sxs-lookup"><span data-stu-id="ddf58-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ddf58-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ddf58-110">Prerequisites</span></span>
<span data-ttu-id="ddf58-111">Prima di poter utilizzare SQLLine, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="ddf58-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="ddf58-112">**Un cluster HBase in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ddf58-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="ddf58-113">Per informazioni sul provisioning di un cluster HBase, vedere l'[introduzione all'uso di Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="ddf58-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="ddf58-114">**Connettere il cluster HBase toohello tramite protocollo desktop remoto hello**.</span><span class="sxs-lookup"><span data-stu-id="ddf58-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="ddf58-115">Per istruzioni, vedere [hello di cluster di gestire Hadoop in HDInsight mediante il portale di Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="ddf58-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="ddf58-116">Quando ci si connette cluster HBase tooan, è necessario tooone tooconnect di hello Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="ddf58-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="ddf58-117">Ogni cluster HDInsight ha tre Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="ddf58-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="ddf58-118">**toofind il nome host di hello Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="ddf58-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="ddf58-119">Aprire Ambari esplorando troppo**https://<ClusterName>. cluster>.azurehdinsight.NET**.</span><span class="sxs-lookup"><span data-stu-id="ddf58-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="ddf58-120">Immettere nome utente e password toologin HTTP (cluster) di hello.</span><span class="sxs-lookup"><span data-stu-id="ddf58-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="ddf58-121">Fare clic su **ZooKeeper** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="ddf58-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="ddf58-122">Vengono elencate tre voci **ZooKeeper Server**.</span><span class="sxs-lookup"><span data-stu-id="ddf58-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="ddf58-123">Fare clic su uno di hello **ZooKeeper Server** elencati.</span><span class="sxs-lookup"><span data-stu-id="ddf58-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="ddf58-124">Nel riquadro Riepilogo hello trovare hello **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="ddf58-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="ddf58-125">È simile troppo*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="ddf58-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="ddf58-126">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="ddf58-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="ddf58-127">Connettere il cluster toohello tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="ddf58-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="ddf58-128">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ddf58-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ddf58-129">Da SSH, eseguire hello comandi toorun SQLLine seguenti:</span><span class="sxs-lookup"><span data-stu-id="ddf58-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="ddf58-130">Esecuzione di una tabella HBase hello toocreate i comandi seguenti e inserire alcuni dati:</span><span class="sxs-lookup"><span data-stu-id="ddf58-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="ddf58-131">Per altre informazioni, vedere il [manuale di SQLLine](http://sqlline.sourceforge.net/#manual) e la [grammatica Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="ddf58-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddf58-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ddf58-132">Next steps</span></span>
<span data-ttu-id="ddf58-133">In questo articolo, si è appreso come toouse Phoenix Apache in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ddf58-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="ddf58-134">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="ddf58-134">toolearn more, see:</span></span>

* <span data-ttu-id="ddf58-135">[Panoramica di HDInsight HBase][hdinsight-hbase-overview]: HBase è un database NoSQL open source Apache basato su Hadoop che fornisce un accesso casuale e coerenza assoluta a grandi quantità di dati non strutturati e semistrutturati.</span><span class="sxs-lookup"><span data-stu-id="ddf58-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="ddf58-136">[Eseguire il provisioning di cluster HBase in rete virtuale di Azure][hdinsight-hbase-provision-vnet]: con l'integrazione di rete virtuale cluster HBase può essere distribuito toohello stessa virtuale rete delle applicazioni in modo che le applicazioni possono comunicare con HBase direttamente.</span><span class="sxs-lookup"><span data-stu-id="ddf58-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="ddf58-137">[Configurare la replica di HBase in HDInsight](hdinsight-hbase-replication.md): informazioni su come la replica di HBase tooconfigure tra due Data Center di Azure.</span><span class="sxs-lookup"><span data-stu-id="ddf58-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="ddf58-138">[Analizzare Twitter sentiment con HBase in HDInsight][hbase-twitter-sentiment]: informazioni su come toodo in tempo reale [analisi del sentiment](http://en.wikipedia.org/wiki/Sentiment_analysis) dei big data dall'utilizzo di HBase in un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ddf58-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
