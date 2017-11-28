---
title: dati del sensore aaaAnalyze con Hive e Hadoop - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come dati del sensore tooanalyze utilizzando hello la Console di Query Hive con HDInsight (Hadoop), quindi visualizzare i dati in Microsoft Excel con PowerView hello.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="5fe60-103">Analizzare i dati del sensore utilizzando la Console di Query Hive hello in Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5fe60-103">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="5fe60-104">Informazioni su come dati del sensore tooanalyze utilizzando hello la Console di Query Hive con HDInsight (Hadoop), quindi visualizzare i dati di hello in Microsoft Excel tramite Power View.</span><span class="sxs-lookup"><span data-stu-id="5fe60-104">Learn how tooanalyze sensor data by using hello Hive Query Console with HDInsight (Hadoop), then visualize hello data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fe60-105">Hello passaggi di questa operazione solo documenti con i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="5fe60-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="5fe60-106">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="5fe60-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="5fe60-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="5fe60-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5fe60-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5fe60-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="5fe60-109">In questo esempio, utilizzare i dati cronologici tooprocess Hive e identificare i problemi con i sistemi di riscaldamento e aria condizionata.</span><span class="sxs-lookup"><span data-stu-id="5fe60-109">In this sample, you use Hive tooprocess historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="5fe60-110">In particolare, identificare i sistemi sono tooreliably non è possibile mantenere una temperatura set eseguendo hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="5fe60-110">Specifically, you identify systems are not able tooreliably maintain a set temperature by performing hello following tasks:</span></span>

* <span data-ttu-id="5fe60-111">Creare tabelle di HIVE tooquery dati archiviati in file separati da virgole (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="5fe60-111">Create HIVE tables tooquery data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="5fe60-112">Creare query HIVE dati hello tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="5fe60-112">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="5fe60-113">i dati analizzato hello tooretrieve, utilizzare tooHDInsight tooconnect Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="5fe60-113">tooretrieve hello analyzed data, use Microsoft Excel tooconnect tooHDInsight.</span></span>
* <span data-ttu-id="5fe60-114">dati hello toovisualize, utilizzare Power View.</span><span class="sxs-lookup"><span data-stu-id="5fe60-114">toovisualize hello data, use Power View.</span></span>

![Un diagramma dell'architettura della soluzione hello](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="5fe60-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5fe60-116">Prerequisites</span></span>

* <span data-ttu-id="5fe60-117">Cluster HDInsight (Hadoop) - Per informazioni sulla creazione di un cluster, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5fe60-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="5fe60-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="5fe60-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="5fe60-119">Microsoft Excel viene usato per la visualizzazione dei dati con [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="5fe60-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="5fe60-120">Microsoft Hive ODBC Driver</span><span class="sxs-lookup"><span data-stu-id="5fe60-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a><span data-ttu-id="5fe60-121">esempio hello toorun</span><span class="sxs-lookup"><span data-stu-id="5fe60-121">toorun hello sample</span></span>

1. <span data-ttu-id="5fe60-122">Dal web browser, passare toohello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="5fe60-122">From your web browser, navigate toohello following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="5fe60-123">Sostituire `<clustername>` con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5fe60-123">Replace `<clustername>` with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="5fe60-124">Quando richiesto, eseguire l'autenticazione tramite nome utente dell'amministratore hello e la password utilizzati durante il provisioning di questo cluster.</span><span class="sxs-lookup"><span data-stu-id="5fe60-124">When prompted, authenticate by using hello administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="5fe60-125">Dalla pagina web hello visualizzata, fare clic su hello **raccolta di introduzione** scheda, quindi in hello **soluzioni con dati di esempio** categoria, fare clic su hello **analisi dei dati del sensore** esempio di.</span><span class="sxs-lookup"><span data-stu-id="5fe60-125">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Sensor Data Analysis** sample.</span></span>

    ![Immagine della raccolta introduttiva](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="5fe60-127">Istruzioni di hello fornita nell'esempio di hello toofinish hello pagina web.</span><span class="sxs-lookup"><span data-stu-id="5fe60-127">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>
