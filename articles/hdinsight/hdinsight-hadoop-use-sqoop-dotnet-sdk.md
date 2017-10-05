---
title: Eseguire processi Sqoop usando .NET e HDInsight - Azure| Microsoft Docs
description: Informazioni su come usare HDInsight .NET SDK per eseguire l'importazione e l'esportazione con Sqoop tra un cluster Hadoop e un database SQL di Azure.
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
ms.openlocfilehash: c95641fc6d20e2911e007d1974b9e2c2398b3133
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="d835a-104">Eseguire processi Sqoop con .NET SDK per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d835a-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="d835a-105">Informazioni su come usare HDInsight .NET SDK per eseguire processi Sqoop in HDInsight per importazioni ed esportazioni tra un cluster HDInsight e un database SQL di Azure o un database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d835a-105">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="d835a-106">La procedura illustrata in questo articolo può essere usata con un cluster HDInsight basato su Windows o su Linux, ma funziona solo se eseguita da un client Windows.</span><span class="sxs-lookup"><span data-stu-id="d835a-106">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="d835a-107">Usare il selettore di schede all'inizio di questo articolo per selezionare altri metodi.</span><span class="sxs-lookup"><span data-stu-id="d835a-107">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="d835a-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d835a-108">Prerequisites</span></span>
<span data-ttu-id="d835a-109">Prima di iniziare questa esercitazione sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d835a-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="d835a-110">**Un cluster Hadoop in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d835a-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="d835a-111">Vedere le informazioni su come [creare un cluster e un database SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="d835a-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="d835a-112">Usare Sqoop su cluster HDInsight con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d835a-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="d835a-113">HDInsight .NET SDK fornisce librerie client .NET che semplificano l'uso dei cluster HDInsight da .NET.</span><span class="sxs-lookup"><span data-stu-id="d835a-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="d835a-114">In questa sezione, si crea un'applicazione console C# per esportare la hivesampletable alla tabella di Database SQL creata in precedenza in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d835a-114">In this section, you create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="d835a-115">Inviare un processo Sqoop</span><span class="sxs-lookup"><span data-stu-id="d835a-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="d835a-116">Creare un'applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d835a-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="d835a-117">Dalla Console di gestione pacchetti di Visual Studio, eseguire il comando NuGet seguente per importare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d835a-117">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="d835a-118">Nel file Program.cs usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d835a-118">Use the following code in the Program.cs file:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="d835a-119">Premere **F5** per eseguire il programma.</span><span class="sxs-lookup"><span data-stu-id="d835a-119">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="d835a-120">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="d835a-120">Limitations</span></span>
* <span data-ttu-id="d835a-121">Esportazione di massa: con HDInsight basato su Linux, attualmente il connettore Sqoop, usato per esportare dati in Microsoft SQL Server o nel database SQL di Azure, non supporta inserimenti di massa.</span><span class="sxs-lookup"><span data-stu-id="d835a-121">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="d835a-122">Invio in batch: con HDInsight basato su Linux, quando si usa il comando `-batch` durante gli inserimenti, Sqoop esegue più inserimenti invece di suddividere in batch le operazioni di inserimento.</span><span class="sxs-lookup"><span data-stu-id="d835a-122">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d835a-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d835a-123">Next steps</span></span>
<span data-ttu-id="d835a-124">In questa esercitazione si è appreso come usare Sqoop.</span><span class="sxs-lookup"><span data-stu-id="d835a-124">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="d835a-125">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="d835a-125">To learn more, see:</span></span>

* <span data-ttu-id="d835a-126">[Usare Oozie con HDInsight](hdinsight-use-oozie.md): usare un'azione di Sqoop nel flusso di lavoro di Oozie.</span><span class="sxs-lookup"><span data-stu-id="d835a-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="d835a-127">[Analizzare i dati sui ritardi dei voli usando HDInsight](hdinsight-analyze-flight-delay-data.md): usare Hive nell'analisi dei dati sui ritardi dei voli e quindi usare Sqoop per esportare dati nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d835a-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="d835a-128">[Caricare i dati in HDInsight](hdinsight-upload-data.md): per altri metodi per il caricamento di file in HDInsight o nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d835a-128">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

