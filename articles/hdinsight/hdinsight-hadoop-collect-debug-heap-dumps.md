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
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>Dump dell'heap in toodebug di archiviazione Blob di raccogliere e analizzare i servizi Hadoop
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Dump dell'heap contengono uno snapshot di memoria dell'applicazione hello, inclusi i valori di hello delle variabili in fase di hello dump hello è stato creato. Si rivelano quindi utili per diagnosticare i problemi che si verificano in fase di esecuzione. Dump dell'heap possono essere raccolti per i servizi Hadoop e posizionato all'interno di account di archiviazione Blob di Azure di un utente in HDInsightHeapDumps hello automaticamente /.

raccolta Hello dei dump di heap per i vari servizi deve essere abilitata per i servizi in cluster singoli. valore predefinito di Hello per questa funzionalità è toobe off per un cluster. I dump di heap può essere estesa, pertanto è account di archiviazione Blob toomonitor consigliabile hello in cui sono viene salvate una volta raccolta hello è stata abilitata.

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). informazioni di Hello in questo articolo si applicano solo in base tooWindows HDInsight. Per informazioni su HDInsight basato su Linux, vedere [Abilitare i dump dell'heap per i servizi Hadoop in HDInsight basato su Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)


## <a name="eligible-services-for-heap-dumps"></a>Servizi idonei per i dump dell'heap
È possibile abilitare dump dell'heap per hello seguenti servizi:

* **hcatalog** - tempelton
* **hive** - hiveserver2, metastore, derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager, nodemanager, timelineserver
* **hdfs** - datanode, secondarynamenode, namenode

## <a name="configuration-elements-that-enable-heap-dumps"></a>Elementi di configurazione per l'abilitazione dei dump dell'heap
tooturn nel dump dell'heap per un servizio, è necessario tooset gli elementi di configurazione appropriato hello nella sezione hello per tale servizio, specificata dalla **service_name**.

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

valore di Hello **service_name** può essere uno dei servizi di hello elencati di seguito: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, o namenode.

## <a name="enable-using-azure-powershell"></a>Abilitare con Azure PowerShell
Ad esempio, tooturn nel dump dell'heap tramite Azure PowerShell per jobhistoryserver, è possibile utilizzare hello lo script seguente:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>Abilitare con .NET SDK
Ad esempio, tooturn nel dump dell'heap tramite hello Azure HDInsight .NET SDK per jobhistoryserver, è possibile utilizzare hello seguente codice:

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
