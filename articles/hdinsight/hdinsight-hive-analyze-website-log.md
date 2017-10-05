---
title: Usare Hive con Hadoop per l'analisi dei log dei siti Web - Azure HDInsight | Microsoft Docs
description: "Informazioni su come usare Hive con HDInsight per analizzare i log dei siti Web. Si userà un file di log come input in una tabella di HDInsight e HiveQL per eseguire query sui dati."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: e1cdb786bb6049980aafc0213abf53013e342618
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="7933e-104">Usare Hive con HDInsight basato su Windows per analizzare i log dei siti Web</span><span class="sxs-lookup"><span data-stu-id="7933e-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="7933e-105">Informazioni su come usare HiveQL con HDInsight per analizzare i log di un sito Web.</span><span class="sxs-lookup"><span data-stu-id="7933e-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="7933e-106">L'analisi dei log dei siti Web può essere usata per segmentare il proprio pubblico in base ad attività simili, classificare i visitatori di un sito in base a dati demografici e scoprire i contenuti che visualizzano, da quali siti Web sono stati indirizzati e così via.</span><span class="sxs-lookup"><span data-stu-id="7933e-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7933e-107">I passaggi descritti in questo documento funzionano solo con i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="7933e-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="7933e-108">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="7933e-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="7933e-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="7933e-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7933e-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7933e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="7933e-111">In questo esempio si userà un cluster HDInsight per analizzare i file di log dei siti Web e ottenere informazioni dettagliate sulla frequenza delle visite da siti Web esterni nell'arco di una giornata.</span><span class="sxs-lookup"><span data-stu-id="7933e-111">In this sample, you will use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="7933e-112">Si genererà inoltre un riepilogo degli errori dei siti Web riscontrati dagli utenti.</span><span class="sxs-lookup"><span data-stu-id="7933e-112">You'll also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="7933e-113">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="7933e-113">You will learn how to:</span></span>

* <span data-ttu-id="7933e-114">Connettersi a un archivio BLOB di Azure, che contiene i file di log dei siti Web.</span><span class="sxs-lookup"><span data-stu-id="7933e-114">Connect to a Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="7933e-115">Creare tabelle HIVE per eseguire query su tali log.</span><span class="sxs-lookup"><span data-stu-id="7933e-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="7933e-116">Creare query HIVE per analizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="7933e-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="7933e-117">Usare Microsoft Excel per connettersi a HDInsight (mediante una connessione ODBC) per recuperare i dati analizzati.</span><span class="sxs-lookup"><span data-stu-id="7933e-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="7933e-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7933e-119">Prerequisites</span></span>
* <span data-ttu-id="7933e-120">È necessario avere completato il provisioning di un cluster Hadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7933e-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="7933e-121">Per istruzioni, vedere [Provisioning di cluster HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="7933e-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="7933e-122">È necessario aver installato Microsoft Excel 2013 o Excel 2010.</span><span class="sxs-lookup"><span data-stu-id="7933e-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="7933e-123">Per importare i dati da Hive in Excel è necessario aver installato [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) .</span><span class="sxs-lookup"><span data-stu-id="7933e-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="7933e-124">Per eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="7933e-124">To run the sample</span></span>
1. <span data-ttu-id="7933e-125">Dal [portale di Azure](https://portal.azure.com/), dalla schermata iniziale (se il cluster è stato aggiunto lì), fare clic sul riquadro del cluster in cui si desidera eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="7933e-125">From the [Azure Portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="7933e-126">Dal pannello del cluster, in **Collegamenti rapidi**, fare clic su **Dashboard cluster**, quindi dal pannello **Dashboard cluster** fare clic su **Dashboard cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7933e-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="7933e-127">In alternativa, è possibile aprire direttamente la dashboard usando l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="7933e-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="7933e-128">Quando richiesto, eseguire l'autenticazione con il nome utente e la password dell'amministratore usati durante il provisioning del cluster.</span><span class="sxs-lookup"><span data-stu-id="7933e-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="7933e-129">Nella pagina Web visualizzata fare clic sulla scheda **Getting Started Gallery** (Guida introduttiva) e quindi nella categoria **Solutions with Sample Data** (Soluzioni con dati di esempio) fare clic sull'esempio **Analisi dei log del sito Web**.</span><span class="sxs-lookup"><span data-stu-id="7933e-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="7933e-130">Seguire le istruzioni fornite nella pagina Web per completare l'esempio.</span><span class="sxs-lookup"><span data-stu-id="7933e-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7933e-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7933e-131">Next steps</span></span>
<span data-ttu-id="7933e-132">Provare l'esempio seguente: [Analizzare i dati dei sensori mediante Hive con HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="7933e-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
