---
title: aaaDebug e analizzare i servizi Hadoop con dump dell'heap - Azure | Documenti Microsoft
description: Raccogliere dump di heap per i servizi Hadoop e inserire all'interno di account di archiviazione Blob di Azure per il debug e analisi hello automaticamente.
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
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="ee1e2-103">Dump dell'heap in toodebug di archiviazione Blob di raccogliere e analizzare i servizi Hadoop</span><span class="sxs-lookup"><span data-stu-id="ee1e2-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="ee1e2-104">Dump dell'heap contengono uno snapshot di memoria dell'applicazione hello, inclusi i valori di hello delle variabili in fase di hello dump hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="ee1e2-105">Si rivelano quindi utili per diagnosticare i problemi che si verificano in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="ee1e2-106">Dump dell'heap possono essere raccolti per i servizi Hadoop e posizionato all'interno di account di archiviazione Blob di Azure di un utente in HDInsightHeapDumps hello automaticamente /.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="ee1e2-107">raccolta Hello dei dump di heap per i vari servizi deve essere abilitata per i servizi in cluster singoli.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="ee1e2-108">valore predefinito di Hello per questa funzionalità è toobe off per un cluster.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="ee1e2-109">I dump di heap può essere estesa, pertanto è account di archiviazione Blob toomonitor consigliabile hello in cui sono viene salvate una volta raccolta hello è stata abilitata.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee1e2-110">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ee1e2-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ee1e2-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="ee1e2-112">informazioni di Hello in questo articolo si applicano solo in base tooWindows HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="ee1e2-113">Per informazioni su HDInsight basato su Linux, vedere [Abilitare i dump dell'heap per i servizi Hadoop in HDInsight basato su Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="ee1e2-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="ee1e2-114">Servizi idonei per i dump dell'heap</span><span class="sxs-lookup"><span data-stu-id="ee1e2-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="ee1e2-115">È possibile abilitare dump dell'heap per hello seguenti servizi:</span><span class="sxs-lookup"><span data-stu-id="ee1e2-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="ee1e2-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="ee1e2-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="ee1e2-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="ee1e2-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="ee1e2-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="ee1e2-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="ee1e2-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="ee1e2-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="ee1e2-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="ee1e2-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="ee1e2-121">Elementi di configurazione per l'abilitazione dei dump dell'heap</span><span class="sxs-lookup"><span data-stu-id="ee1e2-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="ee1e2-122">tooturn nel dump dell'heap per un servizio, è necessario tooset gli elementi di configurazione appropriato hello nella sezione hello per tale servizio, specificata dalla **service_name**.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="ee1e2-123">valore di Hello **service_name** può essere uno dei servizi di hello elencati di seguito: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, o namenode.</span><span class="sxs-lookup"><span data-stu-id="ee1e2-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="ee1e2-124">Abilitare con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee1e2-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="ee1e2-125">Ad esempio, tooturn nel dump dell'heap tramite Azure PowerShell per jobhistoryserver, è possibile utilizzare hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="ee1e2-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="ee1e2-126">Abilitare con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ee1e2-126">Enable using .NET SDK</span></span>
<span data-ttu-id="ee1e2-127">Ad esempio, tooturn nel dump dell'heap tramite hello Azure HDInsight .NET SDK per jobhistoryserver, è possibile utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="ee1e2-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
