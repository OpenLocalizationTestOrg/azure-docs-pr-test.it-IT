---
title: Eseguire il debug e analizzare i servizi Hadoop con i dump dell'heap - Azure | Microsoft Docs
description: Raccogliere automaticamente i dump dell'heap per i servizi Hadoop e inserirli nell'account di archiviazione BLOB di Azure per il debug e l'analisi.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6d1d4d47d279eb7a1f0bf1f587445683f0ace7a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="collect-heap-dumps-in-blob-storage-to-debug-and-analyze-hadoop-services"></a><span data-ttu-id="fa308-103">Raccogliere i dump dell'heap nell'archivio BLOB per eseguire il debug e analizzare i servizi Hadoop</span><span class="sxs-lookup"><span data-stu-id="fa308-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="fa308-104">I dump dell'heap includono uno snapshot della memoria dell'applicazione, ad esempio i valori delle variabili al momento della creazione del dump.</span><span class="sxs-lookup"><span data-stu-id="fa308-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="fa308-105">Si rivelano quindi utili per diagnosticare i problemi che si verificano in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fa308-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="fa308-106">È possibile raccogliere automaticamente i dump dell'heap per i servizi Hadoop e posizionarli nell'account di archiviazione BLOB di Azure di un utente in HDInsightHeapDumps/.</span><span class="sxs-lookup"><span data-stu-id="fa308-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="fa308-107">La raccolta di dump dell'heap relativi ai diversi servizi deve essere abilitata sui singoli cluster.</span><span class="sxs-lookup"><span data-stu-id="fa308-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="fa308-108">Per impostazione predefinita, questa funzionalità è disattivata per un cluster.</span><span class="sxs-lookup"><span data-stu-id="fa308-108">The default for this feature is to be off for a cluster.</span></span> <span data-ttu-id="fa308-109">Poiché i dump dell'heap possono avere dimensioni elevate, è consigliabile monitorare l'account di archiviazione BLOB in cui vengono salvati dopo l'abilitazione della raccolta.</span><span class="sxs-lookup"><span data-stu-id="fa308-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa308-110">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="fa308-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fa308-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fa308-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="fa308-112">Le informazioni contenute in questo articolo si applicano solo a HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="fa308-112">The information in this article only applies to Windows-based HDInsight.</span></span> <span data-ttu-id="fa308-113">Per informazioni su HDInsight basato su Linux, vedere [Abilitare i dump dell'heap per i servizi Hadoop in HDInsight basato su Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="fa308-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="fa308-114">Servizi idonei per i dump dell'heap</span><span class="sxs-lookup"><span data-stu-id="fa308-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="fa308-115">È possibile abilitare dump dell'heap per i servizi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa308-115">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="fa308-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="fa308-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="fa308-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="fa308-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="fa308-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="fa308-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="fa308-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="fa308-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="fa308-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="fa308-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="fa308-121">Elementi di configurazione per l'abilitazione dei dump dell'heap</span><span class="sxs-lookup"><span data-stu-id="fa308-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="fa308-122">Per attivare i dump di heap per un servizio, è necessario impostare gli elementi di configurazione appropriati nella sezione relativa al servizio in questione, specificata da **service_name**.</span><span class="sxs-lookup"><span data-stu-id="fa308-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="fa308-123">Il valore di **service_name** può essere uno qualsiasi dei servizi qui elencati: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode o namenode.</span><span class="sxs-lookup"><span data-stu-id="fa308-123">The value of **service_name** can be any of the services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="fa308-124">Abilitare con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa308-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="fa308-125">Ad esempio, per attivare i dump dell'heap usando Azure PowerShell per jobhistoryserver, è possibile usare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="fa308-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use the following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="fa308-126">Abilitare con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fa308-126">Enable using .NET SDK</span></span>
<span data-ttu-id="fa308-127">Ad esempio, per attivare i dump dell'heap usando Azure HDInsight .NET SDK per jobhistoryserver, è possibile usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="fa308-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you can use the following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
