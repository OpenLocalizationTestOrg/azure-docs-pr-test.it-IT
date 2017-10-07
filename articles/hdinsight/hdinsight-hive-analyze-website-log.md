---
title: aaaUse Hive con Hadoop per l'analisi dei log del sito Web - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su modalità di registrazione toouse Hive con sito Web tooanalyze HDInsight. Verranno utilizzare un file di log come input in una tabella di HDInsight e utilizzare i dati di hello tooquery HiveQL."
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
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="69311-104">Usare l'Hive con i log di tooanalyze HDInsight basati su Windows dai siti Web</span><span class="sxs-lookup"><span data-stu-id="69311-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="69311-105">Informazioni su modalità di registrazione toouse HiveQL con tooanalyze HDInsight da un sito Web.</span><span class="sxs-lookup"><span data-stu-id="69311-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="69311-106">Analisi dei log del sito Web può essere utilizzato toosegment i destinatari in base alle attività simili, classificare i visitatori del sito da dati demografici e toofind visualizzano il contenuto di hello, provengono da siti Web di hello e così via.</span><span class="sxs-lookup"><span data-stu-id="69311-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69311-107">Hello passaggi di questa operazione solo documenti con i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="69311-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="69311-108">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="69311-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="69311-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="69311-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="69311-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="69311-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="69311-111">In questo esempio, si utilizzerà una HDInsight cluster tooanalyze sito Web log file tooget approfondite frequenza hello del sito Web di toohello visite a siti Web esterni in un giorno.</span><span class="sxs-lookup"><span data-stu-id="69311-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="69311-112">Verrà anche generato un riepilogo degli errori di sito Web che gli utenti di hello.</span><span class="sxs-lookup"><span data-stu-id="69311-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="69311-113">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="69311-113">You will learn how to:</span></span>

* <span data-ttu-id="69311-114">Connettersi tooa archiviazione Blob di Azure, che contiene i file di registro del sito Web.</span><span class="sxs-lookup"><span data-stu-id="69311-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="69311-115">Creare HIVE tabelle tooquery tali log.</span><span class="sxs-lookup"><span data-stu-id="69311-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="69311-116">Creare query HIVE dati hello tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="69311-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="69311-117">Utilizzare Microsoft Excel tooconnect tooHDInsight (utilizzando i dati di hello analizzato tooretrieve di open database connectivity (ODBC).</span><span class="sxs-lookup"><span data-stu-id="69311-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="69311-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="69311-119">Prerequisites</span></span>
* <span data-ttu-id="69311-120">È necessario avere completato il provisioning di un cluster Hadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="69311-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="69311-121">Per istruzioni, vedere [Provisioning di cluster HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="69311-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="69311-122">È necessario aver installato Microsoft Excel 2013 o Excel 2010.</span><span class="sxs-lookup"><span data-stu-id="69311-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="69311-123">È necessario disporre di [Driver ODBC di Microsoft Hive](http://www.microsoft.com/download/details.aspx?id=40886) dati tooimport dall'Hive in Excel.</span><span class="sxs-lookup"><span data-stu-id="69311-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="69311-124">esempio hello toorun</span><span class="sxs-lookup"><span data-stu-id="69311-124">toorun hello sample</span></span>
1. <span data-ttu-id="69311-125">Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale (se è stato aggiunto sono cluster hello) hello, fare clic su riquadro cluster hello in cui si desidera toorun: esempio hello.</span><span class="sxs-lookup"><span data-stu-id="69311-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="69311-126">Da hello cluster pannello in **collegamenti rapidi**, fare clic su **Dashboard Cluster**e quindi da hello **Dashboard del Cluster** pannello, fare clic su **HDInsight Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="69311-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="69311-127">In alternativa, è possibile aprire direttamente il dashboard di hello utilizzando hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="69311-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="69311-128">Quando richiesto, eseguire l'autenticazione tramite nome utente dell'amministratore hello e la password utilizzati durante il provisioning di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="69311-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="69311-129">Dalla pagina web hello visualizzata, fare clic su hello **raccolta di introduzione** scheda, quindi in hello **soluzioni con dati di esempio** categoria, fare clic su hello **analisi dei Log del sito Web** esempio di.</span><span class="sxs-lookup"><span data-stu-id="69311-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="69311-130">Istruzioni di hello fornita nell'esempio di hello toofinish hello pagina web.</span><span class="sxs-lookup"><span data-stu-id="69311-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69311-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69311-131">Next steps</span></span>
<span data-ttu-id="69311-132">Provare hello seguente esempio: [analisi dei dati del sensore con Hive di HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="69311-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
