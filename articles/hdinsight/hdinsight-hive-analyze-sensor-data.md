---
title: Analizzare i dati dei sensori con Hive e Hadoop - Azure HDInsight | Microsoft Docs
description: Informazioni su come analizzare i dati dei sensori usando Hive Query Console con HDInsight (Hadoop) e quindi visualizzare i dati in Microsoft Excel mediante Power View.
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
ms.openlocfilehash: 3abb71c12b4769bebd808276f8bdd832aad22d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="08ad1-103">Analizzare i dati dei sensori mediante Hive Query Console su Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="08ad1-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="08ad1-104">Informazioni su come analizzare i dati dei sensori usando Hive Query Console con HDInsight (Hadoop) e quindi visualizzare i dati in Microsoft Excel mediante Power View.</span><span class="sxs-lookup"><span data-stu-id="08ad1-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08ad1-105">I passaggi descritti in questo documento funzionano solo con i cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="08ad1-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="08ad1-106">HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="08ad1-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="08ad1-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="08ad1-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="08ad1-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="08ad1-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="08ad1-109">In questo esempio, usare Hive per elaborare i dati cronologici e identificare i problemi con i sistemi di riscaldamento e condizionamento dell'aria.</span><span class="sxs-lookup"><span data-stu-id="08ad1-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="08ad1-110">In particolare, identificare sistemi che non sono in grado di mantenere in modo affidabile una temperatura impostata eseguendo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="08ad1-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="08ad1-111">Creare tabelle HIVE per eseguire query su dati archiviati in file con valori delimitati da virgole (CSV).</span><span class="sxs-lookup"><span data-stu-id="08ad1-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="08ad1-112">Creare query HIVE per analizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="08ad1-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="08ad1-113">Usare Microsoft Excel per connettersi a HDInsight per recuperare i dati analizzati.</span><span class="sxs-lookup"><span data-stu-id="08ad1-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="08ad1-114">Usare Power View per visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="08ad1-114">To visualize the data, use Power View.</span></span>

![Diagramma dell'architettura della soluzione](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="08ad1-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="08ad1-116">Prerequisites</span></span>

* <span data-ttu-id="08ad1-117">Cluster HDInsight (Hadoop) - Per informazioni sulla creazione di un cluster, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="08ad1-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="08ad1-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="08ad1-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="08ad1-119">Microsoft Excel viene usato per la visualizzazione dei dati con [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="08ad1-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="08ad1-120">Microsoft Hive ODBC Driver</span><span class="sxs-lookup"><span data-stu-id="08ad1-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="08ad1-121">Per eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="08ad1-121">To run the sample</span></span>

1. <span data-ttu-id="08ad1-122">Aprire un Web browser e passare all'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="08ad1-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="08ad1-123">Sostituire `<clustername>` con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="08ad1-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="08ad1-124">Quando richiesto, eseguire l'autenticazione con il nome utente e la password dell'amministratore usati durante il provisioning di questo cluster.</span><span class="sxs-lookup"><span data-stu-id="08ad1-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="08ad1-125">Nella pagina Web visualizzata fare clic sulla scheda **Guida introduttiva** e quindi sull'esempio **Analisi dei dati dei sensori** nella categoria **Soluzioni con dati di esempio**.</span><span class="sxs-lookup"><span data-stu-id="08ad1-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![Immagine della raccolta introduttiva](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="08ad1-127">Seguire le istruzioni fornite nella pagina Web per completare l'esempio.</span><span class="sxs-lookup"><span data-stu-id="08ad1-127">Follow the instructions provided on the web page to finish the sample.</span></span>
