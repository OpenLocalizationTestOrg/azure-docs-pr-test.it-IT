---
title: le query Hive aaaRun tramite HDInsight .NET SDK - Azure | Documenti Microsoft
description: Informazioni su come i processi di Hadoop toosubmit tooAzure HDInsight Hadoop tramite HDInsight .NET SDK.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="14693-103">Eseguire query Hive con HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="14693-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="14693-104">Informazioni su come toosubmit Hive query che utilizzano HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="14693-104">Learn how toosubmit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="14693-105">Scrivere una query Hive per elencare le tabelle Hive di toosubmit un programma c# e visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="14693-105">You write a C# program toosubmit a Hive query for listing Hive tables, and display hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="14693-106">passaggi di Hello in questo articolo devono essere eseguiti da un client di Windows.</span><span class="sxs-lookup"><span data-stu-id="14693-106">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="14693-107">Per informazioni sull'uso di un Linux, OS X o toowork client Unix con Hive, usare il selettore di scheda hello visualizzato nella parte superiore di hello di articolo hello.</span><span class="sxs-lookup"><span data-stu-id="14693-107">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="14693-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="14693-108">Prerequisites</span></span>
<span data-ttu-id="14693-109">Prima di iniziare questo articolo, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="14693-109">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="14693-110">**Un cluster Hadoop in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="14693-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="14693-111">Vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="14693-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="14693-112">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="14693-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="14693-113">Inviare query Hive con HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="14693-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="14693-114">Hello HDInsight .NET SDK fornisce librerie client .NET, che rende più semplice toowork con i cluster HDInsight da .NET.</span><span class="sxs-lookup"><span data-stu-id="14693-114">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="14693-115">**processi tooSubmit**</span><span class="sxs-lookup"><span data-stu-id="14693-115">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="14693-116">Creare un'applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="14693-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="14693-117">Nella Console di gestione pacchetti Nuget hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="14693-117">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="14693-118">Utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="14693-118">Use hello following code:</span></span>

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
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
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. <span data-ttu-id="14693-119">Premere **F5** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="14693-119">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="14693-120">output di Hello di un'applicazione hello deve essere simile a:</span><span class="sxs-lookup"><span data-stu-id="14693-120">hello output of hello application shall be similar to:</span></span>

![Output processo Hive Hadoop di HDInsight](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="14693-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14693-122">Next steps</span></span>
<span data-ttu-id="14693-123">In questo articolo sono state fornite diverse modi toocreate un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14693-123">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="14693-124">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="14693-124">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="14693-125">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="14693-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="14693-126">[Creare cluster Hadoop in HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="14693-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="14693-127">Gestire i cluster Hadoop in HDInsight con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="14693-127">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="14693-128">Riferimento a HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="14693-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="14693-129">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="14693-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="14693-130">Usare Sqoop con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="14693-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="14693-131">Creare applicazioni .NET HDInsight di autenticazione non interattive</span><span class="sxs-lookup"><span data-stu-id="14693-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


