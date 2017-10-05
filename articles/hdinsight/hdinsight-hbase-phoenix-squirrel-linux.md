---
title: Usare Apache Phoenix & SQuirreL con HBase - Azure HDInsight | Microsoft Docs
description: Informazioni su come usare Apache Phoenix in HDInsight e su come installare e configurare SQuirreL sulla workstation per la connessione a un cluster HBase in HDInsight.
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
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="52741-103">Usare Apache Phoenix con cluster HBase basati su Linux in HDinsight</span><span class="sxs-lookup"><span data-stu-id="52741-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="52741-104">Informazioni su come usare [Apache Phoenix](http://phoenix.apache.org/) in HDInsight e su come usare SQLLine.</span><span class="sxs-lookup"><span data-stu-id="52741-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="52741-105">Per altre informazioni su Phoenix, vedere la [breve panoramica su Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="52741-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="52741-106">Per la grammatica Phoenix, vedere [Grammatica Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="52741-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="52741-107">Per informazioni sulla versione di Phoenix in HDInsight, vedere l'articolo relativo alle [novità delle versioni cluster di Hadoop incluse in HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="52741-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="52741-108">Usare SQLLine</span><span class="sxs-lookup"><span data-stu-id="52741-108">Use SQLLine</span></span>
<span data-ttu-id="52741-109">[SQLLine](http://sqlline.sourceforge.net/) è un'utilità della riga di comando per eseguire SQL.</span><span class="sxs-lookup"><span data-stu-id="52741-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="52741-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="52741-110">Prerequisites</span></span>
<span data-ttu-id="52741-111">Per usare SQLLine sono necessari:</span><span class="sxs-lookup"><span data-stu-id="52741-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="52741-112">**Un cluster HBase in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="52741-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="52741-113">Per informazioni sul provisioning di un cluster HBase, vedere l'[introduzione all'uso di Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="52741-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="52741-114">**Connessione al cluster HBase tramite il file RDP (Remote Desktop Protocol)**.</span><span class="sxs-lookup"><span data-stu-id="52741-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="52741-115">Per istruzioni vedere [Gestire i cluster Hadoop in HDInsight con il portale di Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="52741-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="52741-116">Quando ci si connette a un cluster HBase, è necessario connettersi a uno dei Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="52741-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="52741-117">Ogni cluster HDInsight ha tre Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="52741-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="52741-118">**Per scoprire il nome host del Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="52741-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="52741-119">Aprire Ambari passando a **https://<ClusterName>.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="52741-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="52741-120">Immettere il nome utente e la password HTTP (cluster) per effettuare l’accesso.</span><span class="sxs-lookup"><span data-stu-id="52741-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="52741-121">Nel menu a sinistra fare clic su **ZooKeeper** .</span><span class="sxs-lookup"><span data-stu-id="52741-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="52741-122">Vengono elencate tre voci **ZooKeeper Server**.</span><span class="sxs-lookup"><span data-stu-id="52741-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="52741-123">Fare clic su una delle voci **ZooKeeper Server** dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="52741-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="52741-124">Nel riquadro Riepilogo trovare il **Nome host**.</span><span class="sxs-lookup"><span data-stu-id="52741-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="52741-125">Il formato è simile a *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="52741-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="52741-126">**Per usare SQLLine**</span><span class="sxs-lookup"><span data-stu-id="52741-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="52741-127">Connettersi al cluster tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="52741-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="52741-128">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="52741-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="52741-129">Da SSH eseguire i comandi seguenti per avviare SQLLine:</span><span class="sxs-lookup"><span data-stu-id="52741-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="52741-130">Eseguire i comandi seguenti per creare una tabella HBase e inserire alcuni dati:</span><span class="sxs-lookup"><span data-stu-id="52741-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="52741-131">Per altre informazioni, vedere il [manuale di SQLLine](http://sqlline.sourceforge.net/#manual) e la [grammatica Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="52741-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52741-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52741-132">Next steps</span></span>
<span data-ttu-id="52741-133">In questo articolo si è appreso come usare Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52741-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="52741-134">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="52741-134">To learn more, see:</span></span>

* <span data-ttu-id="52741-135">[Panoramica di HDInsight HBase][hdinsight-hbase-overview]: HBase è un database NoSQL open source Apache basato su Hadoop che fornisce un accesso casuale e coerenza assoluta a grandi quantità di dati non strutturati e semistrutturati.</span><span class="sxs-lookup"><span data-stu-id="52741-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="52741-136">[Effettuare il provisioning di cluster HBase nella rete virtuale di Azure][hdinsight-hbase-provision-vnet]: con l'integrazione con la rete virtuale, i cluster HBase possono essere distribuiti nella stessa rete virtuale delle applicazioni in modo che queste ultime possano comunicare direttamente con HBase.</span><span class="sxs-lookup"><span data-stu-id="52741-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="52741-137">[Configurare la replica HBase in HDInsight](hdinsight-hbase-replication.md): informazioni su come configurare la replica HBase in due data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="52741-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="52741-138">[Analizzare il sentiment di Twitter con HBase in HDInsight][hbase-twitter-sentiment]: informazioni su come eseguire l'[analisi del sentiment](http://en.wikipedia.org/wiki/Sentiment_analysis) dei Big Data usando HBase in un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52741-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
