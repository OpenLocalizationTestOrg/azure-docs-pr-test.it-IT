---
title: i processi di Sqoop aaaRun mediante .NET e HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse HDInsight .NET SDK toorun Sqoop importare ed esportare tra un cluster Hadoop e un database SQL di Azure.
keywords: processo sqoop
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="f66c1-104">Eseguire processi Sqoop con .NET SDK per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f66c1-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="f66c1-105">Informazioni su come i processi di toouse HDInsight .NET SDK toorun Sqoop in HDInsight tooimport ed esportare tra cluster HDInsight e database SQL di Azure o database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f66c1-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="f66c1-106">passaggi di Hello in questo articolo possono essere utilizzati con entrambi un cluster HDInsight basati su Linux o Windows. Tuttavia, questa procedura funziona solo da un client di Windows.</span><span class="sxs-lookup"><span data-stu-id="f66c1-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="f66c1-107">Utilizzare il selettore di tabulazione hello in primo piano hello di toochoose questo articolo altri metodi.</span><span class="sxs-lookup"><span data-stu-id="f66c1-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="f66c1-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f66c1-108">Prerequisites</span></span>
<span data-ttu-id="f66c1-109">Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f66c1-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="f66c1-110">**Un cluster Hadoop in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f66c1-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="f66c1-111">Vedere le informazioni su come [creare un cluster e un database SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="f66c1-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="f66c1-112">Usare Sqoop su cluster HDInsight con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f66c1-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="f66c1-113">Hello HDInsight .NET SDK fornisce librerie client .NET, che rende più semplice toowork con i cluster HDInsight da .NET.</span><span class="sxs-lookup"><span data-stu-id="f66c1-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="f66c1-114">In questa sezione è creare una c# console application tooexport hello hivesampletable toohello tabella del Database SQL creata precedentemente in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f66c1-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="f66c1-115">Inviare un processo Sqoop</span><span class="sxs-lookup"><span data-stu-id="f66c1-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="f66c1-116">Creare un'applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f66c1-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="f66c1-117">Dalla Console di gestione di pacchetti di Visual Studio hello, eseguire hello seguente pacchetto Nuget di comando tooimport hello.</span><span class="sxs-lookup"><span data-stu-id="f66c1-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="f66c1-118">Utilizzare hello seguente codice nel file Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="f66c1-118">Use hello following code in hello Program.cs file:</span></span>
   
        using System.Collections.Generic;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
   
        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
                private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
                private const string ExistingClusterUsername = "<Cluster Username>";
                private const string ExistingClusterPassword = "<Cluster User Password>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="f66c1-119">Premere **F5** programma hello toorun.</span><span class="sxs-lookup"><span data-stu-id="f66c1-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="f66c1-120">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="f66c1-120">Limitations</span></span>
* <span data-ttu-id="f66c1-121">Eseguire l'esportazione bulk - HDInsight basati su Linux con, hello Sqoop connettore utilizzato tooexport dati tooMicrosoft SQL Server o Database SQL di Azure attualmente non supporta inserimenti bulk.</span><span class="sxs-lookup"><span data-stu-id="f66c1-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="f66c1-122">Divisione in batch - con HDInsight basati su Linux, quando si utilizza hello `-batch` passare quando l'esecuzione di inserimenti, Sqoop esegue più inserimenti anziché l'invio in batch le operazioni di inserimento hello.</span><span class="sxs-lookup"><span data-stu-id="f66c1-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f66c1-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f66c1-123">Next steps</span></span>
<span data-ttu-id="f66c1-124">Ora si è appreso come toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="f66c1-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="f66c1-125">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="f66c1-125">toolearn more, see:</span></span>

* <span data-ttu-id="f66c1-126">[Usare Oozie con HDInsight](hdinsight-use-oozie.md): usare un'azione di Sqoop nel flusso di lavoro di Oozie.</span><span class="sxs-lookup"><span data-stu-id="f66c1-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="f66c1-127">[Analizzare i dati di ritardo volo tramite HDInsight](hdinsight-analyze-flight-delay-data.md): utilizzare Hive volo tooanalyze ritardare dati e quindi utilizzare il database SQL di Azure tooan di Sqoop tooexport dati.</span><span class="sxs-lookup"><span data-stu-id="f66c1-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="f66c1-128">[Caricare dati tooHDInsight](hdinsight-upload-data.md): trovare altri metodi per il caricamento di archiviazione Blob di dati tooHDInsight/Azure.</span><span class="sxs-lookup"><span data-stu-id="f66c1-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

